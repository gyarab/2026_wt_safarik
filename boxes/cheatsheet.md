# Tahák: responzivní web s Bootstrapem 6

> **Pozor:** Bootstrap 6 (verze `6.0.0-alpha.1`) má **jiné názvy tříd než Bootstrap 5**.
> Většina návodů na internetu (W3Schools, starší StackOverflow, často i AI) ukazuje Bootstrap 5.
> Viz tabulka [v5 → v6](#7-pozor-na-návody-pro-bootstrap-5) dole.
>
> Dokumentace v6: <https://getbootstrap.com/docs/6.0/layout/grid/>

---

## 0. Spuštění projektu (Windows 11 + Git Bash)

```bash
cd ~/Documents/muj-repozitar     # přejdu do svého repozitáře
mkdir boxes                       # nová složka
code .                            # otevřu VS Code v aktuální složce
py -3 -m http.server              # spustím lokální server (běží, dokud ho nezastavím)
```

- Otevři v prohlížeči: **<http://localhost:8000/boxes/>**
- Server zastavíš **Ctrl + C** (v terminálu, kde běží).
- Port je obsazený? → `py -3 -m http.server 8001` a pak `http://localhost:8001/…`
- Změny nevidím? → **Ctrl + F5** (obnovení bez cache), zkontroluj, že je soubor uložený.
- Server spouštěj v **kořeni repozitáře**, ne ve složce `boxes`, jinak ostatní projekty neuvidíš.

## 1. Základní šablona

```html
<!DOCTYPE html>
<html lang="cs" data-bs-theme="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  <!-- NUTNÉ pro mobil! -->
    <title>Můj web</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@6.0.0-alpha.1/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <div class="container"> … </div>

    <script type="module" src="https://cdn.jsdelivr.net/npm/bootstrap@6.0.0-alpha.1/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

- `data-bs-theme="light"`: bez toho se web přepne do tmavého režimu, když ho máš zapnutý ve Windows. Chceš tmavý? Dej `dark`.
- `type="module"` u skriptu je v Bootstrapu 6 **povinné**.
- Celou šablonu (i s `integrity`) najdeš v souboru [sablona.html](sablona.html).

## 2. Breakpointy = šířky, kde se layout mění

| Prefix | Od šířky | Typické zařízení | `.container` má šířku |
|--------|---------:|------------------|-------------:|
| *(žádný)* | 0 px | mobil na výšku | 100 % |
| `sm:` | 576 px | mobil na šířku | 540 px |
| `md:` | 768 px | tablet | 720 px |
| `lg:` | 1024 px | notebook | 960 px |
| `xl:` | 1280 px | monitor | 1200 px |
| `2xl:` | 1536 px | velký monitor | 1440 px |

**Mobile-first:** třída bez prefixu platí **všude**. Třída s prefixem platí **od té šířky výš**.

```
col-12 md:col-6 lg:col-4
│       │        └── od 1024 px: 4/12 = třetina
│       └─────────── od 768 px: 6/12 = polovina
└─────────────────── všude (mobil): celá šířka
```

## 3. Kontejnery

| Třída | Co dělá |
|-------|---------|
| `container` | max. šířka podle breakpointu, vycentrovaný |
| `container-fluid` | vždy 100 % šířky |
| `md:container` | do 768 px na celou šířku, pak jako `container` |

## 4. Grid (mřížka): řádek a sloupce

```html
<div class="container">
  <div class="row g-5">                       <!-- řádek + mezery -->
    <div class="col-12 md:col-6 lg:col-4">…</div>
    <div class="col-12 md:col-6 lg:col-4">…</div>
    <div class="col-12 md:col-6 lg:col-4">…</div>
  </div>
</div>
```

- Řádek má **12 dílů**. Součet `col-*` v jednom řádku má být 12 (víc = přeteče na nový řádek).
- `col` = rozděl se rovným dílem s ostatními, `col-auto` = šířka podle obsahu.
- **Zkratka:** počet sloupců nastavím na řádku:
  `<div class="row row-cols-1 md:row-cols-2 lg:row-cols-4">` a děti mají jen `class="col"`.
- **Mezery mezi sloupci:** `g-0` … `g-12` (`gx-*` vodorovně, `gy-*` svisle).
- **Odsazení zleva:** `md:offset-2`. **Pořadí:** `order-1`, `lg:order-2`, `order-first`, `order-last`.
- **Zarovnání v řádku:** `justify-content-center`, `align-items-center`.

## 5. Užitečné utility (všechny jdou s prefixem `sm: md: lg: xl: 2xl:`)

### Zobrazení / skrytí
| Chci | Třídy |
|------|-------|
| skrýt všude | `d-none` |
| skrýt od tabletu výš (jen mobil) | `md:d-none` |
| zobrazit až od tabletu | `d-none md:d-block` |
| flex | `d-flex`, `md:flex-row`, `flex-column`, `gap-5`, `flex-wrap` |

### Mezery (margin `m`, padding `p`)
`m` / `p` + strana `t` (top), `b` (bottom), `s` (start = vlevo), `e` (end = vpravo), `x`, `y` + velikost:

| číslo | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| rem | 0 | .25 | .375 | .5 | .75 | **1** | 1.25 | 1.5 | 1.75 | 2 | 2.25 | 2.5 | **3** |

Příklady: `mt-5`, `py-12`, `px-3`, `mx-auto` (vycentrovat blok), `md:p-8`.
⚠️ V6 má jinou stupnici než v5: `p-5` je v6 jen **1rem** (v5 to bylo 3rem).

### Text
| Třída | Význam |
|------|--------|
| `text-center`, `text-start`, `text-end` | zarovnání (`md:text-start` …) |
| `fs-sm` `fs-md` `fs-lg` `fs-xl` `fs-2xl` … `fs-6xl` | velikost písma |
| `fw-bold`, `fw-light` | tučnost |
| `h1` … `h6` | vzhled nadpisu na libovolném prvku |
| `text-uppercase`, `text-truncate` | velká písmena, oříznutí … |

### Barvy
| Třída | Význam |
|------|--------|
| `bg-primary`, `bg-success`, `bg-danger`, `bg-warning`, `bg-info` | pozadí |
| `bg-1`, `bg-2` | jemně šedé pozadí sekce |
| `fg-primary`, `fg-danger`, `fg-white` … | barva textu (**ne** `text-primary`!) |
| `theme-primary` (+ `btn-solid`, `alert`, `badge` …) | barevná varianta komponenty |

### Obrázky
| Třída | Význam |
|------|--------|
| `img-fluid` | obrázek se zmenší, nepřeteče rodiče |
| `w-100` | šířka 100 % |
| `ratio-1x1`, `ratio-16x9`, `ratio-4x3` | poměr stran |
| `object-fit-cover` | vyplní plochu a ořízne (s `ratio-*` ideální pro galerii) |
| `rounded-3`, `rounded-circle`, `shadow`, `shadow-lg` | zaoblení, stín |

## 6. Komponenty

```html
<!-- Tlačítka: btn-solid / btn-outline / btn-subtle + theme-* -->
<button class="btn-solid theme-primary">Hlavní</button>
<button class="btn-outline theme-secondary">Vedlejší</button>
<a href="#" class="btn-solid theme-success btn-lg">Velký odkaz</a>

<!-- Karta -->
<div class="card h-100">
  <img src="foto.jpg" class="card-img-top" alt="…">
  <div class="card-body">
    <h3 class="h5">Nadpis</h3>
    <p>Text…</p>
  </div>
</div>

<!-- Upozornění a štítek -->
<div class="alert theme-warning">Pozor!</div>
<span class="badge theme-success">Nové</span>
```

### Navbar s hamburgerem (potřebuje Bootstrap JS!)
```html
<nav class="navbar md:navbar-expand bg-1">
  <div class="container">
    <a class="navbar-brand" href="#">Logo</a>
    <button class="btn-icon navbar-toggler" type="button"
            data-bs-toggle="drawer" data-bs-target="#menu" aria-label="Menu">
      <span class="navbar-toggler-icon"></span>
    </button>
    <dialog class="drawer drawer-end" id="menu">
      <div class="drawer-header">
        <h5 class="drawer-title">Menu</h5>
        <button type="button" class="btn-close" data-bs-dismiss="drawer" aria-label="Zavřít"></button>
      </div>
      <div class="drawer-body">
        <ul class="nav navbar-nav md:ms-auto">
          <li class="nav-item"><a class="nav-link active" href="#">Domů</a></li>
          <li class="nav-item"><a class="nav-link" href="#hra">Hra</a></li>
        </ul>
      </div>
    </dialog>
  </div>
</nav>
```
`md:navbar-expand` = od tabletu je menu v řádku, pod ním hamburger. `data-bs-target="#menu"` musí sedět s `id="menu"`.

## 7. Pozor na návody pro Bootstrap 5

| Bootstrap 5 (návody na webu) | Bootstrap 6 (my) |
|---|---|
| `col-md-6` | `md:col-6` |
| `row-cols-md-3` | `md:row-cols-3` |
| `d-md-none` | `md:d-none` |
| `text-md-center` | `md:text-center` |
| `navbar-expand-lg` | `lg:navbar-expand` |
| `btn btn-primary` | `btn-solid theme-primary` |
| `btn btn-outline-danger` | `btn-outline theme-danger` |
| `alert alert-success` | `alert theme-success` |
| `text-primary`, `text-white` | `fg-primary`, `fg-white` |
| `offcanvas` | `drawer` |
| `modal` | `dialog` |
| `xxl` (1400 px) | `2xl` (1536 px) |
| `lg` = 992 px, `xl` = 1200 px | `lg` = 1024 px, `xl` = 1280 px |
| `<script src="…">` | `<script type="module" src="…">` |

## 8. Testování v prohlížeči (Chrome / Firefox / Safari / Edge)

1. **F12** → DevTools
2. **Ctrl + Shift + M** → režim zařízení (Device toolbar)
3. Nahoře vyber *Dimensions: Responsive* a táhni šířku, nebo vyber konkrétní telefon.
4. Vždy zkontroluj aspoň: **375 px** (mobil), **768 px** (tablet), **1280 px** (notebook).
5. Chyby v JavaScriptu najdeš v záložce **Console**.

---

## 9. JavaScript: práce s HTML (na domácí úkol)

```js
// NAJÍT prvek
const el    = document.getElementById('skore');        // podle id
const el2   = document.querySelector('#skore');        // podle CSS selektoru (první shoda)
const karty = document.querySelectorAll('.karta');     // VŠECHNY shody

// ZMĚNIT obsah
el.textContent = 42;                    // čistý text (bezpečné)
el.innerHTML = '<strong>42</strong>';   // HTML

// TŘÍDY (= měníme vzhled přes CSS / Bootstrap)
el.classList.add('d-none');
el.classList.remove('d-none');
el.classList.toggle('otocena');         // přidá, nebo odebere
el.classList.contains('otocena');       // true / false

// KLIKNUTÍ
el.addEventListener('click', () => {
    console.log('klik!');
});

// VYTVOŘIT nový prvek a vložit ho do stránky
const div = document.createElement('div');
div.classList.add('col');
div.textContent = '🍎';
div.dataset.hodnota = '🍎';            // vznikne atribut data-hodnota="🍎"
document.querySelector('#plocha').appendChild(div);

// PROJÍT pole / více prvků
for (const vec of ['🍎', '🍐']) { … }
karty.forEach((k) => k.classList.remove('otocena'));

// ZAMÍCHAT pole (Fisher–Yates)
function zamichej(pole) {
    for (let i = pole.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [pole[i], pole[j]] = [pole[j], pole[i]];
    }
    return pole;
}

// ZPOŽDĚNÍ (např. otočit karty zpět po 1 s)
setTimeout(() => {
    karta.classList.remove('otocena');
}, 1000);

// ZDVOJIT pole (pro pexeso – každý obrázek 2×)
const dvojice = [...obrazky, ...obrazky];
```
