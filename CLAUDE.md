# Kontext projektu — landing page kurzu AI agentů (NextLevel Impact)

## Co to je
Samostatná landing page pro kurz **"Konfigurace a promptování AI agentů pro
zvýšení efektivity obchodních a týmových procesů"** — 6denní vzdělávací
program pro firmy (56 h, produkt Next.Level Academy). Provozovatel: NextLevel
Impact s.r.o. (Andrea Cigáníková & Martin Vopelka), hlavní web běží na
Miowebu (nadstavba WordPressu): https://nextlevelimpact.cz

Tahle stránka **záměrně neběží na Miowebu**. Hlavní web je uzavřený SaaS
balíček (Mioweb Lite) bez FTP/souborového přístupu — nejde tam nahrát vlastní
statický HTML, a vkládání přes jejich "HTML element" by způsobovalo konflikty
CSS/JS s jejich šablonou a stránku by nešlo editovat jejich drag&drop
editorem stejně jako zbytek webu. Proto stránka žije jako nezávislý statický
web a do hlavního webu je jen zavěšená přes subdoménu a položku v menu.

## Stav nasazení
- **Repo:** toto (`AndyCig/nextlevel-kurz-ai-agenti`), branch `main`
- **Hosting:** Cloudflare Pages, projekt `nextlevel-kurz-ai-agenti`
  (Connect to Git → tenhle repo, žádný build command, output directory = `/`)
- **Produkční URL Cloudflare:** `nextlevel-kurz-ai-agenti.pages.dev`
- **Custom doména:** `kurz.nextlevelimpact.cz` — nastavena jako CNAME
  (`kurz` → `nextlevel-kurz-ai-agenti.pages.dev`) přímo v DNS správě Miowebu
  (Moje domény → nextlevelimpact.cz → Editovat DNS → Uživatelské DNS).
  DNS pro `nextlevelimpact.cz` **zůstává ve správě Miowebu** — Cloudflare
  nemá (a nesmí mít) nad doménou plnou kontrolu (žádný transfer nameserverů).
- Jakýkoliv push do `main` se automaticky nasadí na Cloudflare Pages.
- **Menu na hlavním webu:** zatím NENÍ přidaný odkaz na `kurz.nextlevelimpact.cz`
  v Mioweb navigaci (Nastavení webu → Menu → Vlastní odkaz). Potřeba přidat
  ručně v Mioweb administraci — mimo dosah tohoto repozitáře.

## Struktura repa
- `index.html` — celá stránka, čisté HTML/CSS/JS v jednom souboru, žádný build
  krok, žádné závislosti/frameworky. Fonty přes Google Fonts CDN (Fraunces +
  IBM Plex Sans/Mono), žádné externí JS knihovny.
- `README.md` — stručný technický popis nasazení.

## Design systém (pro konzistenci při dalších úpravách)
- Barvy: `--ink #161A22`, `--paper #F6F3EC`, `--paper-raise #EFEAE0`,
  `--brass #9C7A2E` / `--brass-dim #C9A65C` (accent), `--slate #5B5F6B`,
  `--line #DAD3C2`, `--moss #4B5D45`
- Typografie: Fraunces (display/nadpisy), IBM Plex Sans (běžný text),
  IBM Plex Mono (eyebrow labely, čísla, technické prvky — odkazuje na
  "agent config" motiv obsahu)
- Signature prvek: konzole v hero sekci zobrazující princip
  CÍL→ROLE→KONTEXT→INSTRUKCE→ZNALOSTI→AKCE→KONTROLA (skutečný framework
  z obsahu kurzu, ne generický dekor)
- Vizuálně navazuje na nextlevelimpact.cz (stejná struktura hlavičky/patičky,
  ale samostatná barevná paleta — vlastní subdoména, vlastní design vrstva)

## Obsah stránky
Text vychází z dodaného podkladu `Na_vrh_obsahu_webu.docx` (obsahová
struktura, 5 modulů programu, FAQ, cílové skupiny, příklady agentů). Cílovka:
manažeři/HR/office manažeři hledající vzdělávání pro tým, s důrazem na soulad
s kritérii programu **Vzdělávání pro firmy** (up.gov.cz) a možností dotace.

## Otevřené TODO (označené přímo v index.html jako `TODO(claude-code)`)

1. **Kontaktní formulář (`#contact-form`) neodesílá data nikam.**
   Dřívější verze měla JS, který jen předstíral úspěch (`preventDefault` +
   zobrazení #thanks bez skutečného odeslání) — to bylo záměrně odstraněno,
   ať formulář nepůsobí funkčně, když funkční není.
   Doporučený postup: Formspree nebo Web3Forms (zdarma, bez vlastního
   backendu) — založit účet, vložit endpoint do `action=` u `<form>`, přidat
   `fetch()` volání s zobrazením `#thanks` až po skutečně úspěšné odpovědi.
   Alternativy k zvážení: Cloudflare Pages Function s emailovým API (např.
   Resend), nebo napojení na SmartEmailing (firma ho už používá pro
   e-mailing — viz DKIM/CNAME záznamy na doméně, mohlo by to rovnou plnit
   jejich kontaktní databázi).

2. **"Stáhnout podrobný harmonogram" (2× na stránce) vede na mailto
   placeholder**, protože žádný PDF harmonogram zatím neexistuje. Až bude
   hotový (obsahová struktura s hodinovou dotací modulů je v `index.html`
   sekci `#program`), nahradit oba výskyty odkazem na skutečný PDF soubor.

3. Až bude formulář funkční, ověřit že `#thanks` zpráva se zobrazuje jen po
   reálném úspěchu, ne při chybě odeslání (přidat i chybový stav).

## Co NEMĚNIT bez domluvy
- Neposouvat DNS/custom doménu na jinou hodnotu bez koordinace s tím, kdo má
  přístup do Mioweb DNS správy (majitel: Ondřej / NextLevel Impact) — CNAME
  je nastavený ručně mimo tento repozitář a build zde ho nijak needituje.
- Design tokeny (barvy/fonty) byly vědomě zvolené v kontrastu k obvyklým
  AI-generated defaultům — při úpravách zachovat konzistenci, ne sáhnout po
  genericích (cream+terakota, černá+neon apod.).
