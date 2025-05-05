---
title: OverTheWire Krypton Çözümleri - Adım Adım Rehber (Türkçe)
published: 2024-06-17
updated: 2024-06-17
description: 'A comprehensive Turkish walkthrough guide for solving the OverTheWire Krypton CTF challenges, focusing on cryptography concepts'
image: ''
tags: [Security, Cryptography, CTF, Tutorial, Walkthrough]
category: 'Tutorial'
draft: false
---

## Video

uzakta...

## Walkthrough

Oyun Linki: [overthewire.org/wargames/Krypton/](https://overthewire.org/wargames/Krypton/)

### Krypton Level 0 -> 1

- Verilen bilgilere göre host: `krypton.labs.overthewire.org` port: `2231`

    ```
    Welcome to Krypton! The first level is easy. The following string encodes the password using Base64:

    S1JZUFRPTklTR1JFQVQ=

    Use this password to log in to krypton.labs.overthewire.org with username krypton1 using SSH on port 2231. You can find the files for other levels in /krypton/
    ```

- `S1JZUFRPTklTR1JFQVQ=` değerinin base64 karşılığını istemiş. bunun için online araçları kullanabiliriz. terminalden şu şekilde bulabiliriz:

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi]
    └─$ echo S1JZUFRPTklTR1JFQVQ= | base64 -d
    KRYPTONISGREAT
    ```

- Kolay yoldan [bu](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)&input=UzFKWlVGUlBUa2xUUjFKRlFWUT0) aracı kullanarak da yapabilirdik.

- yeni parola: `KRYPTONISGREAT`

### Krypton Level 1 -> 2

- ssh ile bağlanalım: `ssh krypton1@krypton.labs.overthewire.org -p 2231`

- önceki seviyede bulduğumuz parolayı girelim: `KRYPTONISGREAT`

    ```
    The password for level 2 is in the file `krypton2`. It is `encrypted` using a simple rotation. It is also in non-standard ciphertext format. When using alpha characters for cipher text it is normal to group the letters into 5 letter clusters, regardless of word boundaries. This helps obfuscate any patterns. This file has kept the plain text word boundaries and carried them to the cipher text. Enjoy!
    ```

- Önceki seviyede bahsedildiği üzere `/krypton` dizinine gidip `ls -la` ile listeleyelim:

    ```bash
    krypton1@bandit:~$ cd /krypton/
    krypton1@bandit:/krypton$ ls -la
    total 36
    drwxr-xr-x  9 root root 4096 Jun 16 02:49 .
    drwxr-xr-x 25 root root 4096 Jun 16 02:49 ..
    drwxr-xr-x  2 root root 4096 Jun 16 02:49 krypton1
    drwxr-xr-x  2 root root 4096 Jun 16 02:49 krypton2
    drwxr-xr-x  2 root root 4096 Jun 16 02:49 krypton3
    drwxr-xr-x  2 root root 4096 Jun 16 02:49 krypton4
    drwxr-xr-x  2 root root 4096 Jun 16 02:49 krypton5
    drwxr-xr-x  3 root root 4096 Jun 16 02:49 krypton6
    drwxr-xr-x  2 root root 4096 Jun 16 02:49 krypton7
    krypton1@bandit:/krypton$ 
    ```

- `krypton1` dizinine gidip listeleyelim:

    ```bash
    krypton1@bandit:/krypton$ cd krypton1/
    krypton1@bandit:/krypton/krypton1$ ls -la
    total 16
    drwxr-xr-x 2 root     root     4096 Jun 16 02:49 .
    drwxr-xr-x 9 root     root     4096 Jun 16 02:49 ..
    -rw-r----- 1 krypton1 krypton1   26 Jun 16 02:49 krypton2
    -rw-r----- 1 krypton1 krypton1  882 Jun 16 02:49 README
    krypton1@bandit:/krypton/krypton1$ 
    ```

- readme dosyasını okuyalım:

    ```bash
    krypton1@bandit:/krypton/krypton1$ cat README 
    Welcome to Krypton!

    This game is intended to give hands on experience with cryptography
    and cryptanalysis.  The levels progress from classic ciphers, to modern,
    easy to harder.

    Although there are excellent public tools, like cryptool,to perform
    the simple analysis, we strongly encourage you to try and do these
    without them for now.  We will use them in later excercises.

    ** Please try these levels without cryptool first **


    The first level is easy.  The password for level 2 is in the file 
    'krypton2'.  It is 'encrypted' using a simple rotation called ROT13.  
    It is also in non-standard ciphertext format.  When using alpha characters for
    cipher text it is normal to group the letters into 5 letter clusters, 
    regardless of word boundaries.  This helps obfuscate any patterns.

    This file has kept the plain text word boundaries and carried them to
    the cipher text.

    Enjoy!
    krypton1@bandit:/krypton/krypton1$ 
    ```

- ROT13 şifrelemesi kullanmış ve krypton2 dosyasını okumamızı istiyor. rot şifrelemelerini çözmek için alias atayabiliriz:

    - `alias rot13="tr 'A-Za-z' 'N-ZA-Mn-za-m'"`

    - `alias rot5="tr '0-9' '5-90-4'"`

    - `alias rot="tr 'A-Za-z0-9' 'N-ZA-Mn-za-m5-90-4'"`

- echo ve alias'ımızı kullanarak çözelim:

    ```bash
    krypton1@bandit:/krypton/krypton1$ alias rot13="tr 'A-Za-z' 'N-ZA-Mn-za-m'"
    krypton1@bandit:/krypton/krypton1$ cat krypton2 | rot13 
    LEVEL TWO PASSWORD ROTTEN
    krypton1@bandit:/krypton/krypton1$ 
    ```

- Kolay yoldan [bu](https://gchq.github.io/CyberChef/#recipe=ROT13(true,true,false,13)&input=WVJJUlkgR0pCIENORkZKQkVRIEVCR0dSQQ) aracı kullaranak da yapabilirdik.

- yeni parola: `ROTTEN`

### Krypton Level 2 -> 3

- ssh ile bağlanalım: `ssh krypton2@krypton.labs.overthewire.org -p 2231`

- önceki seviyede bulduğumuz parolayı girelim: `ROTTEN`

- Önceki seviyelerde bahsedildiği üzere `/krypton/krypton2` dizinine gidip listeleyelim:

    ```bash
    krypton2@bandit:/krypton/krypton2$ ls -la
    total 36
    drwxr-xr-x 2 root     root      4096 Jun 16 02:49 .
    drwxr-xr-x 9 root     root      4096 Jun 16 02:49 ..
    -rwsr-x--- 1 krypton3 krypton2 16328 Jun 16 02:49 encrypt
    -rw-r----- 1 krypton3 krypton3    27 Jun 16 02:49 keyfile.dat
    -rw-r----- 1 krypton2 krypton2    13 Jun 16 02:49 krypton3
    -rw-r----- 1 krypton2 krypton2  1815 Jun 16 02:49 README
    krypton2@bandit:/krypton/krypton2$ 
    ```

- readme dosyasını okuyalım:

    ```bash
    krypton2@bandit:/krypton/krypton2$ cat README 
    Krypton 2

    ROT13 is a simple substitution cipher.

    Substitution ciphers are a simple replacement algorithm.  In this example
    of a substitution cipher, we will explore a 'monoalphebetic' cipher.
    Monoalphebetic means, literally, "one alphabet" and you will see why.

    This level contains an old form of cipher called a 'Caesar Cipher'.
    A Caesar cipher shifts the alphabet by a set number.  For example:

    plain:  a b c d e f g h i j k ...
    cipher: G H I J K L M N O P Q ...

    In this example, the letter 'a' in plaintext is replaced by a 'G' in the
    ciphertext so, for example, the plaintext 'bad' becomes 'HGJ' in ciphertext.

    The password for level 3 is in the file krypton3.  It is in 5 letter
    group ciphertext.  It is encrypted with a Caesar Cipher.  Without any 
    further information, this cipher text may be difficult to break.  You do 
    not have direct access to the key, however you do have access to a program 
    that will encrypt anything you wish to give it using the key.  
    If you think logically, this is completely easy.

    One shot can solve it!

    Have fun.

    Additional Information:

    The `encrypt` binary will look for the keyfile in your current working
    directory. Therefore, it might be best to create a working direcory in /tmp
    and in there a link to the keyfile. As the `encrypt` binary runs setuid
    `krypton3`, you also need to give `krypton3` access to your working directory.

    Here is an example:

    krypton2@melinda:~$ mktemp -d
    /tmp/tmp.Wf2OnCpCDQ
    krypton2@melinda:~$ cd /tmp/tmp.Wf2OnCpCDQ
    krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ln -s /krypton/krypton2/keyfile.dat
    krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ls
    keyfile.dat
    krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ chmod 777 .
    krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ /krypton/krypton2/encrypt /etc/issue
    krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ls
    ciphertext  keyfile.dat

    krypton2@bandit:/krypton/krypton2$ 
    ```

- verdiği örneğe bağlı kalarak yeni bir temp dizini oluşturup içine girelim:

    ```bash
    krypton2@bandit:/krypton/krypton2$ mktemp -d
    /tmp/tmp.yPbDUEnXGT
    krypton2@bandit:/krypton/krypton2$ cd /tmp/tmp.yPbDUEnXGT
    krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ 
    ```

- `AAAAA` metni şifreleme yöntemi ile neye dönüşeceğine bakalım:

    ```bash
    krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ ln -s /krypton/krypton2/keyfile.dat
    krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ chmod 777 .
    krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ echo "AAAAA" > encrypt.txt
    krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ /krypton/krypton2/encrypt encrypt.txt
    krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ ls -la
    total 60
    drwxrwxrwx    2 krypton2 krypton2  4096 Jun 17 11:21 .
    drwxrwx-wt 1225 root     root     45056 Jun 17 11:21 ..
    -rw-rw-r--    1 krypton3 krypton2     5 Jun 17 11:21 ciphertext
    -rw-rw-r--    1 krypton2 krypton2     6 Jun 17 11:21 encrypt.txt
    lrwxrwxrwx    1 krypton2 krypton2    29 Jun 17 11:20 keyfile.dat -> /krypton/krypton2/keyfile.dat
    krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ cat encrypt.txt 
    AAAAA
    krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ cat ciphertext 
    MMMMM
    krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ 
    ```

    - `krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ ln -s /krypton/krypton2/keyfile.dat`:

        `/krypton/krypton2/keyfile.dat` dosyasına sembolik bir bağlantı (symlink) oluşturur. Bu, `keyfile.dat` adıyla mevcut dizinde bulunacak ve asıl dosyaya işaret edecektir.

    - `krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ chmod 777 .`:
        
        mevcut dizine (.) tüm kullanıcılar için (sahip, grup ve diğerleri) okuma, yazma ve çalıştırma (execute) izinleri verir.

    - `krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ echo "AAAAA" > encrypt.txt`:
        
        `AAAAA` metnini `encrypt.txt` adlı bir dosyaya yazar. Eğer `encrypt.txt` dosyası daha önce varsa, içeriği silinir ve yeni içerik yazılır.

    - `krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ /krypton/krypton2/encrypt encrypt.txt`:
        
        `/krypton/krypton2/encrypt` programını çalıştırır ve `encrypt.txt` dosyasını parametre olarak bu programa vererek şifreler. Şifrelenmiş sonuç `ciphertext` adlı bir dosyaya yazılır.

    - `krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ ls -la`:
        
        mevcut dizindeki dosyaların ayrıntılı listesini gösterir:
        - `.`: Mevcut dizin
        - `..`: Üst dizin
        - `ciphertext`: Şifrelenmiş metin dosyası (5 bayt uzunluğunda)
        - `encrypt.txt`: Şifrelenecek metin dosyası (6 bayt uzunluğunda, 5 karakter + 1 satır sonu)
        - `keyfile.dat`: Sembolik bağlantı, `/krypton/krypton2/keyfile.dat` dosyasına işaret eder

    - `krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ cat encrypt.txt`:
        
        `encrypt.txt` dosyasının içeriğini ekrana yazdırır. Sonuç: `AAAAA`

    - `krypton2@bandit:/tmp/tmp.yPbDUEnXGT$ cat ciphertext`:
        
        `ciphertext` dosyasının içeriğini ekrana yazdırır. Sonuç: `MMMMM`

- Şifreleme programını `AAAAA` metni ile çalıştırdık çünkü ilk harften kaydırmayı hesaplamak en kolay yoldur.

- Sonuç `MMMMM` oldu. Şimdi sadece anahtarı, `A` harfinden `M` harfine kaydırarak hesaplamamız gerekiyor (1 -> 13).

- `M` 13. karakter olduğuna göre, anahtar `12`dir.

- ROT12 Şifreleme Yöntemi

    - Alfabenin kaydırılması: ROT12, alfabedeki her harfi 12 harf öteye kaydırır. Yani A harfi M olur, B harfi N olur, vb.
    
    - Matematiksel Gösterim: Her harf için, yeni harfi şu formülle bulabilirsiniz:
        
        `Yeni Harf = (Eski Harf Pozisyonu + 12) % 26`.

    - Örnek metin: `HELLO`

        1. `H` harfi, alfabedeki 8. harftir. 8 + 12 = 20, yani `H` harfi `T` olur.
        2. `E` harfi, alfabedeki 5. harftir. 5 + 12 = 17, yani `E` harfi `Q` olur.
        3. `L` harfi, alfabedeki 12. harftir. 12 + 12 = 24, yani `L` harfi `X` olur.
        4. `L` harfi tekrar `X` olur.
        5. `O` harfi, alfabedeki 15. harftir. 15 + 12 = 27, ancak 26 harfli bir alfabe kullanıldığından, 27 % 26 = 1, yani `O` harfi `A` olur.

        Şifrelenmiş metin: `TQXXA`

    - ROT12 ile şifrelenmiş bir metni çözmek için aynı işlemi tersten yaparız, yani her harfi 12 pozisyon geri kaydırırız. Bu da şu formülle yapılır:
    
        `Eski Harf = (Yeni Harf Pozisyonu - 12) % 26`.

    - Örneğin, `TQXXA` metnini deşifre edelim:

        1. `T` harfi, alfabedeki 20. harftir. 20 - 12 = 8, yani `T` harfi `H` olur.
        2. `Q` harfi, alfabedeki 17. harftir. 17 - 12 = 5, yani `Q` harfi `E` olur.
        3. `X` harfi, alfabedeki 24. harftir. 24 - 12 = 12, yani `X` harfi `L` olur.
        4. `X` harfi tekrar `L` olur.
        5. `A` harfi, alfabedeki 1. harftir. 1 - 12 = -11, ancak negatif sonuç alfabede olmadığından, -11 + 26 = 15, yani `A` harfi `O` olur.

        Deşifrelenmiş metin: `HELLO`

    - Terminal ile Şifreleme ve Deşifreleme

        Şifreleme: `echo "METIN" | tr 'A-Za-z' 'M-ZA-Lm-za-l'`

        Deşifreleme: `echo "SIFRELIMETIN" | tr 'A-Za-z' 'O-ZA-No-za-n'`

- ROT12 şifrelemelerini çözmek için alias atayabiliriz:

    - `alias rot12="tr 'A-Za-z' 'O-ZA-No-za-n'"`

- parolayı cat ve ayarladığımız alias ile çözmeye çalışalım:

    `cat /krypton/krypton2/krypton3 | rot12`

    ```bash
    krypton2@bandit:~$ alias rot12="tr 'A-Za-z' 'O-ZA-No-za-n'"
    krypton2@bandit:~$ cat /krypton/krypton2/krypton3 | rot12
    CAESARISEASY
    krypton2@bandit:~$ 
    ```

- Kolay yoldan [bu](https://www.nayuki.io/page/automatic-caesar-cipher-breaker-javascript) aracı veya [bu](https://www.dcode.fr/caesar-cipher) aracı kullanarak da halledebilirdik.

- yeni parola: `CAESARISEASY`

### Krypton Level 3 -> 4

- ssh ile bağlanalım: `ssh krypton3@krypton.labs.overthewire.org -p 2231`

- önceki seviyede bulduğumuz parolayı girelim: `CAESARISEASY`

- Önceki seviyelerde bahsedildiği üzere `/krypton/krypton3` dizinine gidip readme dosyasını okuyalım:

    ```bash
    krypton3@bandit:~$ cd /krypton/krypton3
    krypton3@bandit:/krypton/krypton3$ ls -la
    total 36
    drwxr-xr-x 2 root     root     4096 Jun 16 02:49 .
    drwxr-xr-x 9 root     root     4096 Jun 16 02:49 ..
    -rw-r----- 1 krypton3 krypton3 1542 Jun 16 02:49 found1
    -rw-r----- 1 krypton3 krypton3 2128 Jun 16 02:49 found2
    -rw-r----- 1 krypton3 krypton3  560 Jun 16 02:49 found3
    -rw-r----- 1 krypton3 krypton3   56 Jun 16 02:49 HINT1
    -rw-r----- 1 krypton3 krypton3   37 Jun 16 02:49 HINT2
    -rw-r----- 1 krypton3 krypton3   42 Jun 16 02:49 krypton4
    -rw-r----- 1 krypton3 krypton3  785 Jun 16 02:49 README
    krypton3@bandit:/krypton/krypton3$ cat README 
    Well done.  You've moved past an easy substitution cipher.

    Hopefully you just encrypted the alphabet a plaintext 
    to fully expose the key in one swoop.

    The main weakness of a simple substitution cipher is 
    repeated use of a simple key.  In the previous exercise
    you were able to introduce arbitrary plaintext to expose
    the key.  In this example, the cipher mechanism is not 
    available to you, the attacker.

    However, you have been lucky.  You have intercepted more
    than one message.  The password to the next level is found
    in the file 'krypton4'.  You have also found 3 other files.
    (found1, found2, found3)

    You know the following important details:

    - The message plaintexts are in English (*** very important)
    - They were produced from the same key (*** even better!)


    Enjoy.


    krypton3@bandit:/krypton/krypton3$ 
    ```

- Açıklamada belirtildiğine göre içerik ingilizce olarak yazılmış. Karakter yoğunluğuna göre şifrelemeyi çözelim:

    - `README` ve `foundX` dosyalarını okuyarak elimizdeki şifreli metni inceleyeceğiz.
    - Frekans analizi yaparak şifreli metinden düz metni çıkaracağız.
    - Her harfin (A'dan Z'ye kadar) şifreli metinlerdeki frekansını sayacağız.
    - Frekans analizinde, şifreli metindeki harflerin düz metindeki karşılıklarını bulmak için harflerin dağılımını inceleyeceğiz.
    - İlk olarak, her harfin frekansını bulmak için `tr` ve `wc` komutlarını kullanacağız.
    - Önce bir temp dizin oluşturup dosyaları oraya taşıyalım. Çünkü bu dizinde yeterli izinlere sahip değiliz:

        ```bash
        krypton3@bandit:/krypton/krypton3$ mktemp -d
        /tmp/tmp.mROqtbZfSc
        krypton3@bandit:/krypton/krypton3$ cp * /tmp/tmp.mROqtbZfSc
        krypton3@bandit:/krypton/krypton3$ cd /tmp/tmp.mROqtbZfSc
        krypton3@bandit:/tmp/tmp.mROqtbZfSc$ ls -la
        total 80
        drwx------    2 krypton3 krypton3  4096 Jun 17 12:14 .
        drwxrwx-wt 1264 root     root     45056 Jun 17 12:14 ..
        -rw-r-----    1 krypton3 krypton3  1542 Jun 17 12:14 found1
        -rw-r-----    1 krypton3 krypton3  2128 Jun 17 12:14 found2
        -rw-r-----    1 krypton3 krypton3   560 Jun 17 12:14 found3
        -rw-r-----    1 krypton3 krypton3    56 Jun 17 12:14 HINT1
        -rw-r-----    1 krypton3 krypton3    37 Jun 17 12:14 HINT2
        -rw-r-----    1 krypton3 krypton3    42 Jun 17 12:14 krypton4
        -rw-r-----    1 krypton3 krypton3   785 Jun 17 12:14 README
        krypton3@bandit:/tmp/tmp.mROqtbZfSc$ 
        ```
    
    - Notları okuyalım:

        - HINT1:

            ```bash
            krypton3@bandit:/tmp/tmp.mROqtbZfSc$ cat HINT1 
            Some letters are more prevalent in English than others.
            ```
        - HINT2:

            ```bash
            krypton3@bandit:/tmp/tmp.mROqtbZfSc$ cat HINT2
            "Frequency Analysis" is your friend.
            krypton3@bandit:/tmp/tmp.mROqtbZfSc$ 
            ```

    - Dosyanın (krypton4) orijinal içeriği: `KSVVW BGSJD SVSIS VXBMN YQUUK BNWCU ANMJS`

        - Kolay yoldan [bu](https://www.quipqiup.com/) aracı kullanarak çözebiliriz. Ancak zor olanı yapacağız.

    - Dosyaların İçeriğini Birleştirme:

        ```bash
        cat found1 found2 found3 > combined.txt
        ```
        
        Bu komut `found1`, `found2` ve `found3` dosyalarının içeriklerini `combined.txt` adlı tek bir dosyada birleştirir.

    - Frekans Analizi İçin Script:

        Her harfin frekansını sayan bir döngü oluşturun:

        ```bash
        for i in {A..Z}; do
            echo -n "$i: "
            tr -cd "$i" < combined.txt | wc -c //
        done
        ```

        Bu döngü, A'dan Z'ye kadar her harfin frekansını `combined.txt` dosyasında sayar ve sonuçları ekrana yazdırır.

            - `tr -cd "$i" < combined.txt`: `tr` komutu, belirtilen karakterlerin dışındaki tüm karakterleri siler (`-cd` opsiyonu) ve sadece `$i` karakterini bırakır.

            - `wc -c`: `wc` komutu, `-c` opsiyonu ile karakter sayısını sayar. Böylece, `combined.txt` dosyasında her harfin kaç kez geçtiğini hesaplarız.

        ```bash
        krypton3@bandit:/tmp/tmp.mROqtbZfSc$ for i in {A..Z}; do
                    echo -n "$i: "
                    tr -cd "$i" < combined.txt | wc -c
                done
        A: 55
        B: 246
        C: 227
        D: 210
        E: 64
        F: 28
        G: 227
        H: 4
        I: 19
        J: 301
        K: 67
        L: 60
        M: 86
        N: 240
        O: 12
        P: 2
        Q: 340
        R: 4
        S: 456
        T: 75
        U: 257
        V: 130
        W: 129
        X: 71
        Y: 84
        Z: 132
        krypton3@bandit:/tmp/tmp.mROqtbZfSc$ 
        ```
    - Sıralamaya göre yazdıralım:

        - Basit bir script yazalım:

            ```bash
            for i in {A..Z}; do cat combined.txt | tr -cd $i | wc -c | tr -d '\n'; printf " $i \n"; done | sort -nr
            ```

        1. **For Döngüsü:**
            ```bash
            for i in {A..Z}
            ```
            Bu, `i` değişkenine sırasıyla A'dan Z'ye kadar harfleri atayan bir döngüdür. Yani döngü her çalıştığında `i` değişkeni bir sonraki harfi alır (ilk döngüde A, ikinci döngüde B, vb.).

        2. **Dosya İçeriğini Filtreleme:**
            ```bash
            cat combined.txt | tr -cd $i
            ```
            `cat combined.txt`, `combined.txt` dosyasının içeriğini ekrana yazdırır. Bu içerik `tr -cd $i` komutuna gönderilir. `tr -cd $i` ifadesi, dosya içeriğindeki `i` harfi dışındaki tüm karakterleri siler (yani sadece o harfi bırakır).

        3. **Karakter Sayımı:**
            ```bash
            wc -c
            ```
            `wc -c` komutu, girdideki karakter sayısını sayar. Burada sadece belirli bir harfin kaldığını düşündüğümüzde, bu komut o harfin dosyada kaç kez geçtiğini verir.

        4. **Yeni Satır Karakterini Kaldırma:**
            ```bash
            tr -d '\n'
            ```
            `wc -c` komutu çıktısının sonuna bir yeni satır karakteri ekler. `tr -d '\n'` bu yeni satır karakterini kaldırır, böylece çıktıyı tek bir satırda tutar.

        5. **Harf ve Sayıyı Yazdırma:**
            ```bash
            printf " $i \n"
            ```
            Bu komut, harfin yanına bir boşluk ve ardından bir yeni satır ekleyerek çıktı formatını düzenler. Bu sayede her harfin sayısı ve harf aynı satırda olacak şekilde yazdırılır.

        6. **Çıktıyı Sıralama:**
            ```bash
            done | sort -nr
            ```
            `done` komutu, döngünün bittiğini belirtir ve tüm çıktıyı `sort -nr` komutuna boru hattıyla (`|`) aktarır. `sort -nr` komutu, sayısal olarak tersine sıralama yapar (en yüksekten en düşüğe doğru).

        ```bash
        krypton3@bandit:/tmp/tmp.mROqtbZfSc$ for i in {A..Z}; do cat combined.txt | tr -cd $i | wc -c | tr -d '\n'; printf " $i \n"; done | sort -nr
        456 S 
        340 Q 
        301 J 
        257 U 
        246 B 
        240 N 
        227 G 
        227 C 
        210 D 
        132 Z 
        130 V 
        129 W 
        86 M 
        84 Y 
        75 T 
        71 X 
        67 K 
        64 E 
        60 L 
        55 A 
        28 F 
        19 I 
        12 O 
        4 R 
        4 H 
        2 P 
        krypton3@bandit:/tmp/tmp.mROqtbZfSc$ 
        ```

    - Frekans analizinin sonuçlarını elde ettikten sonra, elde edilen frekansları İngilizce dilindeki harf frekanslarıyla karşılaştırarak hangi harfin hangi harfe dönüştüğünü tahmin edebiliriz. Örneğin, en sık kullanılan harf genellikle `E` harfiyle eşleşir.

    - Elde ettiğiniz frekans bilgilerini kullanarak şifreli metni çözmek için manuel olarak veya bir script yazarak dönüşüm yapabilirsiniz. Örneğin, `E` harfi en sık kullanılan harf ise, en sık görülen şifreli harfi `E` olarak dönüştürebilirsiniz.

    - Örnek Dönüşüm Scripti:

        ```bash
        cat combined.txt | tr 'ŞifreliHarfler' 'DüzMetinHarfler' > decrypted.txt
        ```

    - `S` harfi 456 kez geçtiği için, bunun `E` harfi olduğunu varsayıyoruz (İngilizce'de en sık kullanılan harf).

    - İngilizce'deki harflerin frekans sıralaması: `ETAOINSRHDLUCMFYWGPBVKXQJZ`
        - [letterfrequency.org](http://letterfrequency.org/)
        - ingilizce: `etaoinsrhldcumfpgwybvkxjqz`
        - oxford: `eariotnslcudpmhgbfywkvxzjq`

        ![](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/English_letter_frequency_%28alphabetic%29.svg/1280px-English_letter_frequency_%28alphabetic%29.svg.png)

    - Şifreli metindeki harflerin frekans sıralaması: `SQJUBNGCDZVWMYTXKELAFIORHP`

    - Şifreli metindeki her harfin hangi düz metin harfine karşılık geldiğini bulmak için harf frekanslarını eşleştireceğiz.

    - Bu dönüşümleri uygulamak için `tr` komutunu kullanabiliriz:

        ```bash
        cat krypton4 | tr 'SQJUBNGCDZVWMYTXKELAFIORHP' 'ETAOINSRHDLUCMFYWGPBVKXQJZ'
        ```

    - Bu komut, `krypton4` dosyasındaki şifreli metni, belirlediğimiz harf eşleştirmelerine göre dönüştürerek yazar:

        `WELLU ISEAH ELEKE LYICN MTOOW INURO BNCAE`
    
    - Görünüş göre anlamsız bir yazı ortaya çıktı.

    - combined.txt dosyasını inceleyelim:

        ```bash
        CGZNL YJBEN QYDLQ ZQSUQ NZCYD SNQVU BFGBK GQUQZ QSUQN UZCYD SNJDS UDCXJ ZCYDS NZQSU QNUZB WSBNZ QSUQN UDCXJ CUBGS BXJDS UCTYV SUJQG WTBUJ KCWSV LFGBK GSGZN LYJCB GJSZD GCHMS UCJCU QJLYS BXUMA UJCJM JCBGZ CYDSN CGKDC ZDSQZ DVSJJ SNCGJ DSYVQ CGJSO JCUNS YVQZS WALQV SJJSN UBTSX COSWG MTASN BXYBU CJCBG UWBKG JDSQV YDQAS JXBNS OQTYV SKCJD QUDCX JBXQK BMVWA SNSYV QZSWA LWAKB MVWAS ZBTSS QGWUB BGJDS TSJDB WCUGQ TSWQX JSNRM VCMUZ QSUQN KDBMU SWCJJ BZBTT MGCZQ JSKCJ DDCUE SGSNQ VUJDS SGZNL YJCBG UJSYY SNXBN TSWAL QZQSU QNZCY DSNCU BXJSG CGZBN YBNQJ SWQUY QNJBX TBNSZ BTYVS OUZDS TSUUM ZDQUJ DSICE SGNSZ CYDSN QGWUJ CVVDQ UTBWS NGQYY VCZQJ CBGCG JDSNB JULUJ STQUK CJDQV VUCGE VSQVY DQASJ UMAUJ CJMJC BGZCY DSNUJ DSZQS UQNZC YDSNC USQUC VLANB FSGQG WCGYN QZJCZ SBXXS NUSUU SGJCQ VVLGB ZBTTM GCZQJ CBGUS ZMNCJ LUDQF SUYSQ NSYNB WMZSW TBUJB XDCUF GBKGK BNFAS JKSSG QGWDC USQNV LYVQL UKSNS TQCGV LZBTS WCSUQ GWDCU JBNCS UESGN SUDSN QCUSW JBJDS YSQFB XUBYD CUJCZ QJCBG QGWQN JCUJN LALJD SSGWB XJDSU COJSS GJDZS GJMNL GSOJD SKNBJ STQCG VLJNQ ESWCS UMGJC VQABM JCGZV MWCGE DQTVS JFCGE VSQNQ GWTQZ ASJDZ BGUCW SNSWU BTSBX JDSXC GSUJS OQTYV SUCGJ DSSGE VCUDV QGEMQ ESCGD CUVQU JYDQU SDSKN BJSJN QECZB TSWCS UQVUB FGBKG QUNBT QGZSU QGWZB VVQAB NQJSW KCJDB JDSNY VQLKN CEDJU TQGLB XDCUY VQLUK SNSYM AVCUD SWCGS WCJCB GUBXI QNLCG EHMQV CJLQG WQZZM NQZLW MNCGE DCUVC XSJCT SQGWC GJKBB XDCUX BNTSN JDSQJ NCZQV ZBVVS QEMSU YMAVC UDSWJ DSXCN UJXBV CBQZB VVSZJ SWSWC JCBGB XDCUW NQTQJ CZKBN FUJDQ JCGZV MWSWQ VVAMJ JKBBX JDSYV QLUGB KNSZB EGCUS WQUUD QFSUY SQNSU QVJDB MEDGB QJJSG WQGZS NSZBN WUXBN JDSYS NCBWU MNICI STBUJ ACBEN QYDSN UQENS SJDQJ UDQFS UYSQN SKQUS WMZQJ SWQJJ DSFCG EUGSK UZDBB VCGUJ NQJXB NWQXN SSUZD BBVZD QNJSN SWCGQ ABMJQ HMQNJ SNBXQ TCVSX NBTDC UDBTS ENQTT QNUZD BBVUI QNCSW CGHMQ VCJLW MNCGE JDSSV CPQAS JDQGS NQAMJ JDSZM NNCZM VMTKQ UWCZJ QJSWA LVQKJ DNBME DBMJS GEVQG WQGWJ DSUZD BBVKB MVWDQ ISYNB ICWSW QGCGJ SGUCI SSWMZ QJCBG CGVQJ CGENQ TTQNQ GWJDS ZVQUU CZUQJ JDSQE SBXUD QFSUY SQNST QNNCS WJDSL SQNBV WQGGS DQJDQ KQLJD SZBGU CUJBN LZBMN JBXJD SWCBZ SUSBX KBNZS UJSNC UUMSW QTQNN CQESV CZSGZ SBGGB ISTAS NJKBB XDQJD QKQLU GSCED ABMNU YBUJS WABGW UJDSG SOJWQ LQUUM NSJLJ DQJJD SNSKS NSGBC TYSWC TSGJU JBJDS TQNNC QESJD SZBMY VSTQL DQISQ NNQGE SWJDS ZSNST BGLCG UBTSD QUJSU CGZSJ DSKBN ZSUJS NZDQG ZSVVB NQVVB KSWJD STQNN CQESA QGGUJ BASNS QWBGZ SCGUJ SQWBX JDSMU MQVJD NSSJC TSUQG GSUYN SEGQG ZLZBM VWDQI SASSG JDSNS QUBGX BNJDC UUCOT BGJDU QXJSN JDSTQ NNCQE SUDSE QISAC NJDJB QWQME DJSNU MUQGG QKDBK QUAQY JCUSW BGTQL JKCGU UBGDQ TGSJQ GWWQM EDJSN RMWCJ DXBVV BKSWQ VTBUJ JKBLS QNUVQ JSNQG WKSNS AQYJC USWBG XSANM QNLDQ TGSJW CSWBX MGFGB KGZQM USUQJ JDSQE SBXQG WKQUA MNCSW BGQME MUJQX JSNJD SACNJ DBXJD SJKCG UJDSN SQNSX SKDCU JBNCZ QVJNQ ZSUBX UDQFS UYSQN SMGJC VDSCU TSGJC BGSWQ UYQNJ BXJDS VBGWB GJDSQ JNSUZ SGSCG ASZQM USBXJ DCUEQ YUZDB VQNUN SXSNJ BJDSL SQNUA SJKSS GQGWQ UUDQF SUYSQ NSUVB UJLSQ NUACB ENQYD SNUQJ JSTYJ CGEJB QZZBM GJXBN JDCUY SNCBW DQISN SYBNJ SWTQG LQYBZ NLYDQ VUJBN CSUGC ZDBVQ UNBKS UDQFS UYSQN SUXCN UJACB ENQYD SNNSZ BMGJS WQUJN QJXBN WVSES GWJDQ JUDQF SUYSQ NSXVS WJDSJ BKGXB NVBGW BGJBS UZQYS YNBUS ZMJCB GXBNW SSNYB QZDCG EQGBJ DSNSC EDJSS GJDZS GJMNL UJBNL DQUUD QFSUY SQNSU JQNJC GEDCU JDSQJ NCZQV ZQNSS NTCGW CGEJD SDBNU SUBXJ DSQJN SYQJN BGUCG VBGWB GRBDG QMANS LNSYB NJSWJ DQJUD QFSUY SQNSD QWASS GQZBM GJNLU ZDBBV TQUJS NUBTS JKSGJ CSJDZ SGJMN LUZDB VQNUD QISUM EESUJ SWJDQ JUDQF SUYSQ NSTQL DQISA SSGST YVBLS WQUQU ZDBBV TQUJS NALQV SOQGW SNDBE DJBGB XVQGZ QUDCN SQZQJ DBVCZ VQGWB KGSNK DBGQT SWQZS NJQCG KCVVC QTUDQ FSUDQ XJSCG DCUKC VVGBS ICWSG ZSUMA UJQGJ CQJSU UMZDU JBNCS UBJDS NJDQG DSQNU QLZBV VSZJS WQXJS NDCUW SQJDDSNSM YBGVS ENQGW QNBUS KCJDQ ENQIS QGWUJ QJSVL QCNQG WANBM EDJTS JDSAS SJVSX NBTQE VQUUZ QUSCG KDCZD CJKQU SGZVB USWCJ KQUQA SQMJC XMVUZ QNQAQ SMUQG WQJJD QJJCT SMGFG BKGJB GQJMN QVCUJ UBXZB MNUSQ ENSQJ YNCPS CGQUZ CSGJC XCZYB CGJBX ICSKJ DSNSK SNSJK BNBMG WAVQZ FUYBJ UGSQN BGSSO JNSTC JLBXJ DSAQZ FQGWQ VBGEB GSGSQ NJDSB JDSNJ DSUZQ VSUKS NSSOZ SSWCG EVLDQ NWQGW EVBUU LKCJD QVVJD SQYYS QNQGZ SBXAM NGCUD SWEBV WJDSK SCEDJ BXJDS CGUSZ JKQUI SNLNS TQNFQ AVSQG WJQFC GEQVV JDCGE UCGJB ZBGUC WSNQJ CBGCZ BMVWD QNWVL AVQTS RMYCJ SNXBN DCUBY CGCBG NSUYS ZJCGE CJ
        ```

    - [Bu](http://www.richkni.co.uk/php/crypta/freq.php) aracı kullanarak elde edebileceğimiz bilgiler:

        - En sık kullanılan 3 harfli dizi: `jds` (büyük ihtimalle `the`)
        - Şifredeki "su" büyük ihtimalle "es" 
        - Şifredeki "jc" büyük ihtimalle "ti" 
        - Şifredeki "qn" büyük ihtimalle "ar" 
        - Şifredeki "qgw" büyük ihtimalle "and" 
        - Şifredeki "cbg" büyük ihtimalle "ion" 
        - Şifredeki "x", "f" ("bx" -> "of").
        - Şifredeki "cge" büyük ihtimalle "ing" 
        - Şifredeki "vv" büyük ihtimalle "ll" 
        - Şifredeki "zcydsn" "cipher" 
        - Şifredeki "zqsuqn" "caesar" 
        - "cgznl yjben qydl", "INCRl PTOGR APHl" ve "l" harfini "y" olarak değiştirirsek "IN CRYPTOGRAPHY" olur

        - Kuralı şu şekilde yazalım: `ABCDEFGHIJKLMNOPQRSTUVWXYZ` -> `BOIHGKNJVTWMURXZAQEYSLDFPC`

        | Alfabe    | a | b | c | d | e | f | g | h | i | j | k | l | m | n | o | p | q | r | s | t | u | v | w | x | y | z |
        |-----------|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
        | Şifreleme | b | o | i | h | g | k | n | q | v | i | w | y | u | r | x | z | a | j | e | m | s | l | d | f | p | c |

    - O halde bu komut yerine: `cat krypton4 | tr 'SQJUBNGCDZVWMYTXKELAFIORHP' 'ETAOINSRHDLUCMFYWGPBVKXQJZ'`
        - Bunu kullanmalıyız: `cat krypton4 | tr 'ABCDEFGHIJKLMNOPQRSTUVWXYZ' 'BOIHGKNJVTWMURXZAQEYSLDFPC'`

        ```bash
        krypton3@bandit:/krypton/krypton3$ cat krypton4 | tr 'ABCDEFGHIJKLMNOPQRSTUVWXYZ' 'BOIHGKNJVTWMURXZAQEYSLDFPC'
        WELLD ONETH ELEVE LFOUR PASSW ORDIS BRUTE 
        krypton3@bandit:/krypton/krypton3$ 
        ```
    - Ayrıca [cryptool](https://www.cryptool.org/) aracı ile analiz yapabilirsiniz.
    
    - Ayrıca [bu](http://www.quipqiup.com/) araç yardımıyla `jds=the` ipucunu vererek çözebiliriz:

        - `KSVVW BGSJD SVSIS VXBMN YQUUK BNWCU ANMJS`
        - `jds=the`

    - ve `-2.678` entropi ile metin: `well done the level cour password is brute`
    
        ![](https://i.ibb.co/k8x6qPV/image.png)

- yeni parola: `BRUTE`

### Krypton Level 4 -> 5

- ssh ile bağlanalım: `ssh krypton4@krypton.labs.overthewire.org -p 2231`

- önceki seviyede bulduğumuz parolayı girelim: `brute`

- Parola büyük ihtimalle büyük harflerle: `BRUTE`

- Önceki seviyelerde bahsedildiği üzere `/krypton/krypton4` dizinine gidip readme dosyasını okuyalım:

    ```bash
    krypton4@bandit:/krypton/krypton4$ ls -la
    total 28
    drwxr-xr-x 2 root     root     4096 Jun 16 02:49 .
    drwxr-xr-x 9 root     root     4096 Jun 16 02:49 ..
    -rw-r----- 1 krypton4 krypton4 1740 Jun 16 02:49 found1
    -rw-r----- 1 krypton4 krypton4 2943 Jun 16 02:49 found2
    -rw-r----- 1 krypton4 krypton4  287 Jun 16 02:49 HINT
    -rw-r----- 1 krypton4 krypton4   10 Jun 16 02:49 krypton5
    -rw-r----- 1 krypton4 krypton4 1385 Jun 16 02:49 README
    krypton4@bandit:/krypton/krypton4$ 
    ```

    ```bash
    krypton4@bandit:/krypton/krypton4$ cat README 
    Good job!

    You more than likely used frequency analysis and some common sense
    to solve that one.

    So far we have worked with simple substitution ciphers.  They have
    also been 'monoalphabetic', meaning using a fixed key, and 
    giving a one to one mapping of plaintext (P) to ciphertext (C).
    Another type of substitution cipher is referred to as 'polyalphabetic',
    where one character of P may map to many, or all, possible ciphertext 
    characters.

    An example of a polyalphabetic cipher is called a Vigenère Cipher.  It works
    like this:

    If we use the key(K)  'GOLD', and P = PROCEED MEETING AS AGREED, then "add"
    P to K, we get C.  When adding, if we exceed 25, then we roll to 0 (modulo 26).


    P     P R O C E   E D M E E   T I N G A   S A G R E   E D
    K     G O L D G   O L D G O   L D G O L   D G O L D   G O

    becomes:

    P     15 17 14 2  4  4  3 12  4 4  19  8 13 6  0  18 0  6 17 4 4   3
    K     6  14 11 3  6 14 11  3  6 14 11  3  6 14 11  3 6 14 11 3 6  14
    C     21 5  25 5 10 18 14 15 10 18  4 11 19 20 11 21 6 20  2 8 10 17

    So, we get a ciphertext of:

    VFZFK SOPKS ELTUL VGUCH KR

    This level is a Vigenère Cipher.  You have intercepted two longer, english 
    language messages.  You also have a key piece of information.  You know the 
    key length!

    For this exercise, the key length is 6.  The password to level five is in the usual
    place, encrypted with the 6 letter key.

    Have fun!
    krypton4@bandit:/krypton/krypton4$ 
    ```

    - Şifre çözmeye devam ediyoruz! Şimdiye kadar tek bir harf ile şifreleme gördük. Bu bölümde ise işleri biraz karıştıracağız. 

    - Bu bölümde **çok değişkenli** şifreleme yöntemlerinden biri olan **Vigenère şifresi** ile karşılaşıyoruz. Çok değişkenli olması, şifrelemede kullanılan anahtarın tek bir harften oluşmaması ve metnin içinde değişkenlik göstermesi anlamına geliyor. 

    - Sana verilen ipucu ise anahtarın **6 harften oluştuğu**. Bu bilgi şifreyi çözmende çok işine yarayacak. 

    - Örnek olarak;

        * **Metin (P):** DEVAM ET
        * **Anahtar (K):** ASKERDE

    - Vigenère şifrelemesi şu şekilde yapılır: Her bir harfi metin (P) ile anahtarın (K) aynı konumdaki harfi topla. Eğer toplam 25'ten büyük çıkarsa, 26'ya böl ve kalanı al. 

    - **Örnek:**

        | Metin (P) | D | E | V | A | M |
        |---|---|---|---|---|---|
        | Anahtar (K) | A | S | K | E | R | D |
        | Toplam | 4 | 3 | (19+4)%26=23 | 1 | (13+18)%26=1 |

    - Toplam işleminin sonucu 23 olduğunda, 26'ya bölüp kalanı 3 alıyoruz. 

    - Bu işlem metnin tüm harfleri ve anahtarın döngüsel olarak kullanılarak tüm metin şifrelenene kadar devam eder. 

    - **Şifreli Metin (C):**  HZSGBVQ

    - Artık Vigenère şifresini ve sana verilen ipuçlarını kullanarak şifre çözmeye başlayabilirsin. 

    - Eğer blok boyutunu bilmiyor olsaydık `Kasiski Saldırısı` kullanarak parola uzunluğunu da bulabilirdik. Ancak şu durum için 6 olduğunu bize zaten vermiş.

- Diğer dosyalara bakalım:

    ```bash
    krypton4@bandit:/krypton/krypton4$ cat HINT 
    Frequency analysis will still work, but you need to analyse it
    by "keylength".  Analysis of cipher text at position 1, 6, 12, etc
    should reveal the 1st letter of the key, in this case.  Treat this as
    6 different mono-alphabetic ciphers...

    Persistence and some good guesses are the key!
    ```

    ```bash
    krypton4@bandit:/krypton/krypton4$ cat found1
    YYICS JIZIB AGYYX RIEWV IXAFN JOOVQ QVHDL CRKLB SSLYX RIQYI IOXQT WXRIC RVVKP BHZXI YLYZP DLCDI IKGFJ UXRIP TFQGL CWVXR IEZRV NMYSF JDLCL RXOWJ NMINX FNJSP JGHVV ERJTT OOHRM VMBWN JTXKG JJJXY TSYKL OQZFT OSRFN JKBIY YSSHE LIKLO RFJGS VMRJC CYTCS VHDLC LRXOJ MWFYB JPNVR NWUMZ GRVMF UPOEB XKSDL CBZGU IBBZX MLMKK LOACX KECOC IUSBS RMPXR IPJZW XSPTR HKRQB VVOHR MVKEE PIZEX SDYYI QERJJ RYSLJ VZOVU NJLOW RTXSD LYYNE ILMBK LORYW VAOXM KZRNL CWZRA YGWVH DLCLZ VVXFF KASPJ GVIKW WWVTV MCIKL OQYSW SBAFJ EWRII SFACC MZRVO MLYYI MSSSK VISDY YIGML PZICW FJNMV PDNEH ISSFE HWEIJ PSEEJ QYIBW JFMIC TCWYE ZWLTK WKMBY YICGY WVGBS UKFVG IKJRR DSBJJ XBSWM VVYLR MRXSW BNWJO VCSKW KMBYY IQYYW UMKRM KKLOK YYVWX SMSVL KWCAV VNIQY ISIIB MVVLI DTIIC SGSRX EVYQC CDLMZ XLDWF JNSEP BRROO WJFMI CSDDF YKWQM VLKWM KKLOV CXKFE XRFBI MEPJW SBWFJ ZWGMA PVHKR BKZIB GCFEH WEWSF XKPJT NCYYR TUICX PTPLO VIJVT DSRMV AOWRB YIBIR MVWER QJKWK RBDFY MELSF XPEGQ KSPML IYIBX FJPXR ELPVH RMKFE HLEBJ YMWKM TUFII YSUXE VLJUX YAYWU XRIUJ JXGEJ PZRQS TJIJS IJIJS PWMKK KBEQX USDXC IYIBI YSUXR IPJNM DLBFZ WSIQF EHLYR YVVMY NXUSB SRMPW DMJQN SBIRM VTBIR YPWSP IIIIC WQMVL KHNZK SXMLY YIZEJ FTILY RSFAD SFJIW EVNWZ WOWFJ WSERB NKAKW LTCSX KCWXV OILGL XZYPJ NLSXC YYIBM ZGFRK VMZEH DSRTJ ROGIM RHKPQ TCSCX GYJKB ICSTS VSPFE HGEQF JARMR JRWNS PTKLI WBWVW CXFJV QOVYQ UGSXW BRWCS MSCIP XDFIF OLGSU ECXFJ PENZY STINX FJXVY YLISI MEKJI SEKFJ IEXHF NCPSI PKFVD LCWVA OVCSF JKVKX ESBLM ZJICM LYYMC GMZEX BCMKK LOACX KEXHR MVKBS SSUAK WSSKM VPCIZ RDLCF WXOVL TFRDL CXLRC LMSVL YXGSK LOMPK RGOWD TIXRI PJNIB ILTKV OIQYF SPJCW KLOQQ MRHOW MYYED FCKFV ORGLY XNSPT KLIEL IKSDS YSUXR IJNFR GIPJK MBIBF EHVEW IFAXY NTEXR IEWRW CELIW IVPYX CIOTU NKLDL CBFSN QYSRR NXFJJ GKVCH ISGOC JGMXK UFKGR 
    ```

    ```bash
    krypton4@bandit:/krypton/krypton4$ cat found2
    YYIIA CWVSL PGLVH DSAFD TYYRY YEDRG LYXER BJIEV EPLVX BICNE XRIDT IICXD TIXRI PJNIB ILTYS EWCXE IKVRM VXBIC RRHOE ETFHD LGHBG YZCWZ RQXMU ISDIA YKLOQ DWFQD LCIVA KRBYY IDMLB FSNQY STLYT NJUEQ VCFKT SPCTW AYSBB ZXRLG XRBOE LIUSB SRMPF EMJYR WZPCS UMNJG WVXRE RBRVW IBMVV KRBRR HOLCW WIOPJ JJWVS LJCCC LCFEH DSRTR XOXFJ CECXM KKLOM PGIIK HYSUR YAQMV HSHLT KOXSU BYEDX FJPAY YJIUS PSPGI IKODF JXSJW TLASW FXRMN XFJCM YRGBZ PVKMN EXYXF JWSBI QYRRN OGQCE NICWW SBCMZ PSEGY SISKW RNKFI XFJWM BIQNE GOCMZ IXKWR JJEBI QTGIM YJNRV DLYYP SETPJ WIBGM TBINJ MTUEX HRMVR ISSBZ PVLYA VEFIP DXSYH ZWVEU JYXKH YRRUC IKWCI FRDFC LXINX FJKMX AMTUQ KRGXY SEPBH VVDEG SCCGI CUZJI SSPZP VIBFG SYVBJ VVKRB YYIXQ WORAC AMZCH BYQYR KKMLG LXDLC QZSXA CSKEG EWNEX YXFJW SBIQY RRNJM ZEHRM QTNRC YNUVV KRBSF SXICA VVURC BNLKX GYNEC JMWYI NMBSK QORRN FRSXY SUXRI QHRVO GPTNJ YYLIR XBICK LPVSD SLXCE LIWMV PCIUS BSRMP WLEQP VXGMR MKLOQ QTKLK XQMVA YYJIE SDFCM LRQVW KFVKP MSXXS QCXYI DLMZX LDXFN JAKWT JICUM LIRRN XFTLK RXDZC SPXFJ JGKVC HISGF SYJLO PYZXL OHFJR VDMJD RXDLC FNOGE PINEI MLBYM MLRMV TYSPH IIKXS WVTSG IJUYZ XFJEY DWFNJ TKHBJ ULKRB XNIBI QTTPE QQDRR NXFJE YDWUJ IICSQ RRPVX FFKLO HPTGT OHYQD SCXYX DEXCY XYIZY RNEXR IZFJO OXZZK XRIQH RVOGP TNHSH LTKQS RBMFA VSLLZ XDSMP YMWXM KZPVX FJSEC OCYWS BMRJE ELPCI YMWXM PVIZE UFPJB SKYYI PMPJR WRIDJ RVOHY XGEBO KNXLD KCYZR DSFNJ WDVYB RRNFS WELSQ SUJSR IIJGX KKMTU HSWRF EGOEU FPJBS KYYIP PYRVW KRBTE PIGYR VROEP YFGYZ CWUSB SRMPA SXFII CVIYA VWGLC SJLOP YDUSG RRTJP OINYY ICIIJ GXRIP AVVIW LZXEX HUFIQ KRBXY ICPCU KWYYL ICCER RNCQY VLNEK GLCSZ XGEQI RCVME MKXRI ENIPL ERMVH RIPKR GOMLF CMDXJ JIMZT JNEKL VMTBE XHQTF RKJRJ IXRIW FCPCX YWKIN XMBRV NXFJV QOVYQ UGSXW YYMCA YXKSL IYSVZ ORRKL PNEWK FVDLC YIEFI JJIWD LCDYE NLYWU PIFCJ EAKPI NEKKR FTLVG LCSKL OCQFN FOJMW VXRIK FXVOE RIZXM LRMRX MVMXJ INXFJ ISKHY SUHSZ GIVHD LCKFV OWRFJ JKVYX KLOCA TLPNW CJFRO MRMVV CMBJZ XGEQF MIBCU NUINM RHYEX HUMVR DLCDT VOTRZ GXYXF JVHQI YSUPY SIJUM XXMNK XRIWH FYVHQ JVMDA YXRPC STJIC NICUR RNXFJ IIGIP JDEXC ZNXNK KEJUV YGIXR XDLCG FXDSK YYICM BJJAO VCXFW DICUK LKXLT EIYJR MVQMS SQUGV MKGUS GRYSU JYVYR FQORR NKWOI KJUXR ERYYI SVHTL VXIWR LWDIL INLKX QMRPV ACIFE COCIU SBSRM PHOWN FZVSR EQPMR ETJEX DLCKR MXXCX KMNIY XRMNX FJKMX AMTUQ KRYSU XRIJN FRCLM TBLSW QMRKQ CKFEI KRBQF SUIBY YSEKF YWYVF SYKLO WAFII MVMBJ ESHUJ TEXRM YWPIX FFKMC GCWKE SRLJZ XRIPH RRGIA QZQLH MBEMX XMYYM CKPJR XNMRH YXRIP JWSBI GKNIM ELSFX TYKUF ZOVGY NIWYQ YJXYT UMVVO ACFII SXFNE OSGMZ CHTYK UFZOV GYJES HRMVG YAYWU PIPGT EEPXC WDIKW SWZRQ XFJUM CXYST IMEPJ WYVPW NELSW KNEHD LCSNI KVCFC PBMEM KEXWU JIINX FJJGK VCHIS GJMWP SEGYS TEBVW ZJEVP MAVVY RWTLV LEAPF ROERF KMWIU JCPSP JYICS XQFZH DLCQZ SXAFT NMVPE TWMBW RNNMV PBJTP KVCIK LOWAF IIMVM BWSBM DDFYP SSSUX RERDF YMSSQ URYXH ZDTYZ CWKLO KSQWH YVMYY CGSSQ UFOOG QCINS PYYID MLBFS NQYSS ENPWI VRDIB TEXRI PTTOC FCQFA LYRNW MKQMS PSEVZ FTOSX UNCPX SRRRX DIPXF QEGFK FVDLC KRPVA MZCHX SRMLV DQCFK EVP
    ```

    ```bash
    krypton4@bandit:/krypton/krypton4$ cat krypton5 
    HCIKV RJOX
    krypton4@bandit:/krypton/krypton4$ 
    ```

- Öncelikle Vignere Şifrelemesi için her 6 karakterde x'inci indekteki karakterleri çıkaran fonksiyon yazmalıyız. Bunun için bir python scripti yazalım:

    ```python
    def vignere_shift(text, key_length, shift=0):
        """
        This function extracts every 'key_length'th character from a string,
        with an optional shift.

        Args:
            text: The string to extract characters from.
            key_length: The number of characters to skip between each extracted character.
            shift: The number of characters to shift the extraction by (default: 0).

        Returns:
            A string containing every 'key_length'th character from the input string, shifted by 'shift'.
        """

        # Remove spaces and newlines from the text
        text = text.replace(" ", "").replace("\n", "")
        extracted_string = ""

        # Loop through the text, extracting every 'key_length'th character with the shift applied
        for index in range(shift, len(text)):
            if index % key_length == shift:  # Check if the index is a multiple of the key_length and matches the shift
                extracted_string += text[index]

        return extracted_string

    # Example usage
    text = "your_ciphertext_here"  # Replace with your ciphertext
    key_length = 4  # Replace with the actual key length
    extracted_text = vignere_shift(text, key_length)
    print(extracted_text)
    ```

- `text` değişkenine `found1` dosyasının içeriğini verelim. `key_length` değerini de int(6) olarak atayalım. Açıklamada ipucu olarak bize anahtarın 6 karakterli olduğunu söylemiş. `shift` değeri aynı kalsın.

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python vignere_shift.py 
    YIYWNQRLYTRHYDJTWZSLNNHTMJJYFNYIJJSLWNMFXBBKXIMJTBMIYJJNTYBWKWWLFGWISJSZYSYPJNFJQFWTYWKJJMMNSYWKYSAYMTSQZJRFDMKXFJJPKFSTTTJMBMJDSQIJPFJTSJWJPJIKXISJFFYXMQMYIMZYFSJWJNTWGJYGZTMTYSFFJTWJQBSFSJSJIJJNKWSXZYZKXMSSIFTXSSKTJTYWMYKLTISNJFITWIXNBSJHJF
    ```

