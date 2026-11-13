# Pracovní list: Boxes, responzivní web s Bootstrapem 6

**Jméno:** ______________________  **Třída:** ______  **Datum:** ____________

Po celou dobu měj po ruce [cheatsheet.md](cheatsheet.md).
Hotové úkoly si odškrtávej `[x]`. Odpovědi na otázky piš přímo sem.

---

## Hodina 1: kontejnery a grid

### Úkol 1: příprava (5 min)
- [ ] V Git Bash přejdi do svého repozitáře a vytvoř složku `boxes`.
- [ ] Do ní ulož šablonu [sablona.html](sablona.html) (odkaz dostaneš od vyučujícího) jako `boxes/index.html`.
- [ ] V kořeni repozitáře spusť `py -3 -m http.server` a otevři <http://localhost:8000/boxes/>.
- [ ] Otevři DevTools (**F12**) a režim zařízení (**Ctrl + Shift + M**).

### Úkol 2: najdi breakpointy (5 min)
V režimu zařízení nastav šířku podle tabulky a opiš, co ukazuje černý štítek vpravo dole.

| Šířka okna | 360 px | 600 px | 800 px | 1100 px | 1400 px | 1600 px |
|---|---|---|---|---|---|---|
| Štítek ukazuje | | | | | | |

**Otázka 2a:** Proč je v šabloně řádek `<meta name="viewport" …>`? Co by se stalo na mobilu bez něj?

> ______________________________________________________________

### Úkol 3: kontejnery (5 min)
Pod nadpis vlož tři bloky a porovnej je při různých šířkách:

```html
<div class="krabice">bez kontejneru</div>
<div class="container"><div class="krabice">container</div></div>
<div class="container-fluid"><div class="krabice">container-fluid</div></div>
```

**Otázka 3a:** Při šířce okna 1100 px je `.container` široký ______ px, `.container-fluid` je široký ______ px.

> Tip: v DevTools najeď myší na prvek v záložce *Elements* a uvidíš jeho rozměry.

### Úkol 4: krabice v mřížce (15 min)
Vytvoř 8 krabic (`<div class="krabice">1</div>` …) uvnitř `.row` tak, aby jich vedle sebe bylo:

| Zařízení | mobil | od MD (768) | od LG (1024) | od XL (1280) |
|---|---|---|---|---|
| Krabic vedle sebe | 1 | 2 | 3 | 4 |

- [ ] **4a:** pomocí tříd na každém sloupci (`col-12 md:col-…`)
- [ ] **4b:** zkopíruj řádek a udělej totéž kratší cestou přes `row-cols-*` na řádku
- [ ] **4c:** přidej mezery mezi krabice (`g-…`). Zkus `g-0`, `g-5` a `g-12`.

**Otázka 4d:** Napiš třídy pro sloupec, který je na mobilu přes celou šířku, na tabletu má třetinu a na notebooku čtvrtinu:

> `class="________________________________________"`

**Otázka 4e:** Okno má šířku **900 px**. Kolik krabic je vedle sebe, když mají třídy `col-6 md:col-4 xl:col-3`? ______

### Úkol 5: obsah + boční panel (10 min)
- [ ] Udělej řádek se dvěma sloupci: `<main>` (hlavní obsah) a `<aside>` (boční panel).
- [ ] Na mobilu budou **pod sebou**, od LG vedle sebe v poměru **2 : 1**.
- [ ] ⭐ Bonus: na mobilu ať je panel **nad** obsahem, od LG **vpravo** (`order-…`).

### Úkol 6: git commit + git push (2 min)

---

## Hodina 2: utility, navbar, vlastní stránka

### Úkol 7: skrývání (5 min)
- [ ] Přidej žlutý pruh `<div class="alert theme-warning">📱 Jsi na mobilu</div>`, který je vidět **jen pod 768 px**.
- [ ] Přidej modrý pruh `<div class="alert theme-info">🖥️ Jsi na velkém displeji</div>`, vidět **jen od 1024 px**.

**Otázka 7a:** Jaký je rozdíl mezi `md:d-none` a `d-none md:d-block`?

> ______________________________________________________________

### Úkol 8: navbar (10 min)
- [ ] Z taháku (kapitola 6) vlož na začátek `<body>` navbar se 3 odkazy.
- [ ] Ověř, že na mobilu se ukáže ☰ a menu vyjede z boku.
- [ ] Změň `md:navbar-expand` na `lg:navbar-expand`. Kdy se teď menu sbalí? ______ px

> Hamburger nereaguje? Zkontroluj (1) že máš na konci `<script type="module" …bootstrap.bundle.min.js>`,
> (2) že `data-bs-target="#menu"` sedí s `id="menu"`, (3) záložku Console v DevTools.

### Úkol 9: stránka „Boxes“ (20 min)
Postav jednoduchou stránku firmy, která prodává krabice / pořádá stěhování (nebo cokoli jiného, co tě baví).
Obrázky: zkopíruj si složku [img/](img/) do své složky `boxes` a odkazuj na ně `img/box1.svg` … `img/box8.svg`, `img/hero.svg`. Můžeš použít i vlastní.

| Sekce | Mobil | Od MD | Od LG |
|---|---|---|---|
| **Navbar** | hamburger | menu v řádku | menu v řádku |
| **Hero** (nadpis + text + tlačítko + obrázek) | pod sebou, text na střed | pod sebou | vedle sebe 1 : 1, text vlevo |
| **3 karty** se službami (`card`) | 1 sloupec | 3 sloupce | 3 sloupce |
| **Galerie** 8 obrázků, čtverce (`ratio-1x1 object-fit-cover`) | 2 sloupce | 3 sloupce | 4 sloupce |
| **Patička** | pod sebou, na střed | vedle sebe, rozházené do stran | ← |

- [ ] Zkontroluj stránku v DevTools na **375 px**, **768 px** a **1280 px**.
- [ ] Nikde nesmí být vodorovný posuvník (nic nepřetéká).
- [ ] ⭐ Bonus: přidej `sticky-top` na navbar a `shadow` / `rounded-*` na karty.
- [ ] ⭐ Bonus: přepni `data-bs-theme="dark"` a podívej se, co se stane.

### Úkol 10: git commit + git push (2 min)

---

## Kontrolní otázky (na závěr)

1. Co znamená **mobile-first**? Platí třída `col-6` (bez prefixu) i na velkém monitoru?
2. Kolik dílů má jeden řádek gridu v Bootstrapu?
3. Na stránce z návodu na internetu vidíš `class="col-md-6"`. Proč ti to nefunguje a jak to přepíšeš?
4. Proč nestačí otevřít `index.html` dvojklikem a je lepší spustit `py -3 -m http.server`?
5. Navrhni CSS třídy pro řádek s kartami pexesa: 4 karty vedle sebe na mobilu, 6 od tabletu.
