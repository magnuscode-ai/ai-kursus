# LearnAI — Komplet Projektstatus
*Opdateret efter lang byggesession — alt hvad næste chat skal vide*

---

## 🎯 Hvem er brugeren
Alexander og August bygger **LearnAI** (learnai.dk / magnuscode-ai.github.io/ai-kursus) — en dansk AI-kursusplatform. Gratis kursus D → betalt C → B → A. Bygget i ren HTML/CSS/JS med Firebase og Anthropic API.

**Vigtige arbejdspræferencer:**
- Vil have ærlighed, ikke smigeri — sig det hvis noget er dårligt
- Øvelser og hands-on > masser af prompts
- Premium, professionelt look altid
- Tag beslutninger på hans vegne når han er usikker
- Svar skal matche spørgsmålets længde
- Stil spørgsmål ved tvivl — byg rigtigt frem for hurtigt
- Aggressive animationer foretrukket

---

## 🗂 Filstruktur (GitHub: magnuscode-ai/ai-kursus)

### ✅ FÆRDIGE OG UPLOADEDE
- `platform.html` — hovedplatform med Firebase login
- `eksamen-d.html` — kursus D eksamen del 1
- `eksamen-d-del2.html` — kursus D eksamen del 2
- `kursus-d.html` — kursus D læringsmateriale

### ✅ FÆRDIGBYGGET, KLAR TIL UPLOAD
- `kursus-c1.html` — Prompt-teknik (indigo)
- `kursus-c2.html` — Emails & produktivitet (teal)
- `kursus-c3.html` — Møder, research & indhold (violet)
- `bibliotek.html` — Prompt-bibliotek (localStorage)
- `intro-cplus.html` — C+ forside med cinematic animation
- `kursus-cplus.html` — C+ personlig AI-plan generator

### ✅ EKSISTERER ALLEREDE PÅ GITHUB
- `quiz-c1.html` — Mini-quiz C1 (6 spørgsmål, 5/6 for at bestå)
- `quiz-c2.html` — Mini-quiz C2 (6 spørgsmål, 5/6 for at bestå)

### ❌ MANGLER AT BLIVE BYGGET
- `eksamen-c.html` — **NÆSTE PRIORITET**
- `eksamen-c-del2.html` — **NÆSTE PRIORITET**

---

## 🚨 NÆSTE SKRIDT I PRIORITERET RÆKKEFØLGE

### 1. `eksamen-c.html` — Kursus C Eksamen Del 1
**Bygges som kopi af eksamen-d.html men med nyt indhold:**

15 multiple choice spørgsmål fra C1+C2+C3:
- **C1 (prompt-teknik):** Rolleprompts, kontekst, iterativ forfining, format-styring, outputkontrol
- **C2 (email/produktivitet):** Den svære email, opfølgning, kanalvalg, tonevalg, promptbibliotek
- **C3 (møder/research/indhold):** Mødeforberedelse, referater, stillads-teknikken, kildekritik, kanalskift

