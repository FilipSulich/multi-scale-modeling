# Assignment 4 - Plant Tissue Simulation

## Exercise 1

We start the simulation from the initial state and document it every hour for 4 hours. The screenshots can be seen below.

![Alt Initial state](./screenshots/initial.png)
![Alt Initial state](./screenshots/after_1h.png)
![Alt Initial state](./screenshots/after_2h.png)
![Alt Initial state](./screenshots/after_3h.png)
![Alt Initial state](./screenshots/after_4h.png)

During the 4 hours of simulation, we can see the pathogen slowly infecting the plant tissue. This is shown by the brown area expanding outward from the pathogen source (marked by a red point), infecting more cells with each passing hour. Cells next to the infected region are weakened by the pathogen’s secretion of cell wall–breaking chemicals, while cells farther away stay healthy, remaining green.

## Exercise 2

## Exercise 3

## Exercise 4

We now adjust the diffusion coefficient by a factor of 10. The diffusion coefficient (D[0]) is currently set to 1e-05. First, we increase it to 1e-04. 

![Alt Initial state](./screenshots/d_04_after_1h.png)
![Alt Initial state](./screenshots/d_04_after_2h.png)
![Alt Initial state](./screenshots/d_04_after_3h.png)
![Alt Initial state](./screenshots/d_04_after_4h.png)

Now we decrease it to 1e-06. 

![Alt Initial state](./screenshots/d_06_after_1h.png)
![Alt Initial state](./screenshots/d_06_after_2h.png)
![Alt Initial state](./screenshots/d_06_after_3h.png)
![Alt Initial state](./screenshots/d_06_after_4h.png)

Diffusion coefficient spreads the chemical through tissue. Reducing it by 10 slows transport, so the secretion accumulates near the source. That results in a higher local concentration, but less infected cells furter away from the pathogen source. We can see it through more brown area around the red point, but more green (healthy) cells overall. To compare it to the previous simulation - after 4h we can see around the same number of infected cells as after 1h in the baseline model. Increasing the coefficient by 10 makes the chemical disperse broadly across all tissue. We can see how the brown area spreads faster and across more cells than before. Just after 1h we can see more infected cells than after 4h without adjusting it. However, the maximum concentration at the source will be lower than baseline (because secretion is quickly dispersed). 

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