- Şimdi bu metindeki harf yoğunluğunu ingilizcedeki harf yoğunluğuyla karşılaştıralım. Bunun için bir python scripti yazalım:

    ```python
    def analyze_letter_frequency(text, group_size=1):
    """
    Analyzes the frequency of character groups in a given file.

    Args:
        text: The text.
        group_size (optional): The number of characters to analyze together

    Prints the character groups and their corresponding frequencies in descending order.
    """

    char_table = {}  # Dictionary to store character groups and their counts
    total_groups = 0  # Total number of analyzed character groups


    # Preprocess the text by removing spaces and newlines
    for line in text:
        clean_line = line.replace(" ", "").replace("\n", "")

        # Analyze character groups of the specified size
        for i in range(len(clean_line) - group_size + 1):
            group = clean_line[i:i + group_size]
            char_table[group] = char_table.get(group, 0) + 1  # Count occurrences of the group
            total_groups += 1

    # Sort the character table by frequency (descending order)
    sorted_table = sorted(char_table.items(), key=lambda item: item[1], reverse=True)

    # Print the results
    for group, count in sorted_table:
        print(f"{group}:\t{count}")  # Formatted output with tab separator

    analyze_letter_frequency('text')
    ```

- **Anahtarı Bulalım 1/6**

    - `analyze_letter_frequency()` fonksiyonuna `text` olarak `YIYWNQRLYTRHYDJTWZSLNNHTMJJYFNYIJJSLWNMFXBBKXIMJTBMIYJJNTYBWKWWLFGWISJSZYSYPJNFJQFWTYWKJJMMNSYWKYSAYMTSQZJRFDMKXFJJPKFSTTTJMBMJDSQIJPFJTSJWJPJIKXISJFFYXMQMYIMZYFSJWJNTWGJYGZTMTYSFFJTWJQBSFSJSJIJJNKWSXZYZKXMSSIFTXSSKTJTYWMYKLTISNJFITWIXNBSJHJF` vereceğiz. `group_size` olarak 1 verip çalıştıralım:

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python freq_analysis.py 
    J:      37
    S:      24
    Y:      22
    T:      20
    F:      18
    W:      17
    M:      16
    I:      14
    N:      12
    K:      11
    X:      9
    Z:      7
    B:      7
    Q:      6
    L:      5
    P:      4
    R:      3
    H:      3
    D:      3
    G:      3
    A:      1
    ```

    - Şu anda şifreli metinde (cipher_text) her 6 karakterden ilkini aldık ve harf frekansına baktık. Buradan anladığımıza göre `J` harfi büyük ihtimalle `E` harfine eşit. Bir sonraki aşamada `key_length` değerini de int(6) olarak atayacağız, çünkü anahtarımız 6 karakter uzunluğunda. `shift` değerini `1` yapacağız. Böylece her 6 harften 2. indisi alacağız. Durumu daha iyi anlamanız için şöyle anlatayım:

    - Metin (K): `FR0 STB 1RD`
    - Anahtar (P): `SEK`
    - Şifreli Metin (C): `XV0 CLF 1BV`
    - İlk aşamada şifreli metnin her 0. karakterini al: `XC1`
        - harf frekansına bak, en yüksek olan `E` harfidir.
    - İkinci aşamada şifreli metnin her 1. karakterini al: `VLB`
        - harf frekansına bak, en yüksek olan `E` harfidir.
    - İkinci aşamada şifreli metnin her 2. karakterini al: `0FV`
        - harf frekansına bak, en yüksek olan `E` harfidir.
    - Şimdi, P-C=K olacağından, eğer J harfi, E harfinin şifreli hali ise:
        - P=J(9)
        - K=?
        - C=E(4)
        - olacaktır. o halde J harfi (9) - E harfi (4) = F harfi (5) olacaktır.
    - O halde 6 harflik anahtarımızın ilk harfi: `F`

- **Anahtarı Bulalım 2/6**

    - Şimdi yukarıda bahsettiğim gibi ikinci aşamaya geçelim. `text` değişkenine `found1` dosyasının içeriğini verelim. `key_length` değerini de int(6) olarak atayalım. `shift` değerini bu sefer 1 yapacağız ki her 6 karakterden 2. olanları bulalım.

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python3 vignere_shift.py 
    YZYVJVKYIWVZZIUFVRFRMJVTVTJKTJSKGCVRFVZUKZZKKUPZRVVZYJVJXNKVZZVZKVVKWEFRYKYZNEEPYMYKYVFRJVRWKYUKVVVIVIRCXNRMFVKKBWZVZEFNUPVVYVKFFKYPVEYUUUUJZIJKUYUNZEVUPNVPIVKYTFIZWKCXLNYFEJRCJTEJRKVVURCIUPTXSIICFVFEJYEKKVUKZWFLVKRINKFKRYFYKKUFKEFERWCKFRJIGK
    ```
    - harf frekansına bakalım: `analyze_letter_frequency('YZYVJVKYIWVZZIUFVRFRMJVTVTJKTJSKGCVRFVZUKZZKKUPZRVVZYJVJXNKVZZVZKVVKWEFRYKYZNEEPYMYKYVFRJVRWKYUKVVVIVIRCXNRMFVKKBWZVZEFNUPVVYVKFFKYPVEYUUUUJZIJKUYUNZEVUPNVPIVKYTFIZWKCXLNYFEJRCJTEJRKVVURCIUPTXSIICFVFEJYEKKVUKZWFLVKRINKFKRYFYKKUFKEFERWCKFRJIGK',1)`

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py 
        V:      35
        K:      32
        Y:      19
        F:      19
        Z:      18
        U:      16
        R:      16
        J:      14
        I:      12
        E:      12
        N:      8
        W:      7
        C:      7
        P:      7
        T:      6
        X:      4
        M:      3
        S:      2
        G:      2
        L:      2
        B:      1
        ```

    - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=V(21)
        - K=?
        - C=E(4)
        - olacaktır. o halde V harfi (21) - E harfi (4) = R harfi (17) olacaktır.
    - O halde 6 harflik anahtarımızın ikinci harfi: `R`

- **Anahtarı Bulalım 3/6**

    - Şimdi yukarıda bahsettiğim gibi üçüncü aşamaya geçelim. `text` değişkenine `found1` dosyasının içeriğini verelim. `key_length` değerini de int(6) olarak atayalım. `shift` değerini bu sefer 2 yapacağız ki her 6 karakterden 3. olanları bulalım.

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python3 vignere_shift.py 
    IIXIOHLXIXVXPIXQXVJXISVOMXXLOKSLSCHXYRGPSGXLESXWHVKEIRZLSELARRHVAITLSWAVIVIIMHHSIIEWIGVRXVXJWIMLWLVSVIXCLSOIYLLFISWHIHXCILTAIWWYXSIXHHMFXXXXRJSKSIXMWHVSWSTWILSIIAWWSASVXLIRHRHSKSHAWLWQGWIFEEIVISEPVAJSIMXLEKAMRXRRLLGXIVSLHEVXLSXRMHAXWIILSRGSMG
    ```
    - harf frekansına bakalım: `analyze_letter_frequency('IIXIOHLXIXVXPIXQXVJXISVOMXXLOKSLSCHXYRGPSGXLESXWHVKEIRZLSELARRHVAITLSWAVIVIIMHHSIIEWIGVRXVXJWIMLWLVSVIXCLSOIYLLFISWHIHXCILTAIWWYXSIXHHMFXXXXRJSKSIXMWHVSWSTWILSIIAWWSASVXLIRHRHSKSHAWLWQGWIFEEIVISEPVAJSIMXLEKAMRXRRLLGXIVSLHEVXLSXRMHAXWIILSRGSMG',2)`

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py
        I:      34
        X:      30
        S:      27
        L:      22
        V:      17
        W:      17
        H:      16
        R:      13
        A:      10
        M:      9
        E:      9
        G:      7
        K:      5
        O:      4
        J:      4
        P:      3
        C:      3
        Y:      3
        T:      3
        F:      3
        Q:      2
        Z:      1
        ```

    - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=I(9)
        - K=?
        - C=E(4)
        - olacaktır. o halde I harfi (9) - E harfi (4) = E harfi (4) olacaktır.

    - O halde 6 harflik anahtarımızın üçüncü harfi: `E`

- **Anahtarı Bulalım 4/6**

    - Şimdi yukarıda bahsettiğim gibi dördüncü aşamaya geçelim. `text` değişkenine `found1` dosyasının içeriğini verelim. `key_length` değerini de int(6) olarak atayalım. `shift` değerini bu sefer 3 yapacağız ki her 6 karakterden 4. olanları bulalım.

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python3 vignere_shift.py 
    CBRXODBRORKIDKRGRNDONPEOBKYOSBHOVYDOBNRODUMOCBRXKOEXQYOODIOONADVSKVOBRCOMIGCVIWEBCZKCBGDBYSOKQKOXKNILCEDDEOCKKOEMBGKBWKYCODOBEKMPPBRRLWIEYRGQSPBDBRDSLMBDBBSCKXZLDEOEKXOZSBKDOKCBVGRNICOSCPOCNNYMEXSDOKBCCBOXBKVDODCYOORBOPOODONIDRGBVXRCVODNNKGXR
    ```
    - harf frekansına bakalım: `analyze_letter_frequency('CBRXODBRORKIDKRGRNDONPEOBKYOSBHOVYDOBNRODUMOCBRXKOEXQYOODIOONADVSKVOBRCOMIGCVIWEBCZKCBGDBYSOKQKOXKNILCEDDEOCKKOEMBGKBWKYCODOBEKMPPBRRLWIEYRGQSPBDBRDSLMBDBBSCKXZLDEOEKXOZSBKDOKCBVGRNICOSCPOCNNYMEXSDOKBCCBOXBKVDODCYOORBOPOODONIDRGBVXRCVODNNKGXR',3)`

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py
        O:      37
        B:      26
        D:      22
        K:      21
        C:      18
        R:      17
        N:      11
        E:      11
        X:      10
        S:      9
        I:      8
        G:      8
        Y:      8
        V:      8
        P:      6
        M:      6
        L:      4
        Q:      3
        W:      3
        Z:      3
        H:      1
        U:      1
        A:      1
        ```

    - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=O(15)
        - K=?
        - C=E(4)
        - olacaktır. o halde O harfi (15) - E harfi (4) = K harfi (11) olacaktır.
    - O halde 6 harflik anahtarımızın dördüncü harfi: `K`

- **Anahtarı Bulalım 5/6**

    - Şimdi yukarıda bahsettiğim gibi beşinci aşamaya geçelim. `text` değişkenine `found1` dosyasının içeriğini verelim. `key_length` değerini de int(6) olarak atayalım. `shift` değerini bu sefer 4 yapacağız ki her 6 karakterden 5. olanları bulalım.

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python3 vignere_shift.py 
    SAIAVLSIXIPYLGILIMLWXJRHWGTQRIERMTLJJWVELILAOSISRHESESVWLLRXLYLXPWMQAICMSSMWPSEEWTWMGSISSLWVMYRKSWIIISVLWPWSWWVXEWMRGEPYXVSWIRREEMXEMEKIVAIESIWEXIILIYYSMIIPWHMEYSVWRWKIYXMVSGPXISEMSWXVXSXLXZXYEKHILVVLMGCAHSWPLVLLXMWIIIJQWFRSESIIIEYIEPTLQXVOK
    ```
    - harf frekansına bakalım: `analyze_letter_frequency('SAIAVLSIXIPYLGILIMLWXJRHWGTQRIERMTLJJWVELILAOSISRHESESVWLLRXLYLXPWMQAICMSSMWPSEEWTWMGSISSLWVMYRKSWIIISVLWPWSWWVXEWMRGEPYXVSWIRREEMXEMEKIVAIESIWEXIILIYYSMIIPWHMEYSVWRWKIYXMVSGPXISEMSWXVXSXLXZXYEKHILVVLMGCAHSWPLVLLXMWIIIJQWFRSESIIIEYIEPTLQXVOK',4)`

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py
        I:      32
        S:      26
        W:      24
        L:      21
        E:      20
        X:      17
        M:      16
        V:      15
        R:      11
        Y:      10
        P:      9
        A:      6
        G:      6
        H:      5
        K:      5
        J:      4
        T:      4
        Q:      4
        O:      2
        C:      2
        Z:      1
        F:      1
        ```

    - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=I(9)
        - K=?
        - C=E(4)
        - olacaktır. o halde I harfi (9) - E harfi (4) = E harfi (9) olacaktır.
    - O halde 6 harflik anahtarımızın beşinci harfi: `E`

- **Anahtarı Bulalım 6/6**

    - Şimdi yukarıda bahsettiğim gibi altıncı ve son aşamaya geçelim. `text` değişkenine `found1` dosyasının içeriğini verelim. `key_length` değerini de int(6) olarak atayalım. `shift` değerini bu sefer 5 yapacağız ki her 6 karakterden 6. olanları bulalım (son anahtar karakteri).

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python3 vignere_shift.py 
    JGEFQCSQQCBLCFPCEYCJFGJRNJSZFYLFRCCMPUMBCBMCCRPPQRPDRLURYMYMCGCFJWCYFIMLSDLFDSIJJCLBYUKBWRBCBYMYMCQBDGYMFBJDQMCRPFABCWJRPIRRRQBLGLFLKBMYLYUJTJMQCYPBQRNRJRRIQNLJRFNFBLCLPCZMRIQGCPQRPBFYWMDGFYFLKFFPCCKMLMMCRSSCCLCMGPDPLQCQMCGPLYJPBWNELYUCYFCCU
    ```
    - harf frekansına bakalım: `analyze_letter_frequency('JGEFQCSQQCBLCFPCEYCJFGJRNJSZFYLFRCCMPUMBCBMCCRPPQRPDRLURYMYMCGCFJWCYFIMLSDLFDSIJJCLBYUKBWRBCBYMYMCQBDGYMFBJDQMCRPFABCWJRPIRRRQBLGLFLKBMYLYUJTJMQCYPBQRNRJRRIQNLJRFNFBLCLPCZMRIQGCPQRPBFYWMDGFYFLKFFPCCKMLMMCRSSCCLCMGPDPLQCQMCGPLYJPBWNELYUCYFCCU',5)`

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py
        C:      33
        R:      20
        F:      19
        L:      19
        M:      19
        Y:      17
        B:      16
        P:      16
        J:      14
        Q:      14
        G:      9
        D:      7
        S:      6
        U:      6
        N:      5
        W:      5
        I:      5
        K:      4
        E:      3
        Z:      2
        A:      1
        T:      1
        ```

    - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=C(3)
        - K=?
        - C=E(4)
        - olacaktır. o halde C harfi (3) - E harfi (4) = -1 olacaktır. Alfabede geriye doğru sayarsak `0.` karakter: `Z` ve `-1`. karakter: `Y` harfidir.
    - O halde 6 harflik anahtarımızın altıncı ve son harfi: `Y`

- Anahtarı bulduk: `FREKEY` Şimdi decode etmek için bir python scripti yazalım:

    ```python
    def vignere_decoder(text, key):
        """Decodes a given text using the Vignere cipher with the specified key."""
        out_string = ""
        alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
        text = text.replace(" ", "").upper()  # Remove spaces and convert to uppercase

        for i in range(len(text)):
            char_index = alphabet.index(text[i])
            shift = alphabet.index(key[i % len(key)])
            new_index = (char_index - shift) % 26
            out_string += alphabet[new_index]

        return out_string

    # Example usage:
    text_to_decode = "HCIKV RJOX"
    decoded_text = vignere_decoder(text_to_decode, "FREKEY")
    print(decoded_text)
    ```

- Çalıştıralım: `python3 vignere_decoder.py`

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python3 vignere_decode.py 
    CLEARTEXT
    ```

