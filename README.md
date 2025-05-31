**Hareket Yönetimi**

Açıklama:
Aracımızın hareket sistemi, iki adet ana (büyük) Lego Spike motoru ve tekerlekli diferansiyel
düzenek kullanılarak tasarlandı. Kamera hareketi (rotasyonu) ise, yüksek hassas dönüşler
sağlamak için büyük boy motorlardan daha az güç potansiyeline ssahip olan bir adet dc
(küçük) Lego Spike motorunun yanında ekstra hassaslık ve doğruluk için çap uzunlukları
değişken birçok dişli kullanıldı. Bu sayede araç, kameranın hareketinin hassaslığnı
garantileyerek renk ve engel algılamasının hata katsayısını en aza indirgemiş olduk.

Teknik Detaylar:
Motor Seçimi: Yüksek menavra ve hareket hızı sebebiyle iki adet büyük Lego Spike Motoru
Dengeli Gövde Sistemi Tasarımı: Robot gövdesi bir dik üöçgen biçiminde yapılarak
geometrik olarak en dengeli şekişllerden olan üçgenin denge merkezini kullanduık ve
herhangi bir tarafta toplanabilecek ekstra ağırlıklara önlem olarak bu muhtemel ağırlığın
oluşacağı tarafa bnunu desteklemek ve robotun dengesinin şaşmasını engellemek için 3
adet sarhoş teker eklendi.

Montaj: Motorlar, ve sensörler Lego Teknik parçalarından olan gövdeye direk olarak
monteliyken Husky kamera ise kameraya özel tasarlanan ve kameranın Lego Teknik
parçalarından oluşan bir gövdeye bağlanmasını olağan kılan ekstra bir parçaya oturtularak
monte edildi.

**Güç ve Sensör Yönetimi**

Açıklama:
Aracın güç kaynağı olarak şarj edilip yeniden kullanılabilen Spike beyninin batraryası
kullanıldı. Sensörler Husky kamerası(engel ve engel rengi tespiti) ve renk sensörü (çizgi
takibi) sensörlerinden ibarettir.

Sensör Seçim Nedenleri:
Husky Kamera: Renkleri renk sensöründen daa yüksek bir doğruluk oranıyla algılamak için.
Renk Sensörü: Pistteki çizgileri yüksek doğrulukla algılamak için.

Malzeme Listesi:
Lego Spike Beyin (1x)
Lego Teknik Parçaları
Lego Spike Renk Sensörü (1x)
Lego Spike Sarhoş Teker (3x)
Lego Spike Büyük Motor (2x)
Lego Spike DC Motor (1x)
3D Basılmış Kamera Monte Aparatı Husky Kamera (1x)

**Engellerle baş etme yöntemi**:

Python dilinde yazılmış kodumuzun temel pseudocode'u şudur:

köşe_sürecinde = False # robot mavi ile turuncu çizgilerin arasında ise True'dur
köşe_çıkış_sürecinde = False # turuncu çizgiyi geçiş ile aracın yönünün düzelmesi arasında True'dur
hedef_derece = 0 # robot yönünü bu açıya göre değiştirir. negatif değerler sol tarafı temsil eder.
anlık_derece = 0 # robotun anlık açısı

her zaman ileri gidiyor

program döngüsü:

    while köşe_çıkış_sürecinde:
		hedef derece sıfırlanana kadar bekle (anlık derece 90 olana kadar)
		anlık_derece = 0 # dönüş tamamlandıktan sonra referans açı sıfırlanır
        köşe_çıkış_sürecinde = False

	while değil köşe_sürecinde:
		eğer mavi görürse:
			köşe_sürecinde = True
			hedef_derece -= 45 # robot 45 derece açı dönerek turuncu çizgiye doğru yönelir
		
        kamera()
        eğer sonuç yeşil ışık ise:
            eğer uzak ise:
                ışığa yönelir
            değilse:
                ışığın solundan geçilir
                eski hizaya dönülür
        eğer sonuç kırmızı ışık ise:
            eğer uzak ise:
                ışığa yönelir
            değilse:
                ışığın sağından geçilir
                eski hizaya dönülür

	while köşe_sürecinde:
		eğer turuncu görürse:
			köşe_sürecinde = False
			köşe_çıkış_sürecinde = True
			hedef_derece -= 45 # 45 derece açılık bir dönüş daha ile 90 derecelik dönüş tamamlanır

Işık olmadığı durumda robot köşelerdeki çizgiler yardımıyla dönebilmektedir. Işıklar var ise her zaman önündeki ışığa yönelmekte, ışık kamerada belli bir yüksekliğe ulaşınca yanından dolanmaktadır.

