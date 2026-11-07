# Küresel Yeşil Dönüşüm ve Ekonomik Büyüme Analizi

*Kapsamlı sürdürülebilirlik kalıplarını, ekonomik büyüme ile karbon emisyonu arasındaki ilişkiyi ve küresel anomalileri ortaya çıkarmak için Gözetimsiz Makine Öğrenmesi (K-Means & Isolation Forest) modellerini, dinamik İş Zekası (Power BI) görselleştirmeleriyle entegre eden analitik proje.*

## 🌍 Proje Genel Bakışı

Bu proje, **2000'den 2022'ye** kadar olan küresel ekonomik göstergeleri çevresel performans metrikleriyle birlikte analiz etmek için tasarlanmış kapsamlı bir veri bilimi ve görselleştirme çalışmasıdır.

Geleneksel raporlama, bir ülkenin ekonomik çıktısı (kişi başına düşen GSYİH), yeşil enerji yatırımları ve karbon ayak izi arasındaki karmaşık, doğrusal olmayan ilişkileri yakalamakta genellikle yetersiz kalır. Bu boşluğu doldurmak için bu projede, Python kullanılarak uçtan uca bir **Makine Öğrenmesi iş akışı** uygulanmış (kümeleme ve anomali tespiti algoritmalarından yararlanılarak) ve analitik çıktılar **interaktif bir Power BI panosuna** aktarılmıştır.

## 🧠 Makine Öğrenmesi Mimarisi

Çalışmanın analitik altyapısı, `scikit-learn` kullanılarak uygulanan iki güçlü gözetimsiz makine öğrenmesi modeli tarafından desteklenmektedir:

1. **K-Means Kümeleme (Küresel Tipoloji Segmentasyonu):**
   * Ülkelerin ekonomik durumları, karbon salınımları ve yenilenebilir enerji kullanımları analiz edilerek **4 farklı davranışsal profile** ayrılmıştır:
     * 🟢 **İnovatif Dönüşenler:** Proaktif yeşil teknoloji entegrasyonu ile yüksek GSYİH'yi dengeleyen ekonomiler.
     * 🟤 **Kirli Sanayileşenler:** Geleneksel enerji yapılarına kıyasla yüksek emisyonlar sergileyen sanayileşen uluslar.
     * 🔵 **Zorunlu Yeşiller:** Düşük sanayi ölçeği nedeniyle minimal karbon ayak izine sahip, gelişmekte olan bölgeler.
     * 🔴 **Karbon Anomalileri:** Ekonomik kapasitelerine kıyasla orantısız emisyon seviyeleri gösteren aykırı ülkeler.

2. **Isolation Forest (Küresel Karbon Aykırı Değer Tespiti):**
   * Küresel standartların ve normal çalışma eğilimlerinin ($Skor = 1$) dışında faaliyet gösteren yapısal anomalileri ($Skor = -1$) tespit etmek için kullanılmıştır. Bu model, dünya genelindeki sıra dışı karbon salınımı vakalarını otomatik bir "Alarm Sistemi" gibi yakalar.

## 📊 Power BI Pano Özellikleri

Görselleştirme paketi, karmaşık model çıktılarını sezgisel bir yönetici ve akademik sunum formatına dönüştürür:

* **İnteraktif Dünya Haritası:** Ülke bazlı karbon yoğunluğunu K-Means küme profillerine göre dinamik olarak renklendirerek görselleştirir.
* **Çok Değişkenli Dağılım Grafiği (Scatter Chart):** Makro düzeydeki verimlilik eğilimlerini ortaya çıkarmak için `GDP_Per_Capita` değerini `CO2_Emissions` değerine karşı konumlandırır ve baloncuk büyüklüklerini `Renewable_Energy` kullanımına göre belirler.
* **Dinamik Dilimleyiciler (Slicers):** Coğrafi bölgeye (`Region`) ve gelir sınıflandırmasına (`IncomeGroup`) göre anlık filtreleme yetenekleri sunar.
* **Yapay Zeka Anomali Alarm Tablosu:** Sadece Isolation Forest algoritmasının yakaladığı anomalileri (`-1`) listeleyerek dikkat çekilmesi gereken ülkeleri izole eder.

## 🛠️ Proje Yapısı ve Teknoloji Yığını

- **Python (Jupyter Notebook):** Veri temizleme, eksik değer doldurma, ölçekleme ve ML modellerinin (K-Means, Isolation Forest) inşası.
- **Power BI:** Verilerin harita ve dağılım grafikleriyle modellenmesi, interaktif DAX filtreleri ve renk uyumlandırma işlemleri.
- **Dışa Aktarılan Veri Seti:** Makine öğrenmesi etiketleriyle zenginleştirilmiş nihai CSV dosyası.

---

## 📌 Veri Seti Kaynakları ve Bağlantıları (4 Aşamalı Veri Boru Hattı)

Bu çalışma boyunca kullanılan çok aşamalı analitik varlıklar ve ham/işlenmiş veri bileşenlerine aşağıdaki bağlantılar üzerinden doğrudan erişilebilir:

1. **🔗 1. Ham Küresel Göstergeler Veri Setleri (Dünya Bankası Kaynakları):**
   - [Gayrisafi Sermaye Oluşumu Verisi](https://data.worldbank.org/indicator/NE.GDI.TOTL.KD)
   - [Ar-Ge Harcamaları Verisi](https://data.worldbank.org/indicator/GB.XPD.RSDV.GD.ZS)
   - [Kişi Başına Düşen GSYİH Verisi](https://data.worldbank.org/indicator/NY.GDP.PCAP.KD)
   - [Kişi Başına Düşen CO2 Emisyonları Verisi](https://data.worldbank.org/indicator/EN.GHG.CO2.PC.CE.AR5)

2. [**🔗 2. Python Veri Önişleme ve Özellik Mühendisliği Notebook'u**](./KMeans_IsolationForest_Analysis.ipynb)

3. [**🔗 3. Dışa Aktarılan Nihai ML Sonuçları CSV Dosyası**](./KMeans_Sonuclari_2022.csv)

4. [**🔗 4. İnteraktif Power BI Panosu**](./Global_Emissions_Dashboard.pbix)
