# Kurz: Konfigurace a promptování AI agentů

Statická landing page pro NextLevel Impact — samostatně hostovaná mimo Mioweb,
propojená s hlavním webem přes subdoménu `kurz.nextlevelimpact.cz`.

## Struktura
- `index.html` — celá stránka (HTML/CSS/JS v jednom souboru, bez buildu)

## Nasazení
Repo je připojené na Cloudflare Pages (Connect to Git).
Build command: žádný. Build output directory: kořen repa (`/`).
Každý push do produkční větve se automaticky nasadí.

## Custom doména
`kurz.nextlevelimpact.cz` → CNAME na `<projekt>.pages.dev`,
záznam nastavený v DNS správě Miowebu (Nastavení webu → Změnit DNS).
