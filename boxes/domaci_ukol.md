# Velký domácí úkol: microsite s JS hrou

Postav malý web (microsite) o **jedné jednoduché hře**, kterou naprogramuješ v JavaScriptu.
Web musí být **responzivní** (Bootstrap 6) a hra musí **měnit HTML stránky** pomocí JavaScriptu.

---

## 1. Vyber si hru

| Hra | Co dělá | Obtížnost |
|---|---|---|
| **A) Pexeso** | Karty lícem dolů, otáčím po dvou, shodné zůstanou otočené. Počítám tahy. | ⭐⭐ |
| **B) Interaktivní galerie** | Mřížka obrázků; klik otevře velký náhled, šipky „další / předchozí“, filtrování podle kategorie, ❤️ oblíbené s počítadlem. | ⭐⭐ |
| **C) Vlastní nápad** | Např. chyť krtka, piškvorky, reakční test, kvíz, simon says. **Musíš si ho nechat schválit** do kontrolního dne. | ⭐–⭐⭐⭐ |

> Galerie není „hra“ v pravém slova smyslu, ale kvůli práci s HTML je stejně náročná.
> Chceš ji „zahrát“? Přidej režim „najdi obrázek“: náhodně vyber název a hráč musí kliknout na správný obrázek.

## 2. Povinné požadavky

### Web (HTML + Bootstrap 6)
- [ ] Složka `hra/` ve tvém repozitáři, hlavní soubor `hra/index.html`.
- [ ] Bootstrap **6** z CDN (šablona: [sablona.html](sablona.html)) a správný `<meta name="viewport">`.
- [ ] **Navbar** s hamburgerem na mobilu (`md:navbar-expand` + drawer).
- [ ] Aspoň **3 sekce**: úvod (hero), **hra**, pravidla / jak hrát. Patička se jménem autora.
- [ ] Hrací plocha / galerie je udělaná **gridem** a mění počet sloupců aspoň na **2 breakpointech**
      (např. pexeso 4 → 6 sloupců, galerie 2 → 3 → 4).
- [ ] Funguje bez vodorovného posuvníku na **375 px**, **768 px** a **1280 px**.
- [ ] Vlastní CSS je v `<style>` nebo v `hra/style.css`. Nezahlcuj ho věcmi, které umí Bootstrap.

### JavaScript (manipulace s HTML)
- [ ] JS je ve `<script>` na konci stránky nebo v `hra/script.js`.
- [ ] Prvky hry (karty / obrázky) **vytváří JavaScript z pole** (`createElement` + `appendChild` v cyklu), ne 16× ručně v HTML.
- [ ] Reakce na kliknutí přes `addEventListener`.
- [ ] Vzhled se mění přes **třídy** (`classList.add/remove/toggle`), ne přes `element.style`.
- [ ] Na stránce se zobrazuje **stav hry**: počet tahů / skóre / počet oblíbených apod. (`textContent`).
- [ ] Tlačítko **Nová hra / Reset**, které hru vrátí na začátek (u pexesa i zamíchá karty).
- [ ] Hra pozná **konec** (všechny páry nalezeny / prošel jsem všechny obrázky …) a oznámí to **na stránce**, ne jen přes `alert`.
- [ ] V konzoli (F12 → Console) nejsou **žádné červené chyby**.

### Git
- [ ] Commituješ průběžně, aspoň **5 commitů** s rozumnou zprávou (ne `asdf`, ne jeden commit na konci).
- [ ] V `hra/README.md` napiš:
  - název hry a 2–3 věty, jak se hraje,
  - **zdroje**: odkud máš obrázky, návody a kód. Patří sem i AI nástroje: napiš, s čím ti pomohly.

> Kód musíš umět **vysvětlit**. Na kontrolním dni i při odevzdání se zeptám na libovolný řádek.
> Kód, který nedokážeš vysvětlit, se nepočítá.

## 3. Kontrolní den: co musí být hotové

Na kontrolním dni ukážeš rozpracovaný web (2–3 minuty na každého). Musí být:

