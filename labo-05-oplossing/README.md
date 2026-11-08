# Labo 5 - Plaatsen en verdiepen: vijf nabouw-opdrachten: modeloplossing

Dit is een mogelijke oplossing van labo 5, niet de enige. Vergelijk ze met je eigen werk: niet om over te nemen, maar om te zien waar jouw CSS afwijkt en of dat erg is. Een andere weg naar hetzelfde screenshot is niet fout, zolang ze uit hoofdstuk 4 en 5 komt; een weg die de regels breekt (een gewijzigde `index.html`, marges in plaats van `gap`, position voor structuur, een z-index van 9999, id-selectors, `!important`) wel. De HTML-bestanden, de afbeeldingen en `reset.css` zijn identiek aan de starter. De verwijzingen (5.4, F5.1) zijn naar de syllabus.

## 1. Letterraster

Zie `raster/css/stijl.css`. Een grid van `repeat(4, 1fr)` kolommen en `repeat(3, 1fr)` rijen op `min-height: 100vh`, met `gap` en evenveel padding. De plattegrond staat letterlijk in de CSS: drie regels van vier namen, met een punt voor elke lege cel. Elk vlak kiest zijn gebied met `grid-area`, en de letter staat rechtsboven met `text-align: right` en padding.

Reflectie: een L-vormig gebied maakt de hele `grid-template-areas` ongeldig, en de browser valt stil terug op de impliciete plaatsing: acht vlakken op twee rijen van vier, zonder lege cellen (F5.6). Met lijnnummers heb je voor dezelfde plaatsing op minstens vijf vlakken een `grid-column` én een `grid-row` nodig (b, f, g en h staan niet waar de impliciete vulling ze zet, en zodra één vlak verspringt, verspringt de rest mee), dus zo'n tien declaraties tegenover één template en acht `grid-area`'s. De template is bovendien leesbaar: je ziet de plattegrond.

Veelgemaakte fouten: namen tussen aanhalingstekens vergeten, of de rijen niet op één lijn zetten, waardoor je een telfout niet ziet; een lege cel met een leeg woord in plaats van een punt; `grid-area` op de container in plaats van op de vlakken (F4.2); `height: 100%` op het raster (F3.2: `body` heeft geen hoogte).

## 2. Citaten

Zie `citaten/css/stijl.css`. De container is een flex-rij met `flex-wrap: wrap` en `gap`. Elk citaat krijgt `flex: 1 1 18rem`: een basis van 18rem, mag groeien, mag krimpen. Bij 1280 px passen er vier op een rij (4 x 18rem plus de gaps is minder dan de beschikbare breedte; de rest wordt verdeeld), bij 800 px twee. Eén stylesheet, geen media query. De streep in de eigen kleur is `border-left: 0.5rem solid currentColor`: de kleur van de tekst, die per class gezet is.

Reflectie: flex-wrap maakt een reeks onafhankelijke regels; elke regel verdeelt zijn eigen ruimte en weet niets van de regel erboven (5.2). Een grid spant één raster over alle rijen en lijnt dus wel uit; dat is precies het verschil van 4.2. Met een basis van 30rem passen er bij 1280 px nog maar twee op een rij: de container biedt 1232px, en drie keer 480px plus twee gaps is meer. Flexbox beslist over het breken met de basis, niet met de gekrompen maat; krimpen gebeurt pas bínnen een regel. Acht citaten worden dus vier rijen van twee, en elk paar groeit samen dicht tot de volle breedte.

Veelgemaakte fouten: `flex: 1` zonder basis, waardoor alles op één regel blijft, hoe smal ook (de basis 0 is nooit te breed); `width: 25%` op de citaten, wat met gap net niet past en op 800 px niet verandert (F4.4, F5.7); `flex-wrap` vergeten en zich afvragen waarom de citaten krimpen tot één woord per regel; de tweede regel "uitlijnen" met vaste breedtes.

## 3. Fotolijst

Zie `fotolijst/css/stijl.css`. De lijst is het anker: `position: relative`, 36rem breed, gecentreerd met `margin: 4rem auto`. De foto wordt vierkant met het drieluik: `width: 100%`, `aspect-ratio: 1`, `object-fit: cover`; het landschap wordt bijgesneden, niet vervormd (5.6). Elk vlakje is `position: absolute` met twee afstanden: groen en roze vanaf boven en links, lime en rood vanaf onder en rechts. Roze en rood staan in de HTML vóór het vlakje waar ze op moeten liggen, dus ze krijgen `z-index: 1` (5.5).

Reflectie: zonder `position: relative` op de lijst rekenen de vlakjes vanaf het document: groen en roze belanden in de linkerbovenhoek van de pagina, lime en rood in de rechterbenedenhoek van het venster (F5.1). Zonder z-index beslist de DOM-volgorde: wat later in de HTML staat, ligt hoger. Roze staat vóór groen, dus groen ligt bovenop; dat voelt verkeerd omdat je de HTML niet mag herschikken, en daar is z-index voor.

