---
title: Using Cloudflare Workers as a Proxy - A Step-by-Step Guide
published: 2025-04-15
updated: 2025-04-15
description: 'A tutorial on creating a proxy server using Cloudflare Workers to fetch data from websites while maintaining anonymity'
image: ''
tags: [Cloudflare, Workers, Proxy, Tutorial, Web]
category: 'Tutorial'
draft: false
---

## Introduction

This guide explains how to use **Cloudflare Workers** to create a simple proxy server. A proxy server allows you to fetch data from another website while hiding your identity. For this example, we will use **Wikileaks** as the target website. This guide is for **educational purposes only**.

## What is Cloudflare Workers?

Cloudflare Workers is a serverless platform that lets you run JavaScript code on Cloudflare's global network. It is fast, reliable, and easy to use.

## Why Use a Proxy?

A proxy server can help you:
- Access websites that are blocked in your region.
- Hide your IP address when fetching data.
- Add custom headers to requests.

## Step-by-Step Guide

### 1. Create a Cloudflare Worker

1. Go to the [Cloudflare Workers Dashboard](https://dash.cloudflare.com/).
2. Click on **Workers** in the menu.
3. Create a new Worker.

### 2. Write the Proxy Code

Here is the code for your proxy server. It will fetch data from Wikileaks and return it to the user.

```js
// CORS headers
const corsHeaders = {
  'Access-Control-Allow-Origin': '*',
  'Access-Control-Allow-Methods': 'GET, POST, OPTIONS',
  'Access-Control-Allow-Headers': 'Content-Type',
};

// Handle OPTIONS request for CORS
async function handleOptions(request) {
  return new Response(null, {
    headers: corsHeaders
  });
}

// Main request handler
async function handleRequest(request) {
  // Only allow GET requests
  if (request.method !== 'GET') {
    return new Response('Method not allowed', { status: 405 });
  }

  // Get the target URL from the request
  const url = new URL(request.url);
  const targetUrl = url.searchParams.get('url');

  if (!targetUrl) {
    return new Response('Missing target URL', { status: 400 });
  }

  try {
    // Create new request with custom headers
    const proxyRequest = new Request(targetUrl, {
      headers: {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36',
        'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8',
        'Accept-Language': 'en-US,en;q=0.5',
        'Accept-Encoding': 'gzip, deflate, br',
        'Connection': 'keep-alive',
        'Upgrade-Insecure-Requests': '1',
        'Cache-Control': 'max-age=0',
        'TE': 'Trailers'
      }
    });

    // Fetch the target URL
    const response = await fetch(proxyRequest);

    // Get response headers
    const headers = new Headers(response.headers);
    
    // Add CORS headers
    Object.entries(corsHeaders).forEach(([key, value]) => {
      headers.set(key, value);
    });

    // Create new response with modified headers
    return new Response(response.body, {
      status: response.status,
      statusText: response.statusText,
      headers: headers
    });

  } catch (error) {
    return new Response(`Error: ${error.message}`, { 
      status: 500,
      headers: corsHeaders
    });
  }
}

// Event listener for fetch requests
addEventListener('fetch', event => {
  const request = event.request;
  
  // Handle OPTIONS requests for CORS
  if (request.method === 'OPTIONS') {
    event.respondWith(handleOptions(request));
    return;
  }
  
  // Handle all other requests
  event.respondWith(handleRequest(request));
});
```

### 3. Deploy the Worker

1. Copy the code above.
2. Go to the Cloudflare Workers editor.
3. Paste the code into the editor.
4. Save and deploy your Worker.

### 4. Test the Proxy

To test your proxy, open your browser and go to the Worker URL. Add the `url` parameter with the target website. For example:

`https://your-worker-url.workers.dev/?url=https://wikileaks.org`

You should see the content of Wikileaks.

### 5. Important Notes

- This proxy only supports `GET` requests.
- Do not use this for illegal activities.
- Always respect the terms of service of the websites you access.

### Using the Proxy with Python

You can use the proxy server created with Cloudflare Workers in your Python scripts. Below is an example of how to fetch data from the proxy using the `urllib` library. It is important to ensure the target URL is properly encoded before sending it to the proxy.

#### Example Code

```python
import urllib.parse
import urllib.request

# Proxy URL (replace with your actual Worker URL)
proxy_url = "https://your-worker-url.workers.dev/"

# Target URL (the website you want to fetch, e.g., Wikileaks)
target_url = "https://wikileaks.org"

# Encode the target URL to make it safe for use in a query string
encoded_target_url = urllib.parse.quote(target_url, safe='')

# Construct the full proxy URL with the encoded target URL
full_url = f"{proxy_url}?url={encoded_target_url}"

# Make the request to the proxy
try:
    with urllib.request.urlopen(full_url) as response:
        # Read and print the response content
        content = response.read().decode('utf-8')
        print(content)
except Exception as e:
    print(f"Error: {e}")
```

### Key Points

1. **URL Encoding**: The `urllib.parse.quote` function ensures that the target URL is properly encoded. This prevents issues with special characters in the URL.
2. **Proxy URL**: Replace `https://your-worker-url.workers.dev/` with the actual URL of your deployed Cloudflare Worker.
3. **Error Handling**: Always include error handling to manage cases where the proxy or target website is unreachable.

### Output

When you run the script, it will fetch the content of the target website (e.g., Wikileaks) through the proxy server and print it to the console.

> **Note**: This example is for **educational purposes only**. Always respect the terms of service of the websites you access.

## Conclusion

You have successfully created a simple proxy server using Cloudflare Workers. This is a great way to learn about serverless platforms and web requests. Remember, this guide is for **educational purposes only**. Use it responsibly!

