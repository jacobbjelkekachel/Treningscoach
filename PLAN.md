# Treningscoach App PLAN.md

## Oversikt
En personlig AI-drevet treningscoach som lever som en bookmark på mobilen.
Brukeren logger dagens økt og dagsform, og får tilbake en justert treningsplan
basert på Ingebrigtsen-familiens terskeltrening-filosofi.

---

## Utøverprofil (hardkodet i system prompt)

### Personalia
- **Navn:** Jacob
- **Nivå:** Avansert, 70+ km/uke løping + høy tverrfaglig belastning
- **Treningsdager:** 6 dager per uke
- **Aktiviteter:** Løping (primær), styrke, sykling, svømming, langrenn (vinter)

### Personlige rekorder
| Distanse | Tid | Pace |
|---|---|---|
| 3 000 m | 10:02 | 3:21/km |
| 10 000 m | 35:43 (Drammen 11.04.2026) | 3:34/km |
| Halvmaraton | 1:21:41 (Oslo Halvmaraton 2025) | 3:52/km |
| Benkpress | 115 kg | — |

### Terskelreferanser (beregnet fra PB-er)
- **Terskelltempo (laktatterskel):** 3:50–4:00/km
- **Rolige dager (under 75% maks):** 4:45–5:30/km
- **Intervallltempo (VO2max):** 3:30–3:45/km
- **Maks sprint:** ned mot 3:15–3:20/km

### Nåværende mål
- **Kortsiktig:** Oslo Sentrumsløpet 10 km — 25. april 2026 — mål: **under 35:00**
- **Langsiktig:** Bygge form mot 5K under 17:00 og 10K under 34:30
- **Styrke:** 5x5 benkpress på 100 kg (nåværende: 4x4 på 90 kg)

### Treningshverdag (typisk uke)
- **Mandag:** Løpe til/fra jobb 8+8 km med 8–10 kg sekk
- **Tirsdag:** Styrke overkropp morgen + sykling til/fra jobb 8+8 km
- **Onsdag:** Sykling til/fra jobb + eventuell intervalløkt
- **Torsdag:** Løpe til/fra jobb med sekk
- **Fredag:** Styrke overkropp morgen + sykling til/fra jobb
- **Lørdag:** Nøkkeløkt (intervaller eller terskel)
- **Søndag:** Langtur eller aktiv restitusjon

### Utøverpersonlighet (viktig for coachen å kjenne til)
- Høy konkurranseinstinkt — tenderer til å pushe hardere enn planen i trening
- Tåler uvanlig høy belastning og restituerer godt
- Blander mange treningsformer som fungerer synergistisk
- Kommuniserer åpent om dagsform, alkohol, stress og søvn
- Liker konkrete planer med spesifikke pace- og pulstall — ikke vage anbefalinger

---

## Treningsfilosofi — Ingebrigtsen Terskeltrening

### Kjerneprinsippene
1. **Aerob base er alt** — 80–85% av all løping skal være rolig, under terskel
2. **To terskeløkter per uke** — ikke flere, ikke færre (for løping)
3. **Dobbel terskel (valgfritt)** — to terskeløkter samme dag kun ved meget god form
4. **Rolige dager skal være genuint rolige** — puls under 75% av maks, ikke halvharde
5. **Progresjon styres av dagsform** — ikke av rigid ukesplan
6. **Terskel = laktatterskel** — ca. 3–4 mmol/L, 3:50–4:00/km for Jacob
7. **Aldri to harde dager på rad**
8. **Ved RPE 8+ eller utmattelse** — automatisk reduser neste dag

### Terskeløkt-typer coachen kan foreslå
- **Kontinuerlig terskel:** 20–40 min sammenhengende i terskelltempo
- **Terskelintervaller:** 4–8 x 4–6 min med 60–90 sek pause
- **Progresjonsløp:** Starter rolig, siste 20–30 min i terskelsjiktet
- **Dobbel terskel-dag:** Lett terskel morgen + terskelintervaller ettermiddag (kun ved god form)
- **Lange intervaller:** 3–5 x 2000 m ved 3:40–3:50/km (VO2max grense)
- **Korte intervaller:** 6–10 x 1000 m ved 3:25–3:35/km

