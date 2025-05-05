---
title: PentaMarket - C# ile Barkodlu Satış Programı
published: 2021-06-10
updated: 2021-06-10
description: 'Visual Studio C# ile geliştirilmiş, SqlLocalDb ve EntityFramework kullanan barkodlu satış programı'
image: 'https://i.ibb.co/QQGjGGR/resim.png'
tags: [CSharp, Desktop, EntityFramework, SqlLocalDb, Project]
category: 'Project'
draft: false
---
# PentaMarket: C# Barkodlu Satış Programı

Visual Studio C#, SqlLocalDb, EntityFramework, Database First, Rdlc Report ile Satışa Hazır Barkodlu Satış Programı.

PentaMarket \| 2021 \| [Source Code](https://gitlab.com/fr0stb1rd/pentamarket/) \| [Blog Post](https://fr0stb1rd.gitlab.io/posts/PentaMarket/)

- Udemy kursu projesinden yola çıkılarak yapılmıştır. İndirim, Numpad, Otomatik stok kontrolü gibi özellikler eklenmiştir.

- 5 kişilik grup projesidir. Penta adını buradan almıştır. Emeği geçen isimler: `Can`, `Akif`, `Görkem`, `Ahmet`

- pentarestore, pentamarket'ten ayrı bir projedir. pentamarket ile arasında yedekleyici ilişkisi vardır. biri diğerini program içerisinden kapatır veya açar. ayrıntılı bilgi için doküman okunmalıdır.

- setup hazırdır ancak debug klasörünün içeriği boşaltılmıştır. tekrar build edilip kullanılabilir.

- proje gereksinimleri webden indirecek şekilde ayarlanmıştır.

- offline çalışılmak istenirse bunun için ayarlar isteğe göre değiştirilebilir:

    - proje ayarları > prerequisites > from local

## Öğendiğimiz bazı şeyler

- C# İle Sıfırdan Barkodlu Satış Programı geliştirme
- Visual Studio'da Nesneleri Etkin Kullanma
- C#'da Form Tasarımı
- C# Özel Nesneler Oluşturma (textbox, button, label vb.)
- C# Private - Public Metod Kullanımı
- C# Class Kullanımı
- Entity Framework
- SqlLocalDb Veritabanı Oluşturma/Kullanma
- DateBase First Yöntemi İle Model Oluşturma
- Veritabanı İçin Tablolar Oluşturma/Kullanma
- Lambda Fonksiyonlarını Kullanma (Veritabanı tablo işlemleri için)
- Veritabanı Backup/Restore
- Rldc Report Kullanımı
- C# Termal Yazıcıdan Çıktı Alma (Bilgi Fişi)
- C# İle Temel-Orta ve İleri Düzey Kodlama
- Projenin Setup Haline Getirilmesi
- Toplu Ürün Scripti Oluşturma
- Local Ağda Çok Bilgisayarda Kullanma
- Lisanslama İşlemi (Demo ve Yıllık Kullanım)

## Ekran Görüntüleri

![login](https://i.ibb.co/R3Qk7LG/resim.png)

![ana sayfa](https://i.ibb.co/tYYcPMP/resim.png)

![yeni ürün girişi](https://i.ibb.co/GRDfLJW/resim.png)

![stok izleyici](https://i.ibb.co/W30q8Jw/resim.png)

![fiyat güncelleyici](https://i.ibb.co/N2SFp2y/resim.png)

![raporlar](https://i.ibb.co/7z4YMGV/resim.png)

![ayarlar 1. sayfa](https://i.ibb.co/kXFH2VS/resim.png)

![ayarlar 2. sayfa](https://i.ibb.co/qJvSFWr/resim.png)

![ayarlar 3. sayfa](https://i.ibb.co/bdd2yQ3/resim.png)

![bilgi & sürüm](https://i.ibb.co/fpJr8wj/resim.png)

![hızlı ürün girişi](https://i.ibb.co/FwW8fVB/resim.png)

![yüzdelik indirim örneği](https://i.ibb.co/44KdNzV/resim.png)

![stok uyarıları](https://i.ibb.co/ftmMbCR/resim.png)

## Kurs detayları

- Ad: `C# İle Sıfırdan Barkodlu Satış Programı Yapımı`
- Açıklama: `Visual Studio C#, SqlLocalDb, EntityFramework, Database First, Rdlc Report ile Satışa Hazır Barkodlu Satış Programı`
- Link: https://www.udemy.com/course/c-ile-sifirdan-barkodlu-satis-program-yapimi/
- Veli Öfkeli: https://www.udemy.com/user/veli-ofkeli-2/

## Kurs Açıklamaları

```
C# ile temel düzeyde bilgi sahibi olduğunuzu düşünüyor ve ne yapmanız gerektiğine karar veremiyorsanız bu kurs tam size göre.

Hangi programlama dili olursa olsun belirli bir altyapı sonrası eğer proje üretmiyorsanız, o alanda ilerlemeniz mümkün değildir.

Proje çalışmanızı yaparak hem kendinizi geliştireceksiniz, hem de para kazanmanın kapılarını aralayacaksınız. Bu proje belki de sizin sektörde para kazanacağınız  ilk işiniz olacak, başka alanlar için program yazma yeteneğiniz gelişecek.

Kursumuzda sıfırdan başlayarak gerçek piyasada kullanılabilecek pratik, etkili ve geliştirilmeye açık bir proje yapacağız.

Hiç bir adımı atlamadan adım adım ilerleyeceğiz. Hatalarla karşılaşacağız hataları düzelteceğiz, sonucu elde etmek için en mantıklı yöntemleri deneyeceğiz.

Şunu da söylemeden edemeyeceğim, siz bir projeyi 2 defa yaparsanız 2. yapışınızda daha az ve daha performanslı kod yazarsınız. Dolayısıyla mümkün olduğu kadar proje üretmenizi tavsiye ederim. Her seferinde farklı mantık, algoritma, yaklaşım...

Neler yapacağız?

    Visual Studio'da Nesneleri Etkin Kullanma
    C#'da Form Tasarımı
    C# Özel Nesneler Oluşturma (textbox, button, label vb.)
    C# Private - Public Metod Kullanımı
    C# Class Oluşturma/Kullanma
    Entity Framework
    SqlLocalDb Veritabanı Oluşturma/Kullanma
    DateBase First Yönetemi İle Model Oluşturma
    Veritabanı İçin Tablolar Oluşturma/Kullanma
    Lambda Fonksiyonlarını Kullanma (Veritabanı tablo işlemleri için)
    Veritabanı Backup/Restore
    Rldc Report Kullanımı
    C# Termal Yazıcıdan Çıktı Alma (Bilgi Fişi)
    C# İle Temel-Orta ve İleri Düzey Kodlama
    Toplu Ürün Ekleme Sql Scripti Oluşturma
    Lokal Ağda Birden Fazla Bilgisayarda Programın Çalıştırılması (Sql Server Üzerinden)
    Lisanslama (Demo-Yıllık Kullanım) İşlemleri
    Projenin Setup Haline Getirilmesi
```

## License

![](https://www.gnu.org/graphics/gplv3-127x51.png)

You can use, study share and improve it at your will. Specifically you can redistribute and/or modify it under the terms of the [GNU General Public License](https://www.gnu.org/licenses/gpl-3.0.html) as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
