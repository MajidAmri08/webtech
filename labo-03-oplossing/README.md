# Labo 3 - Alles is een box: vijf nabouw-opdrachten: modeloplossing

Dit is een mogelijke oplossing van labo 3, niet de enige. Vergelijk ze met je eigen werk: niet om over te nemen, maar om te zien waar jouw CSS afwijkt en of dat erg is. Een andere weg naar hetzelfde screenshot is niet fout; een weg die de regels breekt (een gewijzigde `index.html`, een weggehaalde `reset.css`, px buiten een rand, id-selectors, `!important`) wel. De HTML-bestanden en `reset.css` zijn identiek aan de starter. De verwijzingen (3.2, F3.1) zijn naar de syllabus.

De screenshots zijn gemaakt in een venster van 1280 bij 800 px met Arial en Georgia vervangen door gelijkaardige lettertypes; daarom zien de letters er op jouw computer net iets anders uit. De boxen niet.

## 1. Kleurenstalen

Zie `kleuren/css/stijl.css`. De lijst krijgt `list-style: none`, `padding-left: 0` en `margin: 0`, want `reset.css` laat lijsten bewust met rust (3.3). Elk `li` is een band van `height: 50vh` met `padding-top` in rem om de tekst naar beneden te duwen. De kop heeft `letter-spacing: 0.25rem`, de codes zijn kleiner en de drie stukjes krijgen een horizontale marge op de `span`, want op een inline box werken horizontale marges wel en verticale niet (3.6).

Reflectie: de twee waarden uit de user agent stylesheet zijn de insprong (`padding-left: 40px`) en de bolletjes (`list-style-type: disc`); je leest ze af in het Styles-paneel onder de user agent stylesheet en in het boxmodel-diagram (de groene laag links). Maak je het venster hoger, dan worden de banden hoger, want vh hangt aan het venster; de tekst en de ademruimte erboven veranderen niet, want die staan in rem.

Veelgemaakte fouten: de bolletjes en de insprong vergeten; `height: 50%` in plaats van `50vh` (F3.2: `body` heeft geen hoogte, dus de helft daarvan is niets); de tekst verticaal "centreren" met marges op de `h2`, waarna de marge uit de `li` lekt en de band uitrekt (margin collapsing tussen ouder en kind, motorkap hoofdstuk 3), terwijl padding op de `li` dat probleem niet heeft; `letter-spacing: 0.25` zonder eenheid (F2.8).

## 2. Slogan

Zie `slogan/css/stijl.css`. `body` is de kolom: `width: 80vw`, `max-width: 40rem` en `margin: 12rem auto 0`, dus gecentreerd met `auto` en nooit breder dan 40rem. `text-align: center` centreert de tekst erin. De streep onder *made* is een `border-bottom` van 1rem op de `span`, met `border-radius: 50%` om ze te buigen. De knop is een link met `display: inline-block`, waarna padding, achtergrond en ronde hoeken doen wat je verwacht.

Reflectie: `text-align: center` centreert de tekst, `max-width` plus `margin: ... auto` centreert de kolom zelf (F3.4). De link is inline: een inline box meet zichzelf aan haar inhoud en negeert verticale padding en marges (3.7 en het motorkap-kader); `inline-block` of `block` maakt er één onbreekbare rechthoek van.

Veelgemaakte fouten: `text-align: center` op alles en de kolom staat nog links (F3.4); `width: 50rem` zonder `max-width`, dus geen krimp op een smal venster (3.8); padding op de link zonder `display` (F3.5: horizontaal werkt het, verticaal "doet het raar"); `text-decoration: underline` in geel in plaats van een border (de boog ontbreekt); hover zonder focus (F2.11).

## 3. Tabblad

Zie `tabblad/css/stijl.css`. Twee boxen met een border van 0.25rem, padding en een vaste breedte: het tabblad 15rem, de kaart 35rem. Dankzij `box-sizing: border-box` uit de reset is 15rem de visuele breedte, padding en border inbegrepen (3.2). Het tabblad staat op de kaart omdat zijn onderrand ontbreekt (`border-bottom: 0`). De schaduwen hebben geen vervaging: twee lengtes en een kleur; de kaart heeft er twee, gescheiden door een komma.

