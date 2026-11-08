# Labo 4 - Grid voor de pagina, flexbox voor de rij: vijf nabouw-opdrachten: modeloplossing

Dit is een mogelijke oplossing van labo 4, niet de enige. Vergelijk ze met je eigen werk: niet om over te nemen, maar om te zien waar jouw CSS afwijkt en of dat erg is. Een andere weg naar hetzelfde screenshot is niet fout, zolang ze uit hoofdstuk 4 komt; een weg die de regels breekt (een gewijzigde `index.html`, marges in plaats van `gap`, floats, `inline-block` voor een rij, id-selectors, `!important`) wel. De HTML-bestanden en `reset.css` zijn identiek aan de starter. De verwijzingen (4.3, F4.2) zijn naar de syllabus.

## 1. Drie kolommen

Zie `kolommen/css/stijl.css`. Eén as, dus `display: flex` op `main`, met `gap: 4vw` en padding in vh en vw. De drie `div`'s krijgen `flex: 1`, de middelste `flex: 2`; de breedte volgt vanzelf: 1280 - 2 x 51,2 (padding) - 2 x 51,2 (gaps) = 1075,2px beschikbaar, verdeeld in 1 + 2 + 1 = 4 delen van 268,8px. Elke kolom is zelf een grid met `place-items: center` om haar cijfer te centreren (4.7). De hoogte komt gratis: `min-height: 100vh` op `main` en de standaard `align-items: stretch` rekken de kolommen tot de volle rij (4.3).

Reflectie: `display: flex` staat op `main`, want de container organiseert; `flex` staat op de drie `div`'s, want de items ondergaan, en `flex` is de ene property die op een item hoort (4.4). Op hetzelfde element kan niet: `flex` zegt iets over het aandeel van een item in zíjn ouder.

Veelgemaakte fouten: `flex: 1` op `main` (F4.2); `width: 50%` op de middelste kolom in plaats van `flex: 2`, wat met de gaps erbij net niet klopt (F4.4); de cijfers centreren met `text-align` en `padding-top`, wat werkt maar de oude weg is; `height: 80vh` op de items in plaats van de container te laten rekken.

## 2. Navigatiebalk

Zie `navigatie/css/stijl.css`. Twee flex-containers. De `header` zet de naam en de navigatie uit elkaar met `justify-content: space-between` en lijnt ze verticaal uit met `align-items: center`. De `ul` is een rij met `gap: 0.5rem`, zonder bolletjes en insprong (3.3). Elke link is `display: block` met padding, zodat het klikvlak de hele box is (3.7); de actieve link, hover en focus delen één regel met het gele vlak.

Reflectie: `justify-content` verdeelt langs de hoofdas, hier horizontaal; `align-items` lijnt uit op de kruisas, verticaal (4.3). Met `margin-right` op elke `li` krijgt ook de laatste link een marge, die de rij van de rechterrand wegduwt; dan heb je een `:last-child`-uitzondering nodig. `gap` legt tussenruimte alleen tússen de items (motorkap hoofdstuk 4).

Veelgemaakte fouten: `float: right` of `text-align: right` op de nav om de links rechts te krijgen (F4.8); `space-between` op de `ul` in plaats van op de `header`, waardoor de links uitwaaieren over de hele balk (F4.2, verkeerd niveau); `align-items: center` vergeten, de naam hangt bovenaan; padding op `a` zonder `display: block`, het klikvlak blijft klein (F3.5: in een flex-rij is het `li` het item, de `a` erin is nog gewoon inline); hover zonder focus (F2.11).

## 3. Mondriaan

Zie `mondriaan/css/stijl.css`. Twee assen, dus grid: `repeat(4, 1fr)` kolommen, `repeat(3, 1fr)` rijen, `gap: 2vh` en evenveel padding, op een container van 70vh breed en hoog met blauwe achtergrond. Het blauw dat je ziet, is alleen die gap en die padding. De lila en de olijfkleurige vlakken lopen van lijn 1 tot lijn 4 (`grid-column: 1 / 4`); de modeloplossing plaatst voor de duidelijkheid ook de andere vier op hun kolom, maar dat hoeft niet allemaal.

