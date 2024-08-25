---
title: "VLSM Nedir?"
date: 2024-08-25 01:00:00 +0300
categories: [Ağ Yönetimi, IP Adresleme]
tags: [Bilgisayar Ağları, IP, Alt Ağ Maskeleme]
author: akkaya
image:
  path: images/VLSM_Nedir/Cover.jpg
---

Variable Length Subnet Masking (VLSM), ağ mühendislerinin IP adreslerini daha verimli bir şekilde yönetmelerini sağlayan bir alt ağ oluşturma tekniğidir. Klasik alt ağ maskesi yöntemlerinin aksine, VLSM ile her bir alt ağ için farklı uzunlukta subnet maskeleri kullanılarak, IP adresleri ihtiyaç duyulan yerlerde optimize edilebilir. Bu, özellikle büyük ağlarda IP adres israfını önlemeye yardımcı olur.

## VLSM’nin Ortaya Çıkış Sebebi

Ağların büyümesi ve karmaşıklığının artmasıyla, sabit uzunluktaki alt ağ maskeleriyle (Fixed Length Subnet Masking - FLSM) IP adreslerinin dağıtımı yetersiz hale geldi. Bu durumda, özellikle büyük adres blokları küçük ağlara tahsis edildiğinde, birçok IP adresi kullanılmadan boşa giderdi. VLSM, bu sorunun çözümü olarak geliştirildi ve ağ mühendislerine farklı ağ segmentleri için uygun uzunluktaki alt ağ maskelerini seçme özgürlüğü verdi.

## VLSM ve FLSM Arasındaki Farklar

VLSM ve FLSM arasındaki temel fark, subnet maskelerinin esnekliği ve verimliliğidir. FLSM'de tüm alt ağlar aynı subnet maskeyi kullanırken, VLSM ile her bir alt ağ kendi ihtiyaçlarına göre farklı bir subnet maskesi kullanabilir. Bu, büyük ağlarda IP adres israfını önler ve ağ yöneticilerine IP adreslerini daha esnek bir şekilde dağıtma olanağı tanır. Örneğin, bir alt ağda 100 IP adresi gerekliyken, diğer bir alt ağda sadece 10 IP adresi gerekiyorsa, VLSM ile bu alt ağlar için uygun subnet maskeleri seçilebilir.

## Dezavantajlar

VLSM’nin dezavantajlarından biri, ağ yapılandırmasının daha karmaşık hale gelmesidir. FLSM'de tüm alt ağlar için tek bir alt ağ maskesi kullanılırken, VLSM'de her bir alt ağ için farklı alt ağ maskeleri kullanılması gerekir. Bu durum, IP adresleme planlamasını daha karmaşık hale getirir ve ağ yöneticisinin her bir alt ağın gereksinimlerini dikkatlice analiz etmesini gerektirir. Özellikle büyük ağlarda, bu karmaşıklık hatalara yol açabilir ve ağın yönetimini zorlaştırabilir. 

Diğer bir dezavantaj ise, VLSM'nin ölçeklenebilirlik üzerindeki etkisidir. VLSM kullanılarak alt ağ maskeleri genellikle mevcut ihtiyaçlara göre, yani kullanılan host sayısını tam olarak kapsayan bir şekilde belirlenir. Bu, IP adreslerinin verimli kullanılmasını sağlar; ancak, gelecekteki büyüme potansiyeli dikkate alınmazsa, yeni cihazlar eklemek veya alt ağları genişletmek zor hale gelebilir. Bu durumda, ağ mühendisinin gelecekteki büyüme ve değişiklikleri öngörerek VLSM planlaması yapması, ağın ölçeklenebilirliğini korumak açısından kritik öneme sahiptir.

## VLSM ile Ağ Tasarımı ve Alt Ağlar


### Topolojiye Genel Bakış:

![Photo-1](images/VLSM_Nedir/1.png)
_Photo-1_

Şekilde gösterilen topolojide, dört farklı LAN ve routerlar arasındaki bağlantı için toplamda beş alt ağa ihtiyacımız var. Bu gereksinimi karşılamak için, başlangıçta elimizde bulunan "10.11.48.0/24" IP bloğunu daha küçük alt ağlara bölmeliyiz. Ancak, geleneksel alt ağ oluşturma yöntemleri, bazı durumlarda gereksinimlerimizi tam olarak karşılamayabilir.

### Geleneksel Alt Ağlamanın Sınırları:

Eğer geleneksel alt ağa ayırma işlemi ile ilerleyecek olsaydık, son oktetteki host bölümünden 3 bit ödünç alarak 10.11.48.0/24 IP bloğunu sekiz alt ağa bölebilirdik. Bu durumda her bir alt ağda 30 kullanılabilir IP adresi olurdu. Ancak, bu yöntem en büyük LAN'ın host ihtiyacını karşılayamaz ve daha az host ihtiyacı olan alt ağlarda kullanılmayan IP adreslerinin israfına neden olur.

### VLSM'nin Avantajı:

VLSM (Değişken Uzunlukta Alt Ağ Maskesi) kullanarak alt ağlar arasında IP adreslerini daha verimli bir şekilde dağıtabiliriz. VLSM ile, her bir alt ağı gereksinimlerine göre farklı alt ağ maskeleri ile yapılandırarak, hem büyük LAN'ların ihtiyaçlarını karşılayabilir hem de daha küçük LAN'larda IP adres israfını önleyebiliriz.

