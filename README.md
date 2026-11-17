# GNT Parcel Tracking – bursdagspakke til Vishal

En statisk side (index.html + img/) som kan ligge rett på GitHub Pages. Den trenger ingen server.

## Legge den ut
1. Lag et nytt repo, for eksempel `gnt`.
2. Last opp `index.html` og hele `img/`-mappen til roten av repoet.
3. Gå til Settings → Pages → Source: «Deploy from a branch», velg `main` / `(root)` og trykk Save.
4. Etter et minutt eller to ligger siden på `https://<brukernavn>.github.io/gnt/`.

## Adressene
Alt styres med det som står etter `#` i adressen.

| Adresse | Hva den gjør |
|---|---|
| `…/gnt/` | Det Vishal ser: siden låser opp så langt han har kommet. Før første lenke står det bare «Something is coming». |
| `…/gnt/#demo` | Testmodus. Du klikker deg gjennom hele historien med Next/Back. Svar sendes ikke videre. |
| `…/gnt/#sender` | Konsollen din. Her ligger alle WhatsApp-meldingene ferdig utfylt med riktig lenke, med kopiknapp, og loggen over hva som er svart *i denne nettleseren*. |
| `…/gnt/#u-xxxx` | Lenkene til hver hendelse (se under). Når han åpner én, låses hendelsen og alle før den opp, og nettleseren hans husker det. |

## Lenkene, i rekkefølge
Du trenger ikke kopiere herfra. Konsollen (`#sender`) lager ferdige meldinger med riktig adresse.

| # | Hendelse | Slug |
|---|---|---|
| 1 | Sandefjord | #u-r4kw |
| 2 | Stavern | #u-b9tz |
| 3 | Bornholm | #u-m2qx |
| 4 | Reeperbahn | #u-h7vd |
| 5 | Thomas Henry | #u-z3lp |
| 6 | Frankfurt (kidnappet) | #u-c8ny |
| 7 | Frankfurt (quiz) | #u-w5fj |
| 8 | Block House, Bikini | #u-k1sg |
| 9 | IUBH Mitte | #u-p6ub |
| 10 | Späti-turné | #u-e2hm |
| 11 | Groß Glienicke | #u-y9ra |
| 12 | Westendallee (agent) | #u-n4dc |
| 13 | Levert | #u-x7qt |

Du styrer tempoet ved å sende meldingene når det passer deg. Tidspunktene i konsollen er bare forslag. Hopper han rett til en senere lenke, får han også med seg alt før den.

## Få svarene hans (valgfritt, men anbefalt)
Uten dette blir svarene hans liggende bare i hans egen nettleser. Med dette havner hvert svar, og hver gang han åpner en ny hendelse, som en rad i et Google-regneark.

1. Lag et nytt Google-regneark.
2. Gå til Utvidelser → Apps Script, slett det som står der, og lim inn:

```js
function doPost(e) {
  const d = JSON.parse(e.postData.contents);
  SpreadsheetApp.getActiveSpreadsheet().getActiveSheet()
    .appendRow([new Date(), d.game, d.value]);
  return ContentService.createTextOutput('ok');
}
```

3. Trykk Implementer → Ny implementering → type «Nettapp». Velg Utfør som: «Meg», og Hvem har tilgang: «Alle». Godkjenn tilgangen.
4. Kopier nettapp-adressen (den slutter på `/exec`) og lim den inn i `index.html`:
   `const LOG_URL = 'https://script.google.com/macros/s/…/exec';`
5. Test: åpne siden med en hendelseslenke og svar på noe. Da skal det dukke opp en rad i arket.

Raden «opened» betyr at han har åpnet en hendelse. De andre radene er svarene hans: `witness`, `plates`, `wanted` (beskrivelsen av Noah), `quiz`, `pitch`, `bingo`, `found` (hva han fant i postkassa) og `code`.

## Ting du kan endre øverst i koden
- `CARD`: teksten på postkortet han får til slutt.
- `CODE_WORDS`: ord som låser opp gaven. Det holder at svaret hans inneholder ett av dem.
- `MODE`: `'links'` (standard) eller `'clock'`, der hendelsene låses opp etter tidspunktene i `E`.
- `E`: alle hendelsene, med tekst, bilder og WhatsApp-meldinger.

## Før du sender første lenke
- Åpne `…/gnt/#demo` på mobilen og klikk deg gjennom én gang.
- Husk at kona hans skal legge pakken i postkassa søndag 22. november før du sender lenke 13.
