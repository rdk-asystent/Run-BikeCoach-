# RUN/RIDE/COACH

Osobisty asystent treningowy Radka Kokoszki — osteopaty i biegacza.
Progressive Web App (PWA) działająca offline, bez backendu, bez instalacji.

---

## Co robi aplikacja

```
┌─────────────────────────────────────────────────────┐
│  RUN/RIDE/COACH                     [⚙] [+ Trening] │
│─────────────────────────────────────────────────────│
│  📊 Przegląd │ 📅 Plan │ 📈 Forma │ 🎯 │ 🏆 │ 💆   │
└─────────────────────────────────────────────────────┘

  📊 PRZEGLĄD     CTL/ATL/TSB · rekomendacja dziś · strefy HR
  📅 PLAN         20-tygodniowy plan bieg+rower+drążki · postęp sesji
  📈 FORMA        PMC Chart 90 dni · historia treningów
  🎯 PREDYKCJE    Riegel formula · prognozy 5K–maraton
  🏆 REKORDY      PR życiowe · historia drążków
  💆 MOBILNOŚĆ    28 ćwiczeń EBM · timer · 20-tyg. progresja
```

---

## Funkcje

### Główna aplikacja (PMC Coach)
- **Performance Management Chart** — CTL (forma 42d), ATL (zmęczenie 7d), TSB (świeżość)
- **Strefy tętna Karvonen** — auto-kalkulacja Z1–Z5 z RHR i maxHR
- **TSS** — Training Stress Score kalkulowany z HR lub RPE
- **Rekomendacja dzienna** — na podstawie TSB sugeruje typ treningu
- **Plan 20 tygodni** — Baza → Budowanie → Szczyt → Utrzymanie
- **Predykcje Riegel** — 5K, 10K, półmaraton, maraton
- **Eksport/Import** JSON i CSV

### Moduł Mobilność & Stabilizacja
- **28 ćwiczeń EBM** z bazą naukową (PubMed refs)
- **6 kategorii**: Rolling, Głęboka stabilizacja, L-Miedniczna, Biodro-Siła, Mobilność, Balans
- **Timer bilateral** — automatyczne przełączanie stron z beepem (Web Audio API)
- **20-tygodniowa progresja** (L1 tyg.1–6, L2 tyg.7–12, L3 tyg.13–20)
- **Sesja dzienna** — 9 ćwiczeń dopasowanych do fazy planu
- **Streak i statystyki** ukończonych sesji

---

## Stack techniczny

| Element | Technologia |
|---------|-------------|
| Frontend | Vanilla JS (ES2020) · zero frameworków |
| Persystencja | IndexedDB (`runcoach-v1`) — Safari-safe |
| Wykresy | Chart.js 4.4.0 CDN |
| Czcionki | Bebas Neue + JetBrains Mono (Google Fonts) |
| Audio | Web Audio API (timer beep) |
| PWA | manifest.json + Service Worker (offline) |
| Deploy | GitHub Pages (auto via Actions) |

---

## Dane użytkownika (seed)

| Parametr | Wartość |
|----------|---------|
| Max HR | 178 bpm |
| RHR | 61 bpm |
| LTHR | 162 bpm |
| Cel tygodniowy | 60 km/tydzień |
| Start planu | 2026-04-07 |
| Start mobilności | 2026-05-05 |

---

## Deployment

### GitHub Pages (automatyczny)
Każdy push na `main` uruchamia GitHub Actions → deploy.

**Wymagana jednorazowa konfiguracja:**
1. GitHub repo → Settings → Pages
2. Source: **GitHub Actions**
3. Gotowe — URL: `https://rdk-asystent.github.io/Run-BikeCoach-/`

### Netlify Drop (manualne)
Wgraj `index.html` na [app.netlify.com/drop](https://app.netlify.com/drop)

---

## Pliki

```
Run-BikeCoach-/
├── index.html          ← GŁÓWNY PLIK — cała aplikacja (1800+ linii)
├── mobility.html       ← Standalone moduł mobilności (do oddzielnego użycia)
├── manifest.json       ← PWA manifest (ikona, nazwa, tryb standalone)
├── sw.js               ← Service Worker (cache offline)
├── icons/
│   ├── icon-192.png    ← PWA icon (Android)
│   ├── icon-512.png    ← PWA icon (splash screen)
│   └── icon.svg        ← Źródłowy SVG
└── .github/
    └── workflows/
        └── deploy.yml  ← Auto-deploy na GitHub Pages
```

---

## Metodologia treningowa

- **Jack Daniels** — strefy E/T/I/R, tempo prace
- **TSS/PMC** — Performance Management Chart (TrainingPeaks model)
- **EBM** — ćwiczenia mobilności z referencjami PubMed
- **Karvonen** — strefy tętna z Heart Rate Reserve
- **Riegel** — predykcje czasów wyścigów (exponent 1.06)
