# Küresel Yeşil Dönüşüm ve Ekonomik Büyüme Analizi: Kapsamlı Analitik Pano ve Makine Öğrenmesi Mimarisi

*Kapsamlı sürdürülebilirlik kalıplarını, ekonomik büyüme ile karbon emisyonu arasındaki ilişkiyi ve küresel anomalileri ortaya çıkarmak için Gözetimsiz Makine Öğrenmesi (K-Means & Isolation Forest) modellerini, dinamik İş Zekası (Power BI) görselleştirmeleriyle entegre eden analitik tez projesi.*

## 🌍 Proje Genel Bakışı ve Vizyon

Bu proje, **2000'den 2022'ye (ve 2040 Projeksiyonlarına)** kadar olan küresel ekonomik göstergeleri çevresel performans metrikleriyle birlikte analiz etmek için tasarlanmış uçtan uca bir veri bilimi ve görselleştirme çalışmasıdır.

Geleneksel raporlama, bir ülkenin ekonomik çıktısı (kişi başına düşen GSYİH), yeşil enerji yatırımları, Ar-Ge harcamaları ve karbon ayak izi arasındaki karmaşık, doğrusal olmayan ilişkileri yakalamakta genellikle yetersiz kalır. Bu boşluğu doldurmak için bu projede, Python kullanılarak uçtan uca bir **Makine Öğrenmesi iş akışı** uygulanmış (kümeleme ve anomali tespiti algoritmalarından yararlanılarak) ve analitik çıktılar **interaktif, yapay zeka destekli bir Power BI komuta merkezine** aktarılmıştır.

Proje, jüri sunumu ve akademik değerlendirmede en yüksek puanı hedeflemek üzere **Çok Boyutlu Yıldız Şema (Star Schema)** mimarisi üzerine kurulmuştur.

---

## 📌 Veri Seti Kaynakları ve 4 Aşamalı Veri Boru Hattı (Data Pipeline)

Bu çalışma boyunca kullanılan çok aşamalı analitik varlıklar, ham ve işlenmiş veri bileşenlerine aşağıdaki bağlantılar üzerinden erişilebilir:

