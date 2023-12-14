---
hide:
  - navigation
---

# BFY4 workshop on Tailor

The repository for Tailor can be found at [GitHub](https://github.com/davidfokkema/tailor) and the latest release can be downloaded [here](https://github.com/davidfokkema/tailor/releases/latest). Links to the individual binary installers:

* [Windows](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0.msi)
* [Intel Macs (older Macs)](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0_intel.dmg)
* [Apple Silicon (newer Macs)](https://github.com/davidfokkema/tailor/releases/download/v1.8.0/Tailor-1.8.0_apple_silicon.dmg)

This document contains several exercises to explore the features of Tailor and experience its ease-of-use. Special care was given to try and showcase those features which make Tailor ideally suited for data analysis in an educational setting. All analysis tools should incur only low cognitive load and should ideally be directly usable without reading a long manual.


## Measuring the motion of a pendulum with an ultrasonic distance detector

!!! abstract "Learning goal"
    Experience Tailor's intuitive interface for changing initial parameters and visualizing their relevance to the physics of the model.

For periodic functions it can be especially hard to find a working set of initial parameters for curve fitting to succeed. Using other tools, it can be a laborious exercise in trial-and-error. Tailor can show the initial fit in a semitransparent blue color. The initial fit responds to changes in the initial values of the parameters. Those values can be changed by editing the value field, using the little arrows next to the data field but also by placing the mouse cursor in the field and by using the mouse scroll gestures to change the values. Especially this last method makes it very intuitive to visualize the relevance of the different parameters to the physics of the model.

!!! exercise
    Import the :fontawesome-solid-file-csv:`pendulum-USD.csv` data file into a clean project. Change the column names if you'd like. Create a plot of distance versus time and use a model similar to:
    $$
    s = s_0 + A \sin(2\pi f t + \phi),
    $$
    where distance $s$ and time $t$ should be the names of the data columns. Try to fit the model using the default initial values; that probably will not result in a good fit. Now play around with the initial values; you may need to enable `Show initial fit` again. How does changing a parameter affect the model curve? Try to get a good fit.

    Data files:

    * [:fontawesome-solid-file-csv: pendulum-USD.csv](data/pendulum-USD.csv)


## X-ray fluorescence

!!! abstract "Learning goal"
    In this exercise you will learn that Tailor has no restrictions on which model you can fit. You can perform a more complex curve fitting procedure with, for example, multi-peak models. However, you must be very explicit about it.
    
Tailor has no library of included models. Each model that you want to fit has to be explicitly defined in the model function text area. That does make Tailor very flexible though. While tools like Excel can only fit a handful of models, more advanced tools like Origin Pro let you work with user-defined models. The distinction between predefined and user-defined models makes the interface harder to use while using predefined models can also make students a bit lazy. They switch models until one fits and they don't always understand the physics behind it. In Tailor, fitting a peak model like a Gaussian distribution requires students to look up the definition and enter the function explicitly.

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


## Extras

!!! exercise
    Can you determine the half-life of radon-220 using measurements of the activity of a freshly obtained sample of radon?

    Data files:

    * [:fontawesome-solid-file-csv: radon220.csv](data/radon220.csv)