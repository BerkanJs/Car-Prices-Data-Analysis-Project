Bu proje, 1990-2015 yılları arasında satılan araçların fiyatları ve özellikleri üzerine bir analiz yapmayı amaçlamaktadır. Veri seti, araçların üretim yılı, markası, modeli, donanım seviyesi, gövde tipi, şanzıman türü, kilometre durumu, renk, iç mekan özellikleri gibi çeşitli niteliklerin yanı sıra, her aracın satış fiyatı, satış tarihi ve piyasa değeri gibi önemli finansal verileri de içermektedir.

Projenin amacı, araçların çeşitli özelliklerinin, satış fiyatları üzerindeki etkilerini anlamak ve bu bilgileri kullanarak araç fiyatlarını tahmin etmek için bir makine öğrenmesi modeli geliştirmektir. Ayrıca, araç fiyatları ile ilgili genel eğilimleri keşfetmek ve verilerin temel analizlerini yapmak da projenin önemli hedeflerindendir.




Veri Seti Özeti:

Veri Seti Boyutu: 558,837 satır, 15 sütun.
Eksik Veri: Bazı sütunlarda eksik veriler bulunmaktadır. Örneğin, şanzıman türü ve donanım seviyesi gibi sütunlarda eksiklikler mevcuttur.
Önemli Sütunlar:
Year (Üretim Yılı): Aracın üretim yılı bilgisi.
Make (Marka): Aracın markası (Toyota, Ford, vb.).
Model (Model): Aracın modeli.
Trim (Donanım Seviyesi): Aracın donanım seviyesi (Sport, Premium, vb.).
Body (Gövde Tipi): Aracın gövde tipi (Sedan, SUV, vb.).
Transmission (Şanzıman Türü): Aracın şanzıman türü (manuel, otomatik).
Condition (Durum): Aracın durumu (yeni, ikinci el, vb.).
Odometer (Kilometre): Aracın kullandığı toplam mesafe.
Selling Price (Satış Fiyatı): Aracın satış fiyatı.
Sale Date (Satış Tarihi): Aracın satıldığı tarih
Selling Price: Aracın satıldığı fiyat.
Sale Date: Aracın satıldığı tarih.


### Veri Seti Özeti ve Ön İşleme
#### 1. Veri Setinin Tanıtımı:
Veri seti, 1990-2015 yılları arasında araba satış fiyatlarını içermektedir. Toplamda 500.000 satırdan oluşan bu veri seti, çok sayıda nümerik ve kategorik değişken içermektedir. Amacımız, bu veriyi kullanarak bir regresyon modeli geliştirip, araba satış fiyatlarını tahmin etmektir.

#### 2. Veri Setinin Sorunları ve Çarpıklık:
Veri setindeki dağılım çarpık ve normal dağılımdan uzak görünüyor. Çoğu değişkenin varyansları homojen değil, bu da modelin genellenebilirliğini olumsuz etkileyebilir. Özellikle, hedef değişken olan araba satış fiyatları büyük oranda asimetrik ve yüksek varyans gösteriyor.

#### 3. Çarpıklık ve Dağılım Düzeltme:
Verinin çarpıklığını gidermek için, Box-Cox dönüşümü uygulanmıştır. Bu dönüşüm, hedef değişkenin (araba satış fiyatı) daha normal bir dağılıma yaklaşmasını sağlayarak modelin doğruluğunu artırmaya yardımcı olur.

#### 4. Aykırı Değerlerin Tespiti ve Temizlenmesi:
Veri setindeki aykırı değerler (outliers), modelin performansını ciddi şekilde bozabilecek potansiyele sahiptir. Bu nedenle, Isolation Forest algoritması kullanılarak aykırı değerler tespit edilmiştir. Bu adımda, anomaliler ve uç değerler veri setinden çıkarılmış ya da düzeltilmiştir.

#### 5. Kategorik Değişkenlerin Yönetimi:
Veri setinde bulunan kategorik değişkenlerin bir kısmı aşırı kategorik olup, bu değişkenlerin sayısal işleme uygun olmamaktadır. Bu tür değişkenlerle çalışmak için iki yaygın yaklaşım vardır: Label Encoding ve One-Hot Encoding. Ancak, veri setinde bulunan bazı kategorik değişkenlerde yüksek kardinalite (çok sayıda kategori) ve düşük frekansa sahip kategoriler bulunmaktadır. Bu, modelin aşırı karmaşıklaşmasına ve verinin düzensiz bir şekilde temsil edilmesine yol açabilir.

Bu nedenle, az frekansa sahip kategoriler doğrudan silinmek yerine, benzer kategoriler altında birleştirilmiştir. Bu sayede, her kategori daha anlamlı bir şekilde temsil edilerek modelin genelleme kapasitesi artırılmıştır. Örneğin, "Diğer" veya "Bilinmeyen" gibi kategoriler birleştirilmiş ve böylece modelin daha stabil bir şekilde öğrenme yapması sağlanmıştır.