1. [**🔗 1. Ham Küresel Göstergeler Veri Seti (Kaynak)**](INSERT_RAW_DATA_LINK_1_HERE)
2. [**🔗 2. Python Veri Önişleme ve Özellik Mühendisliği Notebook'u**](INSERT_NOTEBOOK_LINK_2_HERE)
3. [**🔗 3. Dışa Aktarılan Nihai ML Sonuçları ve Kümeler CSV Dosyası (`KMeans_Sonuclari_2022.csv`)**](INSERT_CSV_LINK_3_HERE)
4. [**🔗 4. İnteraktif Power BI Panosu (`Dashboard_Visuals.pbix`)**](INSERT_PBIX_LINK_4_HERE)

---

## 🏗️ 1. Veri Mimarisi ve Boyutsal Modelleme (Star Schema)

Optimum sorgu performansı ve hatasız DAX hesaplamaları için veriler ilişkisel veri ambarı prensiplerine göre yapılandırılmıştır:

### Çok Tablolu Yapı:
* **`Fact_YesilDonusum` (Ana Gerçeklik Tablosu):** Yıllık bazda tüm ülkelere ait metrikleri barındırır:
  * `GDP_Per_Capita` (Kişi Başı GSYİH)
  * `CO2_Emissions` (Karbon Emisyonu)
  * `Renewable_Energy` (Yenilenebilir Enerji Tüketimi)
  * `RnD_Expenditure` (Ar-Ge Harcamaları)
  * `Anomali_Skoru` (Isolation Forest aykırı değer skorları)
  * `Tahmini_CO2`, `Alt_Sinir`, `Ust_Sinir` (Güven aralıklı zaman serisi tahminleri)
* **`Dim_Ulke` (Ülke Boyut Tablosu):** Ülke isimleri ve ID'leri (`Country Name`, `Ulke_ID`).
* **`Dim_Cografya` (Coğrafya Boyut Tablosu):** Kıtalar ve bölgesel kırılımlar (`Region`).
* **`Dim_Tarih` (Zaman Boyut Tablosu):** Yıllar bazında zaman hiyerarşisi (`Yil`).
* **`Dim_Kume` (Küme Boyut Tablosu):** Makine öğrenmesi küme tanımları (`Kume_ID`, `Kume_Adi`).

### İlişki Kardinalitesi:
* Fact tablosundan tüm Dimension tablolarına doğru **Çoka-Bir (\*:1)** ilişkiler kurulmuş, görsel toplama hatalarını (tek mavi nokta sorunu) engellemek için **tek yönlü (Single)** filtreleme yönü optimize edilmiştir.

---

## 🧠 2. Makine Öğrenmesi ve İstatistiksel Metodoloji

Çalışmanın arka planındaki yapay zeka motoru:

1. **K-Means Kümeleme (Küresel Tipoloji Segmentasyonu):**
   * Ülkeler ekonomik durumlarına ve emisyonlarına göre **4 ana gruba** ayrılmıştır:
     * 🟢 **İnovatif Dönüşenler:** Yüksek GSYİH ve temiz teknoloji entegrasyonu.
     * 🟤 **Kirli Sanayileşenler:** Yüksek karbon salınımına sahip endüstriyel ekonomiler.
     * 🔵 **Zorunlu Yeşiller:** Düşük sanayileşme ölçeği nedeniyle minimal ayak izi.
     * 🔴 **Karbon Anomalileri:** Kapasitelerine oranla orantısız emisyon üreten aykırı ülkeler.

2. **Isolation Forest (Aykırı Değer / Anomali Tespiti):**
   * Küresel standartlardan saparak ekosistemi tehdit eden yapısal anomalileri otomatik olarak izole eder.

3. **Zaman Serisi Tahminleme (Prophet Tabanlı Modelleme):**
   * Gelecek yıllara yönelik karbon salınım eğilimlerini alt ve üst istatistiksel güven sınırlarıyla projeksiyon eder.

---

## 📊 3. Gelişmiş Power BI Pano Modülleri ve Görselleştirme Komuta Merkezi

Panoda jürinin ve akademisyenlerin teknik yetkinliği doğrudan görebileceği 8 temel gelişmiş modül yer almaktadır:

1. **Geospatial Impact Map (Harita Görseli):** Küresel emisyon dağılımını K-Means kümelerine göre dinamik renklendirir.
2. **Decomposition Tree (Yapay Zeka Kök Neden Analizi):** `Region`, `Kume_Adi` ve `Country Name` kırılımlarında dinamik dallanma yaparak emisyon artış sebeplerini inceler.
3. **Key Influencers (Önemli Etkileyiciler):** Lojistik regresyon altyapısıyla karbon emisyonunu tetikleyen ana faktörleri istatistiksel oranlarla listeler.
4. **Kuznets Eğrisi Kombo Grafik (Line & Clustered Column):** Ekonomik büyüme (`GDP`) ile karbon salınımı (`CO2`) arasındaki Çevresel Kuznets Eğrisini ampirik olarak kanıtlar.
5. **Waterfall Chart (Şelale Grafiği):** Yenilenebilir enerji yatırımlarının yıllara göre kümülatif değişimini gösterir.
6. **Scatter Chart (Animasyonlu Dağılım ve Anomali Grafiği):** `Play Axis` (Zaman Makinesi) desteğiyle ülkelerin 2000'den günümüze ekonomik ve çevresel evrimini hareketli olarak sunar.
7. **100% Stacked Bar Chart (Bölgesel Strateji Karşılaştırması):** Kıtaların Ar-Ge harcamaları ile yenilenebilir enerji bütçeleri arasındaki oransal dağılımı kıyaslar.
8. **Executive KPI Cards:** Özet emisyon, yenilenebilir enerji ve Ar-Ge metriklerini anlık yansıtan kartlar.

---

## 🛠️ Kurulum ve Çalıştırma Rehberi

1. **Ön Koşullar:** En son sürüm **Microsoft Power BI Desktop** uygulamasının yüklü olduğundan emin olun.
2. **Veri Bağlantısı:** Veri setlerini (CSV/SQL) projeye dahil edin.
3. **Model Kontrolü:** `Model View` ekranından tablolar arası `*:1` ilişkilerini doğrulayın.
4. **Sunum:** Panoyu tam ekran moduna alarak interaktif filtreleri ve AI bileşenlerini jüri sunumunda aktif olarak kullanın.

*Akademik mükemmeliyet, ileri düzey veri mühendisliği ve yüksek etkili görsel hikaye anlatımı için geliştirilmiştir.*