Reflectie: strikt genomen moet je alleen `.lila` en `.olijf` (1 / 4) en `.marine` (kolom 4) plaatsen. `.bruin` valt dan vanzelf in kolom 4 van rij 1, `.geel` in kolom 1 van rij 2, en `.rood` in rij 3 na `.olijf`; zonder plaatsing zou `.marine` in kolom 2 van rij 2 landen (4.5). De twee lege cellen ontstaan doordat niets ze opeist. `gap` is één declaratie op de container en geeft overal dezelfde lijndikte; borders op de vlakken verdubbelen tussen twee vlakken, zijn enkel aan de rand, en een lege cel heeft geen border.

Veelgemaakte fouten: `25% 25% 25% 25%` met gap (F4.4: het raster loopt over de rechterrand); lijnen tellen vanaf 0 of in cellen in plaats van lijnen (`grid-column: 1 / 3` voor drie kolommen breed; zet de overlay met nummers aan, 4.9); de buitenrand vergeten (padding op de container, even groot als de gap); een blauwe border op elk vlak in plaats van gap; `height` op de vlakken, terwijl de rijen van het raster de hoogte bepalen (4.5).

## 4. Trap

Zie `trap/css/stijl.css`. Een raster van `repeat(4, 1fr)` kolommen en `repeat(4, 1fr)` rijen op `height: 100vh`. Elke trede krijgt haar eigen `grid-column` én `grid-row`, geselecteerd met `:nth-child()`, want de HTML heeft vier keer dezelfde class. Het cijfer staat gecentreerd met `place-items: center` op de trede.

Reflectie: zonder `grid-row` landen de vier treden op de eerste rij, in kolom 1 tot 4, want de impliciete grid vult in DOM-volgorde kolom na kolom (4.5). `4 / -1` betekent van lijn 4 tot de laatste lijn; een raster van vier kolommen heeft vijf lijnen, dus -1 is lijn 5 en dat is precies de laatste kolom (motorkap hoofdstuk 4).

Veelgemaakte fouten: `grid-row` vergeten (alle vier op rij 1); `height: 100%` op `.trap` (F3.2: `body` heeft geen hoogte; `100vh` is de remedie, 3.2); de rijen niet declareren, waarna de drie onderste rijen zo hoog worden als één cijfer en de trap ineenzakt; `:nth-child` op `.trap` in plaats van op `.trede`.

## 5. Dierenasiel Zonnehoek

Zie `dierenasiel/css/stijl.css`. Het bouwplan van 4.8, van buiten naar binnen. `body` is een grid van drie rijen, `auto 1fr auto`, met `min-height: 100vh`: de sticky footer (4.7). De `header` is de flex-balk van oefening 2. `main` is een gewone leeskolom met `max-width: 60rem` en `margin: 0 auto` (3.6). `.kaarten` is een grid van drie kolommen met `gap`, en `.uitgelicht` loopt van lijn 1 tot lijn 3. Elke `.kaart` is een flex-container in richting column met `align-items: flex-start`, en `.beschrijving` krijgt `flex: 1`, zodat de knop in elke kaart onderaan staat (4.4).

Reflectie: zes layoutcontainers: `body` (grid), `header` (flex), `nav ul` (flex), `.kaarten` (grid) en elke `.kaart` (flex, richting column); `main` is geen container, alleen een gecentreerde kolom. Grid waar rijen en kolommen beide tellen, flexbox voor één rij of kolom. Op een half venster worden de drie kolommen te smal en breekt de tekst in de kaarten per woord; hoofdstuk 6 lost dat op met een raster dat zichzelf aanpast (6.5) en met media queries (6.6).

Veelgemaakte fouten: de footer "onderaan" met `margin-top` of `position: absolute` in plaats van het grondplan (F4.8); `height: 100vh` op `body` in plaats van `min-height` (F3.10: bij meer kaarten loopt de pagina over); `.uitgelicht` met `width: 200%` in plaats van `grid-column`; de knoppen niet onderaan omdat `flex: 1` op de kaart staat in plaats van op de tekst (F4.2); de knop over de volle breedte omdat `align-items: flex-start` ontbreekt (F4.5, stretch); hover zonder focus (F2.11).

## Thuis: B4.1

Geen modeloplossing: je site is van jou. Waar je zelf op controleert: `body` als grid `auto 1fr auto` met `min-height: 100vh`; de navigatie als flex-rij met `gap`; een kaartenrooster in grid met `fr` en `gap`; elke kaart een flex-column met `flex: 1` op de tekst; een commentaarregel per container met zijn taak; nergens `float`, `position` of `inline-block` voor een rij.