Bu adım, modelin yüksek kardinaliteye sahip değişkenlerle daha etkili bir şekilde başa çıkabilmesini sağlamakta ve aynı zamanda modelin aşırı karmaşıklaşmasını engellemektedir.

#### 6. Veri Setinin Son Durumu:
Bu ön işleme adımlarından sonra veri seti, daha dengeli bir hale getirilmiş olup, model eğitimi için daha uygun bir yapıya kavuşmuştur. Verinin daha düzgün bir dağılıma sahip olması, modelin doğruluğunu artırmak ve genellenebilirliğini sağlamak adına önemlidir.

### Modelin Eğitimi ve Değerlendirilmesi

#### 1. Model Seçimi:
Veri setindeki özelliklerin karmaşıklığı ve yüksek boyutluluğu göz önünde bulundurularak, yapay sinir ağı (ANN) tabanlı bir regresyon modeli tercih edilmiştir. Bu model, doğrusal olmayan ilişkileri öğrenebilme kapasitesine sahip olup, büyük veri setlerinde etkili sonuçlar verebilmektedir.

#### 2. Model Performansı:
Modelin eğitimi tamamlandıktan sonra elde edilen performans göstergeleri aşağıda özetlenmiştir:

Eğitim Seti İçin R²: 0.9993
Test Seti İçin R²: 0.9993
Test Seti İçin RMSE: 1.1697
Test Seti İçin MSE: 1.3683
Bu değerler, modelin hem eğitim hem de test verisine mükemmel uyum sağladığını ve doğrulama hatalarının çok düşük olduğunu göstermektedir. R² değeri oldukça yüksek, bu da modelin çok az hata ile veriyi tahmin ettiğini belirtmektedir.

#### 3. Overfitting Durumu:
Eğitim süreci boyunca, eğitim kaybı sürekli azalmış ve doğrulama kaybı bir noktadan sonra sabitlenmiştir. Bu, modelin başlangıçta çok iyi öğrenme sağladığını, ancak daha fazla öğrenmeye çalışırken doğrulama kaybının çok az değiştiğini gösteriyor. Early stopping kullanıldığından dolayı modelin daha fazla öğrenme yapması engellenmiştir.
Eğitim ve test verileri arasındaki R² değerlerinin yüksek olmasına rağmen, modelin eğitim verisine fazla uyum sağlamış olabileceği dikkate alınmalıdır. Eğitim kaybı sürekli azalırken, doğrulama kaybının sabit kalması, modelin aşırı öğrenme eğiliminde olduğunu ve overfitting olasılığını gösteriyor olabilir. Bu durumu netleştirmek için test seti büyütülmeli ve farklı veri alt kümeleriyle daha fazla doğrulama yapılmalıdır.

Eğitim ve Doğrulama Kaybı Grafiği: Eğitim kaybı eğrisinin ilk epochlarda hızlıca azaldığı, ardından sabitlendiği gözlemlenmiştir. Doğrulama kaybı ise hafif azalmış, ancak sonrasında sabit kalmıştır. Bu durum, overfitting'in minimal seviyelerde olduğunu ve modelin iyi genellenebildiğini gösteriyor.
#### 4. Genellenebilirlik ve Değerlendirme:
Modelin eğitim ve test verilerindeki R² değerlerinin birbirine yakın olması, overfitting'in olmadığını ve modelin genelleme yeteneğinin yüksek olduğunu göstermektedir. Ayrıca, RMSE ve MSE değerlerinin düşük olması, modelin hata oranının çok küçük olduğunu işaret etmektedir.


### Sonuç
Özetle, şu anda verilere bakarak overfitting'in çok belirgin olmadığı söylenebilir çünkü eğitim ve test R² değerleri neredeyse birbirine çok yakın ve RMSE/MSE oldukça düşük. Ancak eğitim kaybının sabitlenmesi ve doğrulama kaybının çok az değişmesi, modelin daha fazla öğrenmeye kapalı olduğunu gösteriyor, bu da modelin genellenebilirliğini sorgulamak için bir işaret olabilir.

##### Bu sonucu daha etkili yapmak yani öğrenmeyi arttırmak için : 

 - Daha Fazla Early Stopping Patience: Early stopping için patience değerini arttırarak, modelin daha fazla öğrenmesi için fırsat tanıyabiliriz.

 - Daha Fazla Epoch veya Öğrenme Oranı Değiştirme: Modeli daha fazla eğitim ile veya öğrenme oranını düşürerek eğitebiliriz. Bu, doğrulama kaybının daha iyi gelişmesini sağlar ve overfitting'i engelleyebilir.