Reflectie: 15rem is 240px, en dat is de hele box, omdat `box-sizing: border-box` padding en border ín de width telt. Zonder reset zou het 240 + 2 x 32 + 2 x 4 = 312px zijn (F3.1). Het boxmodel-diagram toont content 176, padding 32, border 4.

Veelgemaakte fouten: een tabblad van 312px omdat `reset.css` niet laadt of is leeggemaakt (F3.1); een schaduw mét vervaging, omdat 3.5 eerst de zachte toont; de tweede schaduw als tweede declaratie in plaats van na een komma, waarna de laatste wint (volgorde, 2.7); een eigen `margin-bottom` op de `h1` "voor de ademruimte", waardoor het tabblad los boven de kaart zweeft.

## 4. Donut

Zie `donut/css/stijl.css`. Alleen `main` krijgt een maat in vh: 90vh breed en hoog, `margin: 5vh auto`. Daarbinnen is alles een percentage van de ouder: de cirkel is 70% breed en hoog met `margin: 15%` en `border-radius: 50%`, en `overflow: hidden` snijdt af wat buiten de cirkel valt. Het gele vierkant is 90% van de cirkel, geschoven met `margin: -7% 0 0 -7%`, met `padding-top: 40%` om het woord naar het midden te duwen.

De rekensom, voor wie ze wil nakijken: main content is 720 - 2 x 12 = 696px; de cirkel is 70% daarvan, 487,2px, met 15% marge, 104,4px, en 104,4 + 487,2 + 104,4 = 696. De content van de cirkel is 487,2 - 24 = 463,2px; het vierkant is 90% daarvan, de marge -7% en de padding 40%, allemaal tegen die breedte.

Reflectie: `height: 70%` werkt omdat de ouder (`main`) een echte hoogte heeft, 90vh; F3.2 gaat over een ouder met auto-hoogte. `margin: 15%` rekent tegen de breedte van de ouder-content, ook boven en onder: het Computed-tabblad toont 104,4px voor alle vier de zijden (3.2).

Veelgemaakte fouten: `height: 70%` doet niets omdat `90vh` alleen op `width` staat; marges in vh of rem "omdat procenten niet klopten" (ze klopten, ze rekenden tegen de breedte); `overflow: hidden` vergeten, het gele vierkant steekt uit de cirkel; `margin: -7%` op alle vier de zijden, waardoor de box ook rechts en onder verschuift en breder wordt dan de cirkel; `border-radius: 50%` op `main` in plaats van op de cirkel.

## 5. Landingspagina

Zie `landing/css/stijl.css`. De banner en de header zijn gewone blokken met padding; de navigatie is een lijst zonder bolletjes waarvan elk `li` `display: inline-block` is, rechts gezet met `text-align` op de header. `main` heeft `min-height: 80vh`, geen `height`. De twee helften zijn `inline-block` met `width: 50%` en `vertical-align: top`; de afbeelding is 70% van haar helft. De knop is een `inline-block` link met padding en ronde hoeken.

Reflectie: `min-height`, want een ondergrens vult de hero en laat de inhoud groeien (3.8, F3.10). Een regeleinde tussen `</article>` en `<div class="afbeelding">` is voor inline-block een spatie: 50% plus een spatie plus 50% past niet op één regel, en de tweede helft valt eronder (3.7). Dat is precies de reden dat hoofdstuk 4 flexbox en grid brengt.

Veelgemaakte fouten: `height: 80vh` op `main` (werkt in het screenshot, F3.10 zodra de tekst langer wordt); de tweede helft valt onder de eerste omdat een van beide padding heeft en de reset ontbreekt (F3.1); `vertical-align: top` vergeten, waardoor de afbeelding lager hangt dan de tekst; de afbeelding met width én height gezet (F3.8); hover zonder focus (F2.11).

## Thuis: B3.1

Geen modeloplossing: je site is van jou. Waar je zelf op controleert: `reset.css` uit de template in `site/css/`, op elke pagina gelinkt vóór `stijl.css`; een leeskolom met `max-width` en `margin: 0 auto`, geen vaste `width`; minstens drie kaartjes met padding, `border-radius` en een zachte schaduw (3.5); spacing via tokens en alleen `margin-bottom`; nergens een `height` op een element met tekst erin.