- yeni parola: `CLEARTEXT`, found1 dosyasını da okumaya çalışalım:

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python3 vignere_decode.py
    THESOLDIERWITHTHEGREENWHISKERSLEDTHEMTHROUGHTHESTREETSOFTHEEMERALDCITYUNTILTHEYREACHEDTHEROOMWHERETHEGUARDIANOFTHEGATESLIVEDTHISOFFICERUNLOCKEDTHEIRSPECTACLESTOPUTTHEMBACKINHISGREATBOXANDTHENHEPOLITELYOPENEDTHEGATEFOROURFRIENDSWHICHROADLEADSTOTHEWICKEDWITCHOFTHEWESTASKEDDOROTHYTHEREISNOROADANSWEREDTHEGUARDIANOFTHEGATESNOONEEVERWISHESTOGOTHATWAYHOWTHENAREWETOFINDHERINQUIREDTHEGIRLTHATWILLBEEASYREPLIEDTHEMANFORWHENSHEKNOWSYOUAREINTHECOUNTRYOFTHEWINKIESSHEWILLFINDYOUANDMAKEYOUALLHERSLAVESPERHAPSNOTSAIDTHESCARECROWFORWEMEANTODESTROYHEROHTHATISDIFFERENTSAIDTHEGUARDIANOFTHEGATESNOONEHASEVERDESTROYEDHERBEFORESOINATURALLYTHOUGHTSHEWOULDMAKESLAVESOFYOUASSHEHASOFTHERESTBUTTAKECAREFORSHEISWICKEDANDFIERCEANDMAYNOTALLOWYOUTODESTROYHERKEEPTOTHEWESTWHERETHESUNSETSANDYOUCANNOTFAILTOFINDHERTHEYTHANKEDHIMANDBADEHIMGOODBYEANDTURNEDTOWARDTHEWESTWALKINGOVERFIELDSOFSOFTGRASSDOTTEDHEREANDTHEREWITHDAISIESANDBUTTERCUPSDOROTHYSTILLWORETHEPRETTYSILKDRESSSHEHADPUTONINTHEPALACEBUTNOWTOHERSURPRISESHEFOUNDITWASNOLONGERGREENBUTPUREWHITETHERIBBONAROUNDTOTOSNECKHADALSOLOSTITSGREENCOLORANDWASASWHITEASDOROTHYSDRESSTHEEMERALDCITYWASSOONLEFTFARBEHINDASTHEYADVANCEDTHEGROUNDBECAMEROUGHERANDHILLIERFORTHEREWERENOFARMSNORHOUSESINTHISCOUNTRYOFTHEWESTANDTHEGROUNDWASUNTILLEDINTHEAFTERNOONTHESUNSHONEHOTINTHEIRFACESFORTHEREWERENOTREESTOOFFERTHEMSHADESOTHATBEFORENIGHTDOROTHYANDTOTOANDTHELIONWERETIREDANDLAYDOWNUPONTHEGRASSANDFELLASLEEPWITHTHEWOODMANANDTHESCARECROWKEEPINGWATCH
    ```

- Kolay yoldan [guballa.de](https://www.guballa.de/vigenere-solver) kullanarak da yapabiliriz:
    - found1 dosyasının içeriğini cipher text olarak verin,
    - Key Length = 6 olarak verin
    - break cipher tuşuna basın
    - "Cleartext using the keyword `frekey`" diyecek. Ardından [buraya gidin](https://www.cs.du.edu/~snarayan/crypt/vigenere.html)
    - text to decode kısmına `HCIKV RJOX` yazın, key kısmına `frekey` yazın. decode tuşuna basın.

- [dcode.fr](https://www.dcode.fr/vigenere-cipher) ile de yapabilirsiniz:
    - cipher text kısmına found1 dosyasının içeriğini verin
    - `Knowing the key-length/size, number of letters` tuşuna tıklayın 6 verin
    - sol tarafta anahtarı `FREKEY` olarak gösterecek
    - cipher text olarak `HCIKV RJOX` yazın, key kısmına `frekey` yazın.
    - `Knowing the Key/Password` tuşuna tıklayın
    - decrypt deyin

- [f00l.de](https://f00l.de/hacking/vigenere.php) ile de yapabilirsiniz:
    - cipher text kısmına found1 dosyasının içeriğini verin
    - key length 6 verin, crack tuşuna tıklayın

        ```
        CRACKING position   1: 102 = f
        CRACKING position   2: 114 = r
        CRACKING position   3: 101 = e
        CRACKING position   4: 107 = k
        CRACKING position   5: 101 = e
        CRACKING position   6: 121 = y

        CRACKED password: frekey
        ```

    - key kısmına `frekey` yazın (otomatik yazıyor)
    - Ciphertext kısmını `HCIKV RJOX` olarak değiştirin
    - decrypt tuşuna tıklayın

- [boxentriq.com](https://www.boxentriq.com/code-breaking/vigenere-cipher) ile de yapabilirsiniz:
    - cipher text kısmına found1 dosyasının içeriğini verin
    - min key ve max key olarak 6 verin
    - auto solve (without key) deyip keyi bulun
    - key kısmına bulduğunuz keyi yazın: `frekey`
    - Ciphertext kısmını `HCIKV RJOX` olarak değiştirin
    - decrypt tuşuna tıklayın

- Bunlara benzer sürüyle online araç var. Ancak mantığını kavramak önemlidir.

- yeni parola: `CLEARTEXT`

### Krypton Level 5 -> 6

- ssh ile bağlanalım: `ssh krypton5@krypton.labs.overthewire.org -p 2231`

- önceki seviyede bulduğumuz parolayı girelim: `CLEARTEXT`

- Önceki seviyelerde bahsedildiği üzere `/krypton/krypton5` dizinine gidip readme dosyasını okuyalım:

    ```bash
    krypton5@bandit:~$ cd /krypton/krypton5
    krypton5@bandit:/krypton/krypton5$ ls -la
    total 28
    drwxr-xr-x 2 root     root     4096 Jun 16 02:49 .
    drwxr-xr-x 9 root     root     4096 Jun 16 02:49 ..
    -rw-r----- 1 krypton5 krypton5 1776 Jun 16 02:49 found1
    -rw-r----- 1 krypton5 krypton5 1915 Jun 16 02:49 found2
    -rw-r----- 1 krypton5 krypton5 2110 Jun 16 02:49 found3
    -rw-r----- 1 krypton5 krypton5    7 Jun 16 02:49 krypton6
    -rw-r----- 1 krypton5 krypton5  151 Jun 16 02:49 README
    krypton5@bandit:/krypton/krypton5$ cat README 
    Frequency analysis can break a known key length as well.  Lets try one
    last polyalphabetic cipher, but this time the key length is unknown.


    Enjoy.


    krypton5@bandit:/krypton/krypton5$ 
    ```

- Diğer dosyalara da bakalım:

    ```bash
    krypton5@bandit:/krypton/krypton5$ cat found1
    SXULW GNXIO WRZJG OFLCM RHEFZ ALGSP DXBLM PWIQT XJGLA RIYRI BLPPC HMXMG CTZDL CLKRU YMYSJ TWUTX ZCMRH EFZAL OTMNL BLULV MCQMG CTZDL CPTBI AVPML NVRJN SSXWT XJGLA RIQPE FUGVP PGRLG OMDKW RSIFK TZYRM QHNXD UOWQT XJGLA RIQAV VTZVP LMAIV ZPHCX FPAVT MLBSD OIFVT PBACS EQKOL BCRSM AMULP SPPYF CXOKH LZXUO GNLID ZVRAL DOACC INREN YMLRH VXXJD XMSIN BXUGI UPVRG ESQSG YKQOK LMXRS IBZAL BAYJM AYAVB XRSIC KKPYH ULWFU YHBPG VIGNX WBIQP RGVXY SSBEL NZLVW IMQMG YGVSW GPWGG NARSP TXVKL PXWGD XRJHU SXQMI VTZYO GCTZR JYVBK MZHBX YVBIT TPVTM OOWSA IERTA SZCOI TXXLY JAZQC GKPCS LZRYE MOOVC HIEKT RSREH MGNTS KVEPN NCTUN EOFIR TPPDL YAPNO GMKGC ZRGNX ARVMY IBLXU QPYYH GNXYO ACCIN QBUQA GELNR TYQIH LANTW HAYCP RJOMO KJYTV SGVLY RRSIG NKVXI MQJEG GJOML MSGNV VERRC MRYBA GEQNP RGKLB XFLRP XRZDE JESGN XSYVB DSSZA LCXYE ICXXZ OVTPW BLEVK ZCDEA JYPCL CDXUG MARML RWVTZ LXIPL PJKKL CIREP RJYVB ITPVV ZPHCX FPCRG KVPSS CPBXW VXIRS SHYTU NWCGI ANNUN VCOEA JLLFI LECSO OLCTG CMGAT SBITP PNZBV XWUPV RIHUM IBPHG UXUQP YYHNZ MOKXD LZBAK LNTCC MBJTZ KXRSM FSKZC SSELP UMARE BCIPK GAVCY EXNOG LNLCC JVBXH XHRHI AZBLD LZWIF YXKLM PELQG RVPAF ZQNVK VZLCE MPVKP FERPM AZALV MDPKH GKKCL YOLRX TSNIB ELRYN IVMKP ECVXH BELNI OETUX SSYGV TZARE RLVEG GNOQC YXFCX YOQYO ISUKA RIQHE YRHDS REFTB LEVXH MYEAJ PLCXK TRFZX YOZCY XUKVV MOJLR RMAVC XFLHO KXUVE GOSAR RHBSS YHQUS LXSDJ INXLH PXCCV NVIPX KMFXV ZLTOW QLKRY TZDLC DTVXB ACSDE LVYOL BCWPE ERTZD TYDXF AILBR YEYEG ESIHC QMPOX UDMLZ VVMBU KPGEC EGIWO HMFXG NXPBW KPVRS XZCEE PWVTM OOIYC XURRV BHCCS SKOLX XQSEQ RTAOP WNSZK MVDLC PRTRB ZRGPZ AAGGK ZIMAP RLKVW EAZRT XXZCS DMVVZ BZRWS MNRIM ZSRYX IEOVH GLGNL FZKHX KCESE KEHDI FLZRV KVFIB XSEKB TZSPE EAZMV DLCSY ZGGYK GCELN TTUIG MXQHT BJKXG ZRFEX ABIAP MIKWA RVMFK UGGFY JRSIP NBJUI LDSSZ ALMSA VPNTX IBSMO
    ```

    ```bash
    krypton5@bandit:/krypton/krypton5$ cat found2
    GLCYX UKFHS PEZXF AVJOW QQYYR RAYHM GIEOG ARIAZ YEYXV PXFPJ BXXUY SLELR NXHNH PLARX TADLC CSLGE NOSPR IUUML VSNPR RJMOO GMLGU JHVBE QSMFI NZDSK HEFNX KSHGE AVZAZ YQCQP BAKPC LMQGR XXTYR WQSEG FHSPH ZYETX FPVMX PBTWV XMLHM AZXYG EQLRN IAPOZ CXIAZ MVMSL RVNZN SKXCL RNJOL XXSCS HYMYK ZCWPR XNWYR ZJXUG MASQC ELRXX DKWMY PLUGL KHTPR GAKVE WRCEI KESOV JPJGH XJYRE CEGAE HDIBQ SEZAL DAMZX UKKZR EBMIR TLLDH MHRNZ MOOMP CIFVX JDMTP VBGWZ SHCOI FZBUK XGZRF ZALWM JOIJE BUCMB PSSZA LMSYN LJOMO SXQOE ZVTUN HGCXL YMYKA GEWQO LHQIC LFYKL TOPJL RQOMZ YFQNY EOMFG EQCEG NXYVM IPEYG KNOVB ZKXKG UOPKC PBXKF DLCAE FYXUQ IPDLN QBUQL GXWRR YVEXM QMGOG JREGY WBLLA BEULX NTZSO SDDLN MZFGV YATRX YSKTN TRTNT AKRBX YQJRS OKQHE FXTAR IPWMX KTSKV EPVFU KAYJB ZKGNX YOAGW POKTW KGIPX GUVHV EGDXB SHYBS UOVNC XYIIQ DMEOY ARIUP EGNXY RSJOW NTWAR IUTRQ YXACX MWIEG USOJY TVGNX ASHCH MYRLL BZCAV RZMFX MAPPL GMHLS SEXJU BUDLC LJGKK UYSLD MEHXK CMPTW UGESX SRRSG UULNX GWPAO ZODFS EMJGG AKFCO VBUFH XHYME EHXYK RBELR TUYOE IQEFZ LPBCC DWVXM OKXUL CFOKP PCMFT YKTZO WFZAP UGJYV BRIAZ ELWEL DZNRB ZOELO LBZPH DIPES PUGJY VBAYY RHMPK CYXYK FHXWZ ZSGYB UMSLN SEJRV EAGWP SOGKK JGYIF KTJYE JQMEK LPBJC EGUHT YLIPE SPUGJ YVBDX VXTIY YRELR XXUYA DZVPU GJYVB ELRIH UMSPO FRJVO KQZPV OKBUQ EJHEL YTZCM EYIQZ HHZEQ DIAMX YLCRS IZGBS KRBAE FYXUQ IPDFL ZALWE GWFRO GNKPU LCFNX HFMJJ AEGIW OHSAJ EUFOO EBESS UHADL CCSBS AHNXF PSQJB UDIPP WGLHY DLCPW GGUSS WFXIA ZHMDL CCSLG ENOSP RIGNT AKPRS SHMAI EXMYI XOGKY JKLRJ GLZOI LESTU BUDSG EEYRD PXHQL RQBTY SIRTI FUYTO RALQR UNAYJ GEGBT LLAYC YXYET UYXFP VQXTD OVYYH GCHWY VRPVF GGKCI TPVNR FHSHQ LRQZA LVELO PNJRD OVCLP YRHPD IPTRT HRHMG GOIAZ TAFEP TSHYI VSRRD SSZAL BSYOF RZPLO RRSIP UGJYV BLRQZ ALMSD QIRXH VWAFP RNMXU DPCXE AUYZS BRJJB XFHVP WOVRY LLNML LFEUP UCYGE SSIEV DLCDT EKMAI ACWPJ UKULY RGIEE PLVPI PTGCB ARPYC KRYJB KVCNY SLLHX HJLVT KYSKT QESGN XWYGI PXFVT ZCIBL PBTZV XLGDA NEMVR MQMVR GDMKW R
    ```

    ```bash
    krypton5@bandit:/krypton/krypton5$ cat found3
    FIPJS EJXYV CYYHZ KMOYH GNEYN XSYSI PHJOM OKLYY HBTXH MLIYI RGGKK PMFHJ GMJRX GNOVT ZHCSL ZVBAL ZOVKZ RHTWL BLGDJ YGIWO HULMF ZVVKX YDXUU NNRMR AMGZX KSXQR VNBBA IELOP BTZLF MRJET GBUCX RSIYK OPDCY YHRBT UOWAP RPKHM DLCMV VYDMS VCSIU GWHQS MOPRM TUNAY DEYOM AVITL MAUYP DJMCL VYUYY ALDXB IDPXK QQMGZ XKCPC PONTW JVSQP EAJPL BIMQE SOGLD IVEYE KAPCW FZIFG GKLYA VPRYM VYXFZ YTNIS KMLHI EKMYS QFPAB XXHXS BOPVZ MSOWJ PIXIK PCTDW EKKGD SKQPX GOGNF IPJGY ULLDS FTWUK TKGLG NLJOZ PDMQE SOKIY OWSXI QCTZW EBPSS NTPBF SEAUO VOVSM VIQLT YWSPP EFZAV EKFTX JKKLC TSYJE UFMSP YXIAZ LVPWG WOBXZ SKWQS MFRBU ORRSS HMAUY XMQES OGLXI QDMAG VJYVB LRPKP PDLFT WFZHJ UMLRW JGLHC AFTXR GLARI RZTFU YARIU LZRYM OKXZC SXKNW YRRSI AKBNR FMFVV TZIOE ASSEZ ALCTC NOFUY ZKMJE LNZZS SRRPH VTMOO WSYPV MAAPE PLXFK THPEA PLNHB AEEJW CFAIW BIQDI QGGKA YGPXR JPHCW RTPYR BNRXC OYCAG KOVRS IDATP XXUTK OETWK MPZJZ UBZDF PTKUZ XFOWR SEGOM TEWRS EIKVV CXRSI VXHDX IPTRL KTYCK MYIOE LVWIN LMAYM VNVGW PGUMO OGMXT BYXKK RBCIF KKCOH CITEK LZSSL ZJGKE SCSLD FNTDO OLYOE UKTSD LWNSY UNYSR FTWPN XLUWY YHUOL MKGCE LBAZO VMLPH OUKLP IUEVN IXZYJ YYBVK MFLYR AIENT WCXFP GBTYP NILEM NRUHM LCWSE IELBO QTRGK ESCSL DFNTD DOVCA VVTVP ZEJWC BIVBZ MCOAV ZAARI ALVRY HMYXF PVCKH WVIYY HCKKO KTQDI PUGKR ELOGN XXZVM IPWRI HUNLY YHPRH ARIQN SZKXH CMJJS SLTUN SLNSZ VELDM LRLVY KLCIK MPNTV LDSYX EACAV GEQDM GZBUQ JMCLV YIVBX PLMGS KSYVP JHEUI WOHMQ JGULS OINEL RGKYS ZYWSS NBZLV CLOSG LABSS DIQNB TKRBS IFGBK DSRSI QXTDO VYDLR SHCOH FTWPN TPBXM TXVCB ZREAN SZSHK KXGZR CXXWK VCOJB XTFYY LRPNJ RDRSK LCPUF LRIPP EGGGF DMKPX BJTFC LCXEL GLRPS PXVWG KCSWJ ZVEEH YCLCX ELUGS IEQVJ BXTNO RRWIZ GGMBS KEIYR LVXWZ LRXVE LKWCE SYKMT OOLZA LKLZS VRPPY YHUCF YYOVT EVXHM YWVXR LCCCD WVXPL RETPS SZXUD MKPWG NXOYR MFVGU XUDIP EEVTR VEVEP RGRXT ORGYX UKBYD VYGIY RBUQF YNOJG KKCEL OJBXP HBHQM IGCBE DPMYH BTTUN TYCMF YBYKZ YDXQK TSYJR CEIKE SSRED MEOGA OPJDS AGGKM SKAEA ELOYY QPCRY PLKVC BYVZX HPVCY GUNHB CIYDA RREHC ELPRT RBZRS LPCRY LPBRM EQHIA PXXFP LNHBA YJQFG UZKHF IJWMA MRVEV QPPSO MOSRI DMETH AYJJL XREXH BWGEM FLBMD ICYCR GKZCM LNIJK LPXGC TGNSX SKWRQ VBSYY KRAP
    ```

    ```bash
    krypton5@bandit:/krypton/krypton5$ cat krypton6 
    BELOS Z
    krypton5@bandit:/krypton/krypton5$ 
    ```

- Öncekinde anahtar uzunluğunu bildiğimiz için her x'inci indexteki harfleri alıp frekans analizini `E` harfine eşitleyerek yapmıştık ancak burada bu işe yaramayacak. Çünkü ne keyi ne de uzunluğunu biliyoruz. Key uzunluğunu bulmak için bir python scripti yazalım:

    ```python
    def vignere_key_length(text:str, max_key_length=20):
        rep_seq = []
        rep_seq_spaces = []
        tallys = [0] * max_key_length

        for line in text.splitlines():    # Assuming the text might have multiple lines
            line = line.replace(" ", "")
            line = line.replace("\n", "")
            for length in range(3, 5 + 1):
                for i in range(len(line) - length + 1):
                    q = line[i:i + length]
                    for j in range(i + 1, len(line) - length + 1):
                        r = line[j:j + length]
                        if q == r:
                            rep_seq.append(q)
                            rep_seq_spaces.append(j - i)

        for n in rep_seq_spaces:
            for i in range(1, max_key_length):
                if n % i == 0:
                    tallys[i] = tallys[i] + 1

        s = sum(tallys)
        if s == 0:
            print("No repeating sequences")
        else:
            print("Chance key length is: ")
            for i in range(1, len(tallys)):
                print(str(i) + " = " + str(round((tallys[i] / s) * 100, 2)) + "%")

    vignere_key_length("ornektext")
    ```

    - Bu kod, metinde tekrar eden karakter dizilerini arayarak anahtar uzunluğu hakkında ipuçları verir.
    - Bu kod, Vigenère şifresinde kullanılan anahtar uzunluğu hakkında ipuçları verir ancak kesin olarak anahtarın ne olduğunu söylemez.
    - Metin uzunluğu ve kullanılan anahtar uzunluğu sonuçların doğruluğunu etkileyebilir.
    - `vignere_key_length(text:str):` isimli bir fonksiyon tanımlar. Bu fonksiyon bir metin (`text`) argümanı alır.
    - `rep_seq = []`: Metinde bulunan tekrar eden karakter dizilerini saklamak için boş bir liste.
    - `rep_seq_spaces = []`: Tekrar eden diziler arasındaki mesafeyi (karakter sayısı) saklamak için boş bir liste.
    - `tallys = [0] * max_key_length`: 3 ile 22 arasındaki sayıları temsil eden `max_key_length` (20) elemanlı bir dizi. Bu dizi, olası anahtar uzunluklarının (3 ile 22 karakter) sayısını tutar.
    - **Satır İşleme:**
        - Metni satırlara ayırmak için `splitlines` kullanılır.
        - Her satırdan boşluklar ve satır sonları silinerek sadece harflerle işlem yapılır.
    - **Tekrar Eden Dizileri Bulma:**
        - 3 ile 5 karakter arasındaki olası anahtar uzunlukları için her bir uzunlukta:
        - Metinde o uzunluktaki tekrar eden dizileri arar.
        - Bulunan tekrar eden dizi ve aralarındaki mesafeyi ilgili listlere (`rep_seq` ve `rep_seq_spaces`) ekler.
    - **Anahtar Uzunluğu Analizi:**
        - Tekrar eden diziler arasındaki mesafe değerlerini (`rep_seq_spaces`) tek tek inceler.
        - Her mesafe değeri için 1 ile 20 arasındaki sayılara bölünür mü diye kontrol eder.
        - Eğer bir mesafe değeri olası bir anahtar uzunluğuna (sayıya) bölünebilirse, `tallys` dizisindeki ilgili konumun değeri 1 arttırılır. Bu, o anahtar uzunluğuna uygun tekrar sayısını gösterir.
    - **Sonuçların Yazdırılması:**
        - `tallys` dizisindeki tüm değerlerin toplamı alınır.
        - Eğer toplam sıfırsa, "Tekrar eden dizi bulunamadı" yazdırır.
        - Eğer toplam sıfırdan farklıysa, "Olası anahtar uzunluğu:" satırını yazdırır.
        - Sonrasında her bir olası anahtar uzunluğu (1 ile max_key_length (20) arası) için `tallys` dizisindeki ilgili konumun değerini toplayarak olasılık yüzdesini hesaplar ve yazdırır.

- found1 dosyasını parametre olarak verip fonksiyonu çalıştıralım:

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python key_length.py
    Chance key length is: 
    1 = 16.6%
    2 = 8.37%
    3 = 14.72%
    4 = 4.79%
    5 = 5.86%
    6 = 7.34%
    7 = 1.79%
    8 = 2.01%
    9 = 14.05%
    10 = 2.64%
    11 = 1.12%
    12 = 4.3%
    13 = 0.45%
    14 = 0.49%
    15 = 5.46%
    16 = 1.52%
    17 = 0.85%
    18 = 7.07%
    19 = 0.58%
    ```

