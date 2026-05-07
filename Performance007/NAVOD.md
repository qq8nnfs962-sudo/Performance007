# Performance 007 – návod na úpravu

Stránka je v jedinom súbore: **`index.html`**.
Otvor ho dvojklikom v prehliadači (Chrome / Edge / Firefox / Safari) — funguje aj bez internetu/servera.

Editovať môžeš v: **VS Code, Notepad++, TextEdit, Sublime Text** alebo akomkoľvek textovom editore.

---

## 1) Ako pridať / upraviť / vymazať vozidlo

Otvor `index.html`, nájdi blok začínajúci komentárom `ZOZNAM VOZIDIEL` (asi okolo riadku 700).
Každé vozidlo je jeden objekt v zátvorkách `{ … }`. Stačí kopírovať existujúci a upraviť hodnoty:

```js
{
  id: "p007-vlastne-id",        // jednoznačný kód, bez medzier
  year: 2024,                    // rok výroby
  make: "Porsche",               // značka
  model: "Cayman GT4 RS",        // model
  price: 199000,                 // cena v EUR (číslo, bez medzier)
  hp: 500,                       // výkon v HP
  drivetrain: "RWD",             // RWD / AWD / 4MATIC / xDrive / FWD
  zeroToHundred: 3.4,            // 0–100 km/h v sekundách
  mileage: 8500,                 // nájazd v km
  image: "images/auto5.webp",    // cesta k fotke v priečinku /images
  tags: ["PCCB", "Sport Chrono"],// krátke štítky (pole)
  dossier: "Krátky popis vozidla."
},
```

- **Pridať vozidlo:** skopíruj jeden blok `{ … },` a uprav hodnoty.
- **Vymazať vozidlo:** zmaž celý blok od `{` po `},`.
- **Zmeniť poradie:** poprehadzuj bloky.

---

## 2) Ako vymeniť fotky

Všetky obrázky sú v priečinku `images/`.

**Pozadia sekcií** (hero, garáž, financie atď.) – súbory:
- `hero.webp`        – hlavný obrázok hore
- `objednavka.webp`  – sekcia „Vozidlá na objednávku“
- `dossier.webp`     – sekcia „Technická zložka“
- `garaz.webp`       – sekcia „Garáž“
- `finance.webp`     – sekcia „Financovanie“

Stačí prepísať/nahradiť rovnako pomenovaný súbor a stránka si ho automaticky natiahne.

**Fotky vozidiel** – `auto1.webp`, `auto2.webp`, `auto3.webp`, `auto4.webp`.
Ak pridáš nové auto, vlož fotku do `images/` (napr. `auto5.webp`) a v `index.html` v poli `image` nastav cestu `images/auto5.webp`.

**Tip:** Ak používaš `.jpg` namiesto `.webp`, jednoducho zmeň príponu v poli `image:`. Ak je obrázok napr. `images/porsche.jpg`, napíš `image: "images/porsche.jpg"`.

---

## 3) Ako zmeniť email pre kontaktný formulár

Otvor `index.html` a hneď na začiatku `<script>` bloku (asi riadok ~690) nájdeš:

```js
const KONTAKT_EMAIL = "info@performance007.sk";
```

Zmeň na svoj email. Po odoslaní formulára sa zákazníkovi otvorí poštový klient (Outlook/Gmail) s pripravenou správou na túto adresu.

---

## 4) Ako zmeniť telefón / adresu / texty

Telefón a adresa sú priamo v HTML (Ctrl+F a vyhľadaj):

- `+421 905 143 257`  – telefón v sekcii Kontakt
- `Hýľov`             – mesto
- `Košice - okolie`   – región

Všetky texty (nadpisy, popisy) sú medzi tagmi v HTML, napr. `<h2>VOZIDLÁ NA OBJEDNÁVKU</h2>` – stačí prepísať text medzi tagmi.

---

## 5) Ako stránku zverejniť na internete (zdarma)

Najjednoduchšie možnosti — všetky **zadarmo**:

1. **Netlify Drop** – https://app.netlify.com/drop
   Pretiahneš tam celý priečinok `Performance007` a o pár sekúnd dostaneš verejný odkaz.

2. **Cloudflare Pages** – https://pages.cloudflare.com
   Zaregistruj sa zdarma, nahodíš priečinok, dostaneš odkaz.

3. **GitHub Pages** – ak používaš GitHub, zapni Pages v nastaveniach repozitára.

4. **Vercel** – https://vercel.com – tiež zdarma pre statické stránky.

Žiadny server / databáza / mesačný poplatok nie sú potrebné.

---

## 6) Ako pripojiť vlastnú doménu (napr. performance007.sk)

Po zverejnení na Netlify/Cloudflare/Vercel (krok 5) tam pridáš svoju doménu a nastavíš DNS záznamy podľa návodu danej služby. Trvá to ~10 minút.

---

## Štruktúra priečinka

```
Performance007/
├── index.html        ← celá stránka v jednom súbore
├── NAVOD.md          ← tento súbor
└── images/
    ├── hero.webp
    ├── objednavka.webp
    ├── dossier.webp
    ├── garaz.webp
    ├── finance.webp
    ├── auto1.webp
    ├── auto2.webp
    ├── auto3.webp
    └── auto4.webp
```

Hotovo. Stránka je tvoja, žiadny MANUS, žiadne kredity. 🏁
