# Assignment 4 - Plant Tissue Simulation

## Exercise 1

Initial state

![Alt Initial state](Assignment4/screenshots/initial.png)

## Exercise 2

## Exercise 3

## Exercise 4

## Exercise 5

General idea is that we can introduce a second chemical (Chemical(1)), which is released by cells when they detect the pathogen chemical from bacteria/funghi. It acts as defense signal, which is sent to the neighbouring uninfected plant cells to inform that a pathogen is nearby and so they should strenghten their cell walls to prevent being infected.

In pseudocode, this can be described as:

1. We need to detect the pathogen chemicals (in the `CellDynamics` method):

```
   if(cell is pathogen) then
       produce the pathogen_chemical at a constant rate (in the code its dchem[0] = 0.01)
   else
       degrade the chemical level (in the code its dchem[0] = -0.001 * c->Chemical(0))
       if(pathogen_chemical_level > activation_threshold) then
           produce the defense_chemical (Chemical(1)) at some rate
```

2.  Then we need to transport the defense chemical throughout cells (in the `CelltoCellTransport` method):

```
   for each cell wall between cells c1 and c2:
       transport the pathogen_chemical (Chemical(0)) from c1 to c2 at a constant rate
       transport the defense_chemical (Chemical(1)) from c1 to c2 at the same rate
```

3.  We need to make the chemical influence the cell to increase the stifness of its wall (in the `CellHouseKeeping` method):

```
   if(cell is uninfected) then
       if (defense_chemical_level > threshold_one) then
           increase the cell wall stifness (for example by 1.5)
       else
            if(pathogen_chemical_level > threshold_two AND cell is not pathogen) then
                decrease the cell wall stifness (for exmaple 2.5 - pathogen_chemical_level)
            else
                set the cell wall stifness to some baseline value (in the code its stifness_inf = 2.5)
```