**Krav:** 12/15 for at bestå  
**Ved beståelse:** Raket-animation → `eksamen-c-del2.html`  
**Journey-bar:** C1 → Q1 → C2 → Q2 → C3 → **E1** → E2 → Bevis  
**Farve:** Violet (#7C3AED) ligesom C3

### 2. `eksamen-c-del2.html` — Kursus C Eksamen Del 2
**Bygges som kopi af eksamen-d-del2.html men med højere niveau:**

Praktisk prompt-opgave: Bruger skal skrive et prompt der demonstrerer:
1. **Rolleprompt** (AI får en klar rolle)
2. **Kontekst** (specifik situation beskrives)
3. **Ønsket format** (output-type specificeres)

JS-bedømmelse — samme mønster som D men strengere.  
**Maks 3 forsøg**  
**Beståelse:** 150 coins + Sølv-badge C gemmes i Firestore via `saveCertificate()`  
**Bevis:** Navn, email, dato — som i D men med sølv styling  
**Knap:** Tilbage til platform + (efter bestået) knap til C+

### 3. `platform.html` — Platform Opdatering
Kursus C-kortet skal:
- Vise "Start Kursus C" (→ `kursus-c1.html`) når C ikke er bestået
- Skifte til "Tag Kursus C+" (→ `intro-cplus.html`) når `completedCourses` indeholder `'kursus-c'`

### 4. Quiz-filer — Tjek coins
`quiz-c1.html` og `quiz-c2.html` eksisterer på GitHub.  
Tjek at de **giver 25 coins i Firestore** ved beståelse (samme mønster som kursus D).

### 5. Firestore Sikkerhedsregler
Test-mode udløber 30 dage efter oprettelse. **Skal strammes** inden launch.

---

## 🔥 Firebase Konfiguration
```javascript
const firebaseConfig = {
  apiKey: "AIzaSyAeJF_1DiT3E4pi2HhmwIq22P1ARPuJ5TA",
  projectId: "learnai-dk",
  appId: "1:3073076360:web:b853d118e943395de4833d"
};
// Firestore region: europe-west1
```

**Firestore struktur per bruger:**
```
users/{uid}: {
  fornavn, efternavn, email,
  coins: Number,
  badges: ['badge-d', 'badge-c', ...],
  completedCourses: ['kursus-d', 'kursus-c', ...]
}
```

---

## 🎨 Design System

### Farver pr. kursus
| Kursus | Primær | Bruges til |
|--------|--------|------------|
| D | #10B981 (emerald) | Kursus D sider |
| C1 | #4F46E5 (indigo) | kursus-c1.html |
| C2 | #0D9488 (teal) | kursus-c2.html |
| C3 | #7C3AED (violet) | kursus-c3.html |
| C+ | #E11D48 (rose) | intro-cplus + kursus-cplus |
| Eksamen | Violet som C3 | eksamen-c filer |

### Fonte
- **Outfit** (sans-serif) — brødtekst, UI
- **Lora** (serif, italic) — hero-headings

### CSS Variabler (standard i alle C-filer)
```css
--vio: #7C3AED; --vio-deep: #5B21B6; --vio-50: #F5F3FF;
--rose: #E11D48; --rose-deep: #9F1239;
--green: #059669; --amber: #D97706;
--ink: #0D1117; --ink-soft: #374151; --muted: #6B7280;
--border: #E5E7EB; --bg: #F9FAFB; --white: #FFFFFF;
```

---

## 🔒 Lås-system (ens i C1/C2/C3)

```
M1: Åben + done fra start
M2: unlocked-next (amber kant) fra start
Åbn M1 → M2 amber (allerede sket)
Åbn M2 → M3 amber
Åbn M3 → M4 amber (UNDTAGEN i C1 og C3)
```

**Specielle regler:**
- **C1 M3→M4:** Kræver at brugeren har sendt mindst 1 besked i AI-chatten
- **C3 M4→M5:** Kræver at simulatoren er bestået ELLER alle 3 forsøg brugt → `unlockM5()`
- **C2 M5→quiz:** Kræver at bibliotek-knappen er klikket → `unlockExam()`
- **Alle:** Eksamen-knap låst til alle moduler åbnet

**Locked-toast** er specifik per situation:
- C1 M4 (hvis chat ikke brugt): "Prøv AI-coachen i modul 3 først..."
- C3 M5: "Du skal gennemføre møde-simulatoren i modul 4 først"
- Alle andre: "Gennemfør det forrige modul først"

---

## 🤖 API Mønstre

### Modeller
- **claude-haiku-4-5-20251001** — Møde-simulator (hurtig, billig)
- **claude-sonnet-4-6** — C+ plan-generering (streaming)

### Streaming (bruges i kursus-cplus.html)
```javascript
async function streamAI(prompt, onChunk, maxTokens = 2000) {
  const res = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      model: 'claude-sonnet-4-6',
      max_tokens: maxTokens,
      stream: true,
      messages: [{ role: 'user', content: prompt }]
    })
  });
  // Læs SSE stream...
}
```

### JSON-parsing (robust)
```javascript
function extractJSON(raw) {
  let s = raw.replace(/```(?:json)?/gi, '').replace(/```/g, '').trim();
  const start = s.indexOf('{');
  const end   = s.lastIndexOf('}');
  s = s.slice(start, end + 1);
  try { return JSON.parse(s); } catch {}
  // Reparer afskåret JSON...
}
```

---

## 📋 Journey-bar (alle C-sider)
```html
C1: Prompt-teknik → Q1: Mini-quiz → C2: Emails → Q2: Mini-quiz → C3: Møder & indhold → E1: Eksamen del 1 → E2: Eksamen del 2 → 🏅: Bevis & coins
```
**CSS:** `justify-content: center; margin: 0 auto;` på `.journey-track`

---

## 🎬 Møde-Simulator Detaljer (C3 Modul 4)

**Karakterer:**
- Sara (Salgschef): Klar inden Q2, konkrete datoer
- Mikkel (IT-chef): API til HubSpot, ingen workarounds
- Lone (Økonomiansvarlig): Max 80.000 kr, ROI inden 18 mdr

**Scoring:** `simScores = {sara: 0-2, mikkel: 0-2, lone: 0-2}`  
**Intern state** sendes med i hver API-besked  
**parseMoodsRobust()** — 3 lag fallback  
**Hint-modal** vises automatisk efter forsøg 1 og 2  
**Løsningsforslag** vises efter 3. fejl + unlockM5()

---

## 💾 Prompt Bibliotek (localStorage)
```javascript
STORAGE_KEY     = 'learnai_prompt_library_v2'
STORAGE_KEY_CAT = 'learnai_prompt_categories_v1'
// Kategorier: C1, C2, C3, C+, Egne
// Hver prompt: { id, emoji, title, source, category, text }
```

---

## 🏅 Badges & Coins
| Begivenhed | Coins | Badge |
|-----------|-------|-------|
| Ny bruger | +50 | - |
| Quiz C1 bestået | +25 | - |
| Quiz C2 bestået | +25 | - |
| Kursus C eksamen bestået | +150 | Sølv C |
| Kursus D eksamen bestået | +100 | Bronze D |

---

## ⚠️ Kendte Issues / Huskeliste
1. **Firestore test-mode** udløber — skal strammes inden launch
2. **quiz-c1 og quiz-c2** — tjek at de giver coins i Firestore
3. **PDF-download af bevis** — ønsket feature, ikke bygget endnu
4. **platform.html** mangler C+ knap logik
5. Alle nye filer skal **uploades til GitHub** efter bygning