- found2 dosyasını parametre olarak verip fonksiyonu çalıştıralım:

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python key_length.py
    Chance key length is: 
    1 = 17.35%
    2 = 8.34%
    3 = 15.83%
    4 = 5.56%
    5 = 3.31%
    6 = 7.57%
    7 = 1.97%
    8 = 1.94%
    9 = 14.88%
    10 = 1.44%
    11 = 1.48%
    12 = 5.07%
    13 = 1.86%
    14 = 0.95%
    15 = 3.13%
    16 = 0.81%
    17 = 0.95%
    18 = 7.04%
    19 = 0.53%
    ```

- found3 dosyasını parametre olarak verip fonksiyonu çalıştıralım:

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python key_length.py
    Chance key length is: 
    1 = 18.22%
    2 = 9.14%
    3 = 14.88%
    4 = 3.67%
    5 = 3.67%
    6 = 8.1%
    7 = 3.61%
    8 = 1.97%
    9 = 13.24%
    10 = 1.86%
    11 = 0.71%
    12 = 2.95%
    13 = 1.91%
    14 = 2.63%
    15 = 2.74%
    16 = 1.15%
    17 = 1.04%
    18 = 7.82%
    19 = 0.71%
    ```

- Gördüğümüz gibi key uzunluğu 3, 6, 9 ve 18 olabilir. 9 olduğunu varsayalım. İkinci tercihimiz 6 olabilir.