1. [ ] Pushnuto na GitHub, aspoň 2 commity.
2. [ ] Kostra webu: navbar s hamburgerem, hero, sekce pro hru, patička.
3. [ ] Responzivní hrací plocha: karty / obrázky jsou v gridu a mění počet sloupců.
4. [ ] Prvky hry **generuje JavaScript** z pole.
5. [ ] **Funguje první interakce**: kliknutím se karta otočí / obrázek se otevře.
6. [ ] Máš vybranou hru (u varianty C je schválená).

Kontrolní den se hodnotí, ale hlavně dostaneš zpětnou vazbu, co opravit do odevzdání.

## 4. Hodnocení finální verze

| Oblast | dílčí hodnocení (suma 30) |
|---|---:|
| Responzivní layout (grid, breakpointy, nic nepřetéká, navbar) | 8 |
| Hra funguje podle pravidel včetně konce hry a resetu | 8 |
| Manipulace s DOM správně (generování z pole, `classList`, `addEventListener`, stav na stránce) | 6 |
| Čitelný kód (odsazení, smysluplné názvy proměnných, komentáře u složitějších míst) | 3 |
| Git: průběžné commity + `README.md` se zdroji | 3 |
| Vzhled a dotažení (konzistentní barvy, texty bez chyb, favicon, titulek) | 2 |
| ⭐ Bonus: časomíra, nejlepší skóre v `localStorage`, obtížnosti, animace otočení karty, tmavý režim … | +3 |


---

## 5. Nápověda: jak na pexeso

**Rozdělení na kroky** (commit po každém):

1. HTML kostra + navbar + sekce. *(commit)*
2. Pole s 8 obrázky / emoji → zdvojit → zamíchat. Vypsat do konzole. *(commit)*
3. V cyklu vytvořit karty do `.row`. Na mobilu 4 sloupce, od MD 6 (`row-cols-4 md:row-cols-6`). *(commit)*
4. Klik na kartu → přidat třídu `otocena` (CSS ukáže obrázek). *(commit, hotovo na kontrolní den)*
5. Pamatovat si první a druhou otočenou kartu (`let prvni = null; let druha = null;`).
6. Porovnat `dataset` obou karet:
   - **shodné** → třída `nalezena`, nechat otočené,
   - **různé** → `setTimeout` za 1 s obě otočit zpět.
7. Zamknout plochu, dokud se karty neotočí zpět (`let zamceno = true;`). Jinak jde otočit třetí kartu.
8. Počítadlo tahů, konec hry (počet nalezených párů = počet obrázků), tlačítko Nová hra. *(commit)*
9. Pravidla, README, doladit vzhled. *(commit + push)*

**Užitečné kousky kódu** najdeš v [cheatsheet.md](cheatsheet.md) (kapitola 9) a v ukázce
[ukazky/06_dom_zaklady.html](ukazky/06_dom_zaklady.html).

## 6. Nápověda: jak na galerii

1. Pole objektů: `{ src: 'img/kocka.jpg', nazev: 'Kočka', kategorie: 'zvirata' }`.
2. Vygenerovat mřížku `row-cols-2 md:row-cols-3 lg:row-cols-4`, obrázky `ratio-1x1 object-fit-cover`.
3. Klik na obrázek → zobrazit velký náhled (vlastní `div` přes celou obrazovku, který skrýváš/ukazuješ třídou `d-none`).
4. Tlačítka ◀ ▶ v náhledu: pamatuj si index aktuálního obrázku (`let aktualni = 0;`).
5. Tlačítka filtrů (Vše / Zvířata / Krajina …): skrýt (`d-none`) obrázky, které nepatří do kategorie.
6. ❤️ u obrázku přepíná třídu `oblibeny`, počítadlo oblíbených v navbaru.
7. ⭐ Bonus: ovládání klávesami ← → Esc (`document.addEventListener('keydown', …)`).

> Obrázky zmenši! Fotka z mobilu má 5 MB. Na web stačí šířka ~800 px (zmenšíš např. v Gimpu nebo v Malování → Změnit velikost).
