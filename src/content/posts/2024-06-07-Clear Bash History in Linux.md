---
title: "Linux'ta Bash ve Zsh Geçmişini Temizleme"
date: 2024-06-07 00:00:00 +0300
categories: Howto
tags: linux bash history
image: 
---

## .zsh_history Dosyasını Bulma

### `echo $HISTFILE` Komutu

Bu komut, Unix tabanlı işletim sistemlerinde bash veya zsh gibi bir shell'de `HISTFILE` çevresel değişkeninin değerini ekrana yazdırır.

- **`echo`**:
    - `echo` komutu, belirtilen metni veya değişkenin değerini ekrana yazdırmak için kullanılır.

- **`$HISTFILE`**:
    - `HISTFILE` değişkeni, shell'de komut geçmişinin saklandığı dosyanın yolunu belirtir.
    - Örneğin, `bash` kabuğu kullanıyorsanız bu genellikle `$HOME/.bash_history` dosyası, `zsh` kabuğu kullanıyorsanız `$HOME/.zsh_history` dosyasıdır.

Bu komut çalıştırıldığında, `HISTFILE` değişkeninin değeri (komut geçmişinin kaydedildiği dosyanın yolu) ekrana yazdırılır. Örneğin, çıktı şu şekilde olabilir:

- `echo $HISTFILE`
- `/home/fr0stb1rd/.zsh_history`

## Üzerine Yazma

### `cat /dev/null > /home/fr0stb1rd/.zsh_history`

Belirli bir dosyanın içeriğini silmek ve boş bir dosya oluşturmak için kullanılan bir shell komutudur. Komutun işleyişi şu şekildedir:

- **`cat /dev/null`**:
    - `cat` komutu, dosyaların içeriğini ekrana yazdırmak için kullanılır.
    - `/dev/null`, "null cihazı" olarak bilinir ve içine yazılan her şeyi yok eder, boş bir veri kaynağı olarak işlev görür. Bu yüzden `cat /dev/null`, hiçbir şey içermeyen bir boş veri akışını temsil eder.

- **`>`**:
    - Bu işaret, yönlendirme operatörüdür ve komutun çıktısını bir dosyaya yazmak için kullanılır. Eğer belirtilen dosya varsa, bu dosyanın içeriğini siler ve yeni bir içerik yazar. Eğer dosya yoksa, dosyayı oluşturur.

- **`/home/fr0stb1rd/.zsh_history`**:
    - Bu, zsh kabuğunun komut geçmişinin saklandığı dosyanın tam yoludur.

Bu komut çalıştırıldığında, `/dev/null` içeriği (`cat /dev/null` ile okunan boş içerik) `/home/fr0stb1rd/.zsh_history` dosyasına yönlendirilir. Sonuç olarak, `.zsh_history` dosyasının içeriği silinir ve dosya boş hale getirilir.

Özetle, `cat /dev/null > /home/fr0stb1rd/.zsh_history` komutu, `/home/fr0stb1rd/.zsh_history` dosyasının içeriğini silerek dosyayı boşaltır. Bu işlem, zsh kabuğunda saklanan komut geçmişini sıfırlamak için kullanılır.

### `:>/home/fr0stb1rd/.zsh_history`

Belirli bir dosyanın içeriğini silmek için kullanılan bir shell komutudur. Bu komutun işlevi ve nasıl çalıştığına dair açıklama aşağıdaki gibidir:

- **`:`**:
    - Bu, shell'de hiçbir şey yapmayan bir built-in komuttur. Genellikle bir no-op (no operation) olarak kullanılır.

- **`>`**:
    - Bu işaret, yönlendirme operatörüdür ve çıktıyı bir dosyaya yazmak için kullanılır. Eğer belirtilen dosya varsa, bu dosyanın içeriğini siler ve yeni bir içerik yazar. Eğer dosya yoksa, dosyayı oluşturur.

- **`/home/fr0stb1rd/.zsh_history`**:
    - Bu, zsh kabuğunun komut geçmişinin saklandığı dosyanın tam yoludur.

Bu komutu çalıştırdığınızda, `:` komutu aslında hiçbir şey yapmaz, ancak yönlendirme operatörü `>` ile birleştiğinde, `/home/fr0stb1rd/.zsh_history` dosyasının içeriği tamamen silinir ve dosya boş hale getirilir.

Özetle, `:>/home/fr0stb1rd/.zsh_history` komutu, `/home/fr0stb1rd/.zsh_history` dosyasının içeriğini silerek dosyayı boşaltır. Bu işlem, zsh kabuğunda saklanan komut geçmişini sıfırlamak için kullanılabilir.

## Birleştirilmiş Komutlar

### `cat /dev/null > $HISTFILE`

Bu komut, shell'de belirli bir dosyanın içeriğini silmek için kullanılır. Komutun bileşenleri ve işleyişi şu şekildedir:

- **`cat /dev/null`**:
    - `cat` komutu, dosyaların içeriğini ekrana yazdırmak için kullanılır.
    - `/dev/null`, "null cihazı" olarak bilinir ve içine yazılan her şeyi yok eder. Bu nedenle, `cat /dev/null` komutu boş bir veri akışını temsil eder.

- **`>`**:
    - Bu işaret, yönlendirme operatörüdür ve komutun çıktısını bir dosyaya yazmak için kullanılır. Eğer belirtilen dosya varsa, bu dosyanın içeriğini siler ve yeni bir içerik yazar. Eğer dosya yoksa, dosyayı oluşturur.

- **`$HISTFILE`**:
    - `HISTFILE` değişkeni, shell'de komut geçmişinin saklandığı dosyanın yolunu belirtir. Örneğin, `zsh` kullanıyorsanız bu genellikle `$HOME/.zsh_history` dosyasıdır.

Bu komut çalıştırıldığında, `/dev/null` içeriği (boş içerik) `HISTFILE` tarafından belirtilen dosyaya yönlendirilir. Sonuç olarak, `HISTFILE` dosyasının içeriği silinir ve dosya boş hale getirilir.

### `:>$HISTFILE`

Bu komut, shell'de belirli bir dosyanın içeriğini silmek için kullanılır. Komutun bileşenleri ve işleyişi şu şekildedir:

- **`:`**:
    - Bu, shell'de hiçbir şey yapmayan bir built-in komuttur. Genellikle bir no-op (no operation) olarak kullanılır.

- **`>`**:
    - Bu işaret, yönlendirme operatörüdür ve komutun çıktısını bir dosyaya yazmak için kullanılır. Eğer belirtilen dosya varsa, bu dosyanın içeriğini siler ve yeni bir içerik yazar. Eğer dosya yoksa, dosyayı oluşturur.

- **`$HISTFILE`**:
    - `HISTFILE` değişkeni, shell'de komut geçmişinin saklandığı dosyanın yolunu belirtir. Örneğin, `bash` kullanıyorsanız bu genellikle `$HOME/.bash_history` veya `zsh` kullanıyorsanız `$HOME/.zsh_history` dosyasıdır.

Bu komut çalıştırıldığında, `:` komutu aslında hiçbir şey yapmaz, ancak yönlendirme operatörü `>` ile birleştiğinde, `HISTFILE` tarafından belirtilen dosyanın içeriği silinir ve dosya boş hale getirilir.