Veelgemaakte fouten: het anker vergeten (F5.1); `object-fit` zonder `aspect-ratio`, waardoor de foto gewoon een landschap blijft (F5.9); de vlakjes met marges "duwen"; `z-index: 999`, wat werkt maar het verkeerde reflex is (F5.4); `top` en `bottom` allebei zetten op één vlakje, waardoor het uitrekt.

## 4. Toonzaal

Zie `balk/css/stijl.css`. De header is `position: sticky` met `top: 0`, en verder een gewone flex-balk: `align-items: center`, vaste hoogte 3.5rem, de naam met `margin-right: auto` zodat de navigatie naar rechts schuift (5.3). De links zijn klein, in kapitalen, grijs; de actieve, hover en focus delen één regel met wit. `scroll-padding-top` op `html`, even groot als de balk, zorgt dat een interne link zijn kop nét onder de balk laat landen (F5.10). De rest is een leeskolom van 44rem.

Reflectie: zonder `top: 0` heeft sticky geen drempel en gebeurt er niets; de header scrolt gewoon mee (F5.2). Met `position: fixed` verlaat de header de flow: de pagina schuift eronder, de h1 verdwijnt achter de balk, en je moet op `body` een `padding-top` zetten die je gokt op de hoogte van de balk. Sticky houdt zijn plek in de flow en heeft dat niet nodig (5.4).

Veelgemaakte fouten: `top` vergeten (F5.2); fixed met padding-top, het Niet zo van 5.4; `scroll-padding-top` op `body` of op `header` in plaats van op `html`; de navigatie rechts krijgen met `float: right` of `text-align` (F4.8); `justify-content: space-between` werkt hier ook, met twee kinderen is dat even goed; hover zonder focus (F2.11).

## 5. Koffiebar Kaai 12

Zie `koffiebar/css/stijl.css`. Van buiten naar binnen. `body` is een grid van twee kolommen (`16rem 1fr`) en drie rijen (`auto 1fr auto`, het grondplan van 4.7), uitgetekend met `grid-template-areas`: kop over beide kolommen, zijbalk naast inhoud, voet over beide kolommen; header, aside, main en footer kiezen hun gebied met `grid-area` (5.1). De header is de balk van oefening 4 zonder sticky. `.kaarten` is een grid van drie kolommen. Elke `.kaart` is `position: relative` (het anker van de badge), een flex-column, en heeft `overflow: hidden` zodat de foto de ronde hoeken volgt. `.kaart:has(img)` verliest zijn padding en geeft ze aan `.tekst`; `.kaart:not(:has(img))` krijgt de streep (5.7). De foto's krijgen het drieluik met `aspect-ratio: 4 / 3` (5.6). `.tekst` is zelf een flex-column met `flex: 1`, en de prijs krijgt `margin-top: auto`: hij zakt naar de bodem van elke kaart (5.3). De badge is `position: absolute` rechtsboven met `z-index: 1` (5.4, 5.5).

Reflectie: de containervraag beantwoordde je op `body`, `header`, `nav ul`, `.kaarten`, `.kaart` en `.tekst`; de itemvraag op de naam (auto-marge) en de prijs (auto-marge in een kolom); de plaatsingsvraag op de badge (het ankerduo). Zonder `aspect-ratio` krijgt elke foto de hoogte van haar eigen verhouding: de espresso (staand) maakt zijn kaart torenhoog, de croissants (panorama) een strookje, en omdat grid-rijen zo hoog worden als hun hoogste cel, rekt de hele rij mee (F5.9, F4.5).

Veelgemaakte fouten: de badge belandt in de hoek van de pagina (F5.1); de zijbalk als `float` of met `position: absolute` in plaats van een area (F5.5); `padding: 0` op álle kaarten en dan de tekst tegen de rand; de foto's met `height` in plaats van `aspect-ratio` (F3.8); `margin-top: auto` op de prijs zonder dat `.tekst` een flex-container is én de kaart vult (de auto-marge heeft restruimte nodig om te verdelen); de streep op de kaarten mét foto omdat `:not()` ontbreekt.

## Thuis: B5.1

Geen modeloplossing: je site is van jou. Waar je zelf op controleert: `body` met `grid-template-areas` en elk gebied benoemd; de navigatie `position: sticky` met `top: 0` en `scroll-padding-top` op `html`; minstens één kaart als anker met een absolute badge en een kleine `z-index`; het drieluik op elke kaartafbeelding; één `:has()`-regel die reageert op echte inhoud; nergens `position` voor structuur, nergens een z-index boven 10.
