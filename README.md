# Web www.janvymetal.cz

Jednostránkový statický web, bez buildu. Vše je v `index.html` (styly i skripty uvnitř), obrázky v `img/`, písmo Manrope v `fonts/`.

## Jak se web publikuje

- Repozitář: `jan355/janvymetal-webcd1`, větev `main`.
- Hosting: Cloudflare Pages. **Každý push do `main` se během minuty objeví naživo.** Větve mimo `main` dostanou náhledovou adresu `<větev>.janvymetal-webcd1.pages.dev`.
- DNS domény je u websupport.sk: `www` míří CNAME záznamem na `janvymetal-webcd1.pages.dev`.
- Pracovní postup: úpravy ve větvi → náhled → kontrola → sloučení do `main`.

## Co kde je

| Soubor / složka | K čemu |
|---|---|
| `index.html` | celý web: hlavička, styly, obsah, skripty |
| `img/` | loga referencí (PNG, výška do 120 px) a fotka lektora (`jan-vymetal.webp`) |
| `fonts/` | Manrope (variabilní, latin + latin-ext), načítá se z vlastní domény |
| `og-image.png` | náhled pro sdílení (1200×630) |
| `favicon-*.png`, `apple-touch-icon.png`, `favicon-jv-sans.svg` | ikony |
| `_headers` | hlavičky pro Cloudflare Pages (HSTS, cache obrázků a písma) |
| `robots.txt`, `sitemap.xml` | pro vyhledávače; při větší změně obsahu aktualizovat `lastmod` |

## Pravidla

- Do repozitáře nikdy nepatří pracovní listy, podklady klientů ani zálohy (`.gitignore` je hlídá). Repozitář je veřejný.
- Nové logo reference: PNG s průhledným pozadím do `img/`, výška do 120 px, do `index.html` přidat `<div class="logo-item">` s `width`/`height`.
- Adresa webu se všude píše s `www` (canonical, og:url, sitemap).
- V textech žádné dlouhé pomlčky „—“; místo nich dvojtečka, čárka nebo tečka.
- Odkaz „Poptat kurz“ je `mailto:` s předvyplněným předmětem a tělem; při změně textu použít URL kódování (např. `urllib.parse.quote` v Pythonu).
