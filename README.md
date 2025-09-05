# Bootstrap & Vite – SOŠ Digital 

## Postup

### Založení Vite Vanilla JS projektu

```
npm create vite@latest bs-sosdigital
```
poté
```
npm install
npm run dev
```

&nbsp;

### Instalace balíčku Bootstrap

Postup dle [dokumentace Bootstrap](https://getbootstrap.com/docs/5.0/getting-started/download/#npm)

```
npm install bootstrap
```

&nbsp;

Před zakončením <body> naimportujeme modul _main.js_ (uvnitř _/src/_)

```
<script type="module" src="/src/main.js"></script>
```


#### main.js

Do souboru _main.js_ uvnitř adresáře _src_ vložíme import Bootstrap JS a CSS souborů.

```
import 'bootstrap/dist/css/bootstrap.min.css';
import 'bootstrap/dist/js/bootstrap.bundle.min.js';
```

Dále také vložíme náš CSS dokument _style.css_
```
import './style.css';
```

#### multimediální soubory

Do adresáře _public_ vložíme statický obsah –  v tomto případě **veškeré multimediální soubory (obrázky, vektor)**.

&nbsp;


### Build projektu

Spustíme build proces
```
npm run build
```
čímž vznikne adresář _/dist_ s obsahem aplikace připravený k nasazení

&nbsp;


### Deploy GitHub Pages

1. Založíme repozitář na GitHub.
1. Do repozitáře do branch **main** pushneme veškerý obsah (zdrojový kód) projektu.
1. Nainstalujeme modul GitHub Pages, který bude součástí _devDependencies_ unvnitř _package.json_
```
npm install gh-pages --save-dev
```
1. V _package.json_ do větve _"Scripts"_ doplníme klíč **deploy**
```
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "deploy": "vite build --base=/nazev-vaseho-repozitare/ && gh-pages -d dist"
  },
```
a to s hodnotou
```
"vite build --base=/nazev-vaseho-repozitare/ && gh-pages -d dist"
```

+ **vite build**
  - Spustí build Vite projektu do složky _/dist_.
+ **--base=/nazev-vaseho-repozitare/**
  - Určuje základní URL cestu, která je potřeba pro správné načítání souborů na GitHub Pages (kde je web dostupný pod https://vas-username.github.io/nazev-vaseho-repozitare/)
+ **gh-pages -d dist**
  - Nasadí obsah složky dist na gh-pages větev v GitHub repozitáři. Díky tomu se web zobrazí na GitHub Pages.
   
&nbsp;

### Aktualizace projektu a GitHub Pages

Pro aktualizaci **branch _main_ se zdrojovým kódem** projektu použijeme klasicky commit a push
```
git add .
git commit -m "update ..."
git push
```

Pro **aktualizaci GitHub Pages** vytvoříme novou deploy verzi = GitHub Pages se automaticky aktualizují nově sestaveným build obsahem
```
npm run deploy
```