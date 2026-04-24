# Portfolio (Hugo + Blowfish)

Dette projekt er en statisk portfolio-side bygget med [Hugo](https://gohugo.io/) og temaet **Blowfish**.

## Kør projektet lokalt

### 1) Forudsætninger

- Git
- Hugo Extended (anbefalet: `0.160.0` eller nyere)

### 2) Klon projektet inkl. submodule

```bash
git clone --recurse-submodules https://github.com/pete399c1/portfolio.git
cd portfolio
```

Hvis repo allerede er klonet uden submodule:

```bash
git submodule update --init --recursive
```

### 3) Start udviklingsserver

```bash
hugo server -D
```

Siden kan herefter ses på:

- `http://localhost:1313`

## Byg projektet til produktion

```bash
hugo --gc --minify
```

Det genererede site bliver lagt i mappen `public/`.

## Deployment

Projektet deployes automatisk via GitHub Actions ved push til `main`:

- Workflow: `.github/workflows/hugo.yaml`
- Output-artifact: `public/`
- Hosting: GitHub Pages

## Teknologier der er brugt

- **Hugo**: statisk site generator
- **Blowfish** (tema): UI/layout ovenpå Hugo
- **Go templates**: templating i layouts/partials
- **Markdown**: indhold i `content/`
- **Git submodules**: temaet ligger i `themes/blowfish`
- **GitHub Actions**: CI/CD og deployment
- **Dart Sass**: CSS-kompilering i build-pipeline
- **Node.js**: bruges i pipeline ved behov for npm-afhængigheder

## Begreber (kort forklaret)

- **Statisk site**: HTML/CSS/JS genereres på build-tid, ikke server-side runtime.
- **Theme**: genbrugelig design- og layoutpakke til Hugo.
- **Partial**: en genanvendelig skabelonfil (fx footer/header).
- **Front matter**: metadata øverst i content-filer (titel, dato, tags osv.).
- **Base URL**: domænet siden bygges til (sat i `hugo.toml`).
- **Minify**: gør output-filer mindre ved at fjerne overflødige tegn.

## Projektstruktur (uddrag)

- `hugo.toml`: hovedkonfiguration
- `content/`: sider og indhold
- `layouts/`: lokale template-overskrivninger
- `themes/blowfish/`: tema (submodule)
- `public/`: bygget output

