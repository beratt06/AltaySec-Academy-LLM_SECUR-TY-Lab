# AltaySec — LLM Jailbreak Lab 🔓

> **AltaySec Academy Eğitim Amaçlı Yapay Zeka Güvenlik Laboratuvarı**
> LLM (Büyük Dil Modeli) güvenlik zafiyetlerini (Prompt Injection, Jailbreak, System Prompt Exfiltration) öğrenmek ve pratik yapmak için hazırlanmış dockerize bir CTF ortamı.

![AltaySec LLM Security Lab](assets/preview.png)
*(Buraya daha sonra projenin bir ekran görüntüsünü ekleyebilirsin)*

---

## 🚀 Hızlı Başlangıç

### Gereksinimler
- [Docker](https://www.docker.com/products/docker-desktop/) ve Docker Compose kurulu olmalı.
- Ücretsiz LLM API Key:
  - **Groq (Önerilen/Hızlı):** [console.groq.com/keys](https://console.groq.com/keys)
  - **Google Gemini:** [aistudio.google.com/apikey](https://aistudio.google.com/apikey)

### Kurulum ve Çalıştırma

1. Repoyu klonlayın:
```bash
git clone https://github.com/beratt06/AltaySec-Academy-LLM-Lab.git
cd AltaySec-Academy-LLM-Lab
```

2. Docker ile projeyi başlatın:
```bash
docker-compose up --build -d
```

3. Tarayıcınızda açın:
**👉 http://localhost:3002**

*(Not: Sunucuya/Production'a kuruyorsanız, Nginx vb. bir Reverse Proxy ile 80 veya 443 portuna bağlayabilirsiniz.)*

---

## 🎯 Nasıl Oynanır?

1. **Bağlantı Kurun:** Arayüze kendi API anahtarınızı (Gemini veya Groq) girin.
2. **Görev Seçin:** Kolaydan zora doğru sıralanmış güvenlik açıklarını inceleyin.
3. **Zafiyet Avı:** Hedef sistemi manipüle ederek (Prompt Injection/Jailbreak) koruduğu sırrı `AltaySec{...}` açığa çıkartmaya çalışın.
4. **Bayrağı Doğrulatın:** Bulduğunuz bayrağı sisteme girerek seviyeyi tamamlayın.
5. **Takılırsanız:** Sağ menüdeki "İpuçları" (Hints) özelliğini kullanabilirsiniz.

---

## 🏆 Seviyeler

| Zorluk | Hedef Sistem | Öğrenim Çıktısı (Konsept) |
|--------|--------------|-------------------------|
| 🟢 **Kolay** | VAULT-BOT 9000 | Rol yapma (Roleplay) / Karakter bypass saldırıları |
| 🟡 **Orta** | CORP-ASSISTANT | Çok katmanlı Prompt Injection atlatma teknikleri |
| 🔴 **Zor** | NEMESIS-AI v2.1 | Gelişmiş System Prompt Exfiltration (Sızdırma) |

---

## 🏗 Sistem Mimarisi ve Güvenlik

Laboratuvar güvenlik odaklı olarak "Sıfır Fatura (Zero-Bill)" prensibiyle tasarlanmıştır.

- **İstemci Taraflı LLM:** Tüm yapay zeka istekleri doğrudan kullanıcının tarayıcısından (girilen API key ile) yapılır. Sunucunuzda LLM çağrısı yapılmadığı için DDoS veya API limiti aşımı nedeniyle sunucu sahibine maliyet çıkmaz.
- **Güvenli Backend:** CTF bayrakları (`AltaySec{...}`) frontend'e gönderilmez. Kullanıcının girdiği bayrak, backend (`Node.js`) üzerinde **SHA-256 hash** kullanılarak doğrulanır. Ağ (Network) izlenerek bayrak çalınamaz.
- **Obfuscation (Gizleme):** Sistem prompt'ları backend'den Base64+XOR şifrelemesiyle istemciye aktarılır.
- **Konteyner İzolasyonu:** Frontend (Nginx proxy) ve Backend izole edilmiş `docker-compose` ağı içinde haberleşir.

```text
llm security/
├── docker-compose.yml
├── backend/                  # Node.js API (Hash Doğrulama)
├── frontend/                 # Static HTML/CSS/JS (Kullanıcı Arayüzü)
└── assets/                   # README ve dökümantasyon görselleri
```

---

## 📝 Lisans

Bu proje eğitim amaçlı geliştirilmiş olup **MIT Lisansı** ile lisanslanmıştır. Dilediğiniz gibi kullanabilir, değiştirebilir ve kendi eğitimlerinizde faydalanabilirsiniz.

*AltaySec CTF Lab — "Sistemleri korumak için, önce nasıl kırıldıklarını anlamalısın."*
