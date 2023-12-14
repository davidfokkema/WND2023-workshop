---
hide:
  - navigation
---

# Workshop: model-leren begint met een experiment

Als je _Tailor_ nog niet hebt geïnstalleerd volg dan [deze instructies](#installatie-instructies-voor-tailor).


## De beweging van een slinger meten met een ultrasone afstandssensor

!!! abstract "Leerdoel"
    Ervaar Tailor's intuïtieve interface voor het veranderen van beginwaardes van parameters en het visualiseren van hun fysische betekenis in het model.

Voor periodieke functies kan het lastig zijn om de beginwaardes van parameters als de frequentie of de amplitude zodanig te kiezen dat het model goed fit aan de datapunten. Met veel programma's is dit een kwestie van blijven proberen tot het lukt. Daarbij helpt het om goed naar de metingen te kijken en door bijvoorbeeld toppen te tellen en af te lezen de frequentie te schatten. Tailor kan een initiële fit laten zien in een lichtblauwe kleur. Wanneer beginwaardes worden veranderd past de curve zich automatisch aan. Je kunt daarvoor een nieuwe waarde intypen in het tekstveld, de pijltjes naast het veld gebruiken om hogere of lagere waardes te kiezen, of door met de muiscursor in het tekstveld te scrollen. Vooral die laatste manier is heel intuïtief en laat prachtig zien wat de invloed van de verschillende parameters is op het fysisch model.


!!! exercise
    Importeer het :fontawesome-solid-file-csv:`pendulum-USD.csv`-bestand in een leeg project. Verander de kolomnamen als je dat fijn vindt. Maak een afstand-tijd-grafiek en fit aan een geschikt model, bijvoorbeeld:
    $$
    s = s_0 + A \sin(2\pi f t + \phi),
    $$
    waar afstand $s$ en tijd $t$ gelijk moeten zijn aan de namen van de datakolommen. Probeer te fitten met de standaardwaardes van het model; dat geeft waarschijnlijk geen goed resultaat. Speel nu een beetje met de waardes; het kan zijn dat je `Show initial fit` weer even aan moet vinken. Hoe verandert het model als je een parameter aanpast? Probeer een goede fit te krijgen.

    Bestanden:

    * [:fontawesome-solid-file-csv: pendulum-USD.csv](data/pendulum-USD.csv)


## Röntgenfluorescentie

!!! abstract "Leerdoel"
    In deze oefening zul je zien dat Tailor geen beperkingen heeft op welk model je wilt fitten. Je kunt complexe modellen fitten, zoals bijvoorbeeld _multipeak_-modellen. Deze vrijheid kent één nadeel: je moet je model heel precies invoeren.

Tailor heeft geen bibliotheek van ingebouwde modellen. Elk model dat je wilt gebruiken zul je zelf expliciet in moeten vullen in het tekstveld. Dit maakt Tailor wel heel flexibel. Waar applicaties als _Excel_ slechts een handjevol modellen kunnen fitten, kunnen meer geavanceerde applicaties als _Origin Pro_ daarnaast ook zogenaamde _user-defined_ modellen gebruiken. Dat onderscheid maakt de gebruikersinterface ingewikkelder. Bovendien kan het gebruik van ingebouwde modellen leerlingen een beetje lui maken. Ze kiezen model na model tot er iets mooi fit aan de metingen zonder dat ze goed begrijpen welke natuurkunde hier achterzit. Met Tailor moeten leerlingen zelf nadenken over welke formule uit Binas ze willen gebruiken als model en deze expliciet invullen.

!!! exercise
    The :fontawesome-solid-file-csv:`X-ray.csv` file contains data of an X-ray fluorescence experiment. Import it into a clean project and try to fit a peak model of your choice to determine the energy of the peak. Do you actually need to use a model that gives a good fit if you're only interested in the peak energy? Don't forget to include the uncertainties. Try to do the same with the :fontawesome-solid-file-csv:`X-ray-invar.csv` data file using a multi-peak model.

    Data files:

    * [:fontawesome-solid-file-csv: X-ray.csv](data/X-ray.csv)
    * [:fontawesome-solid-file-csv: X-ray-invar.csv](data/X-ray-invar.csv)


## Photovoltaic cell

!!! abstract "Learning goal"
    Learn to work with _calculated columns_ to let Tailor calculate additional physical quantities &mdash; including uncertainties &mdash; derived from the observed quantities.

One of the key features of Tailor is the ability to work with calculated columns. It is very simple: a single function specifies the values for the full column. You can use the names of other columns as variables in the function. So, for instance, if you have two columns with the quantities _time_ $t$ and _velocity_ $s$, you can create a new calculated column _distance_ $s$ using:
$$
s = vt.
$$
Mind that all calculations are performed from left to right, so you can only use variables of columns defined _before_, or _to the left_, of the current column. Don't worry though, you can reorder columns by dragging their header to the left or right. In this exercise, we will use data of the performance of a photovoltaic cell that was collected during our _Experiment Control with Python Course_. Annelies Vlaar will present a poster on that subject during the poster session.

!!! exercise
    Import the :fontawesome-solid-file-csv:`pvcell.csv` data file into a clean project. Here, $U_0$ is a control voltage[^voltage] used to vary the load on the photovoltaic cell. It has no simple relation to the precise value of the load and may be ignored. $U_1$ is the voltage across the photovoltaic cell and $U_2$ is the voltage across a 4.7 Ω shunt resistor in series with the load. Define new calculated columns to determine values for the current through the circuit and preferably its uncertainty. Inspect the relation of current versus voltage and, if you have time, fit the simplified model derived from the Shockley equation:
    $$
    I = I_\text{L} - I_0\left[\exp\left(\frac{U}{nU_\text{T}}\right) - 1\right],
    $$
    with the current $I$, the photogenerated current $I_\text{L}$, the reverse saturation current $I_0$, the voltage across the PV cell $U$, and the thermal voltage $U_\text{T} = \frac{kT}{q}$.

    Data files:

    * [:fontawesome-solid-file-csv: pvcell.csv](data/pvcell.csv)

    [^voltage]: The use of $U$ instead of $V$ for voltage seems to be a US/European difference of opinion. Sorry about that.

## Cart moving down a frictionless track

!!! abstract "Learning goal"
    In this exercise you will learn some tricks to perform a repeated analysis on a second measurement with just a few clicks. Also, you will fit a model to only a part of your data.

It is not uncommon to perform a measurement, do a full analysis, and then want to redo that analysis on a second dataset. Since Tailor updates calculated columns and plots when data changes, this need not be hard. Simply save your project under a new name &mdash; for example appending `-dataset-2` to the name &mdash; and enter the data of the new measurement in place of the old. Even better, when using computer-controlled measurements, import the new CSV file. Tailor will overwrite columns with the same name. You then simply have to switch over to the plot and click the `(Re)Fit model` button.

It is important to realize that if you had renamed your data columns Tailor will be confused as to which columns to overwrite. Tailor will add new data columns _before_ other data columns in your sheet and will not overwrite other columns. The best approach in such cases is not to rename columns but to add a new calculated column with the desired name and the original name as its formula. The data will be copied to the new column and you can use the desired names in your plots and model functions. Importing a new dataset will overwrite the original columns and these values will again be copied over to the other columns.[^copied-columns]

[^copied-columns]: You can ask help if this part was confusing.

Often, when performing computer measurements, it is difficult to let the measurements start and end at the exact times you perform the experiment. In that case you want to fit only part of your data. You can select `Use domain` on the plot tab and specify precise start and end values or drag the edges of the blue region to match the data.

!!! exercise
    Import the :fontawesome-solid-file-csv:`cart-dataset1.csv` and create new columns to define short-hand names for the time and position columns. Call them $t$ and $s$, for example. Add a column to define a value of 0.005 for the uncertainty $\delta s$. Plot $s$ versus $t$ and fit a constant-velocity model to the straight part of the data. Save your project twice under different names for dataset 1 _and_ dataset 2 &mdash; to avoid accidentally overwriting results of the first analysis. Now you can import the second dataset choosing `Don't Save` when warned about losing changes. If all went well, you now only have to adjust the fit domain and redo the fit to obtain new results for the seconds dataset. Save the project again[^save] to commit the new data and results to the project for dataset 2.

    [^save]: Using `Save`, not `Save As`.

    Data files:

    * [:fontawesome-solid-file-csv: cart-dataset1.csv](data/cart-dataset1.csv)
    * [:fontawesome-solid-file-csv: cart-dataset2.csv](data/cart-dataset2.csv)

## Examenopdracht 2023-I: Boomwhackers
!!! abstract "Leerdoel"
    Gebruik Tailor om een examenopdracht uit te voeren. 

In examenopdrachten wordt data gepresenteerd wat gekoppeld is aan een experiment. Met behulp van Tailor kunnen studenten leren deze data te verwerken. We laten dit zien aan de hand van de [examenopdracht Boomwhackers uit 2023 tijdvak 1](https://www.examenblad.nl/system/files/2023/ex2023/VW-1023-a-23-1-o.pdf)

!!! opdracht
    ### Akoestische lengte
    Boomwhackers zijn plastic buizen met aan beide kanten een opening waarmee je muziek kunt maken. Wanneer je een boomwhacker ergens tegenaan tikt, produceert dit geluid door de trillingen (staande golven) in de buis. Hoe lang de buis is, bepaalt welke toonhoogte er klinkt.
    
    Wanneer de grondtoon en boventonen van een buis worden gemeten, tonen deze kleine afwijkingen ten opzichte van de verwachte resultaten op basis van de buislengte. Dit verschil ontstaat doordat de knopen niet precies samenvallen met de uiteinden van de buis. De afstand tussen de knopen aan beide uiteinden van de buis staat bekend als de akoestische lengte. Deze akoestische lengte is dus bepalend voor de toonhoogte. 

    De akoestische lengte wordt gegeven door:
    $$
    L_a = L + 2 * 0.31 * d,
    $$
    met $L_a$ de akoestische lengte van de buis in m, $L$ de werkelijke lengte van de buis in m, $0.31$ een experimenteel bepaalde correctiefactor, $d$ de binnendiameter van de buis in m, $2$ het aantal open uiteinde van de buis. 

    1. Leg uit met behulp van bovenstaande formule of de buiken aan de uiteinden van de buis binnen of buiten de buis vallen.

    ### Golflengte bepalen
    De frequenties van de grondtoon van elke buis en de bijbehorende lengtes van de buizen zijn gegeven in :fontawesome-solid-file-csv:`boomwhackers_2023_1.csv`, de binnendiameter van de buizen blijkt na meting 4,0 cm te zijn.


    1. Importeer het [:fontawesome-solid-file-csv: boomwhackers_2023_1.csv](data/boomwhackers_2023_1.csv)-bestand in een leeg project.
    1. Bepaal de golflengte van de grondtoon op basis van de lengte van de buizen en zet deze in een aparte kolom in het Tailor project. 
    
    ### Meetonnauwkeurigheid toevoegen
    De meetonnauwkeurigheid op de frequentie is $2*10^1$ Hz. 
    
    1. Voeg deze meetonnauwkeurigheid als een aparte kolom toe in het Tailor project.
    1. Maak een afschatting van de meetonnauwkeurigheid op de golflengte en voeg deze toe in het Tailor project.
    
    ### Frequentie uitzetten tegen de golflengte
    1. Maak een plot met op de x-as de golflengte en de bijbehordende meetonnauwkeurigheid en op de y-as de frequentie inclusief meetonnauwkeurigheid. 
    1. Geef de assen correcte titels met grootheid en eenheid. Pas het bereik van de plot aan zodat de oorsprong zichtbaar is. 

    ### Bepaal de geluidsnelheid
    Met behulp van deze data is het mogelijk om de geluidsnelheid te bepalen. Daarvoor hebben we een model nodig die de data goed beschrijft. 

    1. Met welk model kan de geluidsnelheid bepaald worden uit de plot? Vul in Tailor het model in. Gebruik 'v' als symbool voor de geluidsnelheid in het model. 
    1. Geef onder het kopje 'Starting values and parameters bounds' aan wat redelijke waardes zijn voor de geluidsnelheid. Het linkervakje geeft de ondergrens aan, het middelste vakje is voor de verwachte waarde en het rechtervakje is voor de bovengrens.
    1. Klik op (Re)Fit model om te zien welke waarde voor de geluidsnelheid het beste bij deze data past. Welke waarde wordt gegeven onder het kopje 'Fit parameters' in het blokje 'Information'?

    ### Lineariseren
    Van een rechte fit-lijn is het makkelijker om te zien hoe goed die bij de datapunten past (of niet) dan van een kromme lijn. Daarom willen we het gebruikte model omschrijven naar de vorm:

    $$
    f = iets*v,
    $$

    met f de frequentie in Hz en v de geluidsnelheid in m/s.

    1. Wat is $iets$ in ons geval?
    1. Maak in Tailor een nieuwe kolom en zet de data om zodat je een rechte lijn kunt trekken over de datapunten. 
    1. Maak een nieuwe plot met op de x-as de omgezette data en op de y-as de frequentie. 
    1. Vul het nieuwe model in en klik op 'Show initial fit'.
    1. Vul voor de startwaarde van de geluidsnelheid een verwachte waarde in. 
    1. Scroll in het vakje voor de startwaarde van de geluidsnelheid om de startwaarde aan te passen. Kijk naar de verandering van de blauwe lijn, wat is de minimale waarde en de maximale waarde die je voor de geluidsnelheid uit deze data kan verwachten?

    Bestanden:

    * [:fontawesome-solid-file-csv: boomwhackers_2023_1.csv](data/boomwhackers_2023_1.csv)


## Extras

!!! exercise
    Can you determine the half-life of radon-220 using measurements of the activity of a freshly obtained sample of radon?

    Data files:

    * [:fontawesome-solid-file-csv: radon220.csv](data/radon220.csv)


## Installatie-instructies voor Tailor

The repository for Tailor can be found at [GitHub](https://github.com/davidfokkema/tailor) and the latest release can be downloaded [here](https://github.com/davidfokkema/tailor/releases/latest). Links to the individual binary installers:

* [Windows](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0.msi)
* [Intel Macs (older Macs)](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0_intel.dmg)
* [Apple Silicon (newer Macs)](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0_apple_silicon.dmg)

This document contains several exercises to explore the features of Tailor and experience its ease-of-use. Special care was given to try and showcase those features which make Tailor ideally suited for data analysis in an educational setting. All analysis tools should incur only low cognitive load and should ideally be directly usable without reading a long manual.