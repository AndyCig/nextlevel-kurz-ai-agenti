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
  krok, žádné závislosti/frameworky. Písmo: systémová **Georgia** (texty) +
  **Roboto** z Google Fonts (tlačítka). Žádné externí JS knihovny.
- Obrázky v kořeni (servíruje je Cloudflare Pages přímo):
  - `banner.jpg` — hero banner nahoře (Next.Level Akademie, portréty
    Andrea + Martin, titulek kurzu, crimson podtržení)
  - `logo-nextlevel.jpg` — logo v hlavičce (ořezaná bílá plocha z
    „Logo Nextlevel.jpeg"); proklik vede na `https://nextlevelimpact.cz/`
  - `Logo-213x213.jpg` — favicon
  - `Logo Nextlevel.jpeg` — původní (neořezaný) zdroj loga, ponechán
- `README.md` — stručný technický popis nasazení.

## Design systém (pro konzistenci při dalších úpravách)
Paleta i písmo jsou **záměrně sladěné s domovským webem `nextlevelimpact.cz`**
(dřívější kontrastní „editorial" paleta byla nahrazena na přání majitele).
- Barvy: `--paper #FFFFFF`, `--paper-raise #FAFAFA`, akcent
  `--brass #AC1C3A` (crimson) / `--brass-dim #CB4A62`, text `--ink #1B1B1B`,
  `--slate #6A6A6A`, `--line #EAEAEA`. (Pozn.: proměnné si drží historické
  názvy `--brass`/`--moss`, ale hodnoty jsou crimson — nezaměňovat za zlatou.)
- Typografie: **Georgia** na nadpisy i běžný text (domovský web používá
  Georgii, barvu textů kolem `#3D3D3D`), **Roboto** na tlačítka.
- Hero: nahoře full-width `banner.jpg`, pod ním text na celou šířku.
  (Dřívější „konzole" CÍL→ROLE→…→KONTROLA byla odstraněna dle podkladu —
  titulek je teď součástí banneru, v HTML zůstává skrytě jako `<h1>` kvůli SEO.)
- Hlavička: logo vlevo (proklik na hlavní web), vpravo navigace napojená na
  reálné podstránky `nextlevelimpact.cz`.

## Obsah stránky
Text vychází z dodaného podkladu `Na_vrh_obsahu_webu.docx` (obsahová
struktura, 5 modulů programu, FAQ, cílové skupiny, příklady agentů). Cílovka:
manažeři/HR/office manažeři hledající vzdělávání pro tým, s důrazem na soulad
s kritérii programu **Vzdělávání pro firmy** (up.gov.cz) a možností dotace.

Úpravy dle podkladu `zmeny_na_strance.pptx`:
- Karta agenta „Funnel Guardian" → **„Osobní Kouč"** (tag „Osobní rozvoj")
  s novým popisem.
- Sekce „Pro koho je program určený" zúžena na 2 skupiny (Obchodníci,
  Manažeři/team leadeři).
- Kontaktní e-mail: `info@nextlevelimpact.cz` (dřív chybně `.eu`).
- Hlavní kontaktní CTA „Kontaktujte nás" → `https://nextlevelimpact.cz/akad-info/`.

## Hotová TODO (historie)
Původní `TODO(claude-code)` z `index.html` jsou vyřešená:
1. Nefunkční kontaktní formulář **odstraněn**; místo něj reálný kontakt
   (mailto/tel) a CTA na `nextlevelimpact.cz/akad-info/`.
2. Tlačítka „Stáhnout podrobný harmonogram" **odstraněna** (PDF neexistovalo).
3. Všechny slepé odkazy (`href="#"`) vyřešeny — menu i patička vedou na
   reálné podstránky `nextlevelimpact.cz`.

## Známé k dořešení / rozpracované
- **Kontinuita hlavičky s Miowebem:** hlavní web má vyšší hlavičku (~202 px)
  s vlastním menu (Next.Level Academy · Vyjednávání · Rodinné firmy · Rodinná
  kontinuita · **Ženám** · O nás · LinkedIn · EN) a „pill" zvýrazněním aktivní
  položky. Tahle stránka má vlastní, nižší hlavičku → přechod působí
  nekonzistentně. Zvolený směr: **replikovat Mioweb hlavičku** na téhle
  stránce (ne embedovat živé menu — to by znamenalo návrat do Miowebu se všemi
  jeho omezeními, viz „Co to je"). K dořešení: přesný vzhled/chování hlavičky
  + URL položek Ženám / LinkedIn / EN.
- **Menu na hlavním webu:** odkaz na `kurz.nextlevelimpact.cz` stále chybí
  v Mioweb navigaci (přidat ručně, mimo tenhle repozitář).
- (Volitelně) PDF harmonogram — kdyby vznikl, lze přidat ke stažení.

## Co NEMĚNIT bez domluvy
- Neposouvat DNS/custom doménu na jinou hodnotu bez koordinace s tím, kdo má
  přístup do Mioweb DNS správy (majitel: Ondřej / NextLevel Impact) — CNAME
  je nastavený ručně mimo tento repozitář a build zde ho nijak needituje.
- **Paleta a písmo jsou teď záměrně sladěné s domovským webem**
  (bílá `#FFFFFF` / `#FAFAFA` + crimson `#AC1C3A`, Georgia + Roboto). Při
  úpravách držet konzistenci s `nextlevelimpact.cz`, nesahat po genericích.
