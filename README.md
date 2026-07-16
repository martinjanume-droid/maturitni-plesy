# MB servis production — jednostránkový web (maturitní ples)

Jednostránkový web pro **MB servis production** — kapela, sál i technika na maturitní ples
a firemní akce. Obsluhuje čtyři reklamní záměry (maturitní ples / kapela / sál / ozvučení)
na jedné stránce s kotvami `#kapela`, `#sal`, `#ozvuceni`.

## Spuštění

Stránka je čisté HTML/CSS/JS, **bez build kroku**. Stačí soubory servírovat přes
statický webserver (kvůli načítání `support.js`, `_ds/` a modulů typu `ogl`):

```bash
# jakýkoli statický server, např.:
npx serve .
# nebo
python3 -m http.server 8000
```

Pak otevřít `http://localhost:8000/` (načte `index.html`, který zobrazí hlavní stránku).

> Přímé otevření `index.html` přes `file://` nemusí fungovat kvůli CORS u modulů —
> použij lokální server (viz výše) nebo nasazení na hosting.

## Struktura

```
.
├── index.html              # vstupní bod (načte hlavní stránku ve full-window iframe)
├── Maturitni ples.dc.html  # hlavní stránka (Design Component: šablona + logika)
├── support.js              # runtime pro .dc.html (needitovat)
├── assets/
│   └── logo-white.svg      # logo MB servis production (bílé)
├── _ds/                    # design systém (tokeny, styly, komponenty)
└── screenshots/            # náhledy (lze smazat / negitovat)
```

## Nasazení

Funguje na jakémkoli statickém hostingu:

- **GitHub Pages** — Settings → Pages → Deploy from branch (`main` / root).
- **Netlify / Vercel / Cloudflare Pages** — žádný build command, publish directory `/`.

## Co upravit

- **Kontakt / telefon / e-mail** — v `Maturitni ples.dc.html` (sekce `#poptavka` a patička).
- **Kapely, moderátoři, DJs, ceník, reference, galerie** — v logice komponenty
  (`renderVals()` → pole `bands`, `moderators`, `djs`, `plans`, `reviews`, `gallery`).
- **Fotky** — nyní placeholdery z Unsplash; nahraď vlastními (URL nebo do `assets/`).
- **Odkazy na ukázky** — `href: "#"` u kapel/DJs doplň skutečnými odkazy.

## Externí závislosti (z CDN, načítané za běhu)

- Google Fonts: Space Grotesk, Inter, Space Mono, Instrument Serif
- `ogl` (WebGL) pro kruhovou galerii — `https://esm.sh/ogl`
