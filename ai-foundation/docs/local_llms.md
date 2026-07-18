# Local LLM'ler Karşılaştırma Rehberi (2026)

Bu doküman, lokalde çalıştırılabilen açık kaynak LLM'leri karşılaştırır. Hangi modelin hangi iş için uygun olduğunu, güçlü ve zayıf yönlerini, donanım gereksinimlerini kapsar.

---

## Model Aileleri ve Genel Karakteristikler

| Aile | Geliştirici | Lisans | Genel Karakter |
|---|---|---|---|
| **Qwen** | Alibaba (Çin) | Apache 2.0 | En geniş boyut yelpazesi, kodlama ve çoklu dilde lider |
| **DeepSeek** | DeepSeek (Çin) | MIT | Akıl yürütme ve matematikte en iyi |
| **Llama** | Meta (ABD) | Llama License | En büyük ekosistem, dengeli genel performans |
| **Gemma** | Google (ABD) | Apache 2.0 | Hafif, verimli, edge cihazlar için ideal |
| **Mistral** | Mistral AI (Fransa) | Apache 2.0 / Research | Hızlı inference, çoklu dil (Avrupa dilleri) |
| **Phi** | Microsoft (ABD) | MIT | Kısıtlı donanımda en iyi akıl yürütme |
| **GLM** | Zhipu AI (Çin) | MIT | Uzun context, agentic kodlama |
| **Kimi** | Moonshot AI (Çin) | Modified MIT | Kodlama ajanları, uzun soluklu görevler |

---

## Model Bazında Detaylı İnceleme

### Qwen 3.x (Alibaba)

**En iyi olduğu alanlar:**
- Kod üretimi ve düzenleme (Qwen Coder varyantları)
- Çoklu dil desteği (İngilizce + Çince + Korece + Japonca)
- Tool calling ve agentic workflow
- Yapılandırılmış çıktı

**Zayıf olduğu alanlar:**
- Batı ekosisteminde daha az community fine-tune'u
- En karmaşık akıl yürütme görevlerinde DeepSeek'in gerisinde

**Öne çıkan modeller ve donanım:**

| Model | Boyut | VRAM (Q4) | Kullanım |
|---|---|---|---|
| Qwen3.6 27B | 27B dense | ~22 GB | Kodlama + agent için en iyi genel model |
| Qwen3-Coder 30B-A3B | 30B (3B aktif) | ~16 GB | Kodlama uzmanı, 24 GB GPU'ya sığar |
| Qwen3.6 35B-A3B | 35B (3B aktif) | ~18 GB | MoE verimliliği, CPU'da hızlı |
| Qwen3.5 9B | 9B dense | ~5 GB | Hafif sistemler için kodlama asistanı |
| Qwen3-Coder-Next | 80B (3B aktif) | ~42 GB | Sunucu seviyesi kodlama |

---

### DeepSeek (DeepSeek)

