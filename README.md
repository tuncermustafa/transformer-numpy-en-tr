## Bir Kara Kutuyu Açmak: Transformer Modelinin PyTorch ve NumPy ile İnşası
Bu repositori, "Attention Is All You Need" [1] makalesinde sunulan Transformer mimarisinin, İngilizce-Türkçe Nöral Makine Çevirisi (NMT) görevi için uygulanmasını içerir. Proje, modelin PyTorch ile eğitilmesini ve ardından çıkarım mekanizmasının temel lineer cebir kütüphanesi NumPy ile sıfırdan yeniden gerçeklenmesini kapsar.

### Proje Hakkında
Bu projenin temel motivasyonu, Transformer gibi karmaşık derin öğrenme modellerinin arkasındaki temel mekanizmaları şeffaf bir şekilde ortaya koymaktır. PyTorch gibi kütüphanelerin soyutlamalarını bir kenara bırakarak, dikkat mekanizmaları, pozisyonel kodlama ve katman normalizasyonu gibi temel bileşenleri saf NumPy ile yeniden inşa ederek, modelin iç işleyişine dair derinlemesine ve pratik bir anlayış sunmayı hedefler.

Bu repositori, hem Transformer modelini belirli bir veri seti üzerinde başarıyla eğiten pratik bir NMT uygulaması, hem de bu modelin "kara kutusunu" açarak temel matematiksel operasyonlarını incelemek isteyen öğrenciler ve araştırmacılar için değerli bir eğitimsel kaynaktır.

### Temel Özellikler
PyTorch Eğitim Script'i: Transformer modelini, verilen paralel metin veri seti üzerinde eğitmek için gereken tüm kodları içerir. Checkpoint kaydetme, öğrenme oranı zamanlayıcısı ve erken durdurma gibi mekanizmaları barındırır.

### NumPy Çıkarım Motoru: 
Herhangi bir derin öğrenme kütüphanesine bağımlı olmaksızın, sadece NumPy kullanarak eğitilmiş bir modelden çeviri yapabilen, sıfırdan yazılmış bir çıkarım motoru.

### Performans Değerlendirme: 
Hem PyTorch hem de NumPy implementasyonlarının hızını (CPU/GPU) karşılaştıran benchmark script'leri.

Dikkat Görselleştirme: Modelin çeviri sırasında nereye "odaklandığını" gösteren dikkat haritası matrislerini üreten ve görselleştiren kodlar.

Veri Seti: Çalışmada kullanılan ve ön işlemden geçirilmiş en2tr_valid.txt ve en2tr_train.txt dosyaları.

### Performans Özeti
Belirtilen kısıtlar (kelime bazlı tokenizasyon, greedy decoding) altında eğitilen model, oldukça başarılı sonuçlar elde etmiştir:

Çeviri Kalitesi (BLEU): 46.13

Performans Oranı: Optimize edilmiş PyTorch (CPU) altyapısı, saf NumPy (CPU) implementasyonundan yaklaşık 2.5 kat daha hızlıdır.

### Kullanım ve Kurulum
Bu projeyi kendi ortamınızda çalıştırmak için aşağıdaki adımları izleyebilirsiniz.

### Gereksinimler
Proje, Python 3.x ortamında geliştirilmiştir. Gerekli tüm kütüphaneler requirements.txt dosyasında listelenmiştir. Bunları aşağıdaki komutla yükleyebilirsiniz:

pip install -r requirements.txt

### Temel bağımlılıklar: 
torch, numpy, sacrebleu, tqdm, matplotlib, seaborn.

### 1. Veri Seti
Çalışmada kullanılan en2tr_train.txt ve en2tr_valid.txt dosyaları, /data klasörü altında bulunmalıdır. Kendi veri setinizi kullanmak isterseniz, aynı formatta (her satırda kaynak cümle\thedef cümle) dosyalar oluşturmanız yeterlidir.

### 2. Modeli Eğitme (PyTorch)
Modeli sıfırdan eğitmek için train_pytorch.py script'ini çalıştırabilirsiniz.

python train_pytorch.py

Bu script, eğitim sonunda model_checkpoints klasörü altına best_model.pth (en iyi modelin ağırlıkları) ve last_checkpoint.pth (eğitimin son durumunu içeren tam checkpoint) dosyalarını kaydedecektir.

### 3. Çeviri Yapma (NumPy)
Eğitilmiş bir modelle çeviri yapmak için inference_numpy.py script'ini kullanabilirsiniz. Bu script, checkpoint dosyalarını yükleyerek interaktif bir şekilde sizden İngilizce cümleler alıp Türkçe'ye çevirecektir.

python inference_numpy.py

### 4. Dikkat Haritalarını Üretme
Belirli bir cümlenin dikkat haritalarını (Encoder Self-Attention, Decoder Cross-Attention, Decoder Masked Self-Attention) üretmek ve görselleştirmek için visualize_attention.py script'ini çalıştırın.

python visualize_attention.py

Bu, /results klasörü altına ısı haritası görsellerini (.png) kaydedecektir.

### Lisans
Bu proje, MIT Lisansı altında lisanslanmıştır. Detaylar için LICENSE dosyasına bakınız.

### Referanslar
[1] Vaswani, A., et al. (2017). "Attention Is All You Need". NeurIPS.