- **Anahtarı Bulalım 1/9**

    - Önceki seviyede yaptığımız gibi `vignere_shift()` fonksiyonunu çalıştıralım. found1 değerini ciphertext olarak verelim, key_length = 9 olarak verelim ve çalıştıralım:

        `SOCGWRCDYCOVDPSRPKYORPCBBBPKLOYDGQMBBYBBSWSRXSOBBOSYCOSKNDKRQOQQAKYXOEGBDYCOKCRXCBCPXNNFCBXMQKNKCRVNXDLPZFVCNVBXROORSXCOMCVBXPXODCBDBIDKOBCOBXODRZWCRSGXDFZDKIKBRYUMB`

    - found2 dosyasını da aynı şekilde yapalım:

        `GSOYRPYNDOVOBDSYCYSPXGOMKXKYSKKEOYDDRDODSKWCMSNKQOYGVOODQQERBOGKKORKYOKVBIRRRCOSBXLDYCXNDKXKOBKPOYWODYPXMEKYBLYYYYMKQCZLKQWKFOODNDDSDOKEYODXSOYAYOYCSVODMFSBOYMWDSVNCDILVRKXKYCXRK`

    - found3 dosyasını da aynı şekilde yapalım:

        `FVYYKMKRCOBOKRSIFCDODSQNVDYXCVBDCLYKSXOCSFDGDOWBVWECSPKOYXYDUCRRKYROCKSOPPEBACROXKDOECXCWNOKOSCODSUKVPYLCNMBCOZZRYVKRVNRCNDCDGQBYOOSLBKDOOBRKKYRRDCPSCIOBXKOSCXCRDYDEODQCBDNKYSOMYKPCCRBXYFESYBDCXKK`

    - Tümünü birleştirip frekans analizi yapalım: 

        ```
        SOCGWRCDYCOVDPSRPKYORPCBBBPKLOYDGQMBBYBBSWSRXSOBBOSYCOSKNDKRQOQQAKYXOEGBDYCOKCRXCBCPXNNFCBXMQKNKCRVNXDLPZFVCNVBXROORSXCOMCVBXPXODCBDBIDKOBCOBXODRZWCRSGXDFZDKIKBRYUMBGSOYRPYNDOVOBDSYCYSPXGOMKXKYSKKEOYDDRDODSKWCMSNKQOYGVOODQQERBOGKKORKYOKVBIRRRCOSBXLDYCXNDKXKOBKPOYWODYPXMEKYBLYYYYMKQCZLKQWKFOODNDDSDOKEYODXSOYAYOYCSVODMFSBOYMWDSVNCDILVRKXKYCXRKFVYYKMKRCOBOKRSIFCDODSQNVDYXCVBDCLYKSXOCSFDGDOWBVWECSPKOYXYDUCRRKYROCKSOPPEBACROXKDOECXCWNOKOSCODSUKVPYLCNMBCOZZRYVKRVNRCNDCDGQBYOOSLBKDOOBRKKYRRDCPSCIOBXKOSCXCRDYDEODQCBDNKYSOMYKPCCRBXYFESYBDCXKK
        ```

    - `text` değişkenine `found1` dosyasının içeriğini verelim. `key_length` değerini de int(6) olarak atayalım. `shift` değerini bu sefer 0 yapacağız ki her 9 karakterden 0. olanları bulalım.

    - harf frekansına bakalım: `analyze_letter_frequency('SOCGWRCDYCOVDPSRPKYORPCBBBPKLOYDGQMBBYBBSWSRXSOBBOSYCOSKNDKRQOQQAKYXOEGBDYCOKCRXCBCPXNNFCBXMQKNKCRVNXDLPZFVCNVBXROORSXCOMCVBXPXODCBDBIDKOBCOBXODRZWCRSGXDFZDKIKBRYUMBGSOYRPYNDOVOBDSYCYSPXGOMKXKYSKKEOYDDRDODSKWCMSNKQOYGVOODQQERBOGKKORKYOKVBIRRRCOSBXLDYCXNDKXKOBKPOYWODYPXMEKYBLYYYYMKQCZLKQWKFOODNDDSDOKEYODXSOYAYOYCSVODMFSBOYMWDSVNCDILVRKXKYCXRKFVYYKMKRCOBOKRSIFCDODSQNVDYXCVBDCLYKSXOCSFDGDOWBVWECSPKOYXYDUCRRKYROCKSOPPEBACROXKDOECXCWNOKOSCODSUKVPYLCNMBCOZZRYVKRVNRCNDCDGQBYOOSLBKDOOBRKKYRRDCPSCIOBXKOSCXCRDYDEODQCBDNKYSOMYKPCCRBXYFESYBDCXKK',5)`

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python3 freq_analysis.py
        O:      63
        K:      51
        C:      49
        D:      48
        Y:      46
        B:      39
        R:      35
        S:      34
        X:      30
        V:      18
        P:      17
        N:      17
        Q:      13
        M:      13
        G:      10
        W:      10
        E:      10
        L:      9
        F:      9
        Z:      6
        I:      6
        A:      3
        U:      3
        ```

    - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=O(15)
        - K=?
        - C=E(4)
        - O-E=11(K)
    - O halde 9 harflik anahtarımızın 1. harfi: `K`

- **Anahtarı Bulalım 2/9**

    - vignere_shift(found1, key_length=9, shift=1):
    
        `XWMSIIHLSMTMLMXIPWRWILXSACSHIAMXISXAXHPISIWSWXGKIWZJSVRVELGVPAAIYJRIMREXEVXVZLMIIIXSIWVITIWIPXTXSECLHLMALEMLIMESEQQIRHXZOXESSXKWLSCTRHMPHWEIHXPLGIESWRLKIISLGGXIVJISS`

    - vignere_shift(found2, key_length=9, shift=1):
    
        `LPWHIXSHLSSGESHQLRPVMEZSXXZRQWHWVRIAEHMMHXMMSXHAIPFEMVPLILXEESVTRKIVJAGESIISIXJHZMSLSMSXFFHRECXCWVEEIVKWSAJEJIVYAVSQEMECRIEPMHELXILWLSPXJISHIRJYXVVIHEVIGERSRVSAPBPMYLAYPPVHTGILMW`

    - vignere_shift(found3, key_length=9, shift=1):
    
        `ICHSLLPXSVLHXMXEMXCWLVSAIJAKPSIIWYXMQSWTKISLMWEFSSKTPWWRXIVLMAIIXRFETMRWEEEIYWXVXMFWWXIKIVGRHSSLLRWGMIJYXILOSVEMIXITEMLIMSMISEJXVHIZVSRSVHXEXVYSIMLSWLERSWWOVFHCEMRIVRVFEHPTZJRPSYVVIESRXJIVRJWIMGWR`

    - birleştir:

        `XWMSIIHLSMTMLMXIPWRWILXSACSHIAMXISXAXHPISIWSWXGKIWZJSVRVELGVPAAIYJRIMREXEVXVZLMIIIXSIWVITIWIPXTXSECLHLMALEMLIMESEQQIRHXZOXESSXKWLSCTRHMPHWEIHXPLGIESWRLKIISLGGXIVJISSLPWHIXSHLSSGESHQLRPVMEZSXXZRQWHWVRIAEHMMHXMMSXHAIPFEMVPLILXEESVTRKIVJAGESIISIXJHZMSLSMSXFFHRECXCWVEEIVKWSAJEJIVYAVSQEMECRIEPMHELXILWLSPXJISHIRJYXVVIHEVIGERSRVSAPBPMYLAYPPVHTGILMWICHSLLPXSVLHXMXEMXCWLVSAIJAKPSIIWYXMQSWTKISLMWEFSSKTPWWRXIVLMAIIXRFETMRWEEEIYWXVXMFWWXIKIVGRHSSLLRWGMIJYXILOSVEMIXITEMLIMSMISEJXVHIZVSRSVHXEXVYSIMLSWLERSWWOVFHCEMRIVRVFEHPTZJRPSYVVIESRXJIVRJWIMGWR`
    
    - frekans analizi:

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py                          
        I:      66
        S:      56
        X:      45
        E:      41
        M:      38
        V:      37
        L:      36
        W:      34
        R:      29
        H:      28
        P:      21
        A:      16
        J:      15
        G:      12
        T:      11
        Y:      10
        C:      9
        K:      9
        Z:      8
        F:      8
        Q:      6
        O:      3
        B:      1
        ```
    
    - Hesapla:
        - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=I(9)
        - K=?
        - C=E(4)
        - I-E=5(E)
    - O halde 9 harflik anahtarımızın 2. harfi: `E`