**En iyi olduğu alanlar:**
- Matematiksel akıl yürütme (AIME, MATH-500'de lider)
- Chain-of-thought reasoning
- Hata ayıklama ve bug detection
- Saf kod üretimi (deepseek-coder 90% pass@1)

**Zayıf olduğu alanlar:**
- Agentic / multi-step görevlerde zayıf (deepseek-coder 10% agent accuracy)
- Full R1 ve V3 modelleri devasa donanım ister (351 GB+)
- Düşük quantize'da kalite kaybı daha belirgin

**Öne çıkan modeller:**

| Model | Boyut | VRAM (Q4) | Kullanım |
|---|---|---|---|
| DS-R1-Distill-Qwen-14B | 14B | ~8 GB | En iyi lokal reasoning modeli |
| DS-R1-Distill-Qwen-32B | 32B | ~17 GB | o1-mini seviyesinde reasoning |
| deepseek-coder:33b | 33B dense | ~18 GB | En yüksek code gen, agent'ta kullanma |
| DeepSeek-V4-Flash | 284B (13B aktif) | Sunucu | Verimli sunucu inference |

---

### Llama (Meta)

**En iyi olduğu alanlar:**
- Genel asistan görevleri (sohbet, özetleme, yazma)
- En geniş community ve tooling desteği
- Instruction following (IFEval'de yüksek)
- Fine-tune ekosistemi (binlerce varyant)

**Zayıf olduğu alanlar:**
- Kodlama performansı Qwen/DeepSeek'in gerisinde
- Llama 4 Scout 55 GB VRAM ister (consumer GPU'ya sığmaz)
- Lisansı 700M MAU sınırı içerir

**Öne çıkan modeller:**

| Model | Boyut | VRAM (Q4) | Kullanım |
|---|---|---|---|
| Llama 3.3 8B | 8B | ~5 GB | Genel amaçlı, dengeli başlangıç modeli |
| Llama 3.3 70B | 70B | ~38 GB | Kaliteli genel asistan |
| Llama 4 Scout | 109B (17B aktif) | ~55 GB | Multimodal, 10M context, çift GPU |
| Llama 4 Maverick | 400B (17B aktif) | ~206 GB | En büyük Llama, sunucu seviyesi |

---

### Gemma (Google)

**En iyi olduğu alanlar:**
- Hafif / edge cihazlar (dizüstü, mobil)
- Multimodal (kod + ekran görüntüsü + diyagram)
- Düşük VRAM'de iyi performans
- Tool calling

**Zayıf olduğu alanlar:**
- Büyük modellerde Qwen'in gerisinde
- Community boyutu Llama kadar geniş değil

**Öne çıkan modeller:**

| Model | Boyut | VRAM (Q4) | Kullanım |
|---|---|---|---|
| Gemma 4 12B | 12B | ~8 GB | 16 GB sistemler için en iyi genel model |
| Gemma 4 26B-A4B | 26B (4B aktif) | ~14 GB | Kodlama + multimodal, 24 GB'a sığar |
| Gemma 4 31B | 31B | ~17 GB | Kodlama + reasoning, güçlü sistemler |

---

### Mistral (Mistral AI)

**En iyi olduğu alanlar:**
- Inference hızı (token/s) — en hızlı 7B modeli
- Avrupa dillerinde en iyi performans
- Instruction following
- Verimli production deployment

**Zayıf olduğu alanlar:**
- Fine-tune ekosistemi Llama'dan dar
- Mistral Large 3 (675B) devasa donanım ister
- Bazı modeller Research License ile sınırlı

**Öne çıkan modeller:**

| Model | Boyut | VRAM (Q4) | Kullanım |
|---|---|---|---|
| Mistral Small 3 7B | 7B | ~5.5 GB | En hızlı lokal model, ~50 tok/s |
| Mistral Small 4 | 119B | ~60 GB | Sunucu için verimli dense model |
| Codestral 22B | 22B | ~12 GB | Kod tamamlama ve fill-in-the-middle |
| Mistral Large 3 | 675B | ~355 GB | En kaliteli, çoklu GPU |

---

### Phi (Microsoft)

**En iyi olduğu alanlar:**
- Kısıtlı donanımda akıl yürütme
- 8 GB RAM'de çalışabilen tek seçenek
- Boyutuna göre yüksek MMLU skoru
- 3.8B modeli edge cihazlar için ideal

**Zayıf olduğu alanlar:**
- Karmaşık çok adımlı görevlerde düşer
- 3.8B varyantı 7B modellerin gerisinde
- Context penceresi sınırlı (16K-32K)

**Öne çıkan modeller:**

| Model | Boyut | VRAM | Kullanım |
|---|---|---|---|
| Phi-4-mini 3.8B | 3.8B | ~3.5 GB | 8 GB RAM'li laptoplar için tek seçenek |
| Phi-4 14B | 14B | ~9 GB | Dengeli kalite, orta seviye donanım |
| Phi-4 Reasoning 14B | 14B | ~9 GB | Akıl yürütme odaklı |

---

## Use Case Bazında En İyi Seçimler

| İhtiyaç | En İyi Model | Neden |
|---|---|---|
| **Günlük kodlama asistanı** | Qwen3.6 27B | 77% SWE-bench, güçlü tool calling, 24 GB'a sığar |
| **Kod review** | Qwen3.6 27B veya GLM-4 32B | Schema disiplini en yüksek (%99), uzun context |
| **Hata ayıklama / Bug fix** | DeepSeek R1-14B | Chain-of-thought ile sistematik analiz |
| **Saf kod üretimi (tek atımlık)** | deepseek-coder:33b | %90 pass@1, agent loop'larında KULLANMA |
| **Agentic workflow (Cline/Aider)** | Qwen3.6 27B | %100 agent accuracy, tool calling lideri |
| **Matematik / Akıl yürütme** | DeepSeek R1-32B | o1-mini'yi geçer, 24 GB'a sığar |
| **Multilingual (Türkçe dahil)** | Qwen3.5 9B veya 27B | En geniş dil desteği |
| **Gizlilik kritik** | Herhangi bir lokal model | Veri dışarı çıkmaz |
| **Edge cihaz / Dizüstü** | Gemma 4 12B veya Phi-4-mini | Düşük VRAM'de iyi çalışır |
| **Avrupa dilleri / GDPR** | Mistral Small 3.1 | Avrupa merkezli, Apache 2.0 |
| **Uzun doküman / repo analizi** | GLM-4 32B-A9B veya Llama 4 Scout | 64K+ context'te en iyi |
| **Vision + Kod** | Gemma 4 26B-A4B | Multimodal, kod + ekran görüntüsü |

---

## Quantization Rehberi

| Seviye | VRAM Tasarrufu | Kalite | Kodlama için öneri |
|---|---|---|---|
| Q8 (8-bit) | ~%50 | Neredeyse kayıpsız | VRAM bolsa en iyisi |
| Q6_K | ~%55 | Çok iyi | 7B-14B modeller için önerilen |
| Q5_K_M | ~%60 | İyi | 14B-30B modeller için dengeli |
| **Q4_K_M** | ~%75 | Kabul edilebilir | **30B+ için önerilen varsayılan** |
| Q3_K_M | ~%80 | Kötü | Kodlama İÇİN ÖNERİLMEZ |
| Q2_K | ~%87 | Çok kötü | Kullanma |

**Kural:** Kodlama için Q4_K_M'nin altına düşme. Daha büyük bir modeli Q2'ye sıkıştırmaktansa, küçük bir modeli Q4'te kullanmak her zaman daha iyidir.

---

## Bu Repodaki Roller İçin En Uygun Model Seçimi

| Rol | Önerilen Model | Alternatif |
|---|---|---|
| **Architect** | Qwen3.6 27B veya Llama 3.3 70B | DeepSeek R1-32B |
| **Researcher** | Qwen3.6 27B | DeepSeek V4-Flash |
| **Coder** | Qwen3-Coder 30B-A3B | deepseek-coder:33b (saf üretim) |
| **Reviewer** | Qwen3.6 27B veya GLM-4 32B | LLM + Open Code Review kombinasyonu |
| **Tester** | Qwen3.6 27B | Qwen3-Coder 30B-A3B |

**Not:** Eğer tek bir model seçmek zorundaysan, **Qwen3.6 27B** en dengeli seçenektir. Tüm roller için "idare eder" seviyesinin üzerindedir ve 24 GB GPU'ya sığar.

---

## Önemli İpuçları

1. **Benchmark'a takılma** — SWE-bench'te yüksek olan model, senin kodlama stiline uymayabilir. Kendi iş yükünle test et.
2. **Quantization seviyesi kodlamada kritik** — Q4 altında syntax hatası ve mantık hatası riski artar.
3. **Context window her şey değil** — 128K context vaat eden model, 32K'da bile performans kaybedebilir. Gerçekçi ihtiyacını belirle.
4. **Aynı anda 2-3 model kullan** — Cloud (zor görevler) + Local (gizlilik/tekrarlı görevler) hibriti en pragmatik yaklaşım.
5. **Ollama ile başla** — `ollama pull qwen3.6:27b` ile 2 dakikada dene, memnun kalmazsan sil.
