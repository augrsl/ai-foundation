# AI Foundation

**AI Foundation**, mühendislik ekiplerinin AI kod asistanlarını (Claude Code, ChatGPT, Gemini, Cursor vb.) kullanırken **tutarlı, tekrarlanabilir ve kaliteli sonuçlar** almasını sağlayan, yapılandırılmış bir prompt/komut framework'üdür.

Bu bir yazılım projesi değildir — AI asistanlarına vereceğiniz **system prompt'ları, rolleri, workflow'ları ve prosedürleri** içeren bir şablondur. Kendi projenize göre özelleştirmek üzere fork'layıp `TODO` alanlarını doldurmanız beklenir.

---

## Dizin Yapısı

```
ai-foundation/
├── README.md
├── TODOs.md
└── ai-foundation/
    ├── README.md
    ├── roles/          # AI asistanının takınacağı roller (system prompt'lar)
    │   ├── architect.md
    │   ├── coder.md
    │   ├── researcher.md
    │   ├── reviewer.md
    │   └── tester.md
    ├── workflows/      # Rollerin hangi sırayla çalışacağı
    │   ├── default.md
    │   └── new_feature.md
    ├── playbooks/      # Sık yapılan işler için adım-adım prosedürler
    │   ├── bug_fix.md
    │   └── new_feature.md
    ├── commands/       # Kısayol prompt'ları
    │   ├── design.md
    │   └── review.md
    ├── context/        # Projeye özgü bilgiler (şablon)
    │   ├── project.md
    │   ├── known_issues.md
    │   └── dxl_reference.md
    ├── standards/      # Kodlama standartları (şablon)
    │   └── coding_rules.md
    ├── templates/      # Çıktı şablonları
    │   └── ADR.md
    ├── checklists/     # Kalite kapıları
    │   └── before_commit.md
    ├── examples/       # Örnek kullanım senaryoları
    │   ├── example_session.md
    │   └── dxl/
    └── docs/           # Dokümantasyon
        ├── ROADMAP.md
        └── local_llms.md
```

---

## Bileşenlerin Amacı

| Klasör | Ne İşe Yarar |
|---|---|
| **roles/** | AI asistanının nasıl davranacağını belirleyen system prompt'lar. Her rol farklı bir uzmanlık alanına odaklanır |
| **workflows/** | Rollerin hangi sırayla zincirleneceğini tanımlar. Örn: Önce architect tasarlar, sonra coder kodlar, sonra reviewer inceler |
| **playbooks/** | Belli bir işi baştan sona yapmak için adım-adım talimatlar (bug fix, yeni feature) |
| **commands/** | Sık kullanılan işlemler için kısayol prompt'ları |
| **context/** | AI asistanının projeyi anlaması için gereken bağlamsal bilgiler |
| **standards/** | AI'ın uyması gereken kodlama kuralları |
| **templates/** | Üretilmesi gereken çıktılar için şablonlar (ADR gibi) |
| **checklists/** | Commit öncesi gibi kalite kapılarında kontrol edilecek maddeler |
| **examples/** | Örnek oturumlar ve referans kod örnekleri |
| **docs/** | Üst düzey dokümantasyon ve referanslar |

---

## Roller (AI Personas)

| Rol | Açıklama |
|---|---|
| **Architect** | Gereksinimleri analiz eder, alternatifleri değerlendirir, tradeoff'ları tartışır. Kod yazmaz |
| **Researcher** | Alternatifleri karşılaştırır, varsayımları belirtir, belirsizlik seviyesini raporlar |
| **Coder** | Sadece onaylanmış tasarımı uygular, minimal değişiklik yapar, standartlara uyar |
| **Reviewer** | Kod incelemesi yapar, hataları severity seviyesine göre sıralar, düzeltme önerir |
| **Tester** | Unit, integration, regression testleri üretir, coverage boşluklarını tespit eder |

---

## Hızlı Başlangıç

### Adım 1: Proje Bağlamını Tanımla

`context/project.md`, `context/known_issues.md` ve `standards/coding_rules.md` dosyalarındaki `TODO` alanlarını kendi projen için doldur.

### Adım 2: Bir AI Asistanı Seç

Bu framework aşağıdaki asistanlarla kullanılabilir:

- **Claude Code** (Anthropic) — önerilen, rolleri ve workflow'ları en iyi takip eder
- **ChatGPT** (OpenAI)
- **Gemini** (Google)
- **Cursor / Codex**
- **OpenCode** ile local LLM (Qwen, DeepSeek, Llama vb. — bkz: `docs/local_llms.md`)

### Adım 3: Rolleri ve Workflow'ları Kullan

**Tek bir iş için (örneğin kod yaz):**
```
/roles/coder.md oku. /context/project.md oku. Şu işlevi yaz: [detay]
```

**Rolleri zincirleme:**
```
Terminal 1: /roles/architect.md oku → tasarım yap
Terminal 2: /roles/coder.md oku → kodu yaz
Terminal 3: /roles/reviewer.md oku → code review yap
```

**Hazır workflow kullan:**
```
/workflows/default.md oku ve uygula. Yapılacak: [iş]
```

**Kısayol komut:**
```
/roles/reviewer.md oku. Mevcut değişiklikleri review et.
```

### Adım 4: Kalite Kapıları

Commit öncesi `/checklists/before_commit.md` oku ve her maddeyi kontrol et.

---

## Kimler İçin?

- **Gömülü sistem / güvenlik-kritik yazılım ekipleri** — reviewer rolünde MISRA, interrupt safety, stack/heap, race condition odaklı inceleme
- **Herhangi bir yazılım ekibi** — sistematik AI destekli geliştirme süreci isteyen
- **AI asistanını ilk kez kullanan ekipler** — neyin, nasıl isteneceğine dair hazır şablonlar

---

## Yol Haritası

| Versiyon | İçerik |
|---|---|
| **v1** (mevcut) | Roller, workflow'lar, playbook'lar, template'ler |
| **v2** | Claude Code / Cursor / Codex entegrasyonu |
| **v3** | MCP (Model Context Protocol) ve RAG desteği |
| **v4** | Takım şablonları ve yönetim araçları |

Detay: `docs/ROADMAP.md`

---

## Katkı

Bu repo bir şablondur. Kendi projenize uyarlamak için fork'layın, `TODO` alanlarını doldurun, kendi rol ve workflow'larınızı ekleyin.

---

## Lisans

Bu proje, AI asistan prompt'ları ve şablonlarından oluşur. İstediğiniz gibi kullanabilir, değiştirebilir ve dağıtabilirsiniz.