### Ağ Gereksinimleri:

Ağımızda beş farklı segment için IP adreslemesi yapacağız:

- SW1 LAN: 14 host IP adresi.
- SW2 LAN: 30 host IP adresi.
- SW3 LAN: 6 host IP adresi.
- SW4 LAN: 60 host IP adresi.
- Routerlar Arası Bağlantı: 2 host IP adresi.

### VLSM Uygulaması:

VLSM kullanırken, en fazla host ihtiyacı olan segmentten başlayarak alt ağları bölmek, IP adreslerini daha verimli kullanmamıza olanak tanır. Örneğin, en büyük alt ağ gereksinimimiz 60 host adresi içindir, bu nedenle bu segment için 255.255.255.192 alt ağ maskesini (64 IP adresi) kullanabiliriz. Bu durumda elimizde 4 adet alt ağ olur:

- 10.11.48.0/26
- 10.11.48.64/26 
- 10.11.48.128/26
- 10.11.48.192/26

İlk alt ağı (10.11.48.0/26) en büyük ağa (SW4 LAN) tahsis edelim. Bu durumda bir sonraki en büyük alt ağ 30 host ihtiyacı ile SW2 LAN olacaktır. Bu ağ için 64 IP adresi sunan 10.11.48.64/26 ağı çok büyük. Bu durumda bu alt ağı "10.11.48.64/27" ve "10.11.48.96/27" olacak şekilde 32 IP adresi sağlayan iki alt ağa bölebiliriz. "10.11.48.64/27" alt ağını SW2 LAN için tahsis edelim. 

Bir sonraki en büyük alt ağ 14 host ihtiyacı ile SW1 LAN olacaktır. Bu ağ için 32 IP adresi sunan 10.11.48.96/27 ağı çok büyük. Bu durumda bu alt ağı "10.11.48.96/28" ve "10.11.48.112/28" olacak şekilde 16 IP adresi sağlayan iki alt ağa bölebiliriz. "10.11.48.96/28" alt ağını SW1 LAN için tahsis edelim. 

Geriye kalan SW3 LAN 6 host IP adresine ihtiyaç duyuyor. Bu ağ için 16 IP adresi sunan "10.11.48.112/28" ağı çok büyük. Bu ağı da 2 alt ağa böldüğümüz durumda 8 IP adresi sunan "10.11.48.112/29" ve "10.11.48.120/29" alt ağlarına sahip oluruz. İlk alt ağ olan "10.11.48.112/29" alt ağını SW3 LAN için tahsis edelim. 

Son olarak routerlar arası bağlantı için alt ağ ihtiyacımız var. Routerlar arası bağlantı 2 IP adresine ihtiyaç duyar. Ancak diğer tüm ağlarda olduğu gibi Network ve Broadcast adresleri unutulmamalıdır. bu durumda 4 IP adresi sunan bir alt ağa ihityacımız var. Bunun için "10.11.48.120/29" alt ağını "10.11.48.120/30" ve "10.11.48.124/30" olacak şekilde 2 alt ağa bölebilir ve ilk alt ağı routerlar arası bağlantı için kullanabiliriz. Topolojimizin son hali şekilde göründüğü gibi olacaktır.

![Photo-2](images/VLSM_Nedir/2.png)
_Photo-2_

Yapılan işlemleri daha iyi okuyabilmek, yönetebilmek ve belgelendirebilmek için alt ağ tablosu oluşturmak önemlidir. Aşağıdaki tabloyu biraz önce yaptığımız uygulama için örnek olarak verebilirim:

| Alt Ağ | Gerekli Host Sayısı | Network Adresi/CIDR | Kullanılabilir İlk Host Adresi | Broadcast Adresi |
|---|---|---|---|---|
| SW1 LAN | 14 | 10.11.48.96/28 | 10.11.48.97/28 | 10.11.48.111/28 |
| SW2 LAN | 30 | 10.11.48.64/27 | 10.11.48.65/27 | 10.11.48.95/27 |
| SW3 LAN | 6 | 10.11.48.112/29 | 10.11.48.113/29 | 10.11.48.119/29 |
| SW4 LAN | 60 | 10.11.48.0/26 | 10.11.48.1/26 | 10.11.48.63/26 |
| Routerlar arası LAN | 2 | 10.11.48.120/30 | 10.11.48.121/30 | 10.11.48.123/30 |

## Sonuç

Bu yazıda, VLSM'nin geleneksel alt ağlama yöntemlerine göre IP adresleme açısından sunduğu esneklik ve verimliliği inceledik. Farklı büyüklükteki alt ağlar için uygun alt ağ maskeleri kullanarak, ağdaki IP adres israfını en aza indirgemiş olduk. VLSM, özellikle büyük ve karmaşık ağ yapılarında IP adreslerini verimli kullanmak isteyen ağ yöneticileri için kritik bir yöntemdir. Bu nedenle, ağ tasarımı yaparken VLSM'yi dikkate almak, hem mevcut ağın performansını artırır hem de gelecekteki genişlemelere daha iyi hazırlıklı olunmasını sağlar.




