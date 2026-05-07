# Performance 007 — nastavenie admin dashboardu

Tento návod ti spustí dashboard na adrese `https://performance007.sk/admin`.
Po nastavení sa prihlásiš cez svoj GitHub účet a môžeš pridávať/editovať vozidlá a obrázky cez pekné formuláre.

**Setup je raz — potom už len používaš.** Trvá ~10 minút.

---

## Krok 1 — Nahraj nové súbory do GitHubu

V tvojom repe `Performance007` musíš mať tieto **nové** súbory (vedľa `index.html`):

```
Performance007/
├── index.html              ← UPDATED (nahraď za novú verziu)
├── vehicles.json           ← NEW (zoznam vozidiel)
├── admin/
│   ├── index.html          ← NEW
│   └── config.yml          ← NEW
├── (obrázky .webp...)
```

Nahraj ich pretiahnutím cez **Add file → Upload files** v GitHube.

✅ **Po nahratí počkaj, kým Netlify dobehne deploy** (~30s). Skontroluj v Deploys, že je "Published" zelené.

---

## Krok 2 — Vytvor GitHub OAuth aplikáciu

Decap CMS sa potrebuje cez GitHub prihlasovať, aby vedel commitovať zmeny do tvojho repa.

1. Otvor: <https://github.com/settings/developers>
2. Vľavo klikni **OAuth Apps** → vpravo hore **New OAuth App**.
3. Vyplň:
   - **Application name:** `Performance007 CMS`
   - **Homepage URL:** `https://performance007.sk`
   - **Authorization callback URL:** `https://api.netlify.com/auth/done`
4. **Register application**.
5. Na ďalšej stránke uvidíš **Client ID** — skopíruj si ho.
6. Klikni **Generate a new client secret** → uvidíš **Client Secret** — skopíruj si ho **hneď**, GitHub ho už neukáže (uloží sa len hash).

Nechaj túto stránku otvorenú, hodnoty potrebuješ v ďalšom kroku.

---

## Krok 3 — Vlož credentials do Netlify

1. Otvor Netlify dashboard tvojho projektu: <https://app.netlify.com/projects/willowy-syrniki-5dbd54>
2. Vľavo: **Project configuration**.
3. Hľadaj sekciu **Access & security** → **OAuth** (alebo **Identity → OAuth providers**, podľa verzie UI).
4. Klikni **Install provider** alebo **Connect with GitHub**.
5. Vyber **GitHub**.
6. Vlož:
   - **Client ID** (z GitHubu, krok 2.5)
   - **Client Secret** (z GitHubu, krok 2.6)
7. Save / Install.

> Ak túto sekciu v Netlify UI nenájdeš, hľadaj cez vyhľadávanie „OAuth" alebo otvor priamo:
> `https://app.netlify.com/teams/<tvoj-team>/oauth-apps`

---

## Krok 4 — Otestuj prístup

1. Otvor: <https://performance007.sk/admin>
2. Mal by si vidieť obrazovku s **„Login with GitHub"**.
3. Klikni → autorizuj prístup k repu.
4. Po prihlásení uvidíš dashboard s kolekciou **Vozidlá**.

Klikni **Vozidlá → Zoznam vozidiel** → uvidíš svoje 4 autá. Skús kliknúť na jedno → otvorí sa formulár.

Skús pridať testovacie vozidlo → klikni **Publish** → uvidíš správu, že zmena je commitnutá.

Otvor `https://performance007.sk` v inkognite za ~30 sekúnd → nové vozidlo by sa malo zobraziť na webe.

---

## Ako to používať odteraz

### Pridať vozidlo
1. `performance007.sk/admin` → Login with GitHub.
2. **Vozidlá → Zoznam vozidiel**.
3. Vpravo dole tlačidlo **+ Add Vozidlo**.
4. Vyplň formulár, nahraj fotku (drag&drop) → **Publish**.
5. Za 30s je vozidlo na webe.

### Vymeniť pozadie sekcie (hero, garáž...)
1. V administrácii vľavo dole **Media**.
2. Vyhľadaj `hero.webp` (alebo `garaz.webp`...) → klik → **Replace**.
3. Nahraj nový obrázok s **rovnakým názvom**.
4. Publish.

### Vymeniť fotku vozidla
1. **Vozidlá → Zoznam vozidiel** → klik na vozidlo.
2. Pri poli **Fotka vozidla** → klik **Choose an image** → upload nový.
3. Publish.

---

## Riešenie problémov

**„Authentication aborted" pri prihlásení**
→ Nesprávny callback URL v GitHub OAuth App. Musí byť presne `https://api.netlify.com/auth/done`.

**Login OK, ale neuvidím vozidlá**
→ V `admin/config.yml` je nesprávny názov repa. Otvor `admin/config.yml` a v riadku `repo:` daj presný názov tvojho GitHub repa (formát `meno/repo`).

**„Permission denied" pri pokuse uložiť**
→ Tvoj GitHub účet nemá write prístup do toho repa. (Pri vlastnom repe by toto nemal byť problém.)

**Decap CMS hodí biely screen**
→ Otvor DevTools (Cmd+Option+I) → Console → pošli screenshot chyby.

---

## Bezpečnosť

- **Client Secret** nikam nedávaj (do verejného repa, do Slacku, atď.). Je uložený len v Netlify a v `github.com/settings/developers`.
- Ak by ti niekto cudzí získal access k tvojmu GitHub účtu, vie editovať web. **Zapni si 2FA na GitHube.**
- Decap CMS commituje zmeny pod tvojím GitHub menom — všetka história zmien je v Git, takže vždy vidíš, čo sa kedy zmenilo a vieš to vrátiť späť (rollback cez `git revert`).
