Yemek Tarifi Benzerlik Analizi Projesi
Bu proje, bir yemek tarifi veri setinde yer alan malzemelere dayalı olarak tarifler arasında benzerlik analizi yapmayı amaçlar. TF-IDF ve Word2Vec modelleri kullanılarak, verilen bir tarifin malzemelerine en benzer tarifler bulunmuş ve modellerin performansı anlamsal ve Jaccard benzerlik ölçütleriyle değerlendirilmiştir.

Amaç
Örnek bir tarifin malzemelerine (ör. ['pork belly', 'smoked paprika', 'kosher salt', 'ground black pepper']) en benzer 5 tarifi bulmak.
TF-IDF ve Word2Vec (CBOW ve Skip-gram) modellerini karşılaştırmak.
Model yapılandırmalarının (pencere boyutu, vektör boyutu) etkisini analiz etmek.
Veri Seti
Dosya: recipe_final (1).csv
Boyut: 48,735 tarif
Sütunlar: recipe_id, recipe_name, ingredients_list, aver_rate, review_nums, calories, fat, carbohydrates, protein, cholesterol, sodium, fiber, image_url
Odak: Yalnızca ingredients_list sütunu kullanıldı.
Yöntem
Ön İşleme:
Malzeme listeleri tokenize edildi, stop words çıkarıldı.
Kelimeler lemmatize ve stem edilerek iki corpus (lemmatized, stemmed) oluşturuldu.
Modeller:
TF-IDF: Malzemeler vektörleştirildi, cosine benzerliği ile en benzer 5 tarif bulundu.
Word2Vec: Lemmatized ve stemmed verilerle 16 model eğitildi (CBOW/Skip-gram, window=2/4, vector_size=100/300). Ortalama vektörlerle cosine benzerliği hesaplandı.
Jaccard Benzerliği: Modellerin önerdiği tarif kümeleri arasında örtüşme oranı hesaplandı.
Kütüphaneler: pandas, numpy, nltk, sklearn, gensim
Kurulum
Gerekli kütüphaneleri yükleyin:
bash

Kopyala
pip install pandas numpy nltk scikit-learn gensim
NLTK verilerini indirin:
python

Kopyala
import nltk
nltk.download('punkt')
nltk.download('stopwords')
nltk.download('wordnet')
nltk.download('punkt_tab')
Veri setini (recipe_final (1).csv) projenin ana dizinine yerleştirin.
Kullanım
Jupyter Notebook dosyasını (yemektarifieslestirme2.ipynb) çalıştırın.
Örnek giriş malzemeleriyle (ör. ['pork belly', 'smoked paprika', 'kosher salt', 'ground black pepper']) benzer tarifleri bulun.
Çıktılar:
TF-IDF ve Word2Vec için en benzer 5 tarif ve benzerlik skorları
Anlamsal değerlendirme tablosu
Jaccard benzerlik matrisi (jaccard_benzerlik_matrisi.csv)
Sonuçlar
En Başarılı Model: lemmatized_model_skipgram_window2_dim300 (Ortalama anlamsal puan: 3.80)
Örnek Çıktı (TF-IDF Lemmatized):
Homemade Bacon
Crispy Pork Belly
Filippino Lechon Kawali
Caramelized Pork Belly (Thit Kho)
Split Pea Soup with Pork Belly
TF-IDF vs. Word2Vec: TF-IDF yüzeysel eşleşmelerde etkili (ortalama 3.20), Word2Vec (özellikle Skip-gram) bağlamsal ilişkileri daha iyi yakaladı.
Yapılandırma Etkisi: Vector_size=300 daha iyi sonuç verdi, window=2 lokal bağlamları daha iyi modelledi.
Değerlendirme
Anlamsal Puanlar: Skip-gram modelleri (özellikle lemmatized, window=2, dim=300) en yüksek puanları aldı.
Jaccard Benzerliği: Lemmatized ve stemmed modeller arasında düşük örtüşme (ör. tfidf_lemmatized vs. tfidf_stemmed: 1.00).
Öneri: Bağlamsal analiz için Word2Vec (Skip-gram), basit eşleşmeler için TF-IDF tercih edilebilir.
Dosyalar
yemektarifieslestirme2.ipynb: Ana kod dosyası
tfidf_lemmatized.csv, tfidf_stemmed.csv: TF-IDF vektör çıktıları
jaccard_benzerlik_matrisi.csv: Jaccard benzerlik matrisi
*.model: Eğitilmiş Word2Vec modelleri
Katkıda Bulunma
İyileştirme önerileri ve hata bildirimleri için lütfen bir issue açın veya pull request gönderin.