### Styrkefilosofi
- Overkropp 2x per uke (tirsdag + fredag)
- Fokus på benkpress progresjon mot 5x5 på 100 kg
- Nåværende nivå: 4x4 på 90 kg
- Styrke skal ikke forstyrre løpeøkter — alltid morgen eller etter rolig dag

---

## App-funksjoner

### 1. Daglig loggføring
Bruker logger etter hver økt:
- **Aktivitetstype:** Løping / Styrke / Sykling / Svømming / Langrenn / Hvile / Annet
- **Varighet** (minutter)
- **Distanse i km** (valgfritt)
- **Gjennomsnittspuls** (valgfritt)
- **Økttype:** Rolig / Terskel / Intervall / Styrke / Restitusjon / Konkurranse
- **RPE (1–10)**
- **Fri tekst:** Dagsform, søvn, stress, bein, motivasjon, alkohol osv.

### 2. AI-coaching
- Sender hele treningsloggen (alle entries) til Claude API
- Claude analyserer belastning, mønster og dagsform
- Returnerer:
  - Kommentar på dagens økt (2–3 setninger)
  - Konkret plan for neste 3–5 dager med økttype, pace og puls
  - Advarsel ved overtreningssignaler
  - Ukentlig sammendrag

### 3. Treningsplan-visning
- Viser gjeldende uke med planlagte økter
- Markerer terskeløkter og nøkkeløkter tydelig
- Oppdateres automatisk etter hver AI-respons

### 4. Historikk
- Enkel liste over tidligere økter
- Kan bla tilbake og se hva coachen anbefalte

---

## Teknisk stack

| Komponent | Valg | Begrunnelse |
|---|---|---|
| Frontend | Én `index.html` fil | Enkel bookmark på mobil, ingen deploy-kompleksitet |
| Styling | CSS i samme fil | Mobil-first, mørkt tema |
| Logikk | Vanilla JavaScript | Ingen build-steg, lett å vedlikeholde |
| Datalagring | `localStorage` | Ingen backend nødvendig |
| AI | Claude API (claude-sonnet-4-20250514) | Beste modell for coaching-resonnering |
| Hosting | GitHub Pages | Gratis, kobler til eksisterende repo |

---

## Datamodell

### Loggentry (lagres i localStorage)
```json
{
  "id": "2026-04-15-1",
  "date": "2026-04-15",
  "timestamp": 1744900000,
  "activityType": "running",
  "durationMinutes": 75,
  "distanceKm": 14.5,
  "avgHeartRate": 142,
  "sessionType": "easy",
  "rpe": 4,
  "notes": "Gode bein, litt trøtt. Sov 7 timer."
}
```

### Treningsplan (lagres i localStorage)
```json
{
  "updatedAt": "2026-04-15",
  "coachComment": "...",
  "weekPlan": [
    {
      "date": "2026-04-16",
      "sessionType": "threshold",
      "description": "4 x 6 min terskelintervaller, 90 sek pause",
      "targetPace": "3:52–3:58/km",
      "targetHR": "168–174"
    }
  ]
}
```

---

## System Prompt (til Claude API)

