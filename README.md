# Göz Retinası Görüntülerinde Damar Yapısı Belirginleştirme ve Analizi

Bu proje, fundus retina görüntülerinden damar yapılarının otomatik olarak segment edilmesini ve ardından damar morfolojisinin analiz edilmesini amaçlamaktadır. Çalışmada derin öğrenme tabanlı **U-Net** mimarisi kullanılarak damar segmentasyonu gerçekleştirilmiş, daha sonra segmentasyon çıktıları üzerinden damar yoğunluğu, iskelet uzunluğu ve dallanma sayısı gibi yapısal ölçümler elde edilmiştir.

## Proje Amacı

Retina damar yapısı; diyabetik retinopati, hipertansiyon, damar tıkanıklıkları ve çeşitli oftalmolojik hastalıkların değerlendirilmesinde önemli biyobelirteçler sunar. Ancak damarların manuel olarak işaretlenmesi zaman alıcı, yorucu ve uzmana bağımlıdır. Bu proje ile amaçlanan:

- Retina görüntülerinde damar yapısını otomatik olarak çıkarmak
- Damar segmentasyonu sonrası morfolojik analiz yapmak
- Klinik karar destek sistemlerine temel oluşturabilecek nicel çıktılar üretmek
- Tekrarlanabilir bir görüntü işleme ve derin öğrenme hattı kurmaktır

## Öne Çıkan Özellikler

- Fundus retina görüntülerinde damar segmentasyonu
- FOV (Field of View) maskeleme ve retina merkezli kırpma
- Veri artırma (augmentation) ile daha güçlü eğitim süreci
- **BCE + Dice Loss** ile segmentasyon eğitimi
- Damar yoğunluğu, iskelet uzunluğu ve dallanma analizi
- Deney sonuçlarının rapor ve sunum ile dokümante edilmesi

## Kullanılan Yöntem

Projede uçtan uca aşağıdaki işlem hattı izlenmiştir:

1. **Veri Ön İşleme**
   - Görüntülerin yeşil kanalının kullanılması
   - Gauss bulanıklaştırma
   - Otsu eşikleme
   - Morfolojik açma/kapama işlemleri
   - En büyük bağlı bileşen ile FOV çıkarımı
   - Retina merkezli kırpma ve yeniden boyutlandırma

2. **Veri Artırma**
   - Yatay/Dikey çevirme
   - Döndürme
   - Parlaklık/Kontrast değişimleri

3. **Model Eğitimi**
   - U-Net mimarisi
   - PyTorch tabanlı eğitim süreci
   - BCE + Dice birleşik kayıp fonksiyonu
   - Adam optimizer

4. **Değerlendirme**
   - Dice skoru
   - IoU
   - Precision
   - Recall

5. **Morfolojik Analiz**
   - Damar yoğunluğu
   - Skeleton uzunluğu
   - Dallanma noktası sayısı

## Veri Seti

Bu projede **FIVES (Fundus Image Vessel Segmentation)** veri seti kullanılmıştır.

FIVES veri seti, retina damar segmentasyonu için hazırlanmış etiketli fundus görüntülerinden oluşur ve damar yapılarının piksel seviyesinde öğrenilmesine olanak sağlar.

## Sonuçlar

Model, test kümesi üzerinde dengeli ve kullanılabilir segmentasyon performansı üretmiştir.

### Test Sonuçları

| Metrik | Değer |
|---|---:|
| Dice (Macro) | 0.8059 ± 0.0752 |
| IoU (Macro) | 0.6807 ± 0.0946 |
| Precision (Macro) | 0.8100 ± 0.0760 |
| Recall (Macro) | 0.8083 ± 0.0883 |
| Dice (Micro) | 0.8202 |
| IoU (Micro) | 0.6952 |
| Precision (Micro) | 0.8166 |
| Recall (Micro) | 0.8237 |

### Morfolojik Analizden Elde Edilen Gözlemler

Segmentasyon çıktıları, genel damar alanını büyük ölçüde koruyabilmektedir. Ancak özellikle:

- ince damar uçlarında,
- düşük kontrastlı bölgelerde,
- küçük dallanmalarda

bazı bilgi kayıpları oluşabilmektedir. Bu nedenle klasik segmentasyon metrikleri iyi görünse bile, topolojik doğruluk ve damar sürekliliği açısından ek iyileştirmeler gerekebilir.

## Proje Yapısı

```bash
.
├── figures/                 # Şekiller, örnek çıktılar ve görseller
├── sections/                # LaTeX rapor bölümleri
├── .github/workflows/       # PDF derleme workflow dosyaları
├── main.tex                 # Ana rapor dosyası
├── *.ipynb                  # Ana deney notebook'u
├── presentation.*           # Sunum dosyaları
└── README.md
