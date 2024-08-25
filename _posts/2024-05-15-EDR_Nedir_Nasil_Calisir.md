---
title: "EDR Nedir ve Nasıl Çalışır?"
date: 2024-05-15 12:38:00 +0300
categories: [Siber Güvenlik, Ağ Güvenliği]
tags: [EDR, Uç Nokta, Katmanlı Savunma]
author: akkaya
image:
  path: images/EDR_Nedir_Nasil_Calisir/Cover.jpg
---

## Giriş

Siber tehditler her geçen gün artıyor ve gelişiyor. Saldırganlar, hassas verileri ele geçirmek ve sistemleri bozmak için giderek daha karmaşık yöntemler kullanıyor. Bu nedenle, siber güvenliği sağlamak için siber savunmanın daha fazla gelişmesi ve yeni saldırı tekniklerine karşı yeni çözümler üretilmesi gerekiyor.

Bundan birkaç yıl öncesi, antivirüs programları gibi tek bir araçla siber saldırılara karşı korunmak bir miktar mümkündü. Fakat günümüzde bu asla yeterli değil. Saldırganlar, sürekli olarak yeni zafiyetler keşfediyor ve bu zafiyetleri kullanarak sistemlerimize sızabiliyorlar.

Neyse ki, siber güvenliğimizi geliştirmek için Katmanlı Savunma veya diğer adıyla Derinlemesine Savunma (DiD) gibi yeni yaklaşımlar ve araçlar mevcut. Katmanlı Savunma, tıpkı bir şatoya saldırganların girmesini engellemek için oluşturulan hendekler, surlar, timsahlı göller, siperler, dikenler gibi birden fazla güvenlik katmanı kullanarak saldırganların sisteme girmesini zorlaştırmayı amaçlar. Bu sebeple Katmanlı Savunma, "şato yaklaşımı" olarak da adlandırılabilir.

![Photo-1](images/EDR_Nedir_Nasil_Calisir/1.png)
_Şato yaklaşımı_

Tıpkı geçmişte yıkılmaz denilen surların yıkıldığı gibi ele geçirilemez denilen kalelerin ele geçirildiği gibi bu yaklaşım da aşılmaz değildir yani %100 güvenlik sağlamaz. Bu nedenle, siber güvenliğimizi korumak için sürekli olarak yeni tehditlere karşı tetikte olmamız gerekiyor.

#### Neden Katmanlı Savunma Yetersiz Kalıyor?
Antivirüs yazılımları ve güvenlik duvarları gibi geleneksel savunma araçları, siber saldırılara karşı önemli bir koruma katmanı sunar. Ancak bu araçlar, her zaman en son tehditlere karşı güncel olmayabilir ve sıfır gün saldırıları gibi yeni saldırı türlerine karşı savunmasız kalabilir.

Ayrıca, saldırganlar, sistemlere sızmak için sosyal mühendislik ve kimlik avı gibi teknikler kullanarak bu savunmaları atlayabilirler. Bu nedenle, katmanlı savunmaya ek olarak, şüpheli aktiviteleri tespit edebilen ve bunlara hızlı bir şekilde yanıt verebilen proaktif bir güvenlik yaklaşımı benimsemek gerekiyor. İşte bu noktada devreye EDR teknolojisi giriyor.

## EDR Nedir?

EDR (Endpoint Detection and Response, Uç Nokta Algılama ve Yanıt), adından da anlaşılacağı üzere uç nokta (kuruluşun verilerine ve ağına erişebilen dizüstü bilgisayarlar, masaüstü bilgisayarlar, mobil cihazlar, sunucular, IoT cihazları) cihazlardaki olası güvenlik ihlallerini tespit etmek ve bunlara yanıt vermek için tasarlanmış bir güvenlik çözümüdür.

EDR teknolojisi, IoC’ler (Indicator of Compromise, Tehlike Göstergeleri) hakkında bilgi toplamak için uç nokta cihazlardan toplanan verileri birleştirir ve ilişkilendirir. EDR teknolojisi, normal ve anormal durumları bilir ve kullanıcıların ve varlıkların izlenmesi ile gerçek zamanlı olarak davranışsal analitik yani algoritmalar ve makine öğrenimi kullanarak şüpheli veya anormal davranışları tespit eder.

![Photo-2](images/EDR_Nedir_Nasil_Calisir/2.png)
_EDR_

Düzenli olarak eğitilen ve güncellenen makine öğrenimi modelleri sayesinde EDR teknolojisi, Antivirüs çözümlerinin tespit etmekte ve yakalamakta zorlandığı dosya içermeyen kötü amaçlı yazılımlar, tanınmayan/imzasız zararlı yazılımlar, gelişmiş zararlı yazılım türleri (polimorfik malware gibi), APT'ler phising saldırıları ve sıfır gün saldırılarına karşı daha iyi bir koruma sağlar. Antivirüs esas olarak dosyaları kötü amaçlı içerik açısından tararken, EDR uç nokta verilerini toplar ve analiz eder. Ayrıca bu sistemler şüpheli dosyaların davranışlarına göre karar vererek tehditleri sınıflandırabilir ve olaylara gerçek zamanlı yanıt vererek güvenlik ekibi müdahalesine olan ihtiyacı en aza indirir.

