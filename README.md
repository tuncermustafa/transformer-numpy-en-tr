# **Bir Kara Kutuyu Açmak: Transformer Modelinin PyTorch ve NumPy ile İnşası**

Bu repositori, "Attention Is All You Need" \[1\] makalesinde sunulan Transformer mimarisinin, İngilizce-Türkçe Nöral Makine Çevirisi (NMT) görevi için uygulanmasını içerir. Proje, modelin PyTorch ile eğitilmesini ve ardından çıkarım mekanizmasının temel lineer cebir kütüphanesi NumPy ile sıfırdan yeniden gerçeklenmesini kapsar.

Bu çalışmanın detaylarını içeren akademik makaleye **[Buraya Makalenizin Linkini veya arXiv Linkini Ekleyebilirsiniz]** adresinden ulaşabilirsiniz.

---

## **Proje Hakkında**

Bu projenin temel motivasyonu, Transformer gibi karmaşık derin öğrenme modellerinin arkasındaki temel mekanizmaları şeffaf bir şekilde ortaya koymaktır. PyTorch gibi kütüphanelerin soyutlamalarını bir kenara bırakarak, dikkat mekanizmaları, pozisyonel kodlama ve katman normalizasyonu gibi temel bileşenleri saf NumPy ile yeniden inşa ederek, modelin iç işleyişine dair derinlemesine ve pratik bir anlayış sunmayı hedefler.

Bu repositori, hem Transformer modelini belirli bir veri seti üzerinde başarıyla eğiten pratik bir NMT uygulaması, hem de bu modelin "kara kutusunu" açarak temel matematiksel operasyonlarını incelemek isteyen öğrenciler ve araştırmacılar için değerli bir eğitimsel kaynaktır.

### **Performans Özeti**

Belirtilen kısıtlar (kelime bazlı tokenizasyon, greedy decoding) altında eğitilen modelin elde ettiği temel performans metrikleri şunlardır:

* **Çeviri Kalitesi (BLEU):** `sacrebleu` ile yapılan değerlendirmede `46.13` gibi rekabetçi bir skora ulaşılmıştır.
* **Göreceli Hız Performansı:** Optimize edilmiş PyTorch (CPU) motorunun, saf NumPy (CPU) implementasyonuna göre yaklaşık **2.5 kat** daha hızlı olduğu tespit edilmiştir.

---

## **Kullanım ve Kurulum**

Bu projeyi kendi ortamınızda çalıştırmak ve sonuçları tekrarlamak için aşağıdaki adımları izleyebilirsiniz.

### **1. Gereksinimler**

Proje, Python 3.x ortamında geliştirilmiştir. Gerekli tüm kütüphaneler `requirements.txt` dosyasında listelenmiştir. Bunları aşağıdaki komutla yükleyebilirsiniz:

```bash
pip install -r requirements.txt
```

*Temel bağımlılıklar: `torch`, `numpy`, `sacrebleu`, `tqdm`, `matplotlib`, `seaborn`.*

### **2. Veri Seti ve Tokenizer'lar**

* **Veri:** Çalışmada kullanılan `en2tr_train.txt` ve `en2tr_valid.txt` dosyaları, `/data` klasörü altında bulunmalıdır.
* **Tokenizer:** Çıkarım ve değerlendirme script'lerinin doğru çalışması için gerekli olan `src_word2idx.json` ve `trg_word2idx.json` dosyaları, bu repositorideki `/tokenizers` klasöründe mevcuttur.

### **3. Modeli Eğitme (PyTorch)**

Bu repositoride önceden eğitilmiş model dosyaları (`.pth`) paylaşılmamaktadır. Çıkarım ve değerlendirme adımlarını çalıştırabilmek için öncelikle modeli kendiniz eğitmelisiniz.

Modeli sıfırdan eğitmek için `notebooks/2_PyTorch_Transformer_Egitimi.ipynb` not defterini çalıştırın. Bu script, eğitim sonunda `checkpoints` klasörü altına `best_model.pth` ve `last_checkpoint.pth` dosyalarını kaydedecektir.

### **4. Çeviri Yapma ve Analiz**

Modelinizi eğittikten sonra, aşağıdaki not defterlerini çalıştırarak sonuçları elde edebilirsiniz:

* `notebooks/3_NumPy_Cikarim_Motoru_ve_Dogrulama.ipynb`: Eğitilmiş modeli kullanarak interaktif çeviri yapar.
* `notebooks/4_Dikkat_Matrislerinin_Analizi_ve_Gorsellestirilmesi.ipynb`: Belirli bir cümlenin dikkat haritalarını üretir ve görselleştirir.
* `notebooks/5_Performans_Degerlendirme_(BLEU_ve_Hiz_Testleri).ipynb`: Modelin BLEU skorunu ve çıkarım hızını hesaplar.

---

## **Lisans**

Bu proje, MIT Lisansı altında lisanslanmıştır. Detaylar için `LICENSE` dosyasına bakınız.

## **Referanslar**

\[1\] Vaswani, A., et al. (2017). "Attention Is All You Need". *NeurIPS*.
