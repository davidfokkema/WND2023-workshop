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


!!! opdracht
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

!!! opdracht
    Het :fontawesome-solid-file-csv:`X-ray.csv`-bestand bevat metingen van een röntgenfluorescentie-experiment. Importeer het bestand in een leeg project and probeer een piekmodel van jouw keuze aan de metingen te fitten met het doel de energie van de piek te bepalen. Moet je per sé een model gebruiken die helemaal past als je alleen maar in de energie geïnteresseerd bent? Vergeet niet na te denken over de onzekerheid op de metingen. Probeer hetzelfde te doen voor het :fontawesome-solid-file-csv:`X-ray-invar.csv`-bestand met een _multipeak_-model.

    Bestanden:

    * [:fontawesome-solid-file-csv: X-ray.csv](data/X-ray.csv)
    * [:fontawesome-solid-file-csv: X-ray-invar.csv](data/X-ray-invar.csv)


## Fotovoltaïsche cel (zonnecel)

!!! abstract "Leerdoel"
    Maak kennis met _calculated columns_ om Tailor extra fysische grootheden uit te laten rekenen &mdash; inclusief onzekerheden &mdash; die afgeleid zijn van gemeten grootheden.

Eén van de belangrijkste mogelijkheden van Tailor is het werken met _calculated columns_. Het idee is eenvoudig: één wiskundige vergelijking berekent de waardes van de hele kolom. Je kunt de namen van andere kolommen gebruiken als variabelen in je functie. Als je bijvoorbeeld twee kolommen met de grootheden _tijd_ $t$ en _snelheid_ $v$ hebt dan kun je een nieuwe kolom _afstand_ $s$ definiëren met de functie:
$$
s = vt.
$$
De notatie die in Tailor gebruikt wordt is dezelfde als in Python. Je zult de vergelijking $vt$ in moeten vullen als: `v * t` en machten als $x^2$ als: `x ** 2`. Let op: alle kolommen worden van links naar rechts doorgerekend. Je kunt dus alleen variabelen gebruiken van kolommen die _eerder_, dus _links_, van je huidige kolom staan. Maar maak je geen zorgen: je kunt de volgorde van kolommen eenvoudig wijzigen door de kolomkoppen naar links of rechts te slepen. In deze opdracht maken we gebruik van metingen die uitgevoerd zijn aan een fotovoltaïsche cel in het kader van onze [_Experiment Control with Python Course_](https://natuurkundepracticumamsterdam.github.io/ecpc/).

!!! opdracht
    Importeer het :fontawesome-solid-file-csv:`pvcell.csv`-bestand in een leeg project. De kolom $U_0$ is een stuurspanning die gebruikt wordt om de belasting[^belasting] van de fotovoltaïsche cel te variëren. Er is geen exacte relatie tussen de waarde van $U_0$ en de waarde van de belastingsweerstand en deze kolom mag je negeren. $U_1$ is de spanning over de fotovoltaïsche cel en $U_2$ is de spanning over een 4.7 Ω weerstand die in serie staat met de belasting. Maak nieuwe _calculated columns_ om de stroomsterkte door het circuit te berekenen en liefst ook de onzekerheid daar op &mdash; dit laatste is echter geen middelbare school-stof. Plot de relatie tussen de stroomsterkte en de spanning en probeer het volgende model te fitten, afgeleid van de Shockley vergelijking:
    $$
    I = I_\text{L} - I_0\left[\exp\left(\frac{U}{nU_\text{T}}\right) - 1\right],
    $$
    met de stroomsterkte $I$, the fotostroom $I_\text{L}$, de sperverzadigingsstroom $I_0$, de spanning over de fotovoltaïsche cel $U$, en de thermische spanning $U_\text{T} = \frac{kT}{q}$.

    Bestanden:

    * [:fontawesome-solid-file-csv: pvcell.csv](data/pvcell.csv)

    [^belasting]: Wanneer je een apparaat of, in dit geval, een weerstand aansluit op een spanningsbron dan _belast_ je de spanningsbron.


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


## Extras

!!! opdracht
    Can you determine the half-life of radon-220 using measurements of the activity of a freshly obtained sample of radon?

    Data files:

    * [:fontawesome-solid-file-csv: radon220.csv](data/radon220.csv)


## Installatie-instructies voor Tailor

The repository for Tailor can be found at [GitHub](https://github.com/davidfokkema/tailor) and the latest release can be downloaded [here](https://github.com/davidfokkema/tailor/releases/latest). Links to the individual binary installers:

* [Windows](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0.msi)
* [Intel Macs (older Macs)](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0_intel.dmg)
* [Apple Silicon (newer Macs)](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0_apple_silicon.dmg)

This document contains several exercises to explore the features of Tailor and experience its ease-of-use. Special care was given to try and showcase those features which make Tailor ideally suited for data analysis in an educational setting. All analysis tools should incur only low cognitive load and should ideally be directly usable without reading a long manual.
