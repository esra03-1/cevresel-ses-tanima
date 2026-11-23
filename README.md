# Çevresel Ses Tanıma ve Otomatik Etiketleme

Kısa ses kayıtlarını analiz ederek 10 çevresel ses türünden birini tahmin eden makine öğrenmesi projesi.

Ses arşivlerinde aranan kaydı bulmayı kolaylaştırmak amacıyla geliştirdim. Uygulama, yüklenen WAV dosyasından sayısal özellikler çıkarır ve tahmin edilen ses türünü Türkçe gösterir.

[Google Colab’da aç ve çalıştır](https://colab.research.google.com/drive/1hITLXapxL36OPzxAYyx8dz8WDrelZtsi?usp=sharing)

## Veri seti

ESC-50 veri setinin ESC-10 alt kümesini kullandım.

- Toplam 400 ses kaydı
- Her biri 5 saniyelik WAV dosyaları
- 10 sınıf ve her sınıfta 40 kayıt

Ses türleri köpek havlaması, horoz ötüşü, yağmur, deniz dalgaları, ateş çıtırtısı, bebek ağlaması, hapşırma, saat tıklaması, helikopter ve motorlu testeredir.

## Kullanılan teknolojiler

Python, Pandas, NumPy, Matplotlib, librosa, scikit-learn ve Google Colab.

## Yöntem

Sesleri tek kanallı ve 22.050 Hz örnekleme hızında okuyarak her kayıttan 16 özellik çıkardım.

- RMS ortalaması ve standart sapması
- Ortalama sıfır geçiş oranı
- 13 MFCC katsayısının zaman boyunca ortalaması

Karar Ağacı ve 200 ağaçlı Random Forest modellerini karşılaştırdım. Veri setindeki hazır fold gruplarını korudum.

| Aşama | Eğitim | Değerlendirme |
|---|---|---|
| Model karşılaştırması | Fold 1–3, 240 kayıt | Fold 4, 80 doğrulama kaydı |
| Seçilen modelin son testi | Fold 1–4, 320 kayıt | Fold 5, 80 test kaydı |

## Sonuçlar

| Model | Doğrulama doğruluğu |
|---|---:|
| Karar Ağacı | %65 |
| Random Forest | %75 |

Doğrulamada daha başarılı olan Random Forest’ı seçip 320 kayıtla yeniden eğittim.

**Son testte 80 kaydın 66’sı doğru sınıflandırıldı. Test doğruluğu %82,5 oldu.**

Yağmur ve saat tıklaması sınıflarında sekizer test kaydının tamamı doğru tanındı. Ateş çıtırtısı sınıfında sekiz kaydın dördü doğru sınıflandırıldı.

## Çalıştırma

1. Yukarıdaki bağlantıdan Colab defterini açın.
2. Hücreleri baştan sona sırayla çalıştırın.
3. Ses dosyalarının indirilmesinin tamamlanmasını bekleyin.
4. Dosya yükleme bölümünde yaklaşık 5 saniyelik bir WAV kaydı seçin.
5. Kaydı dinleyip modelin Türkçe tahminini inceleyin.

Kendi dosyanız yoksa yükleme penceresinde Cancel upload seçeneğine basıp hazır test örnekleriyle devam edebilirsiniz.

İndirme sırasında geçici bağlantı hataları oluşursa kod bekleyip yeniden dener. İndirme tamamlandığında “Hazır ses dosyası: 400 / 400” mesajı görünür.

## Depodaki dosyalar

- `.ipynb` dosyası — Açıklamalı kodlar, grafikler ve kayıtlı sonuçlar
- `esc10_ses_ozellikleri.csv` — 400 kaydın özellik tablosu
- `veri_sozlugu.csv` — Sütunların anlamları ve görevleri
- `Cevresel_Ses_Tanima_Proje_Raporu.pdf` — Bir sayfalık proje raporu
- `Cevresel_Ses_Tanima_Sunum.pptx` — Beş slaytlık sunum

## Sınırlılıklar

Başarı, veri setindeki tek bir 80 kayıtlık test grubunda ölçüldü. Veri seti dışındaki telefon kayıtlarında değerlendirme henüz yapılmadı.

Model her kayda öğrendiği 10 etiketten birini verir. Farklı sesler ve birden fazla ses içeren kayıtlar ayrıca değerlendirilmelidir.

## Veri kaynağı ve atıf

Karol J. Piczak (2015). ESC: Dataset for Environmental Sound Classification.

ESC-10 alt kümesi CC BY lisansıyla sunulmaktadır. Ses dosyalarını defterdeki kod aracılığıyla kaynak depodan indiriyorum.

[Veri seti ve lisans bilgileri](https://github.com/karolpiczak/ESC-50)

## Hazırlayan

Esra Gögebakan
