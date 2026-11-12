# BRFSS 2025 verisiyle sık ruhsal sıkıntının tahmini

CME519 Veri Madenciliği dönem projesi (Faz 1 – vize), İstanbul Topkapı Üniversitesi, Lisansüstü Eğitim Enstitüsü, Yapay Zeka Tezsiz Yüksek Lisans.
Ömer Uslusoy – 26221004006

**Problem:** CDC'nin BRFSS 2025 anket verisinde (356.158 kişi), son 30 günde 14 gün veya daha fazla ruh sağlığının kötü olması ("sık ruhsal sıkıntı") ikili sınıflandırma ile tahmin edilmektedir.

## Defterler (çalıştırma sırası)
1. `00_veri_indirme.ipynb` – CDC'den ham verinin indirilmesi ve parquet olarak kaydedilmesi
2. `01_veri_hazirlama_EDA.ipynb` – değişken seçimi, temizleme, eğitim/test ayrımı, keşifsel veri analizi, aykırı değer analizi
3. `02_modelleme.ipynb` – öznitelik mühendisliği, ön işleme hattı, öznitelik seçimi karşılaştırması, lojistik regresyon ve kNN, GridSearchCV, karar eşiği, test değerlendirmesi, permütasyon önemi, rapor şekilleri

## Ana sonuçlar (test kümesi, n = 69.935, pozitif oran %14,4)
| Model | F1 | ROC-AUC | PR-AUC |
|---|---|---|---|
| Çoğunluk sınıfı (baz çizgi) | 0,000 | 0,500 | 0,144 |
| Lojistik regresyon (RFE-20, C = 0,01, eşik 0,625) | 0,464 | 0,800 | 0,443 |
| kNN (RFE-20, k = 301, eşik 0,193) | 0,459 | 0,793 | 0,434 |

En önemli öznitelikler (permütasyon önemi, lojistik regresyon): fiziksel sağlığın kötü olduğu gün sayısı, yaş, genel sağlık algısı, ideal uykudan sapma, maliyet nedeniyle doktora gidememe.

## Ortam
Google Colab, Python 3, pandas, scikit-learn, matplotlib, seaborn. Tüm rastgele işlemlerde `random_state = 42`.

## Veri
Veri dosyaları depoya eklenmemiştir. `00_veri_indirme.ipynb` veriyi CDC'nin resmi sitesinden indirir ve Google Drive'a kaydeder; diğer defterler dosyaları Drive'da kendileri bulur.