UEBA (User and Entity Behavior Analytics, Kullanıcı ve Varlık Davranışı Analitiği) teknolojisi de EDR gibi veri analitiği ve makine öğrenimi aracılığıyla güvenlik sağlamayı amaçlar. EDR ve UEBA arasında bu anlamda benzerlikler vardır ancak UEBA’nın aksine EDR, kötü amaçlı etkinlikleri veya IoC’leri tanımlamak için sistem günlükleri, ağ trafiği, işlem yürütme, kayıt defteri değişikliklerini ve birçok önemli bilgiyi içeren uç noktalardan veri toplar ve analiz eder. Buna ek olarak EDR, bir uç noktada zararlı kod yürütülmesini algılayabilir ve zararlı faaliyetten etkilenen cihazın izole edilmesini sağlayabilir.

EDR teknolojisi, güvenlik ihlallerini tespit etmek ve yanıt vermek için güçlü bir araç olsa da, bazı zorlukları da bulunmaktadır. Gelin kısaca bu zorluklara değinelim.

Öncelikle, EDR'nin tüm uç noktalarda çalışıp çalışmadığını değerlendirmek gerekiyor. Ayrıca, tehdit avcılığı için gerekli olan tüm uç noktalardan en az 6 ay boyunca veri toplamak gerekiyor. Bunun sebebi de, anormal olanı tespit edebilmek için önce normal işleyişin nasıl olduğunu öğrenmesi gerektiğidir. Ve elbette ki bu zor, maliyetli ve uzun zaman alan bir süreçtir.
     
Son zamanlarda yaygınlaşan uzaktan çalışma modeli veya BYOD (Bring Your Own Device) yöntemi, firmalar için maliyeti azaltan bir etmen olabilir. Ayrıca personeller için verimliliği ve özgürlüğü arttırmasından dolayı da sevilir. Ancak personellerin iş için kullandıkları cihazları günlük yaşantısında da kullanması, uç nokta cihazlarına zararlı yazılım bulaşma riskinin daha yüksek olmasına neden olur.

Böyle bir durumda bir tehdit aktörü, kuruluşun ağına erişen bir cihazı ele geçirirse, hassas verilere ve kaynaklara yetkisiz erişim elde etmenin açık bir yoluna sahip olacaktır. Ve eğer kuruluş tüm uç noktalar üzerinde kontrole sahip olmazsa, siber risk ve potansiyel ihlallerle karşı karşıya kalabilir.

## EDR Nasıl Çalışır?

EDR sistemi kurulduktan sonra, her bir uç noktada gerçekleşen etkinlikleri izlemeye ve analiz etmeye başlar. Bu sayede, sistem her bir kullanıcının normal davranış kalıplarını öğrenir ve herhangi bir anormallik tespit edildiğinde alarm üretir. Bu anormallikler arasında bilinmeyen dosyaların çalıştırılması, olağandışı ağ trafiği veya şüpheli sitelere erişim gibi durumlar yer alabilir.

![Photo-2](images/EDR_Nedir_Nasil_Calisir/2.png)
_EDR Nasıl Çalışır?_

Bir tehdit tespit edildiğinde, EDR sistemi güvenlik ekibini anında haberdar eder ve otomatik müdahale önlemleri alabilir. Bu önlemler arasında uç noktaların izole edilmesi, ağ erişiminin engellenmesi dosyaların karantinaya alınması gibi işlemler yer alabilir. Böylelikle saldırganların sistemde daha fazla ilerlemesi, hasar vermesi veya hassas verilere erişmesi engellenmiş olur.

Tüm bunlara ek olarak EDR sistemleri, adli bilişim ve tehdit avı yetenekleri sayesinde, bir saldırının kaynağını belirleyebilir ve nasıl gerçekleştiğini ayrıntılı bir şekilde analiz edebilir. Bu bilgiler, gelecekteki saldırıları önlemek ve güvenlik açıklarını kapatmak için kullanılabilir. Ayrıca analistlerin incelemesini kolaylaştırmak için veriler ayrıştırılıp daha küçük kategoriler halinde birleştirilebilir. Eğer sistem bir False Positive tespit ederse, alarm iptal edilir ve öğrenilenler kaydedilir.

Sonuç olarak, EDR, Katmanlı Savunma ile birlikte kullanıldığında siber güvenliği önemli ölçüde geliştirmeye yardımcı olan güçlü bir teknolojidir. EDR, uç noktalarda gerçek zamanlı görünürlük, gelişmiş tehdit tespiti, hızlı yanıt verme ve detaylı olay incelemesi sağlayarak siber saldırılara karşı proaktif bir savunma oluşturmaya yardımcı olur. 