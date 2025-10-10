# Assignment 5 

In this Assignment, we implemented computational models of the visual system for three species: human, monkey, and marmoset.

## Methods 

## Gathering data

We found that there are 6 visual areas common across three selected species (human, monkey, and marmoset): V1, V2, V4, IT, MT, LIP.

Ventral stream (object recognition): V1 -> V2 -> V4 -> IT, 
Dorsal stream (spatial processing): V1 -> V2 -> MT -> LIP.

We tried getting the data from the siibra API, however we encountered many problems along the way. Mainly we were struggling to find any relevant data for all of our regions (V1, V2, V4, IT, MT, LIP). We could only get some info about cell density and structural connectivity for the V1 region in human brain (there is a possiblity that we were fetching the data in a incorrect manner). Nevertheless, in the end we decided to create a synthetic connectivity matrix, based on some biological literature, so that we preserve the neuroanatomical inductive biases of our models.
We assumed the connection strengths between the above mentioned regions based on the following studies:
1) Felleman, D. J., & Van Essen, D. C. (1991). Distributed hierarchical processing in the primate cerebral cortex. Cerebral cortex (New York, N.Y. : 1991), 1(1), 1–47. https://doi.org/10.1093/cercor/1.1.1-a
2) Kaas, J. H. (2001). The organization of sensory cortex. Current Opinion in Neurobiology, 11(4), 498–504. https://doi.org/10.1016/S0959-4388(00)00240-3




## Results

## Conclusions