- **Anahtarı Bulalım 3/9**

    - vignere_shift(found1, key_length=9, shift=2):
    
        `URRPQYMCJRMCCLWQGRMQQMFDCRPLDCLMUGRYRUGQBMGPGQCMTSCALCEEOYCMYCGHCYRMLRQFJBYTCCLPRTFSRCCLGTUBYDCRSBYCRZPFCRDYBKLSRCYQEMKCJFGSDCMQCDWYYCLGMKEYCQWCPMADSYGCFBPCCMGAMRLAM`

    - vignere_shift(found2, key_length=9, shift=2):
    
        `CEQMAFLPCPNMQKGCMWHMLQCLCSCZCMTRJEBMBMPTCGJBYQGGCJQQIBKCPGMGUDYNBQPEBGIGUQUJUMYCCASCLPRGSCYBICUMFBLLPBCZLGGJCPBRDBPZJEQRBPGUJSBCFPCFCPRMKLGQRAGCFYRTQLCPGPRYRBDFCRWLGCCRIYCJQIBGQR`

    - vignere_shift(found3, key_length=9, shift=2):
    
        `PYGIYIMGLKGUYRQLRRYACCMYTMLQCQMVFAFLFBJDQPFGQSBSMPFSYGQRMQBFLFRUZRMACJRSPAJQGRCRUPPRRRPMNGMBCLLYWFYCLUYRFLCQLCJCAFYQLIYQJLLKYQMPPMNYCSBRYFMAGCLKPKCPJCQRKZCLRYMCTKMPEGYYLQMYYREJKQCCYLLMFQJQIJGCLCRA`

    - birleştir:

        `URRPQYMCJRMCCLWQGRMQQMFDCRPLDCLMUGRYRUGQBMGPGQCMTSCALCEEOYCMYCGHCYRMLRQFJBYTCCLPRTFSRCCLGTUBYDCRSBYCRZPFCRDYBKLSRCYQEMKCJFGSDCMQCDWYYCLGMKEYCQWCPMADSYGCFBPCCMGAMRLAMCEQMAFLPCPNMQKGCMWHMLQCLCSCZCMTRJEBMBMPTCGJBYQGGCJQQIBKCPGMGUDYNBQPEBGIGUQUJUMYCCASCLPRGSCYBICUMFBLLPBCZLGGJCPBRDBPZJEQRBPGUJSBCFPCFCPRMKLGQRAGCFYRTQLCPGPRYRBDFCRWLGCCRIYCJQIBGQRPYGIYIMGLKGUYRQLRRYACCMYTMLQCQMVFAFLFBJDQPFGQSBSMPFSYGQRMQBFLFRUZRMACJRSPAJQGRCRUPPRRRPMNGMBCLLYWFYCLUYRFLCQLCJCAFYQLIYQJLLKYQMPPMNYCSBRYFMAGCLKPKCPJCQRKZCLRYMCTKMPEGYYLQMYYREJKQCCYLLMFQJQIJGCLCRA`
    
    - frekans analizi:

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py
        C:      74
        R:      46
        M:      43
        Y:      41
        Q:      40
        L:      39
        G:      38
        P:      33
        B:      26
        F:      24
        J:      20
        S:      15
        U:      14
        A:      14
        K:      13
        D:      11
        E:      10
        T:      9
        I:      9
        W:      6
        Z:      6
        N:      4
        H:      2
        O:      1
        V:      1
        ```
    
    - Hesapla:
        - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=C(3)
        - K=?
        - C=E(4)
        - C-E=Y(-1)
    - O halde 9 harflik anahtarımızın 3. harfi: `Y`

- **Anahtarı Bulalım 4/9**

    - vignere_shift(found1, key_length=9, shift=3):
    
        `LZHDTRXLTHNQPNTPRSQTAAPOSSPZZCRSPYSJSLVPEQPTDMTZTAOZZHHPFAZYYCELPTSQMCNLEDEPDDRLEPPCSGOECPPPYLCSECECHWEZEPPOEPNYLYOHFYTYLLOYJCFLDEPDEQZEFPPCCSNPZAZMMXNELXESEXZPFSDVO`

    - vignere_shift(found2, key_length=9, shift=3):
    
        `YZQGZPELCRPLSHEQQQZXHLXRLCWJEYPCPCQZMHCPOZOPNOCELLNCPZCADXQYLDATXHWPZWPDODPOTWTHAPELDTRWEOMEQDLFZRDOEAYZNWYQEEDEZEOPHYDSADWLJAECPPPXCRSYLEELTLEYPYPPLOLTOTDOSLQPXJOLEDWGPCNLEPLDM`

    - vignere_shift(found3, key_length=9, shift=3):
    
        `JYNPYYFNZZDLDAROJSYPMSODLCDQPPQEZVZHPOPWPJTNEXPEVPTYXWSSQDLTRTZLCSFSNEPYLPWDPTOSTZTSSSTYLWXCIZDONTYEPEYAPEWTDAWOLPYDOPYNJNRMXDCLJQEWLDSSDTTNZORLPPXXZXVWELEZPYYDPPFEPYGNOMYCDCDDAPBYDPPEPFWPDLEYNTQP`

    - birleştir:

        `LZHDTRXLTHNQPNTPRSQTAAPOSSPZZCRSPYSJSLVPEQPTDMTZTAOZZHHPFAZYYCELPTSQMCNLEDEPDDRLEPPCSGOECPPPYLCSECECHWEZEPPOEPNYLYOHFYTYLLOYJCFLDEPDEQZEFPPCCSNPZAZMMXNELXESEXZPFSDVOYZQGZPELCRPLSHEQQQZXHLXRLCWJEYPCPCQZMHCPOZOPNOCELLNCPZCADXQYLDATXHWPZWPDODPOTWTHAPELDTRWEOMEQDLFZRDOEAYZNWYQEEDEZEOPHYDSADWLJAECPPPXCRSYLEELTLEYPYPPLOLTOTDOSLQPXJOLEDWGPCNLEPLDMJYNPYYFNZZDLDAROJSYPMSODLCDQPPQEZVZHPOPWPJTNEXPEVPTYXWSSQDLTRTZLCSFSNEPYLPWDPTOSTZTSSSTYLWXCIZDONTYEPEYAPEWTDAWOLPYDOPYNJNRMXDCLJQEWLDSSDTTNZORLPPXXZXVWELEZPYYDPPFEPYGNOMYCDCDDAPBYDPPEPFWPDLEYNTQP`
    
    - frekans analizi:

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py
        P:      72
        E:      48
        L:      43
        D:      39
        Y:      35
        Z:      32
        T:      29
        S:      28
        O:      28
        C:      28
        N:      20
        Q:      19
        W:      18
        X:      17
        A:      15
        H:      13
        R:      13
        J:      10
        M:      10
        F:      10
        V:      5
        G:      4
        I:      1
        B:      1
        ```
    
    - Hesapla:
        - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=P(16)
        - K=?
        - C=E(4)
        - P-E=L(12)
    - O halde 9 harflik anahtarımızın 4. harfi: `L`

