---
title: OverTheWire Bandit Çözümleri - Adım Adım Rehber (Türkçe)
published: 2024-05-12
updated: 2024-05-12
description: 'A comprehensive Turkish walkthrough guide for solving the OverTheWire Bandit CTF challenges, focusing on Linux and security concepts'
image: ''
tags: [Security, Linux, CTF, Tutorial, Walkthrough]
category: 'Tutorial'
draft: false
---

## Video

uzakta...

## Walkthrough

Oyun Linki: [overthewire.org/wargames/bandit/](https://overthewire.org/wargames/bandit/)

### Bandit Level 0 -> 1

- Verilen bilgilere göre host: `bandit.labs.overthewire.org` port: `2220` kullanıcı adı: `bandit0` Parola: `bandit0`. Bu bilgilere göre `/home/bandit0/readme` adresindeki anahtarı bulalım.

- ssh ile bağlanalım: `ssh bandit0@bandit.labs.overthewire.org -p 2220`

- parolayı bize verdiği gibi `bandit0` şeklinde girelim. ssl uyarısına yes diyelim.

- bağlandıktan sonra cat ile içine bakalım: `cat /home/bandit0/readme`

- yeni seviyeye geçiş anahtarımız: `NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL`

- `exit` ile oturumu sonlandıralım. çünkü `su bandit` gibi oturum değiştirmeye izin vermiyor.

### Bandit Level 1 -> 2

- ssh ile bağlanalım: `ssh bandit1@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL`

- `ls` ile listeleyince adı `-` olan bir dosya gördük.

- `cat -` komutunu girdiğimizde çalışmayacak. bunun sebebi:

    ![](https://i.ibb.co/C6V4VM1/image.png)
    https://stackoverflow.com/questions/42187323/how-to-open-a-dashed-filename-using-terminal

    - `cat < -` kullanabiliriz.

    - `cat ./-` kullanabiliriz.

- yeni parola: `rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi`

### Bandit Level 2 -> 3

- ssh ile bağlanalım: `ssh bandit2@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi`

- `ls` ile `spaces in this filename` adındaki dosyayı gördük.

- dosya adında boşluklar olduğu için iki seçeneğimiz var:

    - kaçış karakterinden faydalanırsak: `cat spaces\ in\ this\ filename`

    - string olarak işlersek: `cat "spaces in this filename"`

- yeni parola: `aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG`

### Bandit Level 3 -> 4

- ssh ile bağlanalım: `ssh bandit3@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG`

- `ls` ile `inhere` adında bir dizine ulaştık ve `ch` ile içine girdik.

- `ls` ile listelediğimizde bir sonuç çıkmadı. emin olmak için `ls -lah` ile tüm dosyaları gördük. `.hidden` isimli dosyayı cat ile açarsak:

- yeni parola: `2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe`

### Bandit Level 4 -> 5

- ssh ile bağlanalım: `ssh bandit4@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe`

- `ls` ile `inhere` adında bir dizine ulaştık ve `ch` ile içine girdik.

- `ls` ile birçok dosyanın olduğunu gördük. `file` komutuyla dosyalar hakkında bilgi alabiliriz:

    ```bash
    bandit4@bandit:~/inhere$ file ./*
    ./-file00: data
    ./-file01: data
    ./-file02: data
    ./-file03: data
    ./-file04: data
    ./-file05: data
    ./-file06: data
    ./-file07: ASCII text
    ./-file08: data
    ./-file09: data
    ```

- sadece `-file07` dosyasının ASCII text olduğunu gördük. bakmamız gereken bu dosya.

- `cat ./-file07` ile dosyayı açarsak:

- yeni parola: `lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR`

### Bandit Level 5 -> 6

- ssh ile bağlanalım: `ssh bandit5@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR`

- `ls` ile `inhere` adında bir dizine ulaştık ve `ch` ile içine girdik.

- `ls` ile birçok dizinin bulunduğunu gördük.

- verdiği bilgilere göre ulaşmamız gereken dosya:

    - human-readable
    - 1033 bytes in size
    - not executable

    olmalıymış.

- dosya boyutuna göre listelemede `du` komutu işe yarar. `-a` parametresi verirseniz, dosyaları recursive olarak tarar. vermezseniz sadece o dizini tarar. `-b` parametresi de her dosyanın byte olarak boyutunu verir.

- `grep` ile çıkan sonucu dosya boyutu olan `1033` ile filtrelersek: `du -a -b | grep 1033`

- aradığımız dosyanın `1033    ./maybehere07/.file2` olduğunu görürüz.

- cat: `cat ./maybehere07/.file2 `

- yeni parola: `P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU`

### Bandit Level 6 -> 7

- ssh ile bağlanalım: `ssh bandit6@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU`

- `ls` ile `inhere` adında bir dizine ulaştık ve `ch` ile içine girdik.

- verdiği bilgilere göre ulaşmamız gereken dosya:

    - owned by user bandit7
    - owned by group bandit6
    - 33 bytes in size

    olmalıymış.

- `find` komutuyla `/` araması yapabiliriz. böylece ulaşımımız olan her yerde dosyayı aramış oluruz.

- `-type f` parametresi, sadece dosyaları görmemize yardımcı olacak.

- `-user bandit7` arametresi, bandit7'ye ait olan dosyaları görmemize yardımcı olacak.

- `-group bandit6` arametresi, bandit6 grubuna ait olan dosyaları görmemize yardımcı olacak.

- `-size 33c` arametresi, 33 byte olan dosyaları görmemize yardımcı olacak.

- `find / -type f -user bandit7 -group bandit6 -size 33c` çalıştırdığımızda bir sürü permission denied hatası aldık. hataları görmezden gelmek için:

    ![](https://i.ibb.co/7YWkW45/image.png)

- komutu söylenen şekilde düzenleyelim: `find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null`

- aradığımız dosya: `/var/lib/dpkg/info/bandit7.password`

- cat: `cat /var/lib/dpkg/info/bandit7.password`

- yeni parola: `z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S`

### Bandit Level 7 -> 8

- ssh ile bağlanalım: `ssh bandit7@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S`

- cat ile `data.txt` dosyasını açtığımızda birçok kelime ve parola görünecek.

- bize `millionth` sözcüğünün hemen yanında olduğu bilgisi verilmiş. o zaman grep komutuyla birleştirirsek filtreleyebiliriz: `cat data.txt | grep millionth`

- yeni parola: `TESKZC0XvTetK0S9xNwm25STk5iWrBvP`

### Bandit Level 8 -> 9

- ssh ile bağlanalım: `ssh bandit8@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `TESKZC0XvTetK0S9xNwm25STk5iWrBvP`

- cat ile `data.txt` dosyasını açtığımızda birçok kelime ve parola görünecek. bizden istediği içerisinde tek sefer geçen sözcüğü bulmamız.

- sort komutuyla txt içindeki sözcükleri sıralayabiliriz: `sort data.txt`. ancak bu haliyle de yakalamamız zor olacak. uniq komutu aynı satırlara süzgeç uygulayabilir. `-u` parametresine baktığımızda `-u, --unique only print unique lines` istediğimiz sonuca ulaşabiliriz. bu iki komutu birleştirirsek: `sort data.txt | uniq -u`

- yeni parola: `EN632PlfYiZbn3PhVK3XOGSlNInNE00t`

### Bandit Level 9 -> 10

- ssh ile bağlanalım: `ssh bandit9@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `EN632PlfYiZbn3PhVK3XOGSlNInNE00t`

- cat ile `data.txt` dosyasını açtığımızda okuyamadığımız bir veriyle karşılaştık.

- açıklamalara göre aradığımız sözcüğün başında birkaç tane `=` varmış. bunun için veriyi `cat` ile değil de `strings` ile açmalıyız. çünkü veri, `file data.txt` ile bakarsak `data` türünde. iki tane eşittir işaretiyle filtrelersek: `strings data.txt | grep ==`

- yeni parola: `G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s`

### Bandit Level 10 -> 11

- ssh ile bağlanalım: `ssh bandit10@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s`

- cat ile dosyayı açarsak: `VGhlIHBhc3N3b3JkIGlzIDZ6UGV6aUxkUjJSS05kTllGTmI2blZDS3pwaGxYSEJNCg==`

- bu bir `base64 encoded text`. ister online ister terminalden bunu decode edebiliriz:

- decode: `cat data.txt | base64 -d` ya da `base64 -d data.txt`

- yeni parola: `6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM`

### Bandit Level 11 -> 12

- ssh ile bağlanalım: `ssh bandit11@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM`

- cat ile dosyayı açarsak: `Gur cnffjbeq vf WIAOOSFzMjXXBC0KoSKBbJ8puQm5lIEi`

- ROT13 şifrelemesiyle karşı karşıyayız. ister [online](https://cryptii.com/pipes/rot13-decoder) ister offline decode yapabiliriz:

    ![](https://i.ibb.co/VLPYBKg/image.png)

- terminalimize bunun için bir alias ekleyelim: `alias rot13="tr 'A-Za-z' 'N-ZA-Mn-za-m'"`

- şimdi yapmamız gereken bunları birleştirmek: `cat data.txt | rot13`

- yeni parola: `JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv`

### Bandit Level 12 -> 13

- ssh ile bağlanalım: `ssh bandit12@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv`

- hexdump bir data.txt dosyası vermiş. /tmp/ dizininde yeni bir dizin oluşturup oraya taşımamızı istemiş.

- `cd /tmp` ve `mktemp -d` ile yeni bir temp dizin oluşturalım. benim dizinim burası: `/tmp/tmp.3jUaTPgTT4`. isim farklı olabilir.

- data.txt dosyasını buraya kopyalayalım ve adını data olarak değiştirelim: `cp ~/data.txt data`

- `head data` ile içerisine göz atalım:

    ![](https://i.ibb.co/fG03zCr/image.png)

- xxd komutuyla `reverse hash dump` yapabiliyoruz. o zaman `cat data | xxd -r > dump` komutuyla dump adında bir dosyaya yazalım.

- `file dump` ile özelliklerine baktığımızda: `gzip compressed data, was "data2.bin"` data2.bin adında gzip ile sıkıştırılmış bir dosya olduğunu gördük.

    - adını data.gz yapabiliriz: `mv dump dump.gz`

    - sıkıştırılmış dosyayı çıkaralım: `gzip -d dump.gz`

- `file dump` ile özelliklerine baktığımızda: `bzip2 compressed data` olduğunu gördük. bu, bzip2 ile sıkıştırılmış bir dosya.

    - adını data2.bz yapabiliriz: `mv dump dump.bz`

    - sıkıştırılmış dosyayı çıkaralım: `bzip2 -d dump.bz`

- `file dump` ile özelliklerine baktığımızda: `gzip compressed data, was "data4.bin` data4.bin adında gzip ile sıkıştırılmış bir dosya olduğunu gördük.

    - adını data.gz yapabiliriz: `mv dump dump.gz`

    - sıkıştırılmış dosyayı çıkaralım: `gzip -d dump.gz`

- `file dump` ile özelliklerine baktığımızda: `POSIX tar archive (GNU)` bir tar arşivi olduğunu gördük.

    - adını data.tar yapabiliriz: `mv dump dump.tar`

    - sıkıştırılmış dosyayı çıkaralım ve arşivi silelim: `tar -xf dump.tar && rm dump.tar`

- `file data5.bin` ile özelliklerine baktığımızda: `POSIX tar archive (GNU)` bir tar arşivi olduğunu gördük.

    - adını data.tar yapabiliriz: `mv data5.bin dump.tar`

    - sıkıştırılmış dosyayı çıkaralım ve arşivi silelim: `tar -xf dump.tar && rm dump.tar`

- `file data6.bin` ile özelliklerine baktığımızda: `bzip2 compressed data` yine bu, bzip2 ile sıkıştırılmış bir dosya.

    - adını data2.bz yapabiliriz: `mv data6.bin dump.bz`

    - sıkıştırılmış dosyayı çıkaralım: `bzip2 -d dump.bz`

- `file dump` ile özelliklerine baktığımızda: `POSIX tar archive (GNU)` yine bir tar arşivi olduğunu gördük.

    - adını data.tar yapabiliriz: `mv dump dump.tar`

    - sıkıştırılmış dosyayı çıkaralım ve arşivi silelim: `tar -xf dump.tar && rm dump.tar`

- `file data8.bin` ile özelliklerine baktığımızda: `gzip compressed data, was "data9.bin"` data9.bin adında gzip ile sıkıştırılmış bir dosya olduğunu gördük.

    - adını data.gz yapabiliriz: `mv data8.bin dump.gz`

    - sıkıştırılmış dosyayı çıkaralım: `gzip -d dump.gz`

- `file dump` ile özelliklerine baktığımızda: `ASCII text` olduğunu görüyoruz.

    - cat: `cat dump`

- yeni parola: `wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw`

### Bandit Level 13 -> 14

- ssh ile bağlanalım: `ssh bandit13@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw`

- `ls` ile `sshkey.private` adında bir dosya olduğunu gördük. bunu aktarmamız gerekecek:

    ![](https://i.ibb.co/RCS0mNh/image.png)

- bağlantıyı `logout` veya `exit` ile kapatalım.

- dosyayı bu komutla lokale indirelim: `scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .`

- cat: `cat sshkey.private`

    ```
    -----BEGIN RSA PRIVATE KEY-----
    MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
    gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
    ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
    ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
    ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
    jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
    J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
    pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
    xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
    nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
    o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
    ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
    laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
    M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
    1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
    PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
    8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
    xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
    GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
    3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
    iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
    9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
    qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
    kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
    /+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
    -----END RSA PRIVATE KEY-----
    ```

- indirdiğimiz dosya ile ssh'e bağlanalım. bunun için ssh `-i` parametresini kullanarak private key belirtebiliriz.

- `ssh bandit14@bandit.labs.overthewire.org -p 2220 -i sshkey.private` komutunu girdiğimizde parola istiyor.
    
    - hata mesajı: `Permissions 0640 for 'sshkey.private' are too open.`

    - dosyayı sadece bize ait olarak ayarlayalım: `chmod 700 sshkey.private`

    - dosya artık sadece bana ait: `ls -l`:

    `-rwx------ 1 fr0stb1rd fr0stb1rd 1679 May 12 15:05  sshkey.private`

- tekrar: `ssh bandit14@bandit.labs.overthewire.org -p 2220 -i sshkey.private`

- ve artık `bandit14@bandit` olarak bağlanabiliyoruz.

- bandit14 için anahtarı bulalım: `cat /etc/bandit_pass/bandit14`

- yeni parola: `fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq`

### Bandit Level 14 -> 15

- ister `sshkey.private` istersek de yeni edindiğimiz parola ile bağlanabiliriz.

    - key ile: `ssh bandit14@bandit.labs.overthewire.org -p 2220 -i sshkey.private`

    - ssh ile: `ssh bandit14@bandit.labs.overthewire.org -p 2220`
        
        önceki seviyede bulduğumuz parolayı girelim: `fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq`

- burada istenen şey, 30000 portuna şu anki parolayı girerek yeni parolayı almamız. bakalım 30000 portunda ne varmış?

- basit bir nmap taraması yapalım: `nmap localhost`:

    ```bash
    bandit14@bandit:~$ nmap localhost 
    Starting Nmap 7.80 ( https://nmap.org ) at 2024-05-12 21:41 UTC
    Nmap scan report for localhost (127.0.0.1)
    Host is up (0.00015s latency).
    Not shown: 994 closed ports
    PORT      STATE SERVICE
    22/tcp    open  ssh
    1111/tcp  open  lmsocialserver
    1840/tcp  open  netopia-vo2
    4321/tcp  open  rwhois
    8000/tcp  open  http-alt
    30000/tcp open  ndmps

    Nmap done: 1 IP address (1 host up) scanned in 0.08 seconds
    ```

- 30000 portunda bir ndmps çalışıyormuş. netcat ile bu seviyenin parolasını gönderelim:

    -   `netcat localhost 30000 <<< "fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq"`
    
        ya da `netcat localhost 30000 < /etc/bandit_pass/bandit14`
        
        ya da `netcat localhost 30000` yazıp parolayı yazabiliriz.

    ```
    Correct!
    jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
    ```

- yeni parola: `jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt`

### Bandit Level 15 -> 16

- ssh ile bağlanalım: `ssh bandit15@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt`

- OpenSSL, ağ üzerinde güvenli iletişim için bir kütüphanedir. HTTPS'te kullanılan Transport Layer Security (TLS) ve Secure Sockets Layer (SSL) şifreleme protokollerini destekliyor.

- SSL/TLS kullanarak bir sunucuya bağlanacağız. bunun için openssl'in içinde olan [s_client](https://www.openssl.org/docs/man1.1.1/man1/openssl-s_client.html)'i kullanabiliriz.

- tek komut ile: `echo jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt | openssl  s_client -ign_eof -connect localhost:30001`

    - ya da: `cat /etc/bandit_pass/bandit15 | openssl  s_client -ign_eof -connect localhost:30001`

    - ya da önce: `openssl s_client -connect localhost:30001` ile bağlanıp ardından `jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt` verisini gönderebiliriz.

- yeni parola: `JQttfApK4SeyHwDlI9SXGR50qclOAil1`

### Bandit Level 16 -> 17

- ssh ile bağlanalım: `ssh bandit16@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `JQttfApK4SeyHwDlI9SXGR50qclOAil1`

- 31000 ve 32000 arasındaki portlardan birinde ssl açık olanları taramamızı istiyor. bunun için nmap taraması yapabiliriz. `-sV` parametresini de girerek servis taraması yapalım. bu parametre, her port için ssl olup olmadığını kontrol edecektir. haliyle biraz uzun sürebilir (~5dk).

- nmap: `nmap -sV localhost -p 31000-32000`

    ```bash
    bandit16@bandit:~$ nmap -sV localhost -p 31000-32000
    Starting Nmap 7.80 ( https://nmap.org ) at 2024-05-13 13:09 UTC
    Nmap scan report for localhost (127.0.0.1)
    Host is up (0.00014s latency).
    Not shown: 996 closed ports
    PORT      STATE SERVICE     VERSION
    31046/tcp open  echo
    31518/tcp open  ssl/echo
    31691/tcp open  echo
    31790/tcp open  ssl/unknown
    31960/tcp open  echo
    ```

- işimize yarayan portlar: `31518` ve `31790` olacak. çünkü ssl servisi olarak görüyoruz.

    - önce 31518 portunu deneyelim:

        tek komut ile: `echo JQttfApK4SeyHwDlI9SXGR50qclOAil1 | openssl  s_client -ign_eof -connect localhost:31518`

        - ya da: `cat /etc/bandit_pass/bandit16 | openssl  s_client -ign_eof -connect localhost:31518`

        - ya da önce: `openssl s_client -connect localhost:30001` ile bağlanıp ardından `JQttfApK4SeyHwDlI9SXGR50qclOAil1` verisini gönderebiliriz.

        `31518` portunu denediğimizde aynı parolayı geri döndürdü.

            ```
            read R BLOCK
            JQttfApK4SeyHwDlI9SXGR50qclOAil1
            ```

    - şimdi 31790 portunu deneyelim:

        tek komut ile: `echo JQttfApK4SeyHwDlI9SXGR50qclOAil1 | openssl  s_client -ign_eof -connect localhost:31790`

        - ya da: `cat /etc/bandit_pass/bandit16 | openssl  s_client -ign_eof -connect localhost:31790`

        - ya da önce: `openssl s_client -connect localhost:31790` ile bağlanıp ardından `JQttfApK4SeyHwDlI9SXGR50qclOAil1` verisini gönderebiliriz.

        `31790` portunu denediğimizde bir rsa private key döndürdü.

            ```
            -----BEGIN RSA PRIVATE KEY-----
            MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
            imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
            Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
            DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
            JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
            x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
            KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
            J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
            d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
            YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
            vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
            +TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
            8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
            SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
            HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
            SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
            R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
            Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
            R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
            L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
            blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
            YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
            77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
            dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
            vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
            -----END RSA PRIVATE KEY-----
            ```

- yeni seviyeye bağlanmak için bu anahtarı kullanacağız. bunu `bandit17` isminde yeni bir dosyaya kaydedelim:

    - `nano` yu açalım
    - kopyaladığımız rsa private key'i yapıştıralım.
    - `ctrl+x` ile çıkalım
    - `y` ile kaydedelim
    - `bandit17` yazarak isimlendirelim.
    - cat: `cat bandit17` yazarak oluşturduğumuz dosyayı kontrol edelim.

### Bandit Level 17 -> 18

- önceki seviyede edindiğimiz anahtarla bağlanalım: `ssh bandit17@bandit.labs.overthewire.org -p 2220 -i bandit17`

    - bir hata mesajı alacağız: `It is required that your private key files are NOT accessible by others.`

    - dosyayı sadece bize ait olarak ayarlayalım: `chmod 700 bandit17`

        - dosya artık sadece bana ait: `ls -l`:

        `-rwx------  1 fr0stb1rd fr0stb1rd  1675 May 13 09:25 bandit17`

    - tekrar: `ssh bandit17@bandit.labs.overthewire.org -p 2220 -i bandit17`

    - ve artık `bandit17@bandit` olarak bağlanabiliyoruz.

- bandit17 için anahtarı bulalım: `cat /etc/bandit_pass/bandit17`

- bu seviyenin parolası: `VwOSWtCA7lRKkTfbr2IDh6awj9RNZM5e`

- yeni seviyeye geçmek için home dizinindeki `passwords.new` ve `passwords.old` dosyalarında farklı olan satırı bulmamızı istemiş. ve parolanın `passwords.new` dosyasında olduğu bilgisini vermiş. bunun için `diff` aracını kullanabiliriz.

    - diff: `diff passwords.new passwords.old`

        ```bash
        42c42
        < hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
        ---
        > p6ggwdNHncnmCNxuAt0KtKVq185ZU7AW
        ```
    
    - burada diff aracında anlamamız gereken şey, ilk parametre ve ikinci parametrede ne girdiysek, sonuç da sağ ve sol olarak ikiye ayrılır. önce `passwords.new` parametresini verdiğim için `<` olan her satır `passwords.new` dosyasında, `>` olan her satır da ikinci parametrede yani `passwords.old` dosyasındadır.

        ![](https://i.ibb.co/wsnj6xs/image.png)

    - o halde aradığım anahtar: `hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg`

- ayrıca `sort` ile de bu işlemi yapabiliriz:

    - sort: `sort passwords.old passwords.new | uniq -u`

        ```
        hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
        p6ggwdNHncnmCNxuAt0KtKVq185ZU7AW
        ```
    - bu iki satır unique imiş. o zaman `passwords.new` dosyasında grep ile filtrelersem hangisinin olduğunu bulabilirim:

        ![](https://i.ibb.co/gPqHFTm/image.png)

        - `cat passwords.new | grep p6ggwdNHncnmCNxuAt0KtKVq185ZU7AW` bir yanıt döndürmedi demek ki bulamadı.

        - `cat passwords.new | grep hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg` ise buldu. keyi yine bulmuş olduk.

- yeni parola: `hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg`

### Bandit Level 18 -> 19

- ssh ile bağlanalım: `ssh bandit18@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg`

- hemen server'dan attı:

    ```
    Byebye !
    Connection to bandit.labs.overthewire.org closed.
    ```

- bilgilere göre home dizininde readme isimli dosya varmış. bu dosyaya bir bakalım.

- ssh ile bağlandıktan sonra bir komut girebilirsiniz. örneğin ls komutu çalıştıralım:

    - `ssh bandit18@bandit.labs.overthewire.org -p 2220 ls`

    - ve bir `readme` dosyası gördük. cat ile içine bakalım.

    - `ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme`

    ```bash
                             _                     _ _ _   
                            | |__   __ _ _ __   __| (_) |_ 
                            | '_ \ / _` | '_ \ / _` | | __|
                            | |_) | (_| | | | | (_| | | |_ 
                            |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                        

                        This is an OverTheWire game server. 
                More information on http://www.overthewire.org/wargames

    bandit18@bandit.labs.overthewire.org's password: 
    awhqfNnAbc1naukrpqDYcF95h7HoMTrC
    ```

- bu işlemi yeni bir bash spawn ederek yapabiliriz. özellikle art arda komutlar gireceksek bu daha faydalı bir yöntemdir:

    ![](https://i.ibb.co/FBfp4CR/image.png)

    - `ssh bandit18@bandit.labs.overthewire.org -p 2220 /bin/bash`

    ![](https://i.ibb.co/ZSJfYrG/image.png)

    - `ssh bandit18@bandit.labs.overthewire.org -p 2220 -t /bin/sh`

    ![](https://i.ibb.co/J5YCybq/image.png)

- yeni parola: `awhqfNnAbc1naukrpqDYcF95h7HoMTrC`

### Bandit Level 19 -> 20

- ssh ile bağlanalım: `ssh bandit19@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `awhqfNnAbc1naukrpqDYcF95h7HoMTrC`

- listeleyelim: `ls -l`

- `-rwsr-x--- 1 bandit20 bandit19 14876 Oct  5  2023 bandit20-do`

- bu durumda dosyanın sahibi bandit20 ve grubu bandit19. `-rwsr-x---` bayraklarının anlamı, bandit19 kullanıcısı bu dosyayı çalıştırınca dosya sanki bandit20 çalıştırmış gibi davranabilmesidir. bunun ispatını `./bandit20-do id` ile yapabiliriz:

- `uid=11019(bandit19) gid=11019(bandit19) euid=11020(bandit20) groups=11019(bandit19)`

- `euid=11020(bandit20)` programın bandit20 adına komutları çalıştıracağının kanıtıdır.

- bu dosyayı parametresiz olarak çalıştırmamızı istemiş.

- `./bandit20-do`

    ```
    Run a command as another user.
    Example: ./bandit20-do id
    ```

- her seviyenin anahtarına o seviyedeyken ulaşabiliyorduk. o zaman bandit20'nin anahtarına da bu programı doğru kullanarak ulaşabiliriz.

- önce /etc/bandit_pass dizinini kontrol edelim:

- `ls /etc/bandit_pass`:

    ```
    bandit0   bandit12  bandit16  bandit2   bandit23  bandit27  bandit30  bandit4  bandit8
    bandit1   bandit13  bandit17  bandit20  bandit24  bandit28  bandit31  bandit5  bandit9
    bandit10  bandit14  bandit18  bandit21  bandit25  bandit29  bandit32  bandit6
    bandit11  bandit15  bandit19  bandit22  bandit26  bandit3   bandit33  bandit7
    ```

- bu program olmadan anahtarı göstermeye çalışalım:

    - `cat /etc/bandit_pass/bandit20`

    ![](https://i.ibb.co/hKLqQY1/image.png)

    - erişim engellendi.

- bize verilen programla deneyelim:

    - `./bandit20-do cat /etc/bandit_pass/bandit20`

- yeni parola: `VxCazJaVykI6W36BkBU0mJTCM8rR95XT`

### Bandit Level 20 -> 21

- ssh ile bağlanalım: `ssh bandit20@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `VxCazJaVykI6W36BkBU0mJTCM8rR95XT`

- listeleyelim: `ls -l`

- `-rwsr-x--- 1 bandit21 bandit20 15600 Oct  5  2023 suconnect`

- bir server açıp, herhangi bir bağlantı oluşturulduğunda şu anki parolayı göndermemiz isteniyor. böylece şu anki parola uyuşursa yeni parolayı bize `suconnect` programı verecek.

- netcat ile bir server oluşturabiliriz. bağlantıda bir string göndermek için:

    ![](https://i.ibb.co/T2c2YY9/image.png)

- biraz düzenlersek: `echo -n 'VxCazJaVykI6W36BkBU0mJTCM8rR95XT' | nc -l -p 1234 &`

    - sonuna `&` koyduk ki arkaplanda çalışsın.
    - `1234` portunu açtık.
    - echo'da `-n` parametresini verdik ki `newline` karakterlerini işlemesin.

- şimdi programa açtığımız portu parametre olarak gönderelim: `./suconnect 1234`:

    ```
    Read: VxCazJaVykI6W36BkBU0mJTCM8rR95XT
    Password matches, sending next password
    NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
    ```

- yeni parola: `NvEJF7oVjkddltPSrdKEFOllh9V1IBcq`

### Bandit Level 21 -> 22

- ssh ile bağlanalım: `ssh bandit21@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `NvEJF7oVjkddltPSrdKEFOllh9V1IBcq`

- `/etc/cron.d/` dizinine bakmamızı istemiş. ls: `ls -lah /etc/cron.d/`

- `-rw-r--r--   1 root root  120 Oct  5  2023 cronjob_bandit22` dosyasına bakalım. cat: `cat /etc/cron.d/cronjob_bandit22`

    ```
    @reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
    * * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
    ```

- bu cron, her dakika çalışıyor, sistemi yeniden başlatıyor ve bandit22 kullanıcısı olarak `/usr/bin/cronjob_bandit22.sh` dosyasını çalıştırıyor. bunu manipüle edebiliriz. cat: `cat /usr/bin/cronjob_bandit22.sh`

    ```bash
    #!/bin/bash
    chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
    cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
    ```

- bu shell dosyası çalıştığında, `/tmp/` dizinindeki `t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv` dosyasına 644 bayrağını veriyor ve `/etc/bandit_pass/bandit22` dosyasından okuduğu değeri `/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv` dosyasına yazıyor. o zaman bu dosyaya göz atarsak sonraki parolamızı bulmuş olacağız. cat: `cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`

- yeni parola: `WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff`

### Bandit Level 22 -> 23

- ssh ile bağlanalım: `ssh bandit22@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff`

- `/etc/cron.d/` dizinine bakmamızı istemiş. ls: `ls -lah /etc/cron.d/`

- `-rw-r--r--   1 root root  122 Oct  5  2023 cronjob_bandit23` dosyasına bakalım. cat: `cat /etc/cron.d/cronjob_bandit23`

    ```
    @reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
    * * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
    ```

- bu cron, her dakika çalışıyor, sistemi yeniden başlatıyor ve bandit23 kullanıcısı olarak `/usr/bin/cronjob_bandit23.sh` dosyasını çalıştırıyor. bunu manipüle edebiliriz. cat: `cat /usr/bin/cronjob_bandit23.sh`

    ```bash
    !/bin/bash

    myname=$(whoami)
    mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

    echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

    cat /etc/bandit_pass/$myname > /tmp/$mytarget
    ```

- kodu incelersek, whoami ile çalışacak değer `bandit23` olacaktır. çünkü bu dosyayı çalıştıran kişi crontab'de bandit23 olarak ayarlanmış. o halde `myname`değeri `bandit23` olacaktır.

- `mytarget` değerinin ne döndüreceğini terminalden çalıştırarak bulabiliriz:

    - `echo I am user bandit23 | md5sum | cut -d ' ' -f 1` 

    - bu komut, `I am user bandit23` tümcesini md5 ile hash'leyip sondaki gereksiz karakterleri kaldırıyor ve echo ile yazıyor.

- bu komut `8ca319486bfbbc3663ea0fbe81326349` değerini döndürdü. o halde `mytarget` değeri `8ca319486bfbbc3663ea0fbe81326349` olacaktır.

- `cat /etc/bandit_pass/$myname > /tmp/$mytarget` burada ise `/etc/bandit_pass/bandit23` değerinin `/tmp/8ca319486bfbbc3663ea0fbe81326349` dosyasına yazıldığını anlıyoruz. o halde cat: `cat /tmp/8ca319486bfbbc3663ea0fbe81326349`

- yeni parola: `QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G`

### Bandit Level 23 -> 24

- ssh ile bağlanalım: `ssh bandit23@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G`

- `/etc/cron.d/` dizinine bakmamızı istemiş. ls: `ls -lah /etc/cron.d/`

- `-rw-r--r--   1 root root  120 Oct  5  2023 cronjob_bandit24` dosyasına bakalım. cat: `cat /etc/cron.d/cronjob_bandit24`

    ```
    @reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
    * * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
    ```
- bu cron, her dakika çalışıyor, sistemi yeniden başlatıyor ve bandit24 kullanıcısı olarak `/usr/bin/cronjob_bandit24.sh` dosyasını çalıştırıyor. bunu manipüle edebiliriz. cat: `cat /usr/bin/cronjob_bandit24.sh`

    ```bash
    #!/bin/bash

    myname=$(whoami)

    cd /var/spool/$myname/foo
    echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
    for i in * .*;
    do
        if [ "$i" != "." -a "$i" != ".." ];
        then
            echo "Handling $i"
            owner="$(stat --format "%U" ./$i)"
            if [ "${owner}" = "bandit23" ]; then
                timeout -s 9 60 ./$i
            fi
            rm -f ./$i
        fi
    done
    ```

- bu betik her çalıştığında (yani her dakikada bir) `$myname` değişkenine `bandit24` değeri otomatik atandığı için `/var/spool/bandit24/foo/` dizinindeki tüm dosyaları önce çalıştırıp sonra siliyor:

    - ilk kontrol satırı: `if [ "$i" != "." -a "$i" != ".." ];` dizin veya üst dizin söz konusuysa silmiyor.

    - ikinci kontrol satırı: `if [ "${owner}" = "bandit23" ]; then` dosyanın sahibi `bandit23` ise siliyor yoksa silmiyor.

    - şu anda bandit23 olduğumuz için bizim yazacağımız scripti silecektir.

- o halde bir script yazalım ve bu scripti `/var/spool/bandit24/foo/` dizinine taşıyalım. her seviyede o seviyenin kullanıcısının erişimiyle parolayı bulabiliyorduk. o zaman bu konuma yazacağımız script de bandit24 kullanıcısı tarafından çalıştırılacak.

- öncelikle `/tmp/` dizinine gidelim. burada rahatça çalışabiliriz: `mktemp -d` ve `cd /tmp/tmp.7eLTwOoNAm` diyerek çalışma dizinimize gidelim.

- `nano` text editörünü açalım. içerisine basit bir script yazacağım. istediğimiz dosya: `/etc/bandit_pass/bandit24`. o zaman bunu şu anki konuma kopyalayan basit bir script yazıyorum:

    ```bash
    #!/bin/bash
    cp /etc/bandit_pass/bandit24 /tmp/tmp.7eLTwOoNAm/bandit24
    ```

    - çıkış yapıp `virus.sh` dosya ismiyle kaydediyoruz. siz istediğiniz isimle kaydedebilirsiniz. dosyayı cat ile açıp kontrol etmeyi unutmayın.

    - oluşturduğumuz dizine (`/tmp/tmp.7eLTwOoNAm/bandit24`) herkesin ulaşabilmesi, yazabilmesi ve çalıştırabilmesi gerekiyor. bunun için `chmod 777 .` yapalım ve `ls -la` ile tekrar kontrol edelim.

        ![](https://i.ibb.co/18FqjFx/image.png)

    - virus.sh dosyasına da çalıştırılabilir (executable) bayrağını ekleyelim: `chmod 777 ./virus.sh`

    - `cp ./virus.sh /var/spool/bandit24/foo/virus.sh` ile kopyalayalım ve arada bir `ls` komutunu çalıştıralım ki dosya geldiğinde haberimiz olsun.

    - maksimum 60 saniye sonra `bandit24` belirecek. ancak bir sorun var:

    ![](https://i.ibb.co/CsHWZ6R/image.png)

    - dosya izinleriyle beraber kopyalanmış. bunu aşmamız gerekecek.

    - cp komutuyla dosya izinleri olmadan kopyalamanın yolunu bulmalıyız.

    ![](https://i.ibb.co/4gpCxhh/image.png)

    - virus.sh dosyasını şu şekilde düzenlersek:

    ```bash
    #!/bin/bash
    cp --no-preserve=mode,ownership /etc/bandit_pass/bandit24 /tmp/tmp.7eLTwOoNAm/bandit24
    ```

    - ve bir dakika sonra, cat: `cat bandit24` ta daa.

    - parola: `VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar`

- ayrıca cp ile değil de `cat` ile de yapabiliriz.

    - bunun için şu an varolduğumuz dizinde pass24 adında bir dosya oluşturalım: `touch pass24`

    - pass24 dosyasına tüm izinleri verelim ki bandit24 kullanıcısı içine yazabilsin: `chmod 777 pass24`

    - oluşturduğumuz dizine (`/tmp/tmp.7eLTwOoNAm/bandit24`) herkesin ulaşabilmesi, yazabilmesi ve çalıştırabilmesi gerekiyor. bunun için `chmod 777 .` yapalım ve `ls -la` ile tekrar kontrol edelim.

        ![](https://i.ibb.co/18FqjFx/image.png)

    - virus.sh dosyasının içeriğini şu şekilde değiştirelim:

        ```bash
        #!/bin/bash
        cat /etc/bandit_pass/bandit24 > /tmp/tmp.7eLTwOoNAm/pass24
        ```

    - bu işlem, cat ile dosyayı açıp okuyacak ve `/tmp/tmp.7eLTwOoNAm/pass24` adresindeki oluşturduğumuz dosyanın içine yazacak.

    - `cp ./virus.sh /var/spool/bandit24/foo/virus.sh` ile kopyalayalım ve arada bir `ls -la` komutunu çalıştıralım ki `pass24` dosyasının boyutu değiştiğinde haberimiz olsun.

        ![](https://i.ibb.co/C9vbBQj/image.png)

    - ve parolayı ele geçirdik.

- yeni parola: `VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar`

### Bandit Level 24 -> 25

- ssh ile bağlanalım: `ssh bandit24@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar`

- bizden istediği 30002 portuna 0000-9999 arasındaki tüm pinleri denememiz. bunu yaparken örnek format şu şekilde olmalıymış:

    - `VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 0000`

    - `VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 0001`

    - ...

    - `VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar 9999`

- tüm olasılıkları denemek için öncelikle bir tanesini deneyip çıktı almayı deneyelim.

    ![](https://i.ibb.co/Z6cfYM9/image.png)

- `mktemp -d` ile yeni bir çalışma ortamı oluşturalım ve içine girelim: `cd /tmp/tmp.qUkib7SF1N`

- bunun için bir script yazabiliriz:

    ```bash
    #!/bin/bash
    for i in {0000..9999}
    do
        echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i" >> possible.txt
    done
    ```

- bu script, 0000 ile 9999 arasında dönecek ve `possible.txt` dosyasına yazacak.

- nano ile yazdığımız betiği `write.sh` olarak kaydedelim.

- `chmod +x write.sh` ile çalıştırma bayrağı ekleyelim.

    ![](https://i.ibb.co/qjzNJdp/image.png)

- şimdi bu dosyayı netcat kullanarak 30002 portuna gönderebiliriz.

    - `cat possible.txt | nc localhost 30002 > sonuc.txt &`

    - sonuc.txt dosyasına netcat return değerini yazacak.

    - sonuna `&` koyduk ki arkaplanda çalışsın.

    - arada bir `ls -l` yaparak sonuc.txt dosyasının boyutunu kontrol edebiliriz. dosya boyutu sabit kalıyorsa işlem tamamlanmış demektir.

    ![](https://i.ibb.co/sFh1nnR/image.png)

    - bu şekilde gönderince sunucu çökebiliyor. tıpkı fotoğraftaki gibi. bu yüzden işlemi ikiye ayıralım.

- işlemi ikiye ayırarak deneyelim.

    - ilk script 0000-5555 arasını pos1.txt dosyasına yazsın. bunun için nano ile pos1.sh dosyasını hazırlayalım.

        ```bash
        #!/bin/bash
        for i in {0000..5555}
        do
            echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i" >> pos1.txt
        done
        ```
    - ikinci script 5555-9999 arasını pos2.txt dosyasına yazsın. bunun için nano ile pos2.sh dosyasını hazırlayalım.

        ```bash
        #!/bin/bash
        for i in {5555..9999}
        do
            echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i" >> pos2.txt
        done
        ```

    - ikisine de çalıştırma izinleri verelim: `chmod +x pos1.sh && chmod +x pos2.sh`

    - ikisini de çalıştıralım: `./pos1.sh && ./pos2.sh`

    - brute-force:

        - birinci dosyayı netcat ile 30002 portuna brute-force'layalım.
        
        - `cat pos1.txt | nc localhost 30002 > sonuc.txt`

        - ikinci dosyayı da gönderelim.
        
        - `cat pos2.txt | nc localhost 30002 > sonuc.txt`

    - eğer bu adımlarda sunucu çöküyorsa sonra tekrar oynamayı deneyin.

    - komutların sonuna `&` ekleyerek çalıştırırsanız arkaplanda çalışacaktır.
    
        - örnek: `cat pos2.txt | nc localhost 30002 > sonuc.txt &`.

        - böylece ara sıra `ls -l` yaparak dosya boyutuna bakabilirsiniz.

        - işlem başladığında `[1] 62842` gibi bir yanıt verir. bu `pid` yani process id'dir.

        - bittiğinde de bildirim alırsınız.
        
        - örnek: `[1]+  Done cat pos1.txt | nc localhost 30002 > sonuc.txt`

        - işlemleri görüntülemek için ara sıra `ps aux`'a da bakabilirsiniz (önemli)

    - işlem tamamlandığında `sort sonuc.txt | grep -v "Wrong"` komutunu uygulayalım.

        - `sort sonuc.txt`: bu komut, sonuc.txt dosyasındaki içeriği sıralar. sıralama, satırların alfabetik olarak küçükten büyüğe veya büyükten küçüğe sıralanması anlamına gelir. bu durumda, satırlar varsayılan olarak alfabetik olarak sıralanacaktır.

        - `grep -v "Wrong"`: bu komut, grep aracını kullanarak belirli bir metni içermeyen satırları ekrana yazdırır. `-v` parametresi, belirtilen metni içermeyen satırları seçmek için kullanılır. yani, "Wrong" ifadesini içermeyen tüm satırlar ekrana yazdırılır.

        - bu iki komut pipe (`|`) işaretiyle (`sort sonuc.txt | grep -v "Wrong"`) birbirine bağlanmıştır. bu, bir komutun çıktısını diğerine iletmek için kullanılır. yani, `sort` komutunun çıktısı grep komutuna girer ve "Wrong" ifadesini içermeyen satırlar ekrana yazdırılır. bu şekilde, işlemler sırayla gerçekleştirilir ve sonuçlar filtrelenir.
    
    ![](https://i.ibb.co/z21rrDW/image.png)

    - yeni parola: `p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d`

- başka bir şekilde de yapabiliriz.
    
    - her döngü arasına 0.1 saniyelik bekleme ekleyelim. bunun için sleep komutunu kullanabiliriz.

    ```bash
    #!/bin/bash
    process_lines() {
        while IFS= read -r line; do
            while true; do
                if output=$(echo "$line" | nc -w 2 localhost 30002 2>&1); then
                    echo "$output" >> sonuc.txt
                    break
                fi
            done
            sleep 0.01s
        done < "possible.txt"
    }
    process_lines
    ```

    - bu script:
        
        - daha önceden yazdığımız possible.txt dosyasından her satırı tek tek okuyacak

        - her satırı netcat ile localhost'a 30002 portuna gönderecek

        - her satır için çalışan netcat dönüşünü (return) sonuc.txt'ye ekleyecek.

        - `#!/bin/bash:` bu satır, bash betiğinin yürütülebilir olduğunu belirtir. betiğin bir bash kabuğunda çalıştırılacağını ifade eder.

        - `process_lines()` bu satır, process_lines adında bir fonksiyon tanımlar. fonksiyonun içindeki komutlar, bu fonksiyon çağrıldığında çalıştırılacaktır.

        - `while ifs= read -r line; do:` bu satır, possible.txt dosyasındaki her satırı tek tek işlemek için bir döngü başlatır. her satır, line değişkenine atanır.

        - `while true; do:` sonsuz bir döngü başlatır. her döngü adımında, nc komutunun çalışma durumu kontrol edilecek ve gerekirse tekrar denenecek.

        - `output=$(echo "$line" | nc -w 2 localhost 30002 2>&1):` bu ifade, `echo "$line" | nc -w 2 localhost 30002` komutunu çalıştırır ve bu komutun çıktısını output değişkenine atar. burada:

            - `echo "$line"`: line değişkeninin değerini (possible.txt dosyasından okunan her satır) standart çıktıya yazdırır.
            - `|`: bu, "pipe" operatörüdür ve bir komutun çıktısını başka bir komuta giriş olarak sağlar.
            - `nc -w 2 localhost 30002`: bu, nc komutunu çalıştırır ve -w 2 seçeneği ile 2 saniyelik bir zaman aşımı belirler. localhost üzerindeki `30002` numaralı bağlantı noktasına bir ağ bağlantısı kurmaya çalışır.

            - `2>&1`: bu, standart hata çıktısını (`stderr`) standart çıktıya (`stdout`) yönlendirir. bu sayede, herhangi bir hata mesajı da output değişkenine atanır.

            - yani, bu satır, nc komutunu çalıştırarak bir bağlantı kurar ve output değişkenine bu komutun çıktısını atar. eğer bağlantı kurma işlemi başarılı ise (yani, herhangi bir hata olmadan işlem tamamlanırsa), then bloğu içindeki komutlar çalıştırılır.

        - `echo "$output" >> sonuc.txt:` komutun çıktısını sonuc.txt dosyasına ekler.

        - `break:` iç içe döngülerin içinde bulunduğu döngüden çıkar. yani, while true döngüsünden çıkar ve bir sonraki satıra geçer. diğer yazılım dillerinde gördüğümüz break ile aynı.

        - `done:` iç içe döngülerin iç döngüsünün sonunu belirtir.

        - `sleep 0.01s:` her işlem arasında 0.01 saniye bekleme süresi ekler.

        - `done < "possible.txt":` dış döngünün sonunu belirtir ve possible.txt dosyasındaki satırların sonuna gelindiğini ifade eder.

        - `process_lines:` tanımlanan process_lines fonksiyonunu çağırır. bu, betiğin çalışmasını başlatır.

        - eğer yine sorun çıkarırsa `sleep 0.01s` değerini arttırabiliriz.

        - `nano` ile bu scripti `bekleyerek.sh` olarak kaydedelim.

        - `chmod +x bekleyerek.sh` ile çalıştırma yetkilerini verelim

        - `./bekleyerek.sh` ile çalıştırıp ~3 dakika bekleyelim.

    - betiğin daha gelişmiş ve hızlı hali (aynı anda 5 işlem yaptırdığımız için):

        ```bash
        #!/bin/bash
        process_lines() {
            cat "possible.txt" | xargs -P 5 -I {} -n 1 sh -c '
                while true; do
                    if output=$(echo "$1" | nc -w 2 localhost 30002 2>&1); then
                        echo "$output" >> hizlisonuc.txt
                        break
                    fi
                    sleep 0.01
                done
            ' sh {}
        }
        process_lines
        ```
    
    - sonunda scriptin tamamlandığını göreceğiz. bütün return değerlerini `sonuc.txt` dosyasına yazdı.

    - uyarı: bu, önerdikleri yöntem değil. bu yöntemle, her seferinde tekrar tekrar bağlantı yapmış oluruz.

    - şimdi bu sonuc.txt dosyasından şifreyi ayıklayalım. `sort sonuc.txt | grep -v "Wrong"` komutunu uygulayalım.

        - `sort sonuc.txt`: bu komut, sonuc.txt dosyasındaki içeriği sıralar. sıralama, satırların alfabetik olarak küçükten büyüğe veya büyükten küçüğe sıralanması anlamına gelir. bu durumda, satırlar varsayılan olarak alfabetik olarak sıralanacaktır.

        - `grep -v "Wrong"`: bu komut, grep aracını kullanarak belirli bir metni içermeyen satırları ekrana yazdırır. `-v` parametresi, belirtilen metni içermeyen satırları seçmek için kullanılır. yani, "Wrong" ifadesini içermeyen tüm satırlar ekrana yazdırılır.

        - bu iki komut pipe (`|`) işaretiyle (`sort sonuc.txt | grep -v "Wrong"`) birbirine bağlanmıştır. bu, bir komutun çıktısını diğerine iletmek için kullanılır. yani, `sort` komutunun çıktısı grep komutuna girer ve "Wrong" ifadesini içermeyen satırlar ekrana yazdırılır. bu şekilde, işlemler sırayla gerçekleştirilir ve sonuçlar filtrelenir.
    
    ![](https://i.ibb.co/z21rrDW/image.png)

- yeni parola: `p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d`

### Bandit Level 25 -> 26

- ssh ile bağlanalım: `ssh bandit25@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d`

- `ls` ile `bandit26.sshkey` adında bir dosya olduğunu gördük. bunu aktarmamız gerekecek.

- bağlantıyı `logout` veya `exit` ile kapatalım.

- dosyayı bu komutla lokale indirelim: `scp -P 2220 bandit25@bandit.labs.overthewire.org:bandit26.sshkey .`

- cat: `cat bandit26.sshkey`

    ```
    -----BEGIN RSA PRIVATE KEY-----
    MIIEpQIBAAKCAQEApis2AuoooEqeYWamtwX2k5z9uU1Afl2F8VyXQqbv/LTrIwdW
    pTfaeRHXzr0Y0a5Oe3GB/+W2+PReif+bPZlzTY1XFwpk+DiHk1kmL0moEW8HJuT9
    /5XbnpjSzn0eEAfFax2OcopjrzVqdBJQerkj0puv3UXY07AskgkyD5XepwGAlJOG
    xZsMq1oZqQ0W29aBtfykuGie2bxroRjuAPrYM4o3MMmtlNE5fC4G9Ihq0eq73MDi
    1ze6d2jIGce873qxn308BA2qhRPJNEbnPev5gI+5tU+UxebW8KLbk0EhoXB953Ix
    3lgOIrT9Y6skRjsMSFmC6WN/O7ovu8QzGqxdywIDAQABAoIBAAaXoETtVT9GtpHW
    qLaKHgYtLEO1tOFOhInWyolyZgL4inuRRva3CIvVEWK6TcnDyIlNL4MfcerehwGi
    il4fQFvLR7E6UFcopvhJiSJHIcvPQ9FfNFR3dYcNOQ/IFvE73bEqMwSISPwiel6w
    e1DjF3C7jHaS1s9PJfWFN982aublL/yLbJP+ou3ifdljS7QzjWZA8NRiMwmBGPIh
    Yq8weR3jIVQl3ndEYxO7Cr/wXXebZwlP6CPZb67rBy0jg+366mxQbDZIwZYEaUME
    zY5izFclr/kKj4s7NTRkC76Yx+rTNP5+BX+JT+rgz5aoQq8ghMw43NYwxjXym/MX
    c8X8g0ECgYEA1crBUAR1gSkM+5mGjjoFLJKrFP+IhUHFh25qGI4Dcxxh1f3M53le
    wF1rkp5SJnHRFm9IW3gM1JoF0PQxI5aXHRGHphwPeKnsQ/xQBRWCeYpqTme9amJV
    tD3aDHkpIhYxkNxqol5gDCAt6tdFSxqPaNfdfsfaAOXiKGrQESUjIBcCgYEAxvmI
    2ROJsBXaiM4Iyg9hUpjZIn8TW2UlH76pojFG6/KBd1NcnW3fu0ZUU790wAu7QbbU
    i7pieeqCqSYcZsmkhnOvbdx54A6NNCR2btc+si6pDOe1jdsGdXISDRHFb9QxjZCj
    6xzWMNvb5n1yUb9w9nfN1PZzATfUsOV+Fy8CbG0CgYEAifkTLwfhqZyLk2huTSWm
    pzB0ltWfDpj22MNqVzR3h3d+sHLeJVjPzIe9396rF8KGdNsWsGlWpnJMZKDjgZsz
    JQBmMc6UMYRARVP1dIKANN4eY0FSHfEebHcqXLho0mXOUTXe37DWfZza5V9Oify3
    JquBd8uUptW1Ue41H4t/ErsCgYEArc5FYtF1QXIlfcDz3oUGz16itUZpgzlb71nd
    1cbTm8EupCwWR5I1j+IEQU+JTUQyI1nwWcnKwZI+5kBbKNJUu/mLsRyY/UXYxEZh
    ibrNklm94373kV1US/0DlZUDcQba7jz9Yp/C3dT/RlwoIw5mP3UxQCizFspNKOSe
    euPeaxUCgYEAntklXwBbokgdDup/u/3ms5Lb/bm22zDOCg2HrlWQCqKEkWkAO6R5
    /Wwyqhp/wTl8VXjxWo+W+DmewGdPHGQQ5fFdqgpuQpGUq24YZS8m66v5ANBwd76t
    IZdtF5HXs2S5CADTwniUS5mX1HO9l5gUkk+h0cH5JnPtsMCnAUM+BRY=
    -----END RSA PRIVATE KEY-----
    ```

- indirdiğimiz dosya ile ssh'e bağlanalım. bunun için ssh `-i` parametresini kullanarak private key belirtebiliriz.

- `ssh bandit26@bandit.labs.overthewire.org -p 2220 -i bandit26.sshkey` 
    
    - hata mesajı: `Permissions 0640 for 'bandit26.sshkey' are too open.`

    - dosyayı sadece bize ait olarak ayarlayalım: `chmod 700 bandit26.sshkey`

    - dosya artık sadece bana ait: `ls -l`:

    `-rw------- 1 fr0stb1rd fr0stb1rd 1679 May 16 15:49  bandit26.sshkey`

- tekrar: `ssh bandit26@bandit.labs.overthewire.org -p 2220 -i bandit26.sshkey`

- yeni bir hata mesajı alıyoruz: `Connection to bandit.labs.overthewire.org closed.`

- karşı sunucu anında bağlantıyı sonlandırıyor. bağlantıdan sonra bir bash spawnlamaya çalışalım. böylece yeni shell'imiz kapanmaz.

- her kullanıcının bir varsayılan kabuk (`shell`) ayarı vardır. bu özellikle ssh kullanılırken önemlidir, çünkü bu varsayılan kabuk, gösterilecek olan kabuktur. bir kullanıcının varsayılan kabuğunun ne olduğu bilgisi, `/etc/passwd` dosyasındaki kullanıcı satırının sonunda bulunabilir.

- `bandit25` olarak yeniden giriş yapıp `bandit26` kabuğunu öğrenelim.

- ssh ile bağlanalım: `ssh bandit25@bandit.labs.overthewire.org -p 2220`

- önceki seviyenin parolasını girelim: `p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d`

- `bandit26` için olan bash'i bulalım: `cat /etc/passwd | grep bandit26`

- `bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext`

- cat: `cat /usr/bin/showtext`

    ```bash
    #!/bin/sh
    export TERM=linux
    exec more ~/text.txt
    exit 0
    ```

    - `export TERM=linux`: Bu satır, TERM ortam değişkeninin değerini 'linux' olarak ayarlar. TERM değişkeni, terminal türünü belirtir ve betiğin düzgün bir şekilde çalışması için bazı durumlarda gereklidir. `linux`, terminalin Linux türü olduğunu belirtir.

    - `more`, dosyaları etkileşimli bir modda görüntülemeyi sağlayan bir kabuk komutudur. özellikle, bu etkileşimli mod, dosyanın içeriğinin terminal penceresinde tam olarak görüntülenemeyecek kadar büyük olduğu durumlarda çalışır. bu etkileşimli modda izin verilen bir komut `v`'dir. bu komut dosyayı `vim` adlı düzenleyicide açar.

    - vim bir metin düzenleyicidir. ayrıca kabuk komutlarını çalıştırmanızı sağlar. kısıtlanmış bir ortamdan çıkmak ve bir kabuk oluşturmak için vim'i kullanmak mümkündür. kullanıcının varsayılan kabuğunu oluşturmak için, komut `:shell` kullanılır. kabuğu `/bin/bash` olarak değiştirmek için komut `:set shell=/bin/sh`'dir.

- o zaman terminal penceresini küçülterek işleme devam edelim. böylece `more` işlemine girebiliriz.

- `exit` ile çıkış yapalım.

- `ssh bandit26@bandit.labs.overthewire.org -p 2220 -i bandit26.sshkey` 

    ![](https://i.ibb.co/vZQVm4V/image.png)

- görüldüğü gibi tüm içerik gösterilmiyor. daha fazla içeriği görmek için kaydırma yapmamızı bekleyen bir more komutumuz var, bu komut çalışmasını tamamladığında ise `exit 0` yürütülüyor. yani komutu ortasında durduruyoruz.

- şimdi etkileşimli mod özelliğini kullanabiliriz. etkileşimli modda `v` (görsel mod), belirli metin alanlarını görsel olarak vurgulamanıza (seçmenize) ve onlar üzerinde komut çalıştırmanıza izin verir.

- `v` tuşuna basalım ve vim'e girelim. vim'de `:set shell=/bin/bash` komutu, harici komutları çalıştırırken vim tarafından kullanılan kabuğu değiştirmek için kullanılır. bu komut, kabuğu genellikle bash kabuğu olan `/bin/bash` olarak ayarlar.`:set shell=/bin/bash` diyelim ve bu işlemi gerçekleştirelim.

- şimdi `:shell` diyerek ayarladığımız bash'i çalıştıralım.

    ![](https://i.ibb.co/YDFLLVP/image.png)

- ve bandit26 olarak yeni bir shell açtık: `bandit26@bandit:~$` artık terminal boyutunu büyütebiliriz.

- bandit26 için anahtarı bulalım: `cat /etc/bandit_pass/bandit26`

- yeni parola: `c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1`

### Bandit Level 26 -> 27

- terminal penceremizi küçültelim.

- ssh ile bağlanalım: `ssh bandit26@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1`

- `more` sözcüğü belirince `v` diyelim.

- `:set shell=/bin/bash` ile terminali ayarlayalım.

- `:shell` diyerek ayarladığımız bash'i çalıştıralım, terminal penceresini artık büyütebiliriz.

- `ls -l` diyerek ne var ne yok diyebakalım. `bandit27-do` isminde bir dosya var ve suid yetkisine sahip. programını deneyelim.

    ![](https://i.ibb.co/4FBMN7X/image.png)

- bu, bandit27 kullanıcısı iel komut çalıştırmamızı sağlayacak. o halde parolayı almaya çalışalım.

- `./bandit27-do cat /etc/bandit_pass/bandit27`

- yeni parola: `YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS`

### Bandit Level 27 -> 28

- ssh ile bağlanalım: `ssh bandit27@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS`

- `ssh://bandit27-git@localhost/home/bandit27-git/repo` adresinde bir git reposu varmış. bunu klonlamamızı istemiş. parola bu seviyenin parolasıyla aynıymış. ayrıca port 2220'da çalışıyormuş.

- `mktemp -d` ile yeni bir temp dizin oluşturalım. benim dizinim burası: `/tmp/tmp.pHaDrLfaAc`. isim farklı olabilir. bu dizine gidelim. cd: `cd /tmp/tmp.pHaDrLfaAc`

- `git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo`

    ![](https://i.ibb.co/d0qBm3q/image.png)

- yeni parola: `AVanL161y9rsbcJIsFHuw35rjaOM19nR`

### Bandit Level 28 -> 29

- ssh ile bağlanalım: `ssh bandit28@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `AVanL161y9rsbcJIsFHuw35rjaOM19nR`

- `ssh://bandit28-git@localhost/home/bandit28-git/repo` adresinde bir git reposu varmış, 2220 portundaymış, parola da şu anki seviyenin parolasıymış.

- `mktemp -d` ile yeni bir temp dizin oluşturalım. benim dizinim burası: `/tmp/tmp.bU7UdKcIu4`. isim farklı olabilir. bu dizine gidelim. cd: `cd /tmp/tmp.bU7UdKcIu4`

- `git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo`

    ![](https://i.ibb.co/dpLpLR2/image.png)

- içeride bir readme dosyası var ancak parola sansürlenmiş. git geçmişini kontrol edelim: `git log`

    ![](https://i.ibb.co/CVtkJCm/image.png)

- `fix info leak` commitinden de anlayabileceğimiz gibi, son commit'te parolayı xxx olarak değiştirmiş olma ihtimalleri yüksek. önceki commiti görüntüleyelim: 

    ![](https://i.ibb.co/nPmTnyy/image.png)

- `git show f08b9cc63fa1a4602fb065257633c2dae6e5651b` ile baktığımızda daha önceki commit'te parolayı readme dosyasına yazmış. son sürümde  ise xxx olarak değiştirmiş. tam tahmin ettiğimiz gibi.

- bu işlemi git checkout ile de yapabiliriz.

    - `git checkout f08b9cc63fa1a4602fb065257633c2dae6e5651b`

    ![](https://i.ibb.co/QFP7rxz/image.png)

- yeni parola: `tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S`

### Bandit Level 29 -> 30

- ssh ile bağlanalım: `ssh bandit29@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S`

- `ssh://bandit29-git@localhost/home/bandit29-git/repo` adresinde bir git reposu varmış, 2220 portundaymış, parola da şu anki seviyenin parolasıymış.

- `mktemp -d` ile yeni bir temp dizin oluşturalım. benim dizinim burası: `/tmp/tmp.NMXrq4miBS`. isim farklı olabilir. bu dizine gidelim. cd: `cd /tmp/tmp.NMXrq4miBS`

- `git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo`

    ![](https://i.ibb.co/2jJgpWS/image.png)

- 'No passwords in production!' cümlesi, başka dallar (branches) olabileceği izlenimini veriyor. bu yüzden kontrol edelim: `git branch -a`

    ![](https://i.ibb.co/8s3F0kZ/image.png)

- tüm branşları sıra sıra kontrol edelim: `git checkout dev`

- `ls` ile listeleyip `cat README.md` dersek:

    ![](https://i.ibb.co/TL55zf7/image.png)

- yeni parola: `xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS`

### Bandit Level 30 -> 31

- ssh ile bağlanalım: `ssh bandit30@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS`

- `ssh://bandit30-git@localhost/home/bandit30-git/repo` adresinde bir git reposu varmış, 2220 portundaymış, parola da şu anki seviyenin parolasıymış.

- `mktemp -d` ile yeni bir temp dizin oluşturalım. benim dizinim burası: `/tmp/tmp.qw27gRj8KF`. isim farklı olabilir. bu dizine gidelim. cd: `cd /tmp/tmp.qw27gRj8KF`

- `git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo`

- `cd repo` ile içine girip `ls` dedik ve listeledik. `cat README.md` ile içine bakınca bizime dalga geçti:

    ![](https://i.ibb.co/HBWVsYj/image.png)

- `just an epmty file... muahaha` dedi. başka branşları kontrol edelim: `git branch -a`

    ```bash
    bandit30@bandit:/tmp/tmp.qw27gRj8KF/repo$ git branch -a
    * master
      remotes/origin/HEAD -> origin/master
      remotes/origin/master
    bandit30@bandit:/tmp/tmp.qw27gRj8KF/repo$ 
    ```
- başka branş yok, log yok, hiçbir şey yok. bir de tag'e bakalım. git tag'ini kontrol ettiğimizde, `secret` adlı tarihte bir nokta buluyoruz. `git show secret` dersek:

    ![](https://i.ibb.co/R9NmMWx/image.png)

- yeni parola: `OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt`

### Bandit Level 31 -> 32

- ssh ile bağlanalım: `ssh bandit31@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt`

- `ssh://bandit31-git@localhost/home/bandit31-git/repo` adresinde bir git reposu varmış, 2220 portundaymış, parola da şu anki seviyenin parolasıymış.

- `mktemp -d` ile yeni bir temp dizin oluşturalım. benim dizinim burası: `/tmp/tmp.IU9AtQ0u0I`. isim farklı olabilir. bu dizine gidelim. cd: `cd /tmp/tmp.IU9AtQ0u0I`

- `git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo`

- klonlama bitince `repo` dizinindeki readme dosyasında şöyle yazıyor:

    ```
    This time your task is to push a file to the remote repository.

    Details:
        File name: key.txt
        Content: 'May I come in?'
        Branch: master
    ```
- dediklerini yapmak için,

    - bir `txt` dosyası oluşturacağız ve adı `key.txt` olacak.
    
    - içine `May I come in?` yazacağız
    
    - `master` branşına `push`'layacağız.

- o halde yapalım: `echo -n 'May I come in?' > key.txt`

- `git add key.txt` dediğimizde ya `.gitignore` dosyasında txt dosyaları için olan engeli kaldıracağız ya da `-f` parametresi ile `force` olarak push edeceğiz.

- `git add key.txt -f` diyerek zorla ekledik.

- `git commit -m 'ekleme'` ile dosyayı ekledik.

- `git push` ile master branşına push etmeye çalıştık.

    ![](https://i.ibb.co/KG5KDq2/image.png)

    - bu komutu `git push origin master` olarak kullanmak daha medenicedir ama bu şekilde kullanırsanız da kimse sizi bıçaklamaz (opsiyonel)

- yeni parola: `rmCBvG56y58BXzv98yZGdO7ATVL5dW8y`

### Bandit Level 32 -> 33

- ssh ile bağlanalım: `ssh bandit32@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `rmCBvG56y58BXzv98yZGdO7ATVL5dW8y`

`ls` dediğimizde `LS` şeklinde büyük karakterlerle çalıştıran bir shell'e denk geldik.

- linux'ta, yerel değişkenler, kabuk değişkenleri ve ortam değişkenleri olmak üzere değişkenler bulunur. bu değişkenlerin adları yalnızca büyük harflerle yazılır. Komut satırında `VAR_NAME=var_value` yazarak tanımlanırlar. bir değişkenin içeriğini görmek için `echo $VAR_NAME` yazabilirsiniz. tüm ortam değişkenlerini yazdırmak için printenv kullanabilirsiniz. bilmekte fayda olan bazı yaygın değişkenler şunlardır:

    - `TERM`: geçerli terminal emülasyonu
    - `HOME`: geçerli kullanıcıya ait ev dizininin yolu
    - `LANG`: geçerli yerel ayarları
    - `PATH`: komutların çalıştırılacağı dizinlerin listesi
    - `PWD`: geçerli çalışma dizininin yolu
    - `SHELL`: geçerli kullanıcının kabuğunun yolu
    - `USER`: geçerli oturum açmış kullanıcı

- linux'ta büyük harfle yazılan şeyler değişkenlerdir. özellikle, $0 değişkeni bir kabuğa referans içerir. bunu kendi makinenizde echo $0 yazarak görebilirsiniz. bu sayede büyük harf kabuğundan çıkabilir ve komutları tekrar kullanabiliriz.

- örneğin: `./betik.sh arg1 arg2 arg3` şeklinde bir komut girip çalıştırırsak:

    - `$0`: `./betik.sh`

    - `$1`: `.arg1`

    - `$2`: `arg2`

    - `$3`: `arg3` olacaktır. o halde bizim senaryomuzda şu anda `$0`, shell'e yani bir `sh` komutuna referanstır.
    
    `sh uppercase.sh` diye çalıştırıldığını düşünürsek:

        - `$0`: `sh`

        - `$1`: `uppercase.sh`

- `$0` yazıp denersek, artık normal bir shell'e sahibiz.

    ```bash
    >> $0
    $ ls -la
    total 36
    drwxr-xr-x  2 root     root      4096 Oct  5  2023 .
    drwxr-xr-x 70 root     root      4096 Oct  5  2023 ..
    -rw-r--r--  1 root     root       220 Jan  6  2022 .bash_logout
    -rw-r--r--  1 root     root      3771 Jan  6  2022 .bashrc
    -rw-r--r--  1 root     root       807 Jan  6  2022 .profile
    -rwsr-x---  1 bandit33 bandit32 15128 Oct  5  2023 uppershell
    ```

- burada göreceğimiz gibi:

    `-rwsr-x---  1 bandit33 bandit32 15128 Oct  5  2023 uppershell`

    - uppershell dosyası bandit33 ayrıcalıkları ile çalışıyor. yani şu anda içinde bulunduğumuz shell, bandit33 kullanıcısı yetkilerine sahip. bunu kanıtlamak için `whoami` veya `id` kullanalım.

    ![](https://i.ibb.co/JFdwLtf/image.png)

- bandit33 için anahtarı bulalım: `cat /etc/bandit_pass/bandit33`

- yeni parola: `odHo63fHiFqcWWJG9rLiLDtPm45KzUKy`

### Bandit Level 33 -> 34

- ssh ile bağlanalım: `ssh bandit33@bandit.labs.overthewire.org -p 2220`

- önceki seviyede bulduğumuz parolayı girelim: `odHo63fHiFqcWWJG9rLiLDtPm45KzUKy`

    ```
    bandit33@bandit:~$ ls -l
    total 4
    -rw------- 1 bandit33 bandit33 430 Oct  5  2023 README.txt
    bandit33@bandit:~$ cat README.txt 
    Congratulations on solving the last level of this game!

    At this moment, there are no more levels to play in this game. However, we are constantly working
    on new levels and will most likely expand this game with more levels soon.
    Keep an eye out for an announcement on our usual communication channels!
    In the meantime, you could play some of our other wargames.

    If you have an idea for an awesome new level, please let us know!
    ```

- ve oyunu bitirdik.

## Notlar

- her oyun arası `exit` veya `logout` ile oturumu sonlandırdık. çünkü `su bandit` gibi oturum değiştirmeye izin vermiyor.

- terminalden kopyalama işlemini metni seçtikten sonra `ctrl+shift+c` ile, terminale yapıştırma işlemini `ctrl+shift+v` ile yapabilirsiniz.

- bu makale, linux temellerini gerçekten pratik yaparak deneyimlemenizi sağlayacak. kafanızda bundan önce `ls ile cd'yi öğrendim ben artık linux biliyorum` düşüncesi varsa bunu silmeye yarayacak. `you know nothing Jon Snow`

- seviyeleri bitirdikten sonra, gidip video çekin, not alın, gidip siz de makale şeklinde yazın. benden daha da güzelini yapın. daha da açıklayıcı olun. bunları yapmayacaksanız gidin kafanızı çöp kutusuna sokun daha iyi.

- yeni yazıda ya da projede görüşmek dileğiyle, esenlikler...
