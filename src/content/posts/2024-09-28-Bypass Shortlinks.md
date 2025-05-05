---
title: "Bypass Shortlinks with Fr0stB1rd uBlock Filter List"
date: 2024-09-28 00:00:00 +0300
categories: Project FilterList
tags: shortener bypass shortlink
image: 
---

# Fr0stB1rd uBlock Filter List

This filter list enhances your browsing experience by eliminating unnecessary elements and optimizing page performance on selected websites. [Source Code](https://gitlab.com/fr0stb1rd/ublock_filters/) \| [Blog Post](https://fr0stb1rd.gitlab.io/posts/Bypass-Shortlinks/)

## What This List Does:
- **Removes unwanted ads** from various sections of the sites, including footers, headers, and other ad spaces.
- **Hides irrelevant content** so you can focus on the information that matters most.
- **Bypasses intrusive scripts** that can slow down your browsing or trigger unwanted actions, ensuring a smoother user experience.
    - Affects public-earn domains such as:
        - sabarpratham.in
        - pubprofit.in
        - reliablesp.in
        - sikhehindime.com
        - aajtaklive.org
        - bgmiupdatehub.com
        - jkssbalerts.com
        - carjaankar.com
        - thelatintwistcafe.com

- **Streamlines page layout** by blocking distracting or unnecessary elements, providing a cleaner and faster browsing environment.

## How to Add This List to uBlock Origin:
- Open uBlock Origin in your browser.
- Go to the **Dashboard** by clicking on the uBlock icon, then selecting the gear icon (⚙️).
- Navigate to the **"Filter lists"** tab.
- Scroll down to the **"Custom"** section.
- Click **"Import"** and paste this URL to this filter list:
    
    ```https://gitlab.com/fr0stb1rd/ublock_filters/-/raw/main/filter.txt```
    
- Click **"Apply changes"** to activate the filter list.
- The contents of "My filters" are not trusted by default in ublock origin. You need to use the uBO dev build or append `user-` to trustedListPrefixes in advanced settings.
- WARNING: If you do this, you need to be very careful and NOT add random "trusted" filters from the internet. Use at your own risk.

    ![](https://i.ibb.co/hYp6HtZ/resim.png)

- For more effective filtering, you can use this filter list alongside [Amm0ni4/bypass-all-shortlinks-debloated](https://codeberg.org/Amm0ni4/bypass-all-shortlinks-debloated/). It will help bypass shortlinks and further improve your browsing experience.

## License

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
