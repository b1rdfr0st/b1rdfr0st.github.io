---
title: OverTheWire Leviathan Çözümleri - Adım Adım Rehber (Türkçe)
published: 2024-06-15
updated: 2024-06-15
description: 'A comprehensive Turkish walkthrough guide for solving the OverTheWire Leviathan CTF challenges, focusing on Linux security concepts'
image: ''
tags: [Security, Linux, CTF, Tutorial, Walkthrough]
category: 'Tutorial'
draft: false
---

## Video

uzakta...

## Walkthrough

Oyun Linki: [overthewire.org/wargames/leviathan/](https://overthewire.org/wargames/leviathan/)

### Leviathan Level 0 -> 1

- Verilen bilgilere göre host: `leviathan.labs.overthewire.org` port: `2223` kullanıcı adı: `leviathan0` Parola: `leviathan0`.

- ssh ile bağlanalım: `ssh leviathan0@leviathan.labs.overthewire.org -p 2223`

- parolayı bize verdiği gibi `leviathan0` şeklinde girelim. ssl uyarısına yes diyelim.

- `ls -la` diyerek listeleyelim. burada `.backup` adında bir dizin gördük. burada bir şeyler gizli olabilir.

- `cd .backup` diyerek içine girelim.

- tekrar `ls -la` ile listeleyelim:

    ![](https://i.ibb.co/bHG3bMS/image.png)

    burada `bookmarks.html` adında bir dosya var. içerisinde parola olabilir.

- grep ile filtreleyerek görüntülemeye çalışalım: `cat bookmarks.html | grep leviathan`

    ```bash
    leviathan0@gibson:~/.backup$ cat bookmarks.html | grep leviathan
    <DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is 3QJ3TgzHDq" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
    leviathan0@gibson:~/.backup$ 
    ```

- yeni parola: `3QJ3TgzHDq`

### Leviathan Level 1 -> 2

- ssh ile bağlanalım: `ssh leviathan1@leviathan.labs.overthewire.org -p 2223`

- önceki seviyede bulduğumuz parolayı girelim: `3QJ3TgzHDq`

- `ls -la` ile listeleyince adı `check` olan bir `SUID` dosya gördük.

    ```bash
    leviathan1@gibson:~$ ls -la
    total 36
    drwxr-xr-x  2 root       root        4096 Jun 11 21:30 .
    drwxr-xr-x 83 root       root        4096 Jun 11 21:32 ..
    -rw-r--r--  1 root       root         220 Mar 31 08:41 .bash_logout
    -rw-r--r--  1 root       root        3771 Mar 31 08:41 .bashrc
    -r-sr-x---  1 leviathan2 leviathan1 15080 Jun 11 21:30 check
    -rw-r--r--  1 root       root         807 Mar 31 08:41 .profile
    leviathan1@gibson:~$ 
    ```

- çalıştıralım: `./check`

- parola istiyor. burada `ltrace` aracından yardım alabiliriz. `ltrace`, komut satırı için kullanılan bir tanılama ve hata ayıklama aracıdır. bu araç, çalıştırılan bir süreç tarafından yapılan dinamik kütüphane çağrılarını ve bu sürece gönderilen sinyalleri yakalar ve kaydeder. program tarafından yapılan sistem çağrılarını da yakalayıp ekrana yazdırabilir.

- bir binary dosyasının çalıştırıldığında yaptığı tüm sistem çağrılarını görebiliriz. `ltrace` sayesinde bir programın hangi dış kütüphane fonksiyonlarını kullandığını ve hangi sistem çağrılarını yaptığını detaylı bir şekilde izleyebilir ve analiz edebiliriz.

- `ltrace ./check` ile sistem çağrılarına bir göz atalım:

    ![](https://i.ibb.co/GRd9H67/image.png)

    ```bash
    leviathan1@gibson:~$ ltrace ./check
    __libc_start_main(0x80490ed, 1, 0xffffd4d4, 0 <unfinished ...>
    printf("password: ")                                     = 10
    getchar(0, 0, 0x786573, 0x646f67password: fr0stb1rd
    )                        = 102
    getchar(0, 102, 0x786573, 0x646f67)                      = 114
    getchar(0, 0x7266, 0x786573, 0x646f67)                   = 48
    strcmp("fr0", "sex")                                     = -1
    puts("Wrong password, Good Bye ..."Wrong password, Good Bye ...
    )                     = 29
    +++ exited (status 0) +++
    ```

    - `__libc_start_main(0x80490ed, 1, 0xffffd4d4, 0 <unfinished ...>`
    - Bu, programın başlangıcında `__libc_start_main` fonksiyonunun çağrıldığını gösterir. Bu fonksiyon, programın ana işlevini başlatır ve gerekli başlangıç işlemlerini yapar. Parametreler arasında programın ana fonksiyonu (`0x80490ed`), argüman sayısı (`1`) ve argümanların adresi (`0xffffd4d4`) bulunur.

    - `printf("password: ") = 10`
    - Program `printf` fonksiyonu ile ekrana "password: " mesajını yazar ve bu yazdırma işlemi 10 karakter uzunluğundadır.

    - `getchar(0, 0, 0x786573, 0x646f67password: fr0stb1rd) = 102`
    - Kullanıcıdan bir karakter girişi alınır (`getchar`). Kullanıcı `fr0stb1rd` girdi ve bu girdinin ilk karakteri olan `f` ASCII değerine göre `102` olarak döndü.

    - `getchar(0, 102, 0x786573, 0x646f67) = 114`
    - Kullanıcıdan alınan ikinci karakter `r` ASCII değeri `114` olarak döndü.

    - `getchar(0, 0x7266, 0x786573, 0x646f67) = 48`
    - Kullanıcıdan alınan üçüncü karakter `0` ASCII değeri `48` olarak döndü.

    - `strcmp("fr0", "sex") = -1`
    - Program, kullanıcı girdisinin ilk üç karakterini ("fr0") belirli bir değerle ("sex") karşılaştırıyor. `strcmp` fonksiyonu iki dizeyi karşılaştırır ve eğer eşit değilse negatif bir değer döner. Burada, "fr0" ve "sex" eşleşmediği için `-1` döndü.

    - `puts("Wrong password, Good Bye ..."Wrong password, Good Bye ...) = 29`
    - Karşılaştırma başarısız olduğu için program `puts` fonksiyonu ile "Wrong password, Good Bye ..." mesajını ekrana yazar. Bu yazdırma işlemi 29 karakter uzunluğundadır.

    - `+++ exited (status 0) +++`
    - Program başarıyla (çıkış durumu `0` ile) sona erdiğini belirtir.

    - `ltrace ./check` çıktısı, `./check` programının bir şifre sorduğunu, kullanıcının "fr0stb1rd" şeklinde bir giriş yaptığını, bu girdinin ilk üç karakterinin ("fr0") beklenen şifreyle ("sex") karşılaştırıldığını ve eşleşmediği için "Wrong password, Good Bye ..." mesajı ile programın sonlandığını gösterir.

- `./check` programını çalıştırıp `sex` parolasıyla giriş yapalım.

- whoami yazdığımızda artık `leviathan2` kullanıcısı olarak `bash` başlatmış olduğumuzu görüyoruz. şu anda bu kullanıcı adına işlem yapabiliriz.

- oyunun açıklamalarına göre tüm anahtarlar `/etc/leviathan_pass` adresindeydi. kendi parolamızı alabiliyorsak: `cat /etc/leviathan_pass/leviathan2`

    ![](https://i.ibb.co/BB7X0Mb/image.png)

- yeni parola: `NsN1HwFoyN`

### Leviathan Level 2 -> 3

- ssh ile bağlanalım: `ssh leviathan2@leviathan.labs.overthewire.org -p 2223`

- önceki seviyede bulduğumuz parolayı girelim: `NsN1HwFoyN`

- `ls -la` ile listeleyince adı `printfile` olan bir `SUID` dosya gördük.

    ```bash
    leviathan2@gibson:~$ ls -la
    total 36
    drwxr-xr-x  2 root       root        4096 Jun 11 21:30 .
    drwxr-xr-x 83 root       root        4096 Jun 11 21:32 ..
    -rw-r--r--  1 root       root         220 Mar 31 08:41 .bash_logout
    -rw-r--r--  1 root       root        3771 Mar 31 08:41 .bashrc
    -r-sr-x---  1 leviathan3 leviathan2 15068 Jun 11 21:30 printfile
    -rw-r--r--  1 root       root         807 Mar 31 08:41 .profile
    leviathan2@gibson:~$ 
    ```
- boş olarak çalıştıralım: `./printfile`:

    ```bash
    leviathan2@gibson:~$ ./printfile 
    *** File Printer ***
    Usage: ./printfile filename
    ```

    görünüşe göre bu bir dosya yazdırıcı. `leviathan3` kullanıcısı olarak dosya yazdırmaya yarıyor.

- parolayı almayı deneyelim: `./printfile /etc/leviathan_pass/leviathan3`

    ```bash
    leviathan2@gibson:~$ ./printfile /etc/leviathan_pass/leviathan3
    You cant have that file...
    leviathan2@gibson:~$ 
    ```

- ltrace ile sistem çağrılarını inceleyelim: `ltrace ./printfile /etc/leviathan_pass/leviathan3`

    ```bash
    leviathan2@gibson:~$ ltrace ./printfile /etc/leviathan_pass/leviathan3
    __libc_start_main(0x80490ed, 2, 0xffffd4a4, 0 <unfinished ...>
    access("/etc/leviathan_pass/leviathan3", 4)              = -1
    puts("You cant have that file..."You cant have that file...
    )                       = 27
    +++ exited (status 1) +++
    leviathan2@gibson:~$ 
    ```

    `access` fonksiyonu `-1` döndürüyor. okuma (r) erişimimiz olmadığını söylüyor.

- peki okuma erişimimiz olan `/etc/leviathan_pass/leviathan2` dosyasında ne tepki verecek bakalım:

    ```bash
    leviathan2@gibson:~$ ltrace ./printfile /etc/leviathan_pass/leviathan2
    __libc_start_main(0x80490ed, 2, 0xffffd4a4, 0 <unfinished ...>
    access("/etc/leviathan_pass/leviathan2", 4)              = 0
    snprintf("/bin/cat /etc/leviathan_pass/lev"..., 511, "/bin/cat %s", "/etc/leviathan_pass/leviathan2") = 39
    geteuid()                                                = 12002
    geteuid()                                                = 12002
    setreuid(12002, 12002)                                   = 0
    system("/bin/cat /etc/leviathan_pass/lev"...NsN1HwFoyN
    <no return ...>
    --- SIGCHLD (Child exited) ---
    <... system resumed> )                                   = 0
    +++ exited (status 0) +++
    leviathan2@gibson:~$ 
    ```

    - `__libc_start_main(0x80490ed, 2, 0xffffd4a4, 0 <unfinished ...>`
        - Bu, programın başlangıcında `__libc_start_main` fonksiyonunun çağrıldığını gösterir. Bu fonksiyon, programın ana işlevini başlatır ve gerekli başlangıç işlemlerini yapar. Parametreler arasında programın ana fonksiyonu (`0x80490ed`), argüman sayısı (`2`) ve argümanların adresi (`0xffffd4a4`) bulunur.

    - `access("/etc/leviathan_pass/leviathan2", 4) = 0`
        - Program, `/etc/leviathan_pass/leviathan2` dosyasına erişim iznini kontrol eder ve bu izin kontrolü başarılıdır (`0` döner).

    - `snprintf("/bin/cat /etc/leviathan_pass/lev"..., 511, "/bin/cat %s", "/etc/leviathan_pass/leviathan2") = 39`
        - Program, `snprintf` fonksiyonunu kullanarak bir komut oluşturur: `/bin/cat /etc/leviathan_pass/leviathan2`. Bu komut 39 karakter uzunluğundadır.

    - `geteuid() = 12002`
        - Program, etkili kullanıcı kimliğini (`EUID`) alır ve bu değer `12002` olarak döner.

    - `geteuid() = 12002`
        - Program, tekrar etkili kullanıcı kimliğini (`EUID`) alır ve bu değer yine `12002` olarak döner.

    - `setreuid(12002, 12002) = 0`
        - Program, gerçek ve etkili kullanıcı kimliklerini `12002` olarak ayarlar. Bu işlem başarılıdır (`0` döner).

    - `system("/bin/cat /etc/leviathan_pass/lev"...NsN1HwFoyN<no return ...>`
        - Program, `system` fonksiyonunu kullanarak `/bin/cat /etc/leviathan_pass/leviathan2` komutunu çalıştırır ve dosyanın içeriğini ekrana yazdırır: `NsN1HwFoyN`. Bu komut çağrısından sonra geri dönüş değeri yoktur (`<no return ...>`).

    - `--- SIGCHLD (Child exited) ---`
        - Program, alt süreçlerin sona erdiğini belirten `SIGCHLD` sinyalini alır.

    - `<... system resumed> ) = 0`
        - `system` fonksiyonu çalışmasını tamamlar ve `0` döner.

    - `+++ exited (status 0) +++`
        - Program başarıyla (çıkış durumu `0` ile) sona erdiğini belirtir.

    - `ltrace ./printfile /etc/leviathan_pass/leviathan2` çıktısı, `./printfile` programının `/etc/leviathan_pass/leviathan2` dosyasına erişim iznini kontrol ettiğini, bu dosyayı `cat` komutu ile okumak için bir komut oluşturduğunu ve çalıştırdığını gösterir. Program, etkili kullanıcı kimliğini (`EUID`) alıp ayarladıktan sonra komutu çalıştırarak dosyanın içeriğini (`NsN1HwFoyN`) ekrana yazdırır ve başarıyla sona erer.



- access()

    ```c
    int access(const char *path, int mode);
    ```
    - **Açıklama**: Belirtilen dosya yoluna erişim hakkında bilgi sağlar.
    - **Parametreler**:
    - `path`: Erişim bilgisini almak istediğiniz dosyanın veya dizinin yolu.
    - `mode`: Erişim kontrol modu. Erişim hakları ve kontrol işlemleri bu moda göre yapılır.
    - **Dönüş Değeri**:
    - Fonksiyon başarılıysa, 0 döner (başarılı erişim).
    - Hata durumunda, -1 döner ve `errno` değişkeni ayarlanır.
    - **Erişim Kontrol Modları**:
    - `F_OK`: Dosyanın var olup olmadığını kontrol eder.
    - `R_OK`: Dosyanın okunabilir olup olmadığını kontrol eder.
    - `W_OK`: Dosyanın yazılabilir olup olmadığını kontrol eder.
    - `X_OK`: Dosyanın çalıştırılabilir olup olmadığını kontrol eder.
    - **Örnek Kullanım**:
        ```c
        #include <stdio.h>
        #include <unistd.h>

        int main() {
            if (access("/path/to/file.txt", F_OK) == 0) {
                printf("Dosya mevcut.\n");
            } else {
                printf("Dosya mevcut değil veya erişim izni yok.\n");
            }
            return 0;
        }
        ```


- `snprintf()`

    ```c
    int snprintf(char *str, size_t size, const char *format, ...);
    ```
    - **Açıklama**: Belirtilen karakter dizisine belirli bir boyutta formatlanmış bir dize yazdırır.
    - **Parametreler**:
    - `str`: Yazılacak karakter dizisinin hedef adresi.
    - `size`: Yazılacak maksimum karakter sayısı (null karakter dahil).
    - `format`: Formatlama kurallarını belirten kontrol dizesi (printf formatı).
    - `...`: Format dizesindeki değişken sayıda argümanlar.
    - **Dönüş Değeri**:
    - Yazılan karakter sayısı (null karakter dahil) veya olması gereken toplam karakter sayısının eksik kısmı (size - 1), yazma işlemi başarılıysa döner.
    - Hata durumunda, -1 döner.
    - **Önemli Noktalar**:
    - `size` parametresi, `str` için ayrılan bellek boyutunu belirtir. Yazma işlemi, bu boyutu aşmamalıdır.
    - Yazma işlemi sonunda, `str` dizisinin sonuna null karakter ('\0') eklenir.
    - **Örnek Kullanım**:
        ```c
        #include <stdio.h>
        #include <stdlib.h>

        int main() {
            char buffer[50];
            int num = 123;
            float fnum = 3.14f;

            int written = snprintf(buffer, sizeof(buffer), "Sayı: %d, Float: %.2f", num, fnum);

            if (written >= 0 && written < sizeof(buffer)) {
                printf("Yazılan karakter sayısı: %d\n", written);
                printf("Oluşan dize: %s\n", buffer);
            } else {
                printf("snprintf işlemi başarısız oldu.\n");
            }

            return 0;
        }
        ```



- `access()` Fonksiyonunun TOCTOU Yarış Durumu Zafiyeti

    - C dilindeki access() fonksiyonu, çağıran sürecin belirtilen dosyaya erişip erişemeyeceğini kontrol eder. Eğer dosya bir sembolik bağlantı (`symlink`) ise, bu bağlantı hedef dosyaya yönlendirilir.
    
        - `access()` fonksiyonu, dosyanın okuma, yazma gibi çeşitli izinlerini kontrol edebilir. Ancak, bu fonksiyon **TOCTOU (Time-of-Check to Time-of-Use)** olarak bilinen bir zafiyete sahiptir.

    - Zafiyet Açıklaması

        - Program access() fonksiyonunu çağırdıktan sonra open() fonksiyonunu çağırır. Bu iki çağrı arasındaki kısa süre zarfında, dosya içeriği değiştirilebilir. Bu durumda, kötü niyetli bir kullanıcı access() ve open() arasında dosyayı değiştirerek, bir sembolik bağlantı ile erişmesi gerekmeyen bir dosyaya erişebilir.

    - Sömürü Senaryosu

        - **Sembolik Bağlantı Oluşturma**: Örneğin, hassas bir dosyaya işaret eden bir sembolik bağlantı oluşturulur (`/etc/leviathan_pass/leviathan3`).

        - **access() ve open() Kullanımı**: Zafiyetli programda, access() fonksiyonu dosya erişimini kontrol eder ve ardından open() fonksiyonu ile dosya açılır. Bu süre zarfında, saldırgan dosyayı sembolik bağlantı ile değiştirerek güvenlik önlemlerini aşabilir.

- Symlink ve Boşluk Kullanarak İzinsiz Erişim

  - `/etc/leviathan_pass/leviathan3` dosyasına sembolik bağlantı (symlink) oluşturulur.

  - Sistemde bir dosya oluşturulur ve ismi `symlink space` yapılır.

  - Bu dosya, `access()` fonksiyonu ile kontrol edilir. `access()` fonksiyonu, belirtilen yolun erişim durumunu kontrol eder.
  
  - Dosya var olduğu için program artık yukarıda bahsettiğim `system("/bin/cat /etc/leviathan_pass/lev"...>` kısmına gelir.

  - Burada `cat` programına eğer `symlink space` parametresi gelirse:

    - `cat symlink space`

    - cat programı `symlink` ve `space`'i farklı dosyalar olarak algılar ve sadece ilkini açmaya çalışır.

    - peki ilk dosyamız nedir? tabii ki budur:

    - `lrwxrwxrwx   1 leviathan2 leviathan2    30 Jun 14 03:08 symlink -> /etc/leviathan_pass/leviathan3`

- özetle:

    - access() fonksiyonu dosya varlığını kontrol eder. bunun için `symlink space` adında gerçekten var olan bir dosya oluşturmamız gerekir ki access() fonksiyonu başarılı şekilde çalışsın. çünkü dosya var.
    
    - `symlink` adında bir sembolik bağlantı oluştururuz ve `/etc/leviathan_pass/leviathan3` dosyasına yönlendirir.

    - ``cat symlink space` olarak komut girdiğimizde `cat` programı sadece ilk parametreyi açar.

    - Böylece `/etc/leviathan_pass/leviathan3` dosyasını cat ile açtırmış oluruz.

- **Sömürü Konsepti**

    - `mktemp -d` ile yeni bir temp dizin oluşturalım ve `cd` ile oraya gidelim. benim dizinim burası: `/tmp/tmp.rc5u3EPBZR`. isim farklı olabilir.

    - `symlink space` adında bir dosya oluşturalım: `touch symlink\ space`

    - symlink oluşturalım: `ln -s /etc/leviathan_pass/leviathan3 symlink`

    - izin sorunları yaşamamak için bulunduğumuz dizine tüm izinleri verelim: `chmod 777 . && ls -la`

        ```bash
        leviathan2@gibson:/tmp/tmp.rc5u3EPBZR$ ls -la
        total 24
        drwxrwxrwx   2 leviathan2 leviathan2  4096 Jun 14 03:10 .
        drwxrwx-wt 487 root       root       20480 Jun 14 03:15 ..
        lrwxrwxrwx   1 leviathan2 leviathan2    30 Jun 14 03:08 symlink -> /etc/leviathan_pass/leviathan3
        -rw-rw-r--   1 leviathan2 leviathan2     0 Jun 14 03:10 symlink space
        leviathan2@gibson:/tmp/tmp.rc5u3EPBZR$ 
        ```

    - programı çalıştıralım: `~/printfile symlink\ space`

        ```bash
        leviathan2@gibson:/tmp/tmp.rc5u3EPBZR$ ~/printfile symlink\ space
        f0n8h2iWLP
        /bin/cat: space: No such file or directory
        leviathan2@gibson:/tmp/tmp.rc5u3EPBZR$ 
        ```

    - yeni parola: `f0n8h2iWLP`

### Leviathan Level 3 -> 4

- ssh ile bağlanalım: `ssh leviathan3@leviathan.labs.overthewire.org -p 2223`

- önceki seviyede bulduğumuz parolayı girelim: `f0n8h2iWLP`

- `ls -la` ile listeleyince adı `level3` olan bir `SUID` dosya gördük.

    ```bash
    leviathan3@gibson:~$ ls -la
    total 40
    drwxr-xr-x  2 root       root        4096 Jun 11 21:30 .
    drwxr-xr-x 83 root       root        4096 Jun 11 21:32 ..
    -rw-r--r--  1 root       root         220 Mar 31 08:41 .bash_logout
    -rw-r--r--  1 root       root        3771 Mar 31 08:41 .bashrc
    -r-sr-x---  1 leviathan4 leviathan3 18096 Jun 11 21:30 level3
    -rw-r--r--  1 root       root         807 Mar 31 08:41 .profile
    leviathan3@gibson:~$ 
    ```

- Parola korumalı dosya:

    ```bash
    leviathan3@gibson:~$ ./level3 
    Enter the password> fr0stb1rd
    bzzzzzzzzap. WRONG
    leviathan3@gibson:~$ 
    ```

- ltrace ile bakalım:

    ```bash
    leviathan3@gibson:~$ ltrace ./level3 
    __libc_start_main(0x80490ed, 1, 0xffffd494, 0 <unfinished ...>
    strcmp("h0no33", "kakaka")                                  = -1
    printf("Enter the password> ")                              = 20
    fgets(Enter the password> fr0stb1rd
    "fr0stb1rd\n", 256, 0xf7fae5c0)                       = 0xffffd26c
    strcmp("fr0stb1rd\n", "snlprintf\n")                        = -1
    puts("bzzzzzzzzap. WRONG"bzzzzzzzzap. WRONG
    )                                  = 19
    +++ exited (status 0) +++
    ```

- Parola `strcmp("fr0stb1rd\n", "snlprintf\n")` satırından anlayacağımız gibi `snlprintf` imiş. Bulduğumuz parolayı girelim:

    ```bash
    leviathan3@gibson:~$ ./level3 
    Enter the password> snlprintf
    [You've got shell]!
    $ 
    ```

- Bir shell'e sahip olduk. bakalım kimmişiz?

    ```bash
    $ whoami
    leviathan4
    ```

- O halde parolayı alabiliriz?

    ```bash
    $ cat /etc/leviathan_pass/leviathan4
    WG1egElCvO
    ```

- yeni parola: `WG1egElCvO`

### Leviathan Level 4 -> 5

- ssh ile bağlanalım: `ssh leviathan4@leviathan.labs.overthewire.org -p 2223`

- önceki seviyede bulduğumuz parolayı girelim: `WG1egElCvO`

- `ls -la` ile listeleyince adı `.trash` olan bir yeni dizin görüyoruz:

    ```bash
    leviathan4@gibson:~$ ls -la
    total 24
    drwxr-xr-x  3 root root       4096 Jun 11 21:30 .
    drwxr-xr-x 83 root root       4096 Jun 11 21:32 ..
    -rw-r--r--  1 root root        220 Mar 31 08:41 .bash_logout
    -rw-r--r--  1 root root       3771 Mar 31 08:41 .bashrc
    -rw-r--r--  1 root root        807 Mar 31 08:41 .profile
    dr-xr-x---  2 root leviathan4 4096 Jun 11 21:30 .trash
    leviathan4@gibson:~$ 
    ```

- içine girip listeleyelim:

    ```bash
    leviathan4@gibson:~$ cd  .trash/
    leviathan4@gibson:~/.trash$ ls -la
    total 24
    dr-xr-x--- 2 root       leviathan4  4096 Jun 11 21:30 .
    drwxr-xr-x 3 root       root        4096 Jun 11 21:30 ..
    -r-sr-x--- 1 leviathan5 leviathan4 14936 Jun 11 21:30 bin
    leviathan4@gibson:~/.trash$ 
    ```
- `bin` dosyasını çalıştıralım:

    ```bash
    leviathan4@gibson:~/.trash$ ./bin 
    00110000 01100100 01111001 01111000 01010100 00110111 01000110 00110100 01010001 01000100 00001010 
    leviathan4@gibson:~/.trash$ 
    ```

- bu bir ikili dizilim. ascii'ye çevirmeye çalışalım. ister online ister offline olarak yapın. ben offline şeklinde göstereceğim.

- python kullanarak binary kodunu ASCII karakterlere çevirebiliriz:

    ```bash
    echo "00110000 01100100 01111001 01111000 01010100 00110111 01000110 00110100 01010001 01000100 00001010" | python3 -c "import sys; print(''.join([chr(int(x, 2)) for x in sys.stdin.read().split()]))"
    ```

    - `[chr(int(x, 2)) for x in sys.stdin.read().split()]`

        - int(x, 2) : Her bir ikili (binary) sayı olan x'i ondalık (decimal) sayıya çevirir.

        - chr(int(x, 2)) : Her bir ondalık sayıyı ASCII karakterine çevirir.

        - for x in sys.stdin.read().split() : Okunan her bir ikili sayı üzerinde bu işlemleri gerçekleştirir.

        - [...] : Sonuç olarak elde edilen ASCII karakterlerini içeren bir liste oluşturur.

- yeni parola: `0dyxT7F4QD`

### Leviathan Level 5 -> 6

- ssh ile bağlanalım: `ssh leviathan5@leviathan.labs.overthewire.org -p 2223`

- önceki seviyede bulduğumuz parolayı girelim: `0dyxT7F4QD`

- `ls -la` ile listeleyince adı `leviathan5` olan bir SUID dosya görüyoruz:

    ```bash
    leviathan5@gibson:~$ ls -la
    total 36
    drwxr-xr-x  2 root       root        4096 Jun 11 21:30 .
    drwxr-xr-x 83 root       root        4096 Jun 11 21:32 ..
    -rw-r--r--  1 root       root         220 Mar 31 08:41 .bash_logout
    -rw-r--r--  1 root       root        3771 Mar 31 08:41 .bashrc
    -r-sr-x---  1 leviathan6 leviathan5 15140 Jun 11 21:30 leviathan5
    -rw-r--r--  1 root       root         807 Mar 31 08:41 .profile
    leviathan5@gibson:~$ 
    ```

- çalıştıralım:

    ```bash
    leviathan5@gibson:~$ ./leviathan5 
    Cannot find /tmp/file.log
    leviathan5@gibson:~$ 
    ```

- ltrace ile çalıştıralım:

    ```bash
    leviathan5@gibson:~$ ltrace ./leviathan5 
    __libc_start_main(0x804910d, 1, 0xffffd494, 0 <unfinished ...>
    fopen("/tmp/file.log", "r")                                 = 0
    puts("Cannot find /tmp/file.log"Cannot find /tmp/file.log
    )                           = 26
    exit(-1 <no return ...>
    +++ exited (status 255) +++
    leviathan5@gibson:~$ 
    ```

- bu program büyük ihtimalle `/tmp/file.log` dosyasını açıp yazdırmaya yarıyor. ve bu dosya dizinde yok.

- eğer bu dosyayı `/etc/leviathan_pass/leviathan6` dosyasına bir sembolik link olarak oluşturursak belki okuyabiliriz:

    ```bash
    leviathan5@gibson:~$ ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log
    leviathan5@gibson:~$ 
    ```

- programı tekrar çalıştıralım:

    ```bash
    leviathan5@gibson:~$ ./leviathan5 
    szo7HDB88w
    leviathan5@gibson:~$ 
    ```

- yeni parola: `szo7HDB88w`

### Leviathan Level 6 -> 7

- ssh ile bağlanalım: `ssh leviathan6@leviathan.labs.overthewire.org -p 2223`

- önceki seviyede bulduğumuz parolayı girelim: `szo7HDB88w`

- `ls -la` ile listeleyince adı `leviathan6` olan bir SUID dosya görüyoruz:

    ```bash
    leviathan6@gibson:~$ ls -la
    total 36
    drwxr-xr-x  2 root       root        4096 Jun 11 21:30 .
    drwxr-xr-x 83 root       root        4096 Jun 11 21:32 ..
    -rw-r--r--  1 root       root         220 Mar 31 08:41 .bash_logout
    -rw-r--r--  1 root       root        3771 Mar 31 08:41 .bashrc
    -r-sr-x---  1 leviathan7 leviathan6 15032 Jun 11 21:30 leviathan6
    -rw-r--r--  1 root       root         807 Mar 31 08:41 .profile
    leviathan6@gibson:~$ 
    ```

- çalıştıralım:

    ```bash
    leviathan6@gibson:~$ ./leviathan6 
    usage: ./leviathan6 <4 digit code>
    leviathan6@gibson:~$ 
    ```

- 4 karakterli pin istiyor. örnek olarak `0000` verip çalıştıralım:

    ```bash
    leviathan6@gibson:~$ ./leviathan6 0000
    Wrong
    leviathan6@gibson:~$ 
    ```

- brute force saldırısı kullanabiliriz. ya da programın kodlarını inceleyip ahangi satırda bu 4 pini karşılaştırdığını bulabiliriz. ben ikisini de yapacağım.

- Kaba Kuvvet Saldırısı

    - `./leviathan6` programı her yanlış denemede wrong deyip programı bitiriyor ve bizi terminalimize geri döndürüyor.

    - bu programın pinini doğru girdiğimizde oluşabilecek senaryolar:

        - program yeni bir shell spawn edecek ve `leviathan7` kullanıcısı yetkilerine yükseleceğiz.

        - program `Wrong` harici bir sonuç döndürecek.

    - ilk senaryo gerçekleşeceğini varsayarsak `0000` ve `9999` arasında for döngüsü oluşturalım ve deneyelim. eğer shell spawn ederse for döngüsü duracaktır:

        - `for i in $(seq 0000 9999); do ./leviathan6 $i ; done`

        - Bu döngü, `i` adında bir değişken kullanarak belirli bir aralıkta dolaşmayı sağlar. `seq 0000 9999` komutu, 0000'den 9999'a kadar olan sayıları üretir. Yani, i değişkeni sırasıyla 0000, 0001, 0002, ..., 9999 değerlerini alır.

        - `./leviathan6 $i` her adımda, leviathan6 programını çalıştırır. `$i` burada döngüdeki mevcut değeri temsil eder. Yani, ilk döngüde `./leviathan6 0000`, ikinci döngüde `./leviathan6 0001`, ve böyle devam eder.

    ![](https://i.ibb.co/Q8XhB6h/image.png)

    - birden bire kendimizi bir shell'in içinde bulduk. `whoami` yazıp kim olduğumuza bakalım:

        ```bash
        $ whoami
        leviathan7
        $ 
        ```

    - yeni parolayı almaya çalışalım:

        ```bash
        $ cat /etc/leviathan_pass/leviathan7
        qEs5Io5yM8
        $ 
        ```
    
    - diğer senaryo olsaydı tüm çıktıları bir dosyaya (örneğin sonuc.txt) kaydedip `sort sonuc.txt | grep -v "Wrong"` yaparak bulacaktık. bunu daha fazla merak ediyorsanız [burayı okuyabilirsiniz](/posts/OverTheWire-Bandit-Game/#bandit-level-24---25).

- Tersine Mühendislik

    - GNU Debugger ile açalım: `gdb --args leviathan6 0000` 

    - `disassemble` komutu, belirli bir fonksiyonun veya adres aralığının disasemblesini (assembly koduna çevrilmiş halini) göstermek için kullanılır. O zaman `disassemble main` diyerek ana fonksiyonu disassemble edelim:

    ```bash
    (gdb) disassemble main                   
    Dump of assembler code for function main:       
    0x080491c6 <+0>:     lea    0x4(%esp),%ecx   
    0x080491ca <+4>:     and    $0xfffffff0,%esp    
    0x080491cd <+7>:     push   -0x4(%ecx)       
    0x080491d0 <+10>:    push   %ebp      
    0x080491d1 <+11>:    mov    %esp,%ebp 
    0x080491d3 <+13>:    push   %ebx
    0x080491d4 <+14>:    push   %ecx
    0x080491d5 <+15>:    sub    $0x10,%esp
    0x080491d8 <+18>:    mov    %ecx,%eax
    0x080491da <+20>:    movl   $0x1bd3,-0xc(%ebp)
    0x080491e1 <+27>:    cmpl   $0x2,(%eax)
    0x080491e4 <+30>:    je     0x8049206 <main+64>
    0x080491e6 <+32>:    mov    0x4(%eax),%eax
    0x080491e9 <+35>:    mov    (%eax),%eax
    0x080491eb <+37>:    sub    $0x8,%esp
    0x080491ee <+40>:    push   %eax
    0x080491ef <+41>:    push   $0x804a008
    0x080491f4 <+46>:    call   0x8049040 <printf@plt>
    0x080491f9 <+51>:    add    $0x10,%esp
    0x080491fc <+54>:    sub    $0xc,%esp
    0x080491ff <+57>:    push   $0xffffffff
    0x08049201 <+59>:    call   0x8049080 <exit@plt>
    0x08049206 <+64>:    mov    0x4(%eax),%eax
    0x08049209 <+67>:    add    $0x4,%eax
    0x0804920c <+70>:    mov    (%eax),%eax
    0x0804920e <+72>:    sub    $0xc,%esp
    0x08049211 <+75>:    push   %eax
    0x08049212 <+76>:    call   0x80490a0 <atoi@plt>
    0x08049217 <+81>:    add    $0x10,%esp
    0x0804921a <+84>:    cmp    %eax,-0xc(%ebp)
    0x0804921d <+87>:    jne    0x804924a <main+132>
    0x0804921f <+89>:    call   0x8049050 <geteuid@plt>
    0x08049224 <+94>:    mov    %eax,%ebx
    0x08049226 <+96>:    call   0x8049050 <geteuid@plt>
    0x0804922b <+101>:   sub    $0x8,%esp
    0x0804922e <+104>:   push   %ebx
    0x0804922f <+105>:   push   %eax
    0x08049230 <+106>:   call   0x8049090 <setreuid@plt>
    0x08049235 <+111>:   add    $0x10,%esp
    0x08049238 <+114>:   sub    $0xc,%esp
    0x0804923b <+117>:   push   $0x804a022
    0x08049240 <+122>:   call   0x8049070 <system@plt>
    0x08049245 <+127>:   add    $0x10,%esp
    0x08049248 <+130>:   jmp    0x804925a <main+148>
    0x0804924a <+132>:   sub    $0xc,%esp
    0x0804924d <+135>:   push   $0x804a02a
    0x08049252 <+140>:   call   0x8049060 <puts@plt>
    0x08049257 <+145>:   add    $0x10,%esp
    0x0804925a <+148>:   mov    $0x0,%eax
    0x0804925f <+153>:   lea    -0x8(%ebp),%esp
    0x08049262 <+156>:   pop    %ecx
    0x08049263 <+157>:   pop    %ebx
    0x08049264 <+158>:   pop    %ebp
    0x08049265 <+159>:   lea    -0x4(%ecx),%esp
    0x08049268 <+162>:   ret
    End of assembler dump.
    (gdb) 
    ```

    - rakamların karşılaştırıldığı yeri bulmamız gerekiyor. '+106' numaralı satırın 'setreuid@plt' işlevini çağırdığını ve '+122' numaralı satırın 'system@plt' işlevini çağırdığını görüyoruz. Bu isimler, kullanıcı kimliğinin değiştirildiğini ve bir kabuk komutunun yürütüldüğünü düşündürüyor.
    
    - '+76' numaralı satırda, 'atoi' işlevinin çağrıldığı yer (bir diziyi tamsayıya dönüştürür). Bu nedenle, karşılaştırılan şeyi kontrol etmeliyiz ('+84' numaralı satır).

    - `break *0x0804921a` ile bir kesme noktası yapalım. gdb'nin programı bu adrese kadar çalıştırmasını sağlar ve program bu noktaya ulaştığında durur. bu noktada, programı adım adım ilerletebiliriz, değişkenleri kontrol edebilir veya programın o anki durumunu inceleyebiliriz.

        ```bash
        (gdb) break *0x0804921a
        Breakpoint 1 at 0x804921a
        (gdb) 
        ```
    
    - `run` diyerek çalıştıralım

    - `info registers` diyelim: Bu gdb komutu, tüm işlemci (CPU) kayıtlarının (registers) içeriğini gösterir. İşlemci kayıtları, programın anlık durumunu yansıtan ve programın hangi adımları izlediğini ve değişkenlerin hangi değerlere sahip olduğunu gösteren önemli bileşenlerdir.

        - Örneğin, bir C veya C++ programını hata ayıklarken info registers komutunu kullanarak CPU kayıtlarının içeriğini görebilirsiniz. Bu kayıtlar genellikle rax, rbx, rcx, rdx gibi genel amaçlı kayıtlar, rsp (stack pointer), rbp (base pointer), rip (instruction pointer) gibi özel amaçlı kayıtlar ve işlemcinin bayrak (flag) kayıtlarını içerir.

        ```bash
        (gdb) run
        Starting program: /home/leviathan6/leviathan6 0000    
        [Thread debugging using libthread_db enabled]    
        Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".    
                                            
        Breakpoint 1, 0x0804921a in main ()    
        (gdb) info registers                   
        eax            0x0                 0             
        ecx            0xffffd5cc          -10804        
        edx            0x0                 0
        ebx            0xf7fade34          -134554060
        esp            0xffffd360          0xffffd360
        ebp            0xffffd378          0xffffd378
        esi            0xffffd450          -11184
        edi            0xf7ffcb60          -134231200
        eip            0x804921a           0x804921a <main+84>
        eflags         0x286               [ PF SF IF ]
        cs             0x23                35
        ss             0x2b                43
        ds             0x2b                43
        es             0x2b                43
        fs             0x0                 0
        gs             0x63                99
        k0             0x0                 0
        k1             0x0                 0
        k2             0x0                 0
        k3             0x0                 0
        k4             0x0                 0
        k5             0x0                 0
        k6             0x0                 0
        k7             0x0                 0
        (gdb) 
        ```
    
    - `0x0804921a <+84>:    cmp    %eax,-0xc(%ebp)` satırına bakacak olursak:

        - eax kaydındaki değeri (bu durumda 0, yani başlangıç girdimiz) ebp kaydının değerinden 0xc (12) bayt geriye gidilmiş bellek adresinde saklanan değerle karşılaştırıyoruz.

        - Komut seti içinde `-0xc(%ebp)` ifadesi, ebp kaydının değerinden `0xc` (12) bayt geriye gidilerek, o noktada saklanan bellek adresine erişmeyi ifade eder. Bu, genellikle işlevin yerel değişkenlerine veya parametrelerine erişmek için kullanılır.

        ```bash
        (gdb) print $ebp-0xc
        $1 = (void *) 0xffffd36c
        (gdb) x 0xffffd36c
        0xffffd36c:     0x00001bd3
        (gdb) print/d 0x00001bd3
        $2 = 7123
        (gdb) 
        ```

    - `print $ebp-0xc`: `ebp` kaydının değerinden 0xc (12) bayt geriye (yani daha küçük bir adres) gitmesini ve bu adresin değerini yazdırmasını istiyor. Sonuç olarak, `0xffffd36c` bellek adresini döndürüyor.

    - `x 0xffffd36c`: verilen bellek adresindeki (0xffffd36c) değeri ve bu adresteki bellek bölgesinin içeriğini hexadecimal formatında gösteriyor. `0xffffd36c` adresindeki değer `0x00001bd3` olarak gözüküyor.

    - `print/d 0x00001bd3`: hexadecimal olarak verilen `0x00001bd3` değerini ondalık (decimal) olarak yazdırıyor. Sonuç olarak, `7123` sayısını veriyor.

    - `print $ebp-0xc`, `ebp` kaydının değerinden 0xc (12) bayt geriye giderek, `0xffffd36c` bellek adresini elde eder.
    
    - `x 0xffffd36c`, `0xffffd36c` adresindeki bellek bölgesinin içeriğini gösterir. Burada `0x00001bd3` değeri bulunmaktadır.

    - `print/d 0x00001bd3`, `0x00001bd3` değerini ondalık (decimal) formatında yazdırır ve sonuç olarak `7123` sayısını verir.

    - Demek ki burada, `cmp %eax, -0xc(%ebp)` komutunda `%eax` (0) değeri ile `7123` değeri karşılaştırılıyormuş.

    - programı doğru pinle çalıştıralım && kim olduğumuza bakalım && parolayı ele geçirelim:

        ```bash
        leviathan6@gibson:~$ ./leviathan6 7123
        $ whoami
        leviathan7
        $ cat /etc/leviathan_pass/leviathan7
        qEs5Io5yM8
        $ 
        ```

- yeni parola: `qEs5Io5yM8`

### Leviathan Level 7 -> 8

- ssh ile bağlanalım: `ssh leviathan7@leviathan.labs.overthewire.org -p 2223`

- önceki seviyede bulduğumuz parolayı girelim: `qEs5Io5yM8`

- `ls -la` ile listeleyince adı `CONGRATULATIONS` olan bir dosya görüyoruz:

    ```bash
    leviathan7@gibson:~$ cat CONGRATULATIONS 
    Well Done, you seem to have used a *nix system before, now try something more serious.
    (Please don't post writeups, solutions or spoilers about the games on the web. Thank you!)
    leviathan7@gibson:~$ 
    ```

- ve oyunu bitirdik.

## Notlar

- her oyun arası `exit` veya `logout` ile oturumu sonlandırdık. çünkü `su leviathan` gibi oturum değiştirmeye izin vermiyor.

- terminalden kopyalama işlemini metni seçtikten sonra `ctrl+shift+c` ile, terminale yapıştırma işlemini `ctrl+shift+v` ile yapabilirsiniz.

- bu makale, linux temellerini gerçekten pratik yaparak deneyimlemenizi sağlayacak. kafanızda bundan önce `ls ile cd'yi öğrendim ben artık linux biliyorum` düşüncesi varsa bunu silmeye yarayacak. `you know nothing Jon Snow`

- seviyeleri bitirdikten sonra, gidip video çekin, not alın, gidip siz de makale şeklinde yazın. benden daha da güzelini yapın. daha da açıklayıcı olun. bunları yapmayacaksanız gidin kafanızı çöp kutusuna sokun daha iyi.

- yeni yazıda ya da projede görüşmek dileğiyle, esenlikler...
