---
title: TryHackMe MrPhisher Çözümleri - Adım Adım Rehber (Türkçe)
published: 2024-06-12
updated: 2024-06-12
description: 'A detailed Turkish walkthrough guide for solving the MrPhisher challenge on TryHackMe, focusing on VBA and XOR operations'
image: ''
tags: [Security, CTF, TryHackMe, VBA, Tutorial]
category: 'Tutorial'
draft: false
---

## Video

uzakta...

## Walkthrough

Oda Linki: [tryhackme.com/r/room/mrphisher](https://tryhackme.com/r/room/mrphisher)

### Makinayı Başlatma

- Bize verilen notu okuyalım:

    ```
    I received a suspicious email with a very weird-looking attachment. It keeps on asking me to "enable macros". What are those?


    Access this challenge by deploying the machine attached to this task by pressing the green "Start Machine" button. The files you need are located in /home/ubuntu/mrphisher on the VM. 

    Can't see the VM? Press the "Split Screen" button at the top of the page.

    Please note that the document may take approximately a minute to launch for the first time.
    ```

- VBA (`Visual Basic for Applications`), Microsoft tarafından geliştirilen bir programlama dilidir. Microsoft Office uygulamaları (Excel, Word, Access, Outlook vb.) içinde otomasyon ve kişiselleştirme yapmak için kullanılır. VBA, kullanıcıların görevleri otomatikleştirmesine, özel işlevler oluşturmasına ve çeşitli uygulamaları birbiriyle entegre etmesine olanak tanır. Özellikle Excel'de makro yazmak için yaygın olarak kullanılır.

- Dosyayı atan saldırgan, bu vatandaştan makroları etkinleştirmesini söylemiş. Ofis dokümanlarının içine VBA ile macro yazabiliyorsak bu elbette bazen kötü sonuçlara yol açabilir.

### Zararlı Kodu Bulma

- Makinayı başlatalım:

    ![](https://i.ibb.co/H4WG4H3/image.png)

- `/home/ubuntu/mrphisher/` dizinine gitmemizi istiyor. Gidip dosyaları listeleyelim: 

    -   `cd  /home/ubuntu/mrphisher/`
    -   `ls`

    ```bash
    ubuntu@thm-mr-phisher:~/mrphisher$ ls
    MrPhisher.docm  mr-phisher.zip
    ```

- `MrPhisher.docm` bir ofis dosyası. LibreOffice ile açalım: `libreoffice MrPhisher.docm`

    ![](https://i.ibb.co/m5wm17s/image.png)

    Belgenin içinde macro var diye uyarıyor. Tamam deyip devam edelim.

- Bakalım makrolarda ne varmış. Sırayla `Tools` > `Macros` > `Edit Macros`:

    ![](https://i.ibb.co/NpsWcSK/image.png)

- Sırayla: `MrPhisher.docm` > `Project` > `Modules` > `New Macros`

    ![](https://i.ibb.co/sywCTPd/image.png)

- Ve burada bir VBA görüyoruz:

    ```vb
    Rem Attribute VBA_ModuleType=VBAModule
    Option VBASupport 1
    Sub Format()
    Dim a()
    Dim b As String
    a = Array(102, 109, 99, 100, 127, 100, 53, 62, 105, 57, 61, 106, 62, 62, 55, 110, 113, 114, 118, 39, 36, 118, 47, 35, 32, 125, 34, 46, 46, 124, 43, 124, 25, 71, 26, 71, 21, 88)
    For i = 0 To UBound(a)
    b = b & Chr(a(i) Xor i)
    Next
    End Sub
    ```

### VBA Kodunu İnceleme

- Bu VBA, `Format` adında bir alt prosedür (`Sub`) tanımlıyor. Bu prosedür, belirli bir dizi (`array`) içindeki sayılarla belirli işlemler yaparak bir metin (`string`) oluşturuyor.

    1. `a()` adında bir dizi ve `b` adında bir string değişken tanımlanıyor:

        ```vb
        Dim a()
        Dim b As String
        ```

    2. `a` dizisi, belirli sayılarla dolduruluyor:

        ```vb
        a = Array(102, 109, 99, 100, 127, 100, 53, 62, 105, 57, 61, 106, 62, 62, 55, 110, 113, 114, 118, 39, 36, 118, 47, 35, 32, 125, 34, 46, 46, 124, 43, 124, 25, 71, 26, 71, 21, 88)
        ```

    3. `For` döngüsü kullanılarak `a` dizisinin her elemanı üzerinde işlem yapılıyor:

        ```vb
        For i = 0 To UBound(a)
        ```

    4. Her döngü adımında, `a(i)` elemanı ile `i` (dizinin indeksi) arasında bit seviyesinde XOR işlemi uygulanıyor:

        ```vb
        b = b & Chr(a(i) Xor i)
        ```

    5. Elde edilen sonuç `Chr` fonksiyonu kullanılarak bir karaktere dönüştürülüyor ve bu karakter `b` stringine ekleniyor.

    6. Döngü tamamlandığında, `b` değişkeni içinde XOR işlemi ve `Chr` fonksiyonu ile oluşturulmuş bir metin bulunuyor.

### Yeni Python İmplementi

-   Aynı adımları gerçekleştiren bir Python programı yazıp şifrelenmiş metni çözmeye çalışabiliriz.

    ```python
    # ana liste
    a = [102, 109, 99, 100, 127, 100, 53, 62, 105, 57, 61, 106, 62, 62, 55, 110, 113, 114, 118, 39, 36, 118, 47, 35, 32, 125, 34, 46, 46, 124, 43, 124, 25, 71, 26, 71, 21, 88]
    # boş bir dize oluşturuyoruz. şifreyi çözdüğümüzde tüm harfleri bir araya koyacağımız yer. bkz: akümülatör :D
    b = ""
    # listedeki her sayıyı teker teker ele al
    for i in range(len(a)):
        # her sayıya özel XOR işlemi uygula. bu işlemin sonucunu chr() ile bir harfe dönüştür ve b dizisine ekle
        b += chr(a[i] ^ i) # örnek: a[0] = 102, 102^0=102, ve chr(102) = 'f' harfidir.
    # sonuç
    print(b)
    ```

-   Çalıştıralım:

    ![](https://i.ibb.co/kJk0xR1/image.png)

    ```bash
    $ python3 deneme.py
    flag{a39a07a239aacd40c948d852a5c9f8d1}
    ```

-   Bayrağı yakaladık: `flag{a39a07a239aacd40c948d852a5c9f8d1}`

    ![](https://i.ibb.co/nbt4WxH/image.png)

## Sonuç

-   VBA kodunu inceleyerek, Word belgesindeki zararlı makro kodunu bulduk.
-   Zararlı makrolar, kötü niyetli kişilerin bilgisayarınıza erişmesine ve zararlı eylemler gerçekleştirmesine olanak tanır.
-   Bilinmeyen kaynaklardan gelen ofis belgelerindeki makroları etkinleştirmek, ciddi güvenlik risklerine neden olabilir.
-   Makroları yalnızca güvenilir ve güvenilir kaynaklardan alın. Şüpheli e-postalardan, dosya paylaşım sitelerinden veya bilinmeyen kişilerden gelen belgelerdeki makroları etkinleştirmeyin.

## Uyarılar

-   Bilinmeyen eklentiler içeren belgeleri açmaktan kaçının. Özellikle belgeler, e-posta eki veya bilinmeyen kaynaklardan indirildiğinde dikkatli olun.
-   Ofis belgeleri, "makroları etkinleştir" veya "düzenleme izni ver" gibi isteklerle geldiğinde dikkatli olun. Bu, belge içinde potansiyel olarak zararlı kodları çalıştırmak için bir taktik olabilir.
-   Güncel bir antivirüs veya anti-malware programı kullanarak bilgisayarınızı koruyun. Bu tür programlar, bilgisayarınıza zararlı yazılımların bulaşmasını engelleyebilir veya zararlıları tespit edebilir.

## XOR İşlemi Hakkında

-   **XOR Nedir?**
    - XOR (Exclusive OR), iki şeyin birbirinden farklı olup olmadığını kontrol eden bir matematiksel işlemdir.
    - Bu işlem, iki sayı veya iki durum arasında karşılaştırma yapmak için kullanılır.

-   **Meyve Karşılaştırmasıyla Örnek:**
    - Diyelim ki bir arkadaşınla meyve karşılaştırması yapıyorsun. Sen elmayı seviyorsun, arkadaşın ise muz.
    - Eğer her ikimiz de aynı meyveyi seviyorsak, sonuç "Evet" olur.
    - Ancak, eğer sen elmayı seviyorsan ve arkadaşın muzu seviyorsa, sonuç "Hayır" olur, çünkü farklı meyveleri seviyoruz.

-   **XOR İşlemi Nasıl Yapılır?**
    - İki sayı veya durumu karşılaştırırken, XOR işlemi yaparız.
    - İki durum arasında fark yoksa, sonuç "0" olur.
    - Eğer durumlar farklıysa, sonuç "1" olur.

-   **Örnek XOR İşlemi:**
    - Diyelim ki biz iki arkadaşız ve favori renklerimizi karşılaştırıyoruz.
    - Senin favori rengin mavi, benimki ise yeşil olsun.
    - Mavi ve yeşil farklı renkler olduğu için, XOR sonucu "1" olur.
    - Eğer senin favori rengin de yeşil olsaydı, XOR sonucu "0" olurdu, çünkü aynı renkleri seviyor olurduk.

-   **XOR'un Kullanımı:**
    - Bilgisayarlar, şifreleme, veri iletimi ve doğrulama gibi birçok alanda XOR işlemini kullanır.
    - XOR, bilgisayarların veri ile çalışırken farklı durumları kontrol etmelerine ve işlemelerine yardımcı olur.
    - Python'da XOR işlemi `^` operatörü ile gerçekleştirilir. İki sayı arasında XOR işlemi yapmak için bu operatörü kullanabiliriz.
    - VBA'da XOR işlemi `Xor` anahtar kelimesi ile gerçekleştirilir. İki sayı arasında XOR işlemi yapmak için bu anahtar kelimeyi kullanabiliriz.