```
Du er en erfaren løpetrener med 20+ års erfaring fra toppidrett og mosjonister.
Du er spesialist i Ingebrigtsen-familiens terskeltrening-metodikk og norsk
utholdenhetstrening generelt. Du er direkte, konkret og bruker alltid eksakte
puls- og pace-tall i anbefalingene dine.

UTØVERPROFIL — JACOB:
- Avansert løper, 70+ km/uke løping + høy tverrfaglig belastning (sykling, styrke, langrenn)
- PB: 3000m 10:02 | 10K 35:43 | Halvmaraton 1:21:41
- Terskelltempo: 3:50–4:00/km
- Rolige dager: 4:45–5:30/km
- Intervallltempo (VO2max): 3:30–3:45/km
- Trener 6 dager/uke: løping til/fra jobb med sekk, styrke 2x/uke, sykling
- Høy konkurranseinstinkt — tenderer til å pushe hardere enn planlagt i trening
- Kommuniserer åpent om søvn, alkohol, stress og dagsform
- Nåværende mål: Oslo Sentrumsløpet 10K 25. april — sub 35:00
- Styrke: bygger mot 5x5 benkpress på 100 kg (nåværende: 4x4 på 90 kg)

TRENINGSFILOSOFI DU ALLTID FØLGER:
1. 80–85% av løpevolumet skal være rolig aerob trening (under terskel)
2. Maks 2 intensive/terskelbaserte løpeøkter per uke
3. Rolige dager skal være genuint rolige — ikke halvharde
4. Terskel = laktatterskel (~3–4 mmol), 3:50–4:00/km for Jacob
5. Progresjon og justering styres alltid av Jacobs subjektive dagsform og RPE
6. Aldri to harde dager på rad
7. Ved RPE 8+ eller tegn på utmattelse: reduser neste dag automatisk
8. Styrke skal ikke kollidere med nøkkeløkter i løping

VIKTIG OM JACOB SOM UTØVER:
- Han har nettopp løpt 35:43 på 10K (11. april 2026) etter en tøff påske med mye langrenn og fyll
- Dette tyder på at han er i eksepsjonell form — sub 35 på sentrumsløpet er realistisk
- Han tenderer til å pushe for hardt i intervaller — minn ham på å holde igjen
- Løping til/fra jobb med sekk teller som lett belastning, ikke hvile

OPPGAVE:
Du mottar en logg over de siste ukene med økter, RPE og notater.
Du skal:
1. Kommentere dagens økt kort (2–3 setninger) — vær ærlig, ikke bare positiv
2. Gi en konkret plan for de neste 3–5 dagene med økttype, varighet, pace og puls
3. Flagge eventuelle advarsler (overtrening, for lite restitusjon, for mye intensitet)
4. Holde deg til terskeltrening-prinsippene uansett hva Jacob ber om

Svar alltid på norsk. Vær direkte som en ekte trener — ikke vag eller overdrevent oppmuntrende.
Bruk alltid konkrete pace-tall og pulssoner i planen.
Hvis Jacob har trent for hardt, si det tydelig.
```

---

## Filstruktur i repo

```
treningscoach/
├── index.html        # Hele appen i én fil
├── PLAN.md           # Denne filen
└── README.md         # Kort beskrivelse
```

---

## Lørdag — byggeplan

| Tid | Oppgave |
|---|---|
| 09:00–09:30 | Sett opp repo, GitHub Pages, åpne Claude Code |
| 09:30–11:00 | HTML-struktur + CSS (mobil-first, mørkt tema) |
| 11:00–12:30 | Loggføring-skjema + localStorage lagring/lesing |
| 13:00–14:30 | Claude API-integrasjon + system prompt |
| 14:30–15:30 | Treningsplan-visning + historikk-liste |
| 15:30–16:30 | Test på mobil, deploy til GitHub Pages |
| 16:30–17:00 | Legg til som bookmark på telefonen, test med ekte økt |

---

## Første instruksjon til Claude Code (lørdag morgen)

Lim inn dette når du starter Claude Code:

```
Les PLAN.md grundig før du skriver en eneste linje kode.

Bygg index.html — én enkelt fil med HTML, CSS og JavaScript.
Mobil-first design med mørkt tema. Ingen rammeverk, ingen build-steg.

Start med følgende i denne rekkefølgen:
1. HTML-struktur med to views: "Logg økt" og "Min plan"
2. Loggføringsskjema med alle feltene beskrevet i PLAN.md
3. Lagring og lesing fra localStorage
4. Enkel historikk-liste

Ikke bygg Claude API-integrasjonen ennå — det tar vi som steg 2.
Spør meg før du tar arkitekturvalg som ikke er beskrevet i PLAN.md.
```
