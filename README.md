# **Bir Kara Kutuyu Açmak: PyTorch İle Eğitilmiş Transformer Modelinin NumPy İle Yeniden İnşası**

Bu repositori, "Attention Is All You Need" \[1\] makalesinde sunulan Transformer mimarisinin, İngilizce-Türkçe Nöral Makine Çevirisi (NMT) görevi için uygulanmasını içerir. Proje, modelin PyTorch ile eğitilmesini ve ardından çıkarım mekanizmasının temel lineer cebir kütüphanesi NumPy ile sıfırdan yeniden gerçeklenmesini kapsar.


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

### **2. Veri Seti**

Çalışmada kullanılan `en2tr_train.txt` ve `en2tr_valid.txt` dosyaları, projenin ana dizinindeki `/data` klasörü altında bulunmalıdır. Kendi veri setinizi kullanmak isterseniz, aynı formatta (her satırda `kaynak cümle\thedef cümle`) dosyalar oluşturmanız yeterlidir.

### **3. Modeli Eğitme (PyTorch)**

Bu repositoride önceden eğitilmiş model dosyaları (`.pth`) paylaşılmamaktadır. Çıkarım ve değerlendirme adımlarını çalıştırabilmek için öncelikle modeli kendiniz eğitmelisiniz.

Modeli sıfırdan eğitmek için `notebooks/2_PyTorch_Transformer_Egitimi.ipynb` not defterini çalıştırın. Bu script, **öncelikle `en2tr_train.txt` dosyasını okuyarak kaynak ve hedef dil için kelime dağarcıklarını (tokenizer) oluşturur.** Eğitim tamamlandığında, `checkpoints` klasörü altına hem modelin ağırlıklarını (`best_model.pth`) hem de tokenizer'ları içeren tam durum dosyasını (`last_checkpoint.pth`) kaydedecektir.

### **4. Çeviri Yapma ve Analiz**

Modelinizi eğittikten sonra, aşağıdaki not defterlerini çalıştırarak sonuçları elde edebilirsiniz. Bu not defterleri, çalışmak için `checkpoints` klasöründeki dosyaları okuyarak gerekli model ağırlıklarını ve tokenizer'ları yükleyecektir.

* `notebooks/3_NumPy_Cikarim_Motoru_ve_Dogrulama.ipynb`: Eğitilmiş modeli kullanarak interaktif çeviri yapar.
* `notebooks/4_Dikkat_Matrislerinin_Analizi_ve_Gorsellestirilmesi.ipynb`: Belirli bir cümlenin dikkat haritalarını üretir ve görselleştirir.
* `notebooks/5_Performans_Degerlendirme_(BLEU_ve_Hiz_Testleri).ipynb`: Modelin BLEU skorunu ve çıkarım hızını hesaplar.

---

## **Katkıda Bulunma (Contributing)**

Bu projenin gelişmesine yardımcı olmak isterseniz, her türlü katkıya açığız! Hata bildirimleri, özellik önerileri ve kod katkıları projenin daha iyi bir kaynak haline gelmesine yardımcı olur.

### **Hata Bildirimi ve Öneriler**
Eğer kodda veya dokümantasyonda bir hata fark ederseniz ya da bir geliştirme öneriniz varsa, lütfen bu repositorinin **"Issues"** sekmesini kullanarak yeni bir başlık açmaktan çekinmeyin.

### **Kod Katkısı (Pull Requests)**
Koda doğrudan katkıda bulunmak isterseniz, standart "fork & pull request" iş akışını izleyebilirsiniz:
1.  Bu repoyu kendi hesabınıza **Fork**'layın.
2.  Yeni bir özellik veya düzeltme için kendi **Branch**'inizi oluşturun (`git checkout -b ozellik/yeni-gorsellestirme`).
3.  Değişikliklerinizi yapın ve **Commit**'leyin.
4.  Oluşturduğunuz Branch'i kendi reponuza **Push**'layın (`git push origin ozellik/yeni-gorsellestirme`).
5.  GitHub üzerinden bu repoya bir **Pull Request** açarak değişikliklerinizi açıklayın.

---

## **Lisans**

Bu proje, MIT Lisansı altında lisanslanmıştır. Detaylar için `LICENSE` dosyasına bakınız.

## **Referanslar**

\[1\] Vaswani, A., et al. (2017). "Attention Is All You Need". *NeurIPS*.
