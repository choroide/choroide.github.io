---
title: "Soflink ve Hardlink Nedir?"
date: 2023-05-27 20:20:00 +0300
categories: [GNU/Linux, CLI]
tags: [Bash, Commands]
author: akkaya
image:
  path: images/Softlink&Hardlink/Cover.jpg
---

## Giriş

Merhaba, bu yazıda Linux dünyasında yaygın olarak kullanılan ve dosya sistemlerinde oldukça faydalı olan "Hardlink" ve "Softlink" kavramlarından bahsedeceğim. Bu terimlerin tanımı ve işlevleri, bazen karmaşık veya kafa karıştırıcı olabilir ancak ben gayet sade anlaşılır bir şekilde anlatmaya çalışacağım.
Bu kavramları anlatmaya başlamadan önce “inode” yada “index node” nedir kısaca değinmek istiyorum. Çünkü bu kavram yazının devamında karşımıza çıkacak önemli bir kavramdır.

## "İndex node" Nedir?

İndex node, dosya ve dizinlerin sahibi, oluşturulma tarihi, boyutu, link sayısı, yetkileri gibi meta verilerinin saklandığı bir veri yapısıdır ve her bir dosya veya dizin eşsiz bir inode numarasına sahiptir. Dosya ve dizinlerin inode numaralarını görebilmek için ls komutunun -i veya --inode parametresi ile çalıştırılması yeterlidir.
Örneğin bir dizin oluşturup bu dizin içerisinde birkaç tane dosya oluşturalım:

![Photo-1](images/Softlink&Hardlink/1.jpg)
_Photo-1_

Şimdi de bu dosyaların inode numaralarını öğrenelim:

![Photo-2](images/Softlink&Hardlink/2.jpg)
_Photo-2_

Ekran görüntüsünde de görüldüğü üzere en başta bulunan bu numaralar o dosyanın inode numarasıdır. Peki bu inode numaralarının konumuzla ne ilgisi var? Birazdan değineceğim.

## Softlink Nedir?

Softlink veya diğer adıyla sembolik bağlantı, Windows işletim sistemindeki kısayollar ile benzer bir işlevi yerine getirir. Bir softlink, bir dosyanın veya klasörün yolunu belirleyen bir referanstır. Bu referans, kullanıcıya belirli bir dosya veya klasöre hızlı ve kolay erişim imkanı sağlar. 
İster softlink ister biraz sonra bahsedeceğim hardlink olsun dosyalar arasında bağlantı oluşturmak için `ln` komutunu kullanırız. Önce bağlantı dosyalarımızı saklayacağımız bir "baglantilar" dizini oluşturalım ve ardından birinci dosya için softlink oluşturalım.

![Photo-3](images/Softlink&Hardlink/3.jpg)
_Photo-3_

Dizinimizi ve dosya1 için softlink dosyamızı oluşturduk. Şimdi inceleyelim:

![Photo-4](images/Softlink&Hardlink/4.jpg)
_Photo-4_

Öncelikle dikkatimizi çeken şey “baglantilar” dizininin altındaki dosya1 yanında ok işareti ile gösterilen köken dosyanın yoludur. Buradan bakarak bu dosyanın bir sembolik bağlantı olduğunu anlayabiliriz.

Bunu anlamanın bir diğer yöntemi de dosya/dizin yetkilerinin gösterildiği yerin “l” ile başlaması. Bir diğer dikkat çeken şey inode numaralarının farklı olması. Bu durum softlink dosyasında görebileceğimiz bir durumdur. Asıl dosya ile sembolik bağlantı arasındaki farklı inode numaraları, asıl dosya silindiğinde sembolik bağlantının hâlâ var olmasını sağlar. Ancak köken dosya silindiği için sembolik bağlantı artık hiçbir işe yaramaz, hedefini kaybeder ve bozulur. Bağlantıyı takip etmeye çalıştığınızda veya etkileşim kurmak istediğinizde "hedef bulunamadı" veya "geçersiz dosya" gibi bir hata alırsınız. Hemen bunu bir örnekle gösterelim:

