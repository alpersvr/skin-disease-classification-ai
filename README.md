# SWE308: Yapay Zeka ile Cilt Lezyonu Sınıflandırması

Bu proje, SWE308 Yapay Zeka Temelleri dersi kapsamında gerçekleştirilmiş olup, HAM10000 veri setindeki cilt lezyonu görüntülerinin iyi huylu (benign) veya kötü huylu (malignant) olarak sınıflandırılmasını amaçlamaktadır[cite: 1].

## Proje Hakkında

Projenin temel amacı, derin öğrenme modelleri kullanarak cilt lezyonlarının otomatik olarak sınıflandırılmasıdır. Bu, potansiyel olarak cilt kanseri teşhisine yardımcı olabilecek bir adımdır. Projede iki farklı yaklaşım denenmiştir: sıfırdan özel bir Evrişimli Sinir Ağı (CNN) modeli oluşturmak ve önceden eğitilmiş bir model olan ResNet50 ile transfer öğrenme uygulamak[cite: 1, 25].

## Veri Seti

* **Veri Kaynağı:** [HAM10000 ("Human Against Machine with 10000 training images")](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/DBW86T) veri seti kullanılmıştır[cite: 2].
* **Alt Küme:** Dosya erişim kısıtlamaları nedeniyle veri setinin 796 örneklik bir alt kümesi ile çalışılmıştır[cite: 3].
* **Veri Dağılımı:** Kullanılan alt kümede 553 iyi huylu ve 243 kötü huylu lezyon bulunmaktadır[cite: 6].
* **Veri Hazırlığı:** Görüntüler %80 eğitim / %20 doğrulama seti olarak bölünmüş[cite: 4], çeşitli veri artırma teknikleri (döndürme, çevirme, kaydırma, yakınlaştırma, parlaklık ayarı vb.) uygulanmış ve piksel değerleri [0, 1] aralığına normalize edilmiştir[cite: 5].

## Modeller ve Yöntemler

1.  **Özel CNN Modeli:**
    * 3 Evrişimli + Maksimum Ortaklama katmanı bloğu, ardından Tam Bağlı ve Seyreltme (Dropout) katmanlarından oluşan bir modeldir[cite: 7].
    * Adam optimize edici ve İkili Çapraz Entropi kayıp fonksiyonu ile 10 epok eğitilmiştir[cite: 8].
2.  **Transfer Öğrenme (ResNet50):**
    * ImageNet üzerinde önceden eğitilmiş ResNet50 modeli temel alınmıştır[cite: 14].
    * Modelin baş kısmı 5 epok, ardından son 15 katmanı 8 epok daha düşük öğrenme oranıyla ince ayar (fine-tuning) yapılarak eğitilmiştir[cite: 15]. Sınıf ağırlıkları ve Erken Durdurma (EarlyStopping) kullanılmıştır[cite: 15, 24].

