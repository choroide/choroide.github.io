---
title: "Pyramid of Pain"
date: 2024-02-11 21:53:00 +0300
categories: [Siber Güvenlik, Tehdit İstihbaratı]
tags: [TTPs, Pyramid of Pain, Siber Tehdit]
author: akkaya
image:
  path: images/PyramidOfPain/Cover.jpg
---

## Giriş

Pyramid of Pain, siber tehditlerin tespit ve engelleme stratejilerini geliştirmek için kullanılır. Bu model, bir saldırganın tespitten kaçınmayı ve saldırılarını sürdürmeyi zorlaştırmak için karşılaştığı zorlukları ve maliyetleri gösterir. Bu piramit, en basit (Hash değerleri, IP adresleri vb.) ile en karmaşık (TTP'ler - Taktik, Teknik ve Prosedürler) göstergeleri arasında bir dizi seviyeyi içerir. 

Piramitte yukarı çıktıkça saldırganların bu göstergeleri değiştirmek için harcadıkları zaman, çaba ve kaynakları artar, böylece onların başarılı olma şansları azalır. Bu model, güvenlik uzmanlarına, saldırıların saldırgan için en çok acı veren ve onu en çok uğraştıracak elemanlarına odaklanmalarını sağlar, böylece saldırganların işlerini sürdürmek için daha fazla zaman, çaba ve kaynak yatırımı gerekir. Şimdi ise piramidin en altından en tepesine doğru anlatalım.

![Pyramid of Pain](images/PyramidOfPain/1.png)
_Pyramid of Pain_

## Hash Values
Hash değeri, SHA-1 veya MD5 gibi karmaşık bir şifreleme algoritmasının çıktısı olan eşsiz bir dosya özetidir. Hash değerleri, iki dosyanın birbirinden farklı olduğunu veya aynı olduğunu bize gösterir.

Ancak birbirinin kopyası olan iki dosyadan birinde çok ufak dahi olsa bir değişiklik yapılması, hash değerini tamamen değiştirir. 

Pyramid of Pain'de hash değerleri elimizdeki zararlı yazılım hashleri ile karşılaştırma yaparak basit saldırıları önlememizi sağlar. Ancak bu saldırgan için pek bir sorun oluşturmaz. Bunun sebebi de biraz önce bahsettiğim gibi ilgili zararlı yazılımdaki ufak bir değişiklik, zararlı yazılımın hash değerini değiştirecek ve bu savunmayı kolaylıkla atlatmasını sağlayacaktır.

Tabii ki buna karşı kullanılabilecek Fuzzy Hash tekniği de vardır. Fuzzy hash bir dosyanın yaklaşık bir özetini oluşturur ve küçük değişikliklere daha az hassastır ve benzer verileri karşılaştırmada kullanılabilir. Bu teknik saldırganlar tarafından biraz daha uğraş gerektirse bile yine de atlatılabilir.

## IP Adresses
IP adresleri, siber güvenlikte en temel göstergelerden biridir. Bunun nedeni siber saldırıların doğrudan veya dolaylı olarak internet bağlantısı ile gerçekleştirilmesidir. Saldırganlar verileri çalmak veya sistemlere sızmak için internet bağlantısını kullanır. 

IP adreslerinin alt katmanlarda olmasının sebebi ise IP adreslerinin saldırganlar tarafından kolaylıkla değiştirilebiliyor olmasıdır. Hatta Tor gibi proxy hizmeti kullanıyorlarsa sık sık IP adreslerini değiştireceklerdir

## Domain Names
Alan adları, IP adreslerinden bir adım yukarıda yer alır. Bu, alan adlarının değiştirilmesinin IP adreslerini değiştirmekten biraz daha zor olduğu anlamına gelir. Peki neden daha zor?

Her bir alan adı için belirli bir ödeme gereklidir. Her ne kadar ücretsiz alan adı sağlayıcıları olsa da (ücretsiz paketler bazı kısıtlamalar ile sunulur) yeni alan adlarının görünür hale gelmesi için biraz süre gerekir. Ancak çok sayıda gevşek kayıt standartlarına sahip alan adı sağlayıcısı da mevcuttur.

## Network/Host Artifacts
Ağ ve Ana Bilgisayar Eserleri, Pyramid of Pain'in orta kısmında yer alır ve sarı bölgeyi oluşturur. Bu bölgede, saldırganlar üzerinde asıl olumsuz etkileri yaratmaya başlarız.

Bu aşamada saldırganın bıraktığı eserlerin tespit edilmesi ve müdahalesi saldırganı kendi laboratuvar ortamına geri dönmeye zorlayacaktır. Saldırgan geri dönüp neyi yanlış yaptığına bakacak bıraktığı izleri inceleyip daha temiz hareket etmek için kullandığı araçları yeniden yapılandıracaktır.  Bu saldırgana belirli bir süre vakit kaybettirecek ve motivasyonunu düşürecektir.

Saldırganın bıraktığı eserlere Windows olay günlükleri kaydı, Registry'e yapılan bir değişiklik veya oluşturulan bir dosyayı örnek olarak verebiliriz. 

## Tools
Araçlar katmanı, saldırganın hedefine ulaşmak için kullandığı yazılımları veya kod parçalarını temsil eder. 

Bu araçlara örnek olarak ağ tarama araçları (Örn: Nmap), backdoor oluşturma araçları, phising için kullanılacak zararlı Macro içeren belge oluşturma araçları, sosyal mühendislik araçları veya Metasploit gibi zafiyet sömürü araçlarını örnek olarak verebiliriz.

Saldırganın kullandığı araçların tespit edilmesi, saldırganı yeni araçlar bulmaya, geliştirmeye veya para karşılığı geliştirtmeye zorlar. Bu durum da elbette ki saldırganın çokça vakit veya para kaybetmesine neden olur. Ayrıca bu aşamada Saldırganın vazgeçme olasılığı da daha yüksektir. Çünkü tüm bu uğraşlar sonucunda saldırganın bu uğraşlarının karşılığını alıp alamayacağını düşünmeye başlar.

## TTPs (Tactics, Techniques and Procedures)
Artık en üst katmandayız. Taktik, teknik ve prosedürler, saldırganın Cyber Kill Chain esas alındığında, tüm aşamalarda işleri nasıl yürüttüğü ve görevleri nasıl gerçekleştirdiğine dair yöntemler bütünüdür. Kimlik avı saldırıları, zararlı Macro içeren dokümanlar, truva atı gömülmüş bir pdf, zip dosyasına sıkıştırılmış zararlı yazılımlar yaygın TTP' lerden sadece birkaçıdır. 

TTP'lerin en tepede olmasının sebebi, TTP'lerin saldırgan tarafından kapsamlı bir şekilde planlanması, uzun zamanlar boyunca vakit ve para olarak masraflar yapılması, denemeler ve simülasyonlar ile desteklenerek oluşturulmasıdır. Bu önemli bir ustalık, yaratıcılık ve derinlemesine araştırma gerektiren bir konudur. 

Bu sebeple ki saldırgana ait TTP'lerin keşfedilmesi ve anlaşılması saldırganı çok zora sokacaktır ve tüm bu planları baştan oluşturmasını gerektirecektir. Saldırgan böyle bir durumda iki seçenekten birinde karar kılması gerekir. Ya hedeflerinden vazgeçip saldırıyı sonlandıracak ya da en baştan itibaren tüm planı iptal edip önceki deneyimlerinden de ders çıkararak tespit edilmesi ve anlaşılması daha zor yeni pir plan oluşturup saldırıya yeniden başlayacak.

Bu karar saldırganın amacına ve hedeflerine göre değişebilir. Maddi amaçla bu işe başlamış olan bir saldırganın bu aşamada vazgeçme olasılığı yüksektir. Ancak devlet gibi arkasında büyük desteğe sahip olan bir saldırgan bu aşamada da vazgeçmeyebilir. 

MITRE ATT&CK  siber saldırılarda kullanılan teknikleri kategorize ederek analiz edilmesini kolaylaştıran bir framework'tür ve saldırganlara ait TTP'leri anlamak için ideal bir kaynaktır. Bu framework kullanılarak firmalar veya kurumlar hangi TTP'lere karşı zayıf olduğu ve hangilerine karşı güçlü olduğunu tespit edebilir ve siber savunmasını tespit ettiği zayıflıklara göre güçlendirebilir.

## Başvurular
- <https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html>
- <https://www.picussecurity.com/resource/glossary/what-is-pyramid-of-pain>
