# Assignment 5 

In this Assignment, we implemented computational models of the visual system for three species: human, monkey, and marmoset.

## Methods 

1. Gathering data about brain regions and connectivity:

We found that there are 6 visual areas common across three selected species (human, monkey, and marmoset): V1, V2, V4, IT, MT, LIP.

Ventral stream (object recognition): V1 -> V2 -> V4 -> IT, 
Dorsal stream (spatial processing): V1 -> V2 -> MT -> LIP.

We tried getting the data from the siibra API, however we encountered many problems along the way. Mainly we were struggling to find any relevant data for all of our regions (V1, V2, V4, IT, MT, LIP). We could only get some info about cell density and structural connectivity for the V1 region in human brain (there is a possiblity that we were fetching the data in a incorrect manner). Nevertheless, in the end we decided to create a synthetic connectivity matrix, based on some biological literature, so that we preserve the neuroanatomical inductive biases of our models.
We assumed the connection strengths between the above mentioned regions based on the following studies:
1) Felleman, D. J., & Van Essen, D. C. (1991). Distributed hierarchical processing in the primate cerebral cortex. Cerebral cortex (New York, N.Y. : 1991), 1(1), 1–47. https://doi.org/10.1093/cercor/1.1.1-a
2) Kaas, J. H. (2001). The organization of sensory cortex. Current Opinion in Neurobiology, 11(4), 498–504. https://doi.org/10.1016/S0959-4388(00)00240-3

2. Neural Network Architecture

- Implemented in PyTorch.
- One network per species.
- Early layers (V1, V2) are shared for both pathways. Afterwards the network splits into two streams: Ventral stream: V4 → IT for object classification, and Dorsal stream: MT → LIP for spatial regression.
- Layer outputs were scaled by connectivity strengths to mimic biological signal flow and let early layers influence later ones proportionally, like skip connections. The weight were selected based on the connectivity strength between regions calculated beforehand.
- We used ReLU activation and max pooling after each convolutional layer to introduce non-linearity, highlight key features, and reduce spatial dimensions.

3. Dataset and Training

-To train our models we used the Fashion MNIST dataset of 28×28 images with 10 classes.
-Training details:
Optimizer: Adam, learning rate = 0.001
Loss: CrossEntropy for ventral stream
Epochs: 5–10 depending on species model

Ventral stream is trained for object classification. The dorsal stream processes the spatial information, but we do not have corresponding spatial labels in Fashion MNIST, therefore we cannot compute a loss function for this stream. Its activations are still computed, and training only the ventral stream is sufficient for the representational similarity and connectivity analyses. 
   
4. Representational Similarity and Connectivity

- We extracted activations from all layers of the ventral stream (V1, V2, V4, IT) using 10 batches of test data.
- To investigate the representational similarity between the three models we used RSA (Spearman correlation) between representational dissimilarity matrices (RDMs) across all species and layers.
- To measure the functional connectivity before and after training,we calculated correlation between activations of each pair of layers.
- We used t-SNE to reduce high-dimensional activations to a lower dimension (2D) to visualize the representational topology for each layer and species.

## Results

## Conclusions