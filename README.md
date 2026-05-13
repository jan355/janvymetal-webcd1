# Publikace webu janvymetal.cz

## Co je v této složce

```
publish/
├── index.html              ← hlavní soubor webu (přejmenováno z Muj-web-v6.html)
├── favicon-jv-sans.svg     ← favikona (zelený kruh s „JV")
├── og-image.png            ← náhledový obrázek pro sdílení (1200×630)
└── README.md               ← tento návod
```

Tyto tři soubory tvoří kompletní web. **Jsou statické** — žádný build, žádný server-side kód. Můžete je nahrát na jakýkoliv hosting.

---

## Co dořešit v Claude Code

Otevřete tuto složku v Claude Code a požádejte ho o tyto kroky. Můžete mu rovnou předat tento README jako kontext.

### 1. Funkční tlačítka a odkazy
V `index.html` jsou tyto interaktivní prvky, které dnes nikam nevedou nebo vedou jen na placeholder:

- **Tlačítko „Rezervovat hovor"** v hero a v sekci Kontakt
  → propojit s **Calendly / Cal.com / SimpleMeet** (nebo `mailto:` s předvyplněným předmětem)
- **Tlačítko „Prozkoumat služby"** — funguje (kotva `#sluzby`), ale ověřit
- **Kontaktní formulář** v sekci Kontakt
  → propojit s **Formspree / Web3Forms / Resend** nebo vlastním endpointem
- **E-mail a telefon** v sekci Kontakt
  → ověřit, že jsou správné a aktivní

### 2. Analytika
Doporučuji **Plausible** (GDPR-friendly, jednoduché). Vložit do `<head>`:
```html
<script defer data-domain="janvymetal.cz" src="https://plausible.io/js/script.js"></script>
```
Alternativně Google Analytics 4 (vyžaduje cookie lištu) nebo Umami (self-hosted).

### 3. Cookie lišta (jen pokud použijete GA)
Pokud Plausible → není potřeba. Pokud GA → použít např. **CookieConsent** (vanilla JS).

### 4. Doména a hosting

**Doporučené hostingy** (zdarma pro statický web):
- **Cloudflare Pages** ← doporučuji (rychlé, CDN, https zdarma, neomezený provoz)
- **Vercel** (snadný deploy z GitHubu)
- **Netlify** (podobné)
- Tradiční FTP hosting (Wedos, Forpsi, atd.) — funguje, ale méně pohodlné

**Postup pro Cloudflare Pages:**
1. Push složky do GitHub repa
2. V Cloudflare → Pages → Connect repo
3. Build settings: žádný build, output `/`
4. Custom domain → `janvymetal.cz` → nastavit DNS dle pokynů

### 5. Po nasazení otestovat sdílení
- LinkedIn: https://www.linkedin.com/post-inspector/
- Facebook: https://developers.facebook.com/tools/debug/
- Google Rich Results: https://search.google.com/test/rich-results

Tyto nástroje navíc obnoví cache, takže pokud OG obrázek upravíte, použijte je k vynucení refreshe.

### 6. Doplnit `robots.txt` a `sitemap.xml`
Drobnost, ale pomáhá SEO:

**robots.txt:**
```
User-agent: *
Allow: /
Sitemap: https://janvymetal.cz/sitemap.xml
```

**sitemap.xml:**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://janvymetal.cz/</loc>
    <lastmod>2026-05-10</lastmod>
    <priority>1.0</priority>
  </url>
</urlset>
```

---

## Technické poznámky k souboru `index.html`

- **Jeden HTML soubor** — všechny styly jsou inline v `<style>`, žádný externí CSS.
- **Loga referencí a fotka v sekci O mně** jsou vložené jako **base64 data URI**. To zvětšuje velikost souboru (~500 KB), ale eliminuje další HTTP requesty. Pokud chcete optimalizovat, lze loga extrahovat do `/img/` složky a referencovat klasicky.
- **Fonty** — Manrope se načítá z Google Fonts (`<link>` v head). Pokud chcete plnou nezávislost, lze fonty self-hostovat (stáhnout z google-webfonts-helper).
- **Scroll-spy navigace** — vanilla JS na konci souboru, žádné dependency.
- **Tweaks panel a improvements panel** (vpravo dole, žluté/tmavé tlačítko) — to jsou interní pomůcky z procesu návrhu. **Před publikací smazat** sekce `<button class="improvements-toggle">` a `<div id="improvements-panel">` a celý `<script>` na konci, který je obsluhuje. Hlavní stránka tím není ovlivněna.

---

## Co dál

Pokud byste cokoliv potřeboval doladit ještě tady (přidat sekci, změnit copy, optimalizovat výkon), dejte vědět.
