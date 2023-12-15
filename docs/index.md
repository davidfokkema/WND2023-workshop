---
hide:
  - navigation
---

# Workshop: model-leren begint met een experiment

Op deze webpagina vind je verschillende opdrachten om metingen te vergelijken met modellen. Hierbij komen verschillende mogelijkheden van Tailor voorbij waarbij we zoveel mogelijk hebben geprobeerd om aan te sluiten bij de onderwijspraktijk van practica en praktische opdrachten. We hebben Tailor ook gebruikt tijdens het begeleiden van profielwerkstukken &mdash; meest recent drie leerlingen die op de VU verschillende metingen gedaan hebben met een Michelsoninterferometer.

Als je _Tailor_ nog niet hebt geïnstalleerd volg dan [deze instructies](#installatie-instructies-voor-tailor).


## De halfwaardetijd van radon-220 bepalen

!!! abstract "Leerdoel"
    Echte metingen zijn vaak minder _mooi_ dan het verhaal in het boek.

Tekstje over echte metingen waar je last hebt van andere effecten die je mee moet nemen in je model of het domein waarover je fit.

!!! opdracht
    Bepaal de halfwaardetijd van radon-220. Maak daarbij gebruik van de gemeten activiteit van een pas verkregen monster van radon.

    Bestanden:

    * [:fontawesome-solid-file-csv: radon220.csv](data/radon220.csv)


## Examenopdracht 2023-I: Boomwhackers
!!! abstract "Leerdoel"
    Gebruik Tailor om een examenopdracht uit te voeren. 

!!! abstract "Berekeningen doen met Tailor"
    Eén van de belangrijkste mogelijkheden van Tailor is het werken met _calculated columns_. Het idee is eenvoudig: één wiskundige vergelijking berekent de waardes van de hele kolom. Je kunt de namen van andere kolommen gebruiken als variabelen in je functie. Als je bijvoorbeeld twee kolommen met de grootheden _tijd_ $t$ en _snelheid_ $v$ hebt dan kun je een nieuwe kolom _afstand_ $s$ definiëren met de functie:
    $$
    s = vt.
    $$
    De notatie die in Tailor gebruikt wordt is dezelfde als in Python. Je zult de vergelijking $vt$ in moeten vullen als: `v * t` en machten als $x^2$ als: `x ** 2`. Let op: alle kolommen worden van links naar rechts doorgerekend. Je kunt dus alleen variabelen gebruiken van kolommen die _eerder_, dus _links_, van je huidige kolom staan. Maar maak je geen zorgen: je kunt de volgorde van kolommen eenvoudig wijzigen door de kolomkoppen naar links of rechts te slepen. 

In examenopdrachten wordt data gepresenteerd wat gekoppeld is aan een experiment. Met behulp van Tailor kunnen studenten leren deze data te verwerken. We laten dit zien aan de hand van de [examenopdracht Boomwhackers uit 2023 tijdvak 1](https://www.examenblad.nl/system/files/2023/ex2023/VW-1023-a-23-1-o.pdf)

!!! opdracht
    ### Akoestische lengte
    Boomwhackers zijn plastic buizen met aan beide kanten een opening waarmee je muziek kunt maken. Wanneer je een boomwhacker ergens tegenaan tikt, produceert dit geluid door de trillingen (staande golven) in de buis. Hoe lang de buis is, bepaalt welke toonhoogte er klinkt.
    
    Wanneer de grondtoon en boventonen van een buis worden gemeten, tonen deze kleine afwijkingen ten opzichte van de verwachte resultaten op basis van de buislengte. Dit verschil ontstaat doordat de knopen niet precies samenvallen met de uiteinden van de buis. De afstand tussen de knopen aan beide uiteinden van de buis staat bekend als de akoestische lengte. Deze akoestische lengte is dus bepalend voor de toonhoogte. 

    De akoestische lengte wordt gegeven door:
    $$
    L_a = L + 2 \cdot 0.31 \cdot d,
    $$
    met $L_a$ de akoestische lengte van de buis in m, $L$ de werkelijke lengte van de buis in m, $0.31$ een experimenteel bepaalde correctiefactor, $d$ de binnendiameter van de buis in m, $2$ het aantal open uiteinde van de buis. 

    1. Leg uit met behulp van bovenstaande formule of de buiken aan de uiteinden van de buis binnen of buiten de buis vallen.

    ### Golflengte bepalen
    De frequenties van de grondtoon van elke buis en de bijbehorende lengtes van de buizen zijn gegeven in :fontawesome-solid-file-csv:`boomwhackers_2023_1.csv`, de binnendiameter van de buizen blijkt na meting 4,0 cm te zijn.


    1. Importeer het [:fontawesome-solid-file-csv: boomwhackers_2023_1.csv](data/boomwhackers_2023_1.csv)-bestand in een leeg project.
    1. Bepaal de golflengte van de grondtoon op basis van de lengte van de buizen en zet deze in een aparte kolom in het Tailor project. 
    
    ### Meetonnauwkeurigheid toevoegen
    De meetonnauwkeurigheid op de frequentie is $2 \cdot 10^1$ Hz. 
    
    1. Voeg deze meetonnauwkeurigheid als een aparte kolom toe in het Tailor project.
    1. Maak een afschatting van de meetonnauwkeurigheid op de golflengte en voeg deze toe in het Tailor project.
    
    ### Frequentie uitzetten tegen de golflengte
    1. Maak een plot met op de x-as de golflengte en de bijbehorende meetonnauwkeurigheid en op de y-as de frequentie inclusief meetonnauwkeurigheid. 
    1. Geef de assen correcte titels met grootheid en eenheid. Pas het bereik van de plot aan zodat de oorsprong zichtbaar is. 

    ### Bepaal de geluidsnelheid
    Met behulp van deze data is het mogelijk om de geluidsnelheid te bepalen. Daarvoor hebben we een model nodig die de data goed beschrijft. 

    1. Met welk model kan de geluidsnelheid bepaald worden uit de plot? Vul in Tailor het model in. Gebruik 'v' als symbool voor de geluidsnelheid in het model. 
    1. Geef onder het kopje `Starting values and parameters bounds` aan wat redelijke waardes zijn voor de geluidsnelheid. Het linkervakje geeft de ondergrens aan, het middelste vakje is voor de verwachte waarde en het rechtervakje is voor de bovengrens.
    1. Klik op `(Re)Fit model` om te zien welke waarde voor de geluidsnelheid het beste bij deze data past. Welke waarde wordt gegeven onder het kopje `Fit parameters` in het blokje `Information`?

    ### Lineariseren
    Van een rechte fit-lijn is het makkelijker om te zien hoe goed die bij de datapunten past (of niet) dan van een kromme lijn. Daarom willen we het gebruikte model omschrijven naar de vorm:

    $$
    f = \text{iets} \cdot v,
    $$

    met f de frequentie in Hz en v de geluidsnelheid in m/s.

    1. Wat is $iets$ in ons geval?
    1. Maak in Tailor een nieuwe kolom en zet de data om zodat je een rechte lijn kunt trekken over de datapunten. 
    1. Maak een nieuwe plot met op de x-as de omgezette data en op de y-as de frequentie. 
    1. Vul het nieuwe model in en klik op `Show initial fit`.
    1. Vul voor de startwaarde van de geluidsnelheid een verwachte waarde in. 
    1. Scroll in het vakje voor de startwaarde van de geluidsnelheid om de startwaarde aan te passen. Kijk naar de verandering van de blauwe lijn, wat is de minimale waarde en de maximale waarde die je voor de geluidsnelheid uit deze data kan verwachten?

    Bestanden:

    * [:fontawesome-solid-file-csv: boomwhackers_2023_1.csv](data/boomwhackers_2023_1.csv)


## De beweging van een slinger meten met een ultrasone afstandssensor

!!! abstract "Leerdoel"
    Een afstandsdetector is een mooi hulpmiddel tijdens een praktische opdracht. Periodieke functies zijn echter vaak lastig te fitten _en_ leerlingen hebben vaak moeite met wat de verschillende parameters in het model betekenen. Visualiseren en uitproberen helpt daarbij!

Voor periodieke functies kan het lastig zijn om de beginwaardes van parameters als de frequentie of de amplitude zodanig te kiezen dat het model goed fit aan de datapunten. Met veel programma's is dit een kwestie van blijven proberen tot het lukt. Daarbij helpt het om goed naar de metingen te kijken en door bijvoorbeeld toppen te tellen en af te lezen de frequentie te schatten. Tailor kan een initiële fit laten zien in een lichtblauwe kleur. Wanneer beginwaardes worden veranderd past de curve zich automatisch aan. Je kunt daarvoor een nieuwe waarde intypen in het tekstveld, de pijltjes naast het veld gebruiken om hogere of lagere waardes te kiezen, of door met de muiscursor in het tekstveld te scrollen. Vooral die laatste manier is heel intuïtief en laat prachtig zien wat de invloed van de verschillende parameters is op het fysisch model.

!!! opdracht
    Importeer het :fontawesome-solid-file-csv:`pendulum-USD.csv`-bestand in een leeg project. Verander de kolomnamen als je dat fijn vindt. Maak een afstand-tijd-grafiek en fit aan een geschikt model, bijvoorbeeld:
    $$
    s = s_0 + A \sin(2\pi f t + \phi),
    $$
    waar afstand $s$ en tijd $t$ gelijk moeten zijn aan de namen van de datakolommen. Probeer te fitten met de standaardwaardes van het model; dat geeft waarschijnlijk geen goed resultaat. Speel nu een beetje met de waardes; het kan zijn dat je `Show initial fit` weer even aan moet vinken. Hoe verandert het model als je een parameter aanpast? Probeer een goede fit te krijgen.

    Bestanden:

    * [:fontawesome-solid-file-csv: pendulum-USD.csv](data/pendulum-USD.csv)


## Karretje over een wrijvingslozebaan

!!! abstract "Leerdoel"
    De wrijvingsloze baan &mdash; of _luchtkussenbaan_ &mdash; is in veel scholen wel te vinden, maar hoe ga je om met een beweging die _niet_ bij $t = 0$ start? Als je meer dan één dataset moet analyseren kan het handig zijn om niet alles steeds opnieuw te doen.

!!! abstract "Eventueel: meerdere datasets analyseren"
    In de praktijk wordt vaak een meting uitgevoerd en de data volledig geanalyseerd, waarna dezelfde analyse wordt toegepast op een tweede dataset. Omdat Tailor de 'calculated columns' en plots herlaad wanneer de data veranderd kunnen we deze handelingen snel in Tailor uitvoeren. Doe dit door het project onder een nieuwe naam op te slaan &mdash; door bijvoorbeeld `-dataset-2` aan de naam toe te voegen &mdash; en vervolgens de data van de oude meting te vervangen door de nieuwe dataset. Wanneer het data betreft van een computer gestuurde meeting is dit helemaal eenvoudig door het nieuwe CSV-bestand te importeren. Tailor zal in dat geval de kolommen met dezelfde naam overschrijven. Klik dan op `(Re)Fit model` in de plot en de resultaten voor de nieuwe meting zijn bekend. 

    Bij het importeren van data vanuit een CSV-bestand kan het voorkomen dat de kolomnamen niet handig dan wel logisch zijn. Het lijkt eenvoudig om dan de kolomnamen aan te passen, maar dit geeft problemen wanneer een nieuwe dataset wordt geïmporteerd in het oude project. Tailor zal de oude data niet overschrijven omdat de kolomnamen in de datasheet niet overeenkomen met de kolomnamen in het CSV-bestand. In plaats daarvan zal Tailor de nieuwe datakolommen toevoegen _voor_ de andere datakolommen. Met als gevolg dat er twee datasets in het project staan en de analyse niet automatisch wordt uitgevoerd op de nieuwe data. Daarom is het handig om de kolomnamen niet aan te passen maar om een nieuwe `calculated column` toe te voegen met de nieuwe naam en een verwijzing naar de originele naam als formule. De data wordt daarmee gekopieerd naar de nieuwe kolom en de nieuwe naam kan gebruikt worden in de plots en model functies. [^copied-columns]

    [^copied-columns]: Het is wellicht wat verwarrend, schroom niet om ons om hulp te vragen als het niet meteen duidelijk is.

Bij het uitvoeren van een computer gestuurde meting is het vaak lastig om het experiment precies op hetzelfde moment te laten starten en eindigen. Met als gevolg de fit uitgevoerd moet worden op slechts een gedeelte van de data. In de plot tab kan je daarvoor `Use domain` selecteren en daarbij het domein aangeven of door de randen van de blauwe vlak te slepen om de data te selecteren. Ook zul je in met model een passing moeten doen zodat de meting niet op $t = 0$ hoeft te beginnen.

!!! opdracht
    Importeer het :fontawesome-solid-file-csv:`cart-dataset1.csv`-bestand en voeg eventueel nieuwe kolommen toe om afkortingen te definiëren voor de tijd en positie kolommen. Geef de nieuwe kolommen als naam $t$ and $s$. Voeg een kolom toe met 0.005 als meetonnauwkeurigheid voor $\delta s$. Plot $s$ tegen $t$ en fit een model voor constante snelheid aan het rechte deel van de data. Sla het bestand twee keer op onder verschillende namen voor dataset 1 _en_ dataset 2 &mdash; om te voorkomen dat de resultaten van de eerste analyse per ongeluk worden overschreven. Importeer nu de tweede dataset en kies voor `Don't Save` wanneer een waarschuwing verschijnt over het verliezen van wijzigingen. Als alles goed gegaan is hoeft in de plot alleen het fit domein aangepast te worden en de fit opnieuw uitgevoerd om de resultaten voor de tweede dataset te verkrijgen. Sla het project opnieuw[^save] op om de nieuwe data en resultaten voor dataset 2 te bewaren. 

    [^save]: Gebruik nu `Save`, in plaats van `Save As`.

    Bestanden:

    * [:fontawesome-solid-file-csv: cart-dataset1.csv](data/cart-dataset1.csv)
    * [:fontawesome-solid-file-csv: cart-dataset2.csv](data/cart-dataset2.csv)


## Extra

### Fotovoltaïsche cel (zonnecel)

!!! abstract "Leerdoel"
    Soms meet je niet direct waarin je geïnteresseerd bent maar moet je de interesante grootheden afleiden uit je metingen. De zonnecel is welbekend, maar gedraagt zich _niet_ als een spanningsbron en _ook niet_ als een stroombron &mdash; lastig, maar leuk voor een profielwerkstuk!

In deze opdracht maken we gebruik van metingen die uitgevoerd zijn aan een fotovoltaïsche cel in het kader van onze [_Experiment Control with Python Course_](https://natuurkundepracticumamsterdam.github.io/ecpc/).

!!! opdracht
    Importeer het :fontawesome-solid-file-csv:`pvcell.csv`-bestand in een leeg project. De kolom $U_0$ is een stuurspanning die gebruikt wordt om de belasting[^belasting] van de fotovoltaïsche cel te variëren. Er is geen exacte relatie tussen de waarde van $U_0$ en de waarde van de belastingsweerstand en deze kolom mag je negeren. $U_1$ is de spanning over de fotovoltaïsche cel en $U_2$ is de spanning over een 4.7 Ω weerstand die in serie staat met de belasting. Maak nieuwe _calculated columns_ om de stroomsterkte door het circuit te berekenen en liefst ook de onzekerheid daar op &mdash; dit laatste is echter geen middelbare school-stof. Plot de relatie tussen de stroomsterkte en de spanning en probeer het volgende model te fitten, afgeleid van de Shockley vergelijking:
    $$
    I = I_\text{L} - I_0\left[\exp\left(\frac{U}{nU_\text{T}}\right) - 1\right],
    $$
    met de stroomsterkte $I$, the fotostroom $I_\text{L}$, de sperverzadigingsstroom $I_0$, de spanning over de fotovoltaïsche cel $U$, en de thermische spanning $U_\text{T} = \frac{kT}{q}$.

    Bestanden:

    * [:fontawesome-solid-file-csv: pvcell.csv](data/pvcell.csv)

    [^belasting]: Wanneer je een apparaat of, in dit geval, een weerstand aansluit op een spanningsbron dan _belast_ je de spanningsbron.


### Röntgenfluorescentie

!!! abstract "Leerdoel"
    In deze oefening zul je zien dat Tailor geen beperkingen heeft op welk model je wilt fitten. Je kunt complexe modellen fitten, zoals bijvoorbeeld _multipeak_-modellen. Deze vrijheid kent één nadeel: je moet je model heel precies invoeren.

Tailor heeft geen bibliotheek van ingebouwde modellen. Elk model dat je wilt gebruiken zul je zelf expliciet in moeten vullen in het tekstveld. Dit maakt Tailor wel heel flexibel. Waar applicaties als _Excel_ slechts een handjevol modellen kunnen fitten, kunnen meer geavanceerde applicaties als _Origin Pro_ daarnaast ook zogenaamde _user-defined_ modellen gebruiken. Dat onderscheid maakt de gebruikersinterface ingewikkelder. Bovendien kan het gebruik van ingebouwde modellen leerlingen een beetje lui maken. Ze kiezen model na model tot er iets mooi fit aan de metingen zonder dat ze goed begrijpen welke natuurkunde hier achterzit. Met Tailor moeten leerlingen zelf nadenken over welke formule uit Binas ze willen gebruiken als model en deze expliciet invullen.

!!! opdracht
    Het :fontawesome-solid-file-csv:`X-ray.csv`-bestand bevat metingen van een röntgenfluorescentie-experiment. Importeer het bestand in een leeg project and probeer een piekmodel van jouw keuze aan de metingen te fitten met het doel de energie van de piek te bepalen. Moet je per sé een model gebruiken die helemaal past als je alleen maar in de energie geïnteresseerd bent? Vergeet niet na te denken over de onzekerheid op de metingen. Probeer hetzelfde te doen voor het :fontawesome-solid-file-csv:`X-ray-invar.csv`-bestand met een _multipeak_-model.

    Bestanden:

    * [:fontawesome-solid-file-csv: X-ray.csv](data/X-ray.csv)
    * [:fontawesome-solid-file-csv: X-ray-invar.csv](data/X-ray-invar.csv)


## Installatie-instructies voor Tailor

Tailor is als repository te vinden op [GitHub](https://github.com/davidfokkema/tailor) en de laatste versie kan [hier](https://github.com/davidfokkema/tailor/releases/latest) gedownload worden. Links naar de verschillende installatieprogramma's:

* [Windows](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0.msi)
* [Intel Macs (oudere Macs)](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0_intel.dmg)
* [Apple Silicon (Macs met M1-processor of nieuwer)](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0_apple_silicon.dmg)