- **Anahtarı Bulalım 5/9**

    - vignere_shift(found1, key_length=9, shift=4):
    
        `WJEXXIMKWELMTVXELIHXVIAIEMYXVIHIVKIMIWIRLMWXXIZHPIIQRIMNIPRIHILARVIJSMPRSSIWEXWPPVCPSIECMPVHHZMMLIXJIILQMMKLLEIGVXIETERXRHSHIVXKTLEXYMVCXVWXSESRAPRVNILSZSEYLQRMKISP`

    - vignere_shift(found2, key_length=9, shift=4):
    
        `XXYIYJLASIRGMEAPGSYPMRIVRSPXLPREJESXIRIVIRISLEXWFRYEEKPELWMWXLTRYEMVKPXXVMEWRIVMVPXJMWSPMVELEWCTAIZLSYXSSPIMGSXLVLFVEIIIEFFCAJSSSWWISISIRSERIQGXVHVVRPPRISSFIRIREJVFSTPITKYVSXPAV`

    - vignere_shift(found3, key_length=9, shift=4):
    
        `SHEHHIHOVRJMXMVPEIHRVIPEMLXMOEEYIPYIAPIEXGWLSISAIEXJIOMSEMRWWXTZSIVSOLHPXLCIXPYIKJKEEIRIMPTITJFESWHLHVBIGMSRFVCAVVHIGWHSSSLPEMLMHJLSOIIILWXSRJPCEXEVVEJIIRSAPOWWSWVERXIOJIHMXEMSECYGARCQLGMPMXMCIGV`

    - birleştir:

        `WJEXXIMKWELMTVXELIHXVIAIEMYXVIHIVKIMIWIRLMWXXIZHPIIQRIMNIPRIHILARVIJSMPRSSIWEXWPPVCPSIECMPVHHZMMLIXJIILQMMKLLEIGVXIETERXRHSHIVXKTLEXYMVCXVWXSESRAPRVNILSZSEYLQRMKISPXXYIYJLASIRGMEAPGSYPMRIVRSPXLPREJESXIRIVIRISLEXWFRYEEKPELWMWXLTRYEMVKPXXVMEWRIVMVPXJMWSPMVELEWCTAIZLSYXSSPIMGSXLVLFVEIIIEFFCAJSSSWWISISIRSERIQGXVHVVRPPRISSFIRIREJVFSTPITKYVSXPAVSHEHHIHOVRJMXMVPEIHRVIPEMLXMOEEYIPYIAPIEXGWLSISAIEXJIOMSEMRWWXTZSIVSOLHPXLCIXPYIKJKEEIRIMPTITJFESWHLHVBIGMSRFVCAVVHIGWHSSSLPEMLMHJLSOIIILWXSRJPCEXEVVEJIIRSAPOWWSWVERXIOJIHMXEMSECYGARCQLGMPMXMCIGV`
    
    - frekans analizi:

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py
        I:      73
        S:      46
        E:      45
        X:      40
        V:      39
        M:      38
        R:      34
        P:      33
        L:      30
        W:      24
        H:      21
        J:      16
        Y:      14
        A:      13
        C:      11
        G:      11
        K:      10
        T:      10
        F:      8
        O:      7
        Z:      5
        Q:      5
        N:      2
        B:      1
        ```
    
    - Hesapla:
        - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=I(9)
        - K=?
        - C=E(4)
        - I-E=E(5)
    - O halde 9 harflik anahtarımızın 5. harfi: `E`

- **Anahtarı Bulalım 6/9**

    - vignere_shift(found1, key_length=9, shift=5):
    
        `GGFBJBGRUFBGBRJFGFNJVVVFQAFURNVNRQBACFGGNGGVRVRBVETCYEGNRNGBGNNNJSGEGRRPGSCBAUVJRVRBHAASGNRGNBBFPPNVAFQNPAHRRCOVEFSYBAFUROAQNNVRVVEFEPVEGRVUSQZTARTVREFEREAZNHFIUPSN`

    - vignere_shift(found2, key_length=9, shift=5):
    
        `UFYEEBRRLURUFFVBREEBANANNHRURLGIGGEURNFBFFJSJZLQYQEGYXBFNRGBNNRTQFXFGOGBNEGNQEGYRLJGEUGAJBERFVFYPANBPYYGESFEUPVRPRROLQAZFLRFEESBQGGALGHXJTYQFRBYQGFNQNYTAHSRPQRNABRESEJEGRSTGFBNR`

    - vignere_shift(found3, key_length=9, shift=5):
    
        `EZYJBRJVBHYFUGNBTYRPVURYAVBGNASEFRTEBVXKGYUJOQSUQFJEABFHSAPFJRFRXAVEFNVVFNFQRYCDOZUGIVLOAGBFEGNUYPUBONVEBNEGNVBVRCCPNRPZSZVNAGVGEGRSSQFQRPVZCBNPGBLWELBZYXYLYVVVSGGVGUYJBGBFQIEAARVURTRHNUASERFRJNB`

    - birleştir:

        `GGFBJBGRUFBGBRJFGFNJVVVFQAFURNVNRQBACFGGNGGVRVRBVETCYEGNRNGBGNNNJSGEGRRPGSCBAUVJRVRBHAASGNRGNBBFPPNVAFQNPAHRRCOVEFSYBAFUROAQNNVRVVEFEPVEGRVUSQZTARTVREFEREAZNHFIUPSNUFYEEBRRLURUFFVBREEBANANNHRURLGIGGEURNFBFFJSJZLQYQEGYXBFNRGBNNRTQFXFGOGBNEGNQEGYRLJGEUGAJBERFVFYPANBPYYGESFEUPVRPRROLQAZFLRFEESBQGGALGHXJTYQFRBYQGFNQNYTAHSRPQRNABRESEJEGRSTGFBNREZYJBRJVBHYFUGNBTYRPVURYAVBGNASEFRTEBVXKGYUJOQSUQFJEABFHSAPFJRFRXAVEFNVVFNFQRYCDOZUGIVLOAGBFEGNUYPUBONVEBNEGNVBVRCCPNRPZSZVNAGVGEGRSSQFQRPVZCBNPGBLWELBZYXYLYVVVSGGVGUYJBGBFQIEAARVURTRHNUASERFRJNB`
    
    - frekans analizi:

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py
        R:      57
        G:      51
        F:      44
        N:      44
        B:      41
        V:      39
        E:      39
        A:      29
        U:      23
        Y:      23
        Q:      21
        S:      20
        J:      18
        P:      18
        L:      11
        T:      10
        Z:      10
        H:      9
        C:      8
        O:      8
        X:      6
        I:      4
        K:      1
        D:      1
        W:      1
        ```
    
    - Hesapla:
        - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=R(18)
        - K=?
        - C=E(4)
        - I-E=N(14)
    - O halde 9 harflik anahtarımızın 6. harfi: `N`
    - Büyük ihtimalle anahtar `KEYLENGTH` ancak `KEYLENKEY` olarak da çıkabilir. O halde anahtar `KEYLEN` olurdu ve 6 karakterli olurdu.

- **Anahtarı Bulalım 7/9**

    - vignere_shift(found1, key_length=9, shift=6):
    
        `NOZLGLCUTZLCIJGUOKXGTZTVKMCOARXBGOZYKUNVZYGKJTJXTRXGEKNCTONLNQRTOGNGNYGXNZXLJGTKJZGXYNJOAZIUZAJSUKOBZYGVVZGXYVETGCURLJZKMKRUXVZYXYRAGOMGNSTRKRKRGLXZIOZKVKZGTTEKGNZT`

    - vignere_shift(found2, key_length=9, shift=6):
    
        `KAROYXNXGUJJINZAXGTTZIZZJYXGXUAKHAZKTZVGZZEZOVYOKOONGKXYQROLTMXNJXKUNKUSCONTYGNRZGUKHGUOGUHTZXOKUZRZURKYJOKKHUXXUIJKYZMGYZONGUUSJLGZGNMOGURBUUTEXCGRZJRHZYZZUZXMUXYUIKUECYLKNVTEG`

    - vignere_shift(found3, key_length=9, shift=6):
    
        `JKNOTGGTATGZUZBTGKBKYGMOUYIZTJOKGYNKXZIKOUKOKCNOLZKUZXRMOGKZGGUYKKTZUZTMKHAGJRAAEUZOKXKEYUYKKKTKUNOAUIKNTRIKTTIZYKKUXIRKLVYTCZYSUUGNGNGXSNCSXXJUGJGGEUXGRVKKYTXXZNUTRKRGXCTYKKOGEYZNRRYIHZMOTELGKSS`

    - birleştir:

        `NOZLGLCUTZLCIJGUOKXGTZTVKMCOARXBGOZYKUNVZYGKJTJXTRXGEKNCTONLNQRTOGNGNYGXNZXLJGTKJZGXYNJOAZIUZAJSUKOBZYGVVZGXYVETGCURLJZKMKRUXVZYXYRAGOMGNSTRKRKRGLXZIOZKVKZGTTEKGNZTKAROYXNXGUJJINZAXGTTZIZZJYXGXUAKHAZKTZVGZZEZOVYOKOONGKXYQROLTMXNJXKUNKUSCONTYGNRZGUKHGUOGUHTZXOKUZRZURKYJOKKHUXXUIJKYZMGYZONGUUSJLGZGNMOGURBUUTEXCGRZJRHZYZZUZXMUXYUIKUECYLKNVTEGJKNOTGGTATGZUZBTGKBKYGMOUYIZTJOKGYNKXZIKOUKOKCNOLZKUZXRMOGKZGGUYKKTZUZTMKHAGJRAAEUZOKXKEYUYKKKTKUNOAUIKNTRIKTTIZYKKUXIRKLVYTCZYSUUGNGNGXSNCSXXJUGJGGEUXGRVKKYTXXZNUTRKRGXCTYKKOGEYZNRRYIHZMOTELGKSS`
    
    - frekans analizi:

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py
        K:      59
        G:      55
        Z:      53
        U:      43
        T:      37
        X:      36
        O:      33
        Y:      32
        N:      31
        R:      26
        J:      21
        I:      14
        L:      13
        A:      13
        C:      12
        V:      12
        E:      12
        M:      11
        S:      9
        H:      7
        B:      5
        Q:      2
        ```
    
    - Hesapla:
        - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=K(11)
        - K=?
        - C=E(4)
        - K-E=G(7)
    - O halde 9 harflik anahtarımızın 7. harfi: `G`

- **Anahtarı Bulalım 8/9**

    - vignere_shift(found1, key_length=9, shift=7):
    
        `XFAMLPTYXAUTANLGMTDLZPMTOUXGLEXXEKAAKYXXLGNLHZYYMTXKMTTTPGXXXBTWMVKGVBKRXAXEYMZKYPKWTNLOTBHXMKTKMGGXBXRKKAKTNXTZGXKHEPXVAXRSLILTBOTIEXBIXXMROTMBGKXBMVKEKBMGTBXWGBAX`

    - vignere_shift(found2, key_length=9, shift=7):
    
        `FVRGXXXTEMMHNXAKXFXWXAMNOMNMXGKEXEAKLMXWBABAMTMLLMMXKGKXBYGLZZYTRTTKXTVHXYXWXUXLMMBKXEUZGFXULMKTGEBPGHFBRGTLTGTXGHVBTHXBXAGXIFHABHUHETAGLBDTYNLTTHGFARHRTIAPGAHXYFLPEMKPBJLYXTZMD`

    - vignere_shift(found3, key_length=9, shift=7):
    
        `XMXMXGMZLWIVNXBZBOTHDWTMYUDXWPGAGMIMXMKGGLTZITTVTAKFLZBAGVPHLLYMNBZAYZMATBIGPBGTTBXMVHTLMMXKLEDTNXLZKXMTYUEEDVVAHHKGXHHXTEKVABIKILKBLBBTHTBHXTRFGTLKHGTGLEMLHERPXXXRXBBKPBTBTEGGLPXHEBLABKRMHXBKLXY`

    - birleştir:

        `XFAMLPTYXAUTANLGMTDLZPMTOUXGLEXXEKAAKYXXLGNLHZYYMTXKMTTTPGXXXBTWMVKGVBKRXAXEYMZKYPKWTNLOTBHXMKTKMGGXBXRKKAKTNXTZGXKHEPXVAXRSLILTBOTIEXBIXXMROTMBGKXBMVKEKBMGTBXWGBAXFVRGXXXTEMMHNXAKXFXWXAMNOMNMXGKEXEAKLMXWBABAMTMLLMMXKGKXBYGLZZYTRTTKXTVHXYXWXUXLMMBKXEUZGFXULMKTGEBPGHFBRGTLTGTXGHVBTHXBXAGXIFHABHUHETAGLBDTYNLTTHGFARHRTIAPGAHXYFLPEMKPBJLYXTZMDXMXMXGMZLWIVNXBZBOTHDWTMYUDXWPGAGMIMXMKGGLTZITTVTAKFLZBAGVPHLLYMNBZAYZMATBIGPBGTTBXMVHTLMMXKLEDTNXLZKXMTYUEEDVVAHHKGXHHXTEKVABIKILKBLBBTHTBHXTRFGTLKHGTGLEMLHERPXXXRXBBKPBTBTEGGLPXHEBLABKRMHXBKLXY`
    
    - frekans analizi:

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py
        X:      71
        T:      55
        M:      43
        B:      41
        G:      39
        K:      37
        L:      36
        A:      28
        H:      27
        E:      21
        Y:      17
        P:      15
        Z:      15
        V:      14
        R:      13
        N:      11
        I:      11
        F:      10
        W:      9
        U:      8
        D:      7
        O:      6
        S:      1
        J:      1
        ```
    
    - Hesapla:
        - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=X(24)
        - K=?
        - C=E(4)
        - X-E=T(20)
    - O halde 9 harflik anahtarımızın 8. harfi: `T`

- **Anahtarı Bulalım 9/9**

    - vignere_shift(found1, key_length=9, shift=8):
    
        `ILLPAPZMZLLZVSAVDZUAVHLPLLONDNJUSLLVPHWYVVAPUYVVOALPORSUPMAUYUYHOLVJVALZSLZVPALLVHVVUULLSVUUOLZZAALHLKVVPLKSIHUANYADVLYVVUHLHPTZALZLSUUWPZOVLAVZKVZZZHHHVTVYUJAAFJLI`

    - vignere_shift(found2, key_length=9, shift=8):
    
        `HJAAVUHANLOVZKZPTHFVYPVSLYWADLVSJHLZLOJZULULOUYHTZFYNUFUUVJASFSASASAYWHYYAYAASALFHUUKSLOAHYYPOPZJLZHJMHUVKJPYJIUJUOUZHYSULNHWOAHUYSMNAIKZUPYTALUDWKHLDPHAVLLJLVUZHLUVAULABHSWZVVM`

    - vignere_shift(found3, key_length=9, shift=8):
    
        `YOSOHKJHZLWVNKALUPUMMHUAPYPKJLLPKVSYHSPDNLKPYZPOYVLMVSUULJPJHAAOWNILZSOAHAWKHNKPWZFTVDYVVOKCZSOSYLMOLZFWPHLSDPBAMWOKZUAHULLLVUVSWSYZATKDCPZKWFDLFFRCYSNMVLTZUVLLUOUVTYUKHEUYSSAKOLHBHZPPAHVOAHMZPSY`

    - birleştir:

        `ILLPAPZMZLLZVSAVDZUAVHLPLLONDNJUSLLVPHWYVVAPUYVVOALPORSUPMAUYUYHOLVJVALZSLZVPALLVHVVUULLSVUUOLZZAALHLKVVPLKSIHUANYADVLYVVUHLHPTZALZLSUUWPZOVLAVZKVZZZHHHVTVYUJAAFJLIHJAAVUHANLOVZKZPTHFVYPVSLYWADLVSJHLZLOJZULULOUYHTZFYNUFUUVJASFSASASAYWHYYAYAASALFHUUKSLOAHYYPOPZJLZHJMHUVKJPYJIUJUOUZHYSULNHWOAHUYSMNAIKZUPYTALUDWKHLDPHAVLLJLVUZHLUVAULABHSWZVVMYOSOHKJHZLWVNKALUPUMMHUAPYPKJLLPKVSYHSPDNLKPYZPOYVLMVSUULJPJHAAOWNILZSOAHAWKHNKPWZFTVDYVVOKCZSOSYLMOLZFWPHLSDPBAMWOKZUAHULLLVUVSWSYZATKDCPZKWFDLFFRCYSNMVLTZUVLLUOUVTYUKHEUYSSAKOLHBHZPPAHVOAHMZPSY`
    
    - frekans analizi:

        ```bash
        ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
        └─$ python freq_analysis.py
        L:      64
        V:      50
        U:      48
        A:      47
        H:      42
        Z:      38
        P:      33
        Y:      33
        S:      32
        O:      25
        K:      21
        J:      18
        W:      15
        M:      12
        N:      12
        D:      11
        F:      11
        T:      9
        I:      6
        B:      3
        C:      3
        R:      2
        E:      1
        ```
    
    - Hesapla:
        - Şimdi, P-C=K olacağından ve yine en sık kullanılan harf E olduğundan:
        - P=L(12)
        - K=?
        - C=E(4)
        - L-E=H(8)
    - O halde 9 harflik anahtarımızın 9. harfi: `H`

- Anahtarı bulduk: `KEYLENGTH` Şimdi yeni seviye anahtarımızı bulalım. 

    ```bash
    krypton5@bandit:/krypton/krypton5$ cat krypton6 
    BELOS Z
    krypton5@bandit:/krypton/krypton5$ 
    ```

    ```bash
    ┌──(fr0stb1rd㉿sekademi)-[/media/fr0stb1rd/sekademi/fr0stb1rd]
    └─$ python3 vignere_decode.py 
    RANDOM
    ```