![Photo-5](images/Softlink&Hardlink/5.jpg)
_Photo-5_

Eğer köken dosyayi silip link dosyasını okumaya çalışırsak ekran görüntüsünde de gördüğümüz gibi bir hata ile karşılaşırız. Aynı zamanda ls komutu bu bağlantıda bir sorun olduğunu bize kırmızı renkle göstererek belirtir:

![Photo-6](images/Softlink&Hardlink/6.jpg)
_Photo-6_

Softlink dosyalarının gördüğünüz gibi Windows işletim sistemindeki kısayollar dosyalarından pek farkı yoktur. Ancak hardlink dosyaları daha farklı çalışır. Şunu da unutmamak gerekir eğer köken dosyanın yetkileri değişirse linklenmiş dosyanın yetkileri de değişir ancak link dosyanın yetkileri değişirse köken dosyada herhangi bir yetki değişikliği olmaz. 

Ek olarak eğer bir dosyanın sembolik link bağlantıya sahip olup olmadığını öğrenmek istersek `sudo find / -lname /tam/yol/orjinal_dosya` şeklinde komut çalıştırmak bize yardımcı olacaktır.

## Hardlink Nedir?

Hardlink, seçilen dosyanın bir kopyası gibi davranır. Köken dosyadaki verilere erişir. Eğer köken dosya silinirse, hardlink hala o dosyanın verilerini içerir. Ancak bu kopyalar softlink dosyalarında olduğu gibi kısayol mantığı ile çalışmazlar. Örnekler ile açıklayayım.

Daha önceden oluşturduğumuz dosya2 nin 2 adet hardlink dosyasını oluşturalım. Bunun için yine “ln” komutunu kullanacağız. Hardlink kopyası oluştururken köken dosya ile aynı adı vermek zorunda değiliz (bu durum softlink için de geçerli). Ardından önce orjinal kopyada sonra da hardlink dosyada değişiklik yapalım ve son durumu inceleyelim:

![Photo-7](images/Softlink&Hardlink/7.jpg)
_Photo-7_

Ekran görüntüsünde gördüğümüz gibi bu dosyaların hepsinin inode numaraları aynı. Yani bu aslında bu dosyaların aynı dosya olduğu anlamına geliyor. Aynı zamanda hardlink dosyaları, softlink dosyaları gibi “l” harfi ile ve yanında orjinal dosyanın konumunu gösterir şekilde değil de normal bir dosya gibi görüntüleniyor. 

Oluşturma işleminden sonra her bir dosyada ayrı değişiklikler yaptık ancak hepsinin içeriği aynı. Bu da az önce bahsettiğimiz gibi hard link şeklinde oluşturulan kopyaların aynı dosya olduğunu, diskte ek yer kaplamadığını ve hardlink kopyalardan birinin veya orjinal dosyanın silinmesinin/yerinin değiştirilmesinin diğer dosyaları hiçbir şekilde etkilemeyeceğini gösterir. Hemen bu durum için de bir örnek yapalım:

![Photo-8](images/Softlink&Hardlink/8.jpg)
_Photo-8_

Örnekte görüldüğü üzere orjinal dosyayı silmemize rağmen hardlink kopyaların içeriğinde veya diğer özelliklerinde herhangi bir değişiklik yaşanmadı. Hardlink dosyalardan birinde yaşanan değişiklik diğer hardlink dosyalarda yaşanmaya devam eder. Ayrıca eğer herhangi bir hardlink dosyasında bir yetki değişikliği yapılırsa diğer bütün hardlink dosyaları da değişiklikten etkilenir.

Peki bir dosyanın hardlink kopyası olup olmadığını veya diğer bir deyişle aynı inode numarasına sahip başka bir dosyanın varlığını nasıl öğrenebiliriz?  Yardımımıza yine find komutu koşuyor.  “find” komutunun -inum parametresi bize inode numarası ile eşleşen diğer dosyaları da görmemizi sağlar. bunun için `sudo find / -inum <inode numarası>` veya `sudo find / -type f -links +1 -ls | grep <inode numarası>` komutlarını kullanmak yeterli olacaktır.