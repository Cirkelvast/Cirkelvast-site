# Cirkelvast Website — Deployment Handleiding

## Wat je hebt
Een compleet Hugo-project met:
- ✅ Homepage met alle secties (hero, expertise, projecten, about, blog, contact)
- ✅ Blog-systeem met individuele post-pagina's
- ✅ Decap CMS dashboard (Cheimaa kan inloggen en bloggen)
- ✅ Tweetalig (NL/EN)
- ✅ Foto van Cheimaa + logo
- ✅ Reacties via Giscus (gratis, via GitHub)
- ✅ SEO-geoptimaliseerd (meta tags, Open Graph, sitemap, RSS)
- ✅ Responsive design (mobiel, tablet, desktop)

---

## Stap 1: GitHub Repository aanmaken (5 min)

1. Ga naar https://github.com/new
2. Repository naam: `cirkelvast-site`
3. Zet op **Public**
4. Klik **Create repository**
5. Upload alle bestanden uit de `cirkelvast-site` map:
   - Klik **uploading an existing file**
   - Sleep de HELE inhoud van de `cirkelvast-site` map erin
   - Klik **Commit changes**

### Tip: Of via command line (als je git hebt):
```bash
cd cirkelvast-site
git init
git add .
git commit -m "Initial commit - Cirkelvast website"
git branch -M main
git remote add origin https://github.com/JOUW-USERNAME/cirkelvast-site.git
git push -u origin main
```

---

## Stap 2: Netlify koppelen (5 min)

1. Ga naar https://app.netlify.com/signup
2. **Sign up with GitHub**
3. Klik **Add new site** → **Import an existing project**
4. Kies **GitHub** → selecteer `cirkelvast-site`
5. Build settings worden automatisch herkend (via netlify.toml):
   - Build command: `hugo --minify`
   - Publish directory: `public`
6. Klik **Deploy site**
7. Wacht 1-2 minuten → je site is live! 🎉

---

## Stap 3: Domein koppelen — cirkelvast.nl (10 min)

1. In Netlify: ga naar **Domain management** → **Add a domain**
2. Typ: `cirkelvast.nl`
3. Netlify geeft je DNS-instellingen (nameservers)
4. Ga naar je domeinregistrar (bijv. TransIP, Antagonist, Hostnet)
5. Wijzig de **nameservers** naar die van Netlify:
   - `dns1.p01.nsone.net`
   - `dns2.p01.nsone.net`
   - (etc. — Netlify toont de exacte waarden)
6. Wacht 15-60 minuten op DNS-propagatie
7. Netlify regelt automatisch een SSL-certificaat (HTTPS)

---

## Stap 4: Netlify Identity activeren — voor het CMS (5 min)

Dit is nodig zodat Cheimaa kan inloggen op cirkelvast.nl/admin

1. In Netlify: ga naar **Integrations** → **Identity**
2. Klik **Enable Identity**
3. Onder **Registration**: kies **Invite only** (veiligheid!)
4. Ga naar **Services** → **Git Gateway** → **Enable Git Gateway**
5. Ga naar **Identity** → **Invite users**
6. Voer Cheimaa's e-mailadres in
7. Ze ontvangt een e-mail om haar account te activeren
8. Daarna kan ze naar `cirkelvast.nl/admin` en inloggen!

---

## Stap 5: Giscus reacties instellen (optioneel, 10 min)

1. Ga naar https://giscus.app
2. Vul in:
   - Repository: `JOUW-USERNAME/cirkelvast-site`
   - Mapping: `pathname`
   - Theme: `light`
3. Kopieer de gegenereerde `data-repo-id` en `data-category-id`
4. Open `layouts/blog/single.html`
5. Vervang de placeholder waarden bij het Giscus script
6. Commit en push naar GitHub → Netlify bouwt automatisch opnieuw

**Let op:** Je moet eerst **Discussions** activeren in je GitHub repo:
- Ga naar repo **Settings** → **Features** → vink **Discussions** aan

---

## Hoe Cheimaa blogt

### Via het dashboard:
1. Ga naar `cirkelvast.nl/admin`
2. Log in met e-mail
3. Klik **Blog / Inzichten** → **Nieuw**
4. Vul in:
   - **Titel**: bijv. "Waarom schoolgebouwen niet kunnen wachten"
   - **Beschrijving**: korte samenvatting (wordt getoond in previews + SEO)
   - **Categorie**: VMV / POHV / Strategie / etc.
   - **Afbeelding**: upload een foto (optioneel)
   - **Inhoud**: schrijf het artikel in markdown (of gebruik de visual editor)
5. Klik **Publish**
6. De site bouwt zichzelf automatisch opnieuw (duurt ~1 minuut)

### Content tips:
- Gebruik `##` voor tussenkoppen (goed voor SEO)
- Voeg altijd een afbeelding toe (beter voor social media delen)
- Houd de beschrijving onder 160 tekens (SEO)
- Gebruik de categorie consistent

---

## Mapstructuur uitleg

```
cirkelvast-site/
├── hugo.toml              ← Configuratie (titel, talen, parameters)
├── netlify.toml           ← Build-instellingen voor Netlify
├── content/
│   ├── _index.md          ← Homepage content
│   └── blog/
│       ├── _index.md      ← Blog overzichtspagina
│       └── *.md           ← Individuele blogposts (Decap CMS maakt deze aan)
├── layouts/
│   ├── index.html         ← Homepage template
│   ├── _default/
│   │   ├── baseof.html    ← Base layout (head, nav, footer)
│   │   ├── single.html    ← Default pagina template
│   │   └── list.html      ← Default lijst template
│   ├── blog/
│   │   ├── list.html      ← Blog overzicht
│   │   └── single.html    ← Individuele blogpost
│   └── partials/
│       ├── nav.html       ← Navigatie
│       └── footer.html    ← Footer
├── static/
│   ├── css/style.css      ← Alle styling
│   ├── js/main.js         ← JavaScript
│   ├── images/            ← Foto's en logo
│   └── admin/
│       ├── index.html     ← CMS dashboard
│       └── config.yml     ← CMS configuratie
└── archetypes/
    └── default.md         ← Template voor nieuwe content
```

---

## Veelgestelde vragen

**Hoe lang duurt het voordat een nieuwe blogpost live is?**
~1-2 minuten na publiceren in het CMS.

**Kan ik de homepage teksten aanpassen?**
Ja, in `hugo.toml` staan alle teksten. Pas aan, commit, push.

**Hoe voeg ik een nieuwe taal toe?**
De site is al voorbereid voor NL/EN. Voor EN content, maak een `content.en/` map aan.

**Wat als er iets kapot gaat?**
Netlify bewaart elke versie. Ga naar **Deploys** en klik **Publish deploy** op een eerdere versie.

**Kost dit geld?**
- Netlify: gratis (tot 100GB bandbreedte/maand — ruim voldoende)
- Domein: wat je al betaalt voor cirkelvast.nl
- SSL: gratis via Netlify
- CMS: gratis
- Reacties: gratis via Giscus

---

## Support nodig?
Je kunt altijd terug naar Claude om aanpassingen te maken aan het design, nieuwe secties toe te voegen, of content te laten genereren!