- Bu yaptığımız saldırıya `Kasiski Saldırısı` denir.

- "Benim bu kadar zamanım yok" culardansanız (`benim öğrenmeye merakım yok amacım soytarılık` diyorsanız) bazı online çözümler:

    - [oxentriq.com](https://www.boxentriq.com/code-breaking/vigenere-cipher)
        - tüm found keyleri yapıştır, key_length=9 olarak ayarla, decode without key'e tıkla.
    - [dcode.fr](https://www.dcode.fr/vigenere-cipher)
        - tüm found keyleri yapıştır, key_length=9 olarak ayarla, decrypt'a tıkla.
    - ve bunun gibi onlarca online tool...

- yeni parola: `RANDOM` 


### Krypton Level 6 -> 7

- ssh ile bağlanalım: `ssh krypton6@krypton.labs.overthewire.org -p 2231`

- önceki seviyede bulduğumuz parolayı girelim: `RANDOM`

- Önceki seviyelerde bahsedildiği üzere `/krypton/krypton6` dizinine gidip readme dosyasını okuyalım:

    ```bash
    krypton6@bandit:/krypton/krypton6$ cat README 
    Hopefully by now its obvious that encryption using repeating keys
    is a bad idea.  Frequency analysis can destroy repeating/fixed key
    substitution crypto.

    A feature of good crypto is random ciphertext.  A good cipher must
    not reveal any clues about the plaintext.  Since natural language 
    plaintext (in this case, English) contains patterns, it is left up
    to the encryption key or the encryption algorithm to add the 
    'randomness'.

    Modern ciphers are similar to older plain substitution 
    ciphers, but improve the 'random' nature of the key.

    An example of an older cipher using a complex, random, large key
    is a vigniere using a key of the same size of the plaintext.  For
    example, imagine you and your confident have agreed on a key using
    the book 'A Tale of Two Cities' as your key, in 256 byte blocks.

    The cipher works as such:

    Each plaintext message is broken into 256 byte blocks.  For each 
    block of plaintext, a corresponding 256 byte block from the book
    is used as the key, starting from the first chapter, and progressing.
    No part of the book is ever re-used as key.  The use of a key of the 
    same length as the plaintext, and only using it once is called a "One Time Pad".

    Look in the krypton6/onetime  directory.  You will find a file called 'plain1', a 256 
    byte block.  You will also see a file 'key1', the first 256 bytes of
    'A Tale of Two Cities'.  The file 'cipher1' is the cipher text of 
    plain1.  As you can see (and try) it is very difficult to break
    the cipher without the key knowledge.

    (NOTE - it is possible though.  Using plain language as a one time pad
    key has a weakness.  As a secondary challenge, open README in that directory)

    If the encryption is truly random letters, and only used once, then it
    is impossible to break.  A truly random "One Time Pad" key cannot be
    broken.  Consider intercepting a ciphertext message of 1000 bytes.  One
    could brute force for the key, but due to the random key nature, you would
    produce every single valid 1000 letter plaintext as well.  Who is to know
    which is the real plaintext?!?

    Choosing keys that are the same size as the plaintext is impractical.
    Therefore, other methods must be used to obscure ciphertext against 
    frequency analysis in a simple substitution cipher.  The
    impracticality of an 'infinite' key means that the randomness, or
    entropy, of the encryption is introduced via the method.

    We have seen the method of 'substitution'.  Even in modern crypto,
    substitution is a valid technique.  Another technique is 'transposition',
    or swapping of bytes.

    Modern ciphers break into two types; symmetric and asymmetric.

    Symmetric ciphers come in two flavours: block and stream.

    Until now, we have been playing with classical ciphers, approximating
    'block' ciphers.  A block cipher is done in fixed size blocks (suprise!).
    For example, in the previous paragraphs we discussed breaking text and keys
    into 256 byte blocks, and working on those blocks.  Block ciphers use a
    fixed key to perform substituion and transposition ciphers on each
    block discretely.

    Its time to employ a stream cipher.  A stream cipher attempts to create
    an on-the-fly 'random' keystream to encrypt the incoming plaintext one
    byte at a time.  Typically, the 'random' key byte is xor'd with the 
    plaintext to produce the ciphertext.  If the random keystream can be
    replicated at the recieving end, then a further xor will produce the
    plaintext once again.

    From this example forward, we will be working with bytes, not ASCII 
    text, so a hex editor/dumper like hexdump is a necessity.  Now is the
    right time to start to learn to use tools like cryptool.

    In this example, the keyfile is in your directory, however it is 
    not readable by you.  The binary 'encrypt6' is also available.
    It will read the keyfile and encrypt any message you desire, using
    the key AND a 'random' number.  You get to perform a 'known ciphertext'
    attack by introducing plaintext of your choice.  The challenge here is 
    not simple, but the 'random' number generator is weak.

    As stated, it is now that we suggest you begin to use public tools, like cryptool,
    to help in your analysis.  You will most likely need a hint to get going.
    See 'HINT1' if you need a kicktstart.

    If you have further difficulty, there is a hint in 'HINT2'.

    The password for level 7 (krypton7) is encrypted with 'encrypt6'.

    Good Luck!
    krypton6@bandit:/krypton/krypton6$ 
    ```

    - Metin, tekrar eden anahtarlar kullanılarak yapılan şifrelemenin kötü bir fikir olduğunu ve frekans analizi ile kolayca kırılabileceğini anlatıyor. İyi bir şifrenin, düz metin hakkında hiçbir ipucu vermemesi gerektiği belirtiliyor. Modern şifreler, eski basit yerine koyma şifrelerine benzese de, anahtarın rastgele doğasını geliştirirler.

    - Metin, "One Time Pad" (Tek Seferlik Blok Şifreleme) yönteminden bahsediyor. Bu yöntemde, her düz metin mesajı 256 baytlık bloklara bölünür ve her blok için aynı uzunlukta ve sadece bir kez kullanılacak bir anahtar kullanılır. Örneğin, "A Tale of Two Cities" kitabının ilk 256 baytı bu amaçla kullanılabilir. Bu yöntemin güçlü bir şifreleme sağladığı, ancak pratik olmadığı belirtiliyor.

    - Şifrelemenin rastgele harfler kullanarak yapılması ve sadece bir kez kullanılması durumunda kırılamaz olduğu ifade ediliyor. Ancak, anahtarların düz metinle aynı boyutta olması pratik değildir, bu yüzden diğer yöntemler kullanılır.

    - Modern şifreler iki türe ayrılır: simetrik ve asimetrik. Simetrik şifreler blok ve akış şifreleri olarak ikiye ayrılır. Blok şifrelerinde sabit boyutlu bloklar üzerinde çalışılırken, akış şifrelerinde veri akışı sırasında her bayt için rastgele bir anahtar bayt kullanılarak şifreleme yapılır. Akış şifreleri, gelen düz metni bir bayt bir bayt şifrelemek için 'rastgele' bir anahtar dizisi oluşturur ve bu anahtar bayt, düz metinle XOR işlemine tabi tutulur.

    - Bu örnekte, dizindeki anahtar dosyası okunamıyor ve "encrypt6" adlı bir ikili dosya kullanılıyor. Bu dosya anahtar dosyasını okuyarak istediğiniz mesajı şifreler. Şifreleme sırasında zayıf bir rastgele sayı üreteci kullanılır, bu da bilinen bir şifre metni saldırısı yapmanıza olanak tanır.

    - Şifreleme ve analiz için Cryptool gibi kamuya açık araçları kullanmanız tavsiye ediliyor. Eğer yardıma ihtiyaç duyarsanız, HINT1 ve HINT2 adlı dosyalarda ipuçları bulunuyor.

    - Seviye 7'nin (krypton7) şifresi "encrypt6" ile şifrelenmiştir. İyi şanslar!

- İpuçları:

    ```bash
    krypton6@bandit:/krypton/krypton6$ cat HINT1
    The 'random' generator has a limited number of bits, and is periodic.
    Entropy analysis and a good look at the bytes in a hex editor will help.

    There is a pattern!
    ```

    ```
    "Rastgele" sayı üreticisi sınırlı sayıda bit içerir ve periyodiktir. Entropi analizi ve hex editörde baytlara iyi bir bakış yardımcı olacaktır.

    Bir desen var!
    ```

    ```bash
    krypton6@bandit:/krypton/krypton6$ cat HINT2
    8 bit LFSR
    ```

- Bizden akış şifrelemesini kırmamızı istiyor. Biraz bilgi:

    - Akış şifrelemesi, her baytı şifrelemek için bir anahtar akışı (keystream) kullanarak veriyi bayt bayt şifreleyen bir şifreleme yöntemidir. XOR (Exclusive OR) işlemi genellikle kullanılır:
        - **Anahtar Akışı (Keystream)**: Bir rastgele veya pseudo-rastgele anahtar akışı oluşturulur.
        - **XOR İşlemi**: Düz metin baytları ile anahtar akışı baytları XOR işlemiyle şifrelenir.
            - Her bayt için `Şifreli Metin = Düz Metin XOR Anahtar` işlemi yapılır.

    - Çözme:
        - **XOR İşlemi**: Aynı anahtar akışı kullanılarak şifreli metin çözülür. `Düz Metin = Şifreli Metin XOR Anahtar` işlemiyle orijinal düz metin elde edilir.

    - Akış Şifrelemesinin Kırılması
        - Akış şifrelemeleri, genellikle XOR işlemi ve pseudo-rastgele anahtar akışı kullanır. Akış şifrelemesinin kırılması, genellikle anahtar akışının zayıf yönlerinden yararlanarak yapılır.

    - **Bilinen Düz Metin Saldırısı (Known Plaintext Attack)**:
        - Şifreli metnin bir kısmı ve buna karşılık gelen düz metin biliniyorsa, bu kısım kullanılarak anahtar akışı bulunabilir.
        - Düz metin ve şifreli metin XOR işlemi ile anahtar akışını verir: `Anahtar = Düz Metin XOR Şifreli Metin`

    - **Seçili Düz Metin Saldırısı (Chosen Plaintext Attack)**:
        - Saldırgan, belirli bir düz metni şifreleterek şifreli metni elde eder. Bu şekilde anahtar akışını belirleyebilir.
        - Belirli düz metinler (örneğin uzun bir 'A' dizisi) kullanılarak anahtar akışı elde edilebilir.

    - **Zayıf Anahtar Akışı (Weak Keystream)**:
        - Pseudo-rastgele anahtar akışı üreten algoritmanın zayıflıkları bulunabilir.
        - Anahtar akışı periyodikse veya tahmin edilebilirse, bu durum şifrelemenin kırılmasını sağlar.

    - **Doğrusal Geri Beslemeli Kaydırma Yazmacı (LFSR) Analizi**:
        - LFSR'ler genellikle tekrar eden ve tahmin edilebilir desenler üretir.
        - LFSR'nin dönme periyodu ve doğrusal geri besleme fonksiyonu çözülerek anahtar akışı bulunabilir.

    - Örnek:
        - Diyelim ki bir akış şifrelemesi şu şekilde çalışıyor:
            - Düz Metin: `HELLO`
            - Anahtar Akışı: `XMCKL`
            - Şifreli Metin: `DHLNO`
        - Eğer şifreli metin ve düz metin biliniyorsa:
            - `H (72) XOR X (88) = D (68)` bu işlem tekrarlanarak anahtar akışı bulunur.
        - Anahtar akışı: `XMCKL`

- Biz `Seçili Düz Metin Saldırısı (Chosen Plaintext Attack)` kullanacağız.
    - her 'A', 'A'nın konumuna bağlı olarak şifreli metinde farklı bir alfabe karakteriyle eşleşecek.

- yeni bir temp dizin oluşturup oraya gidelim:

    ```bash
    krypton6@bandit:/krypton/krypton6$ mktemp -d
    /tmp/tmp.aG2mWXRG9k
    krypton6@bandit:/krypton/krypton6$ cd /tmp/tmp.aG2mWXRG9k
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ ln -s /krypton/krypton6/keyfile.dat 
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ ln -s /krypton/krypton6/encrypt6
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ chmod 777 .
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ 
    ```

- Örnek bir dosya oluşturalım ve içine 40 tane A harfi yerleştirelim:
    - terminal ile: `printf 'A%.0s' {1..40} > plain.txt`
    - veya python3 ile yapabilirsiniz: `python3 -c 'print("A" * 40)' > plain.txt`

    ```bash
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ cat plain.txt 
    AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ 
    ```

- Oluşturduğumuz dosyayı şifreleyelim ve sonuçlara bakalım:

    ```bash
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ ./encrypt6 plain.txt enc_plain.txt
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ cat plain.txt 
    AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ cat enc_plain.txt 
    EICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZ
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ 
    ```

- İki dosyaya da ipucunda söylediği gibi bayt cinsinden göz atalım:

    ```bash
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ xxd -b plain.txt 
    00000000: 01000001 01000001 01000001 01000001 01000001 01000001  AAAAAA
    00000006: 01000001 01000001 01000001 01000001 01000001 01000001  AAAAAA
    0000000c: 01000001 01000001 01000001 01000001 01000001 01000001  AAAAAA
    00000012: 01000001 01000001 01000001 01000001 01000001 01000001  AAAAAA
    00000018: 01000001 01000001 01000001 01000001 01000001 01000001  AAAAAA
    0000001e: 01000001 01000001 01000001 01000001 01000001 01000001  AAAAAA
    00000024: 01000001 01000001 01000001 01000001 00001010           AAAA.
    ```

    ```bash
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ xxd -b enc_plain.txt 
    00000000: 01000101 01001001 01000011 01010100 01000100 01000111  EICTDG
    00000006: 01011001 01001001 01011001 01011010 01001011 01010100  YIYZKT
    0000000c: 01001000 01001110 01010011 01001001 01010010 01000110  HNSIRF
    00000012: 01011000 01011001 01000011 01010000 01000110 01010101  XYCPFU
    00000018: 01000101 01001111 01000011 01001011 01010010 01001110  EOCKRN
    0000001e: 01000101 01001001 01000011 01010100 01000100 01000111  EICTDG
    00000024: 01011001 01001001 01011001 01011010                    YIYZ
    krypton6@bandit:/tmp/tmp.aG2mWXRG9k$ 
    ```

- İlk baytı ele alırsak:
    - P: `01000001`
    - C: `01000101`
    - K: ?
    - Burada Key (K), P ve C'nin XOR'udur. O halde K: `00000100` Bu da ondalık olarak 4'e eşittir ki 4. harf E harfidir.

- O halde:
    - A: `00000000`
    - B: `00000001`
    - K: `00000001` olacaktır. Yani B'ye eşit olacaktır. Bundan dolayı uzun bir A dizisi oluşturursak tekrar eden deseni bulabiliriz.

- Biz zaten 40 tane A harfini yan yana dizdik:
    - P: `AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA`
    - C: `EICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZ`
    - K: ?
    - K bu durumda yukarıda bahsettiğim üzere C'ye eşit.
    - K: `EICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZ`
    - K'ye dikkatli bakarsak şifreyi bulabiliriz. Tekrar eden bir kısım olmalı:
        - `EICTDGYIYZKTHNSIRFXYCPFUEOCKRN`
        - `EICTDGYIYZ`
        - Ortalardan böldüğümde tekrar eden kısmı buldum.
        - O halde şifre: `EICTDGYIYZKTHNSIRFXYCPFUEOCKRN`

- Bu, vignere şifrelemesini kırarken yaptığımız aynı yöntem. Aynı python scripti ile krypton7 dosyasını kırmaya çalışalım:
    ```bash
    krypton6@bandit:/krypton/krypton6$ ls -la
    total 56
    drwxr-xr-x 3 root     root      4096 Jun 16 02:49 .
    drwxr-xr-x 9 root     root      4096 Jun 16 02:49 ..
    -rwsr-x--- 1 krypton7 krypton6 16520 Jun 16 02:49 encrypt6
    -rw-r----- 1 krypton6 krypton6   164 Jun 16 02:49 HINT1
    -rw-r----- 1 krypton6 krypton6    11 Jun 16 02:49 HINT2
    -rw-r----- 1 krypton7 krypton7    11 Jun 16 02:49 keyfile.dat
    -rw-r----- 1 krypton6 krypton6    15 Jun 16 02:49 krypton7
    drwxr-xr-x 2 root     root      4096 Jun 16 02:49 onetime
    -rw-r----- 1 krypton6 krypton6  4342 Jun 16 02:49 README
    krypton6@bandit:/krypton/krypton6$ cat krypton7 
    PNUKLYLWRQKGKBE
    krypton6@bandit:/krypton/krypton6$ 
    ```

    ```python
    vignere_decoder("PNUKLYLWRQKGKBE", "EICTDGYIYZKTHNSIRFXYCPFUEOCKRN")
    ```

- yeni parola: `LFSRISNOTRANDOM`

### Krypton Level 7 -> 8

- ssh ile bağlanalım: `ssh krypton7@krypton.labs.overthewire.org -p 2231`

- önceki seviyede bulduğumuz parolayı girelim: `LFSRISNOTRANDOM`

- Büyük ihtimalle tebrikler yazısını okuyacağız:

    ```bash
    krypton7@bandit:~$ cd /krypton/krypton7/
    krypton7@bandit:/krypton/krypton7$ ls -la
    total 12
    drwxr-xr-x 2 root     root     4096 Jun 16 02:49 .
    drwxr-xr-x 9 root     root     4096 Jun 16 02:49 ..
    -rw-r----- 1 krypton7 krypton7   36 Jun 16 02:49 README
    krypton7@bandit:/krypton/krypton7$ cat README 
    Congratulations on beating Krypton!
    krypton7@bandit:/krypton/krypton7$ 
    ```

- ve oyunu bitirdik.

## Notlar

- her oyun arası `exit` veya `logout` ile oturumu sonlandırdık. çünkü `su krypton` gibi oturum değiştirmeye izin vermiyor.

- terminalden kopyalama işlemini metni seçtikten sonra `ctrl+shift+c` ile, terminale yapıştırma işlemini `ctrl+shift+v` ile yapabilirsiniz.

- bu makale, kriptografik bazı teknik temelleri size öğretecek. nasıl çalıştığını anlamak için youtube'da videolar izlemelisiniz. özellikle Sadi Evren Şeker'in videoları güzeldir. Hocama selamlar.

- seviyeleri bitirdikten sonra, gidip video çekin, not alın, gidip siz de makale şeklinde yazın. benden daha da güzelini yapın. daha da açıklayıcı olun. bunları yapmayacaksanız gidin kafanızı çöp kutusuna sokun daha iyi.

- yeni yazıda ya da projede görüşmek dileğiyle, esenlikler...
