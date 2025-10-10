# Assignment 5 

In this Assignment, we implemented computational models of the visual system for three species: human, mouse, and marmoset.

## Methods 

1. Gathering data about brain regions and connectivity:

We found that there are 6 visual areas common across three selected species (human, mouse, and marmoset): V1, V2, V4, IT, MT, LIP.

Ventral stream (object recognition): V1 -> V2 -> V4 -> IT, 
Dorsal stream (spatial processing): V1 -> V2 -> MT -> LIP.

We tried getting the data from the siibra API, however we encountered many problems along the way. Mainly we were struggling to find any relevant data for all of our regions (V1, V2, V4, IT, MT, LIP). We could only get some info about cell density and structural connectivity for the V1 region in human brain (there is a possiblity that we were fetching the data in a incorrect manner). Nevertheless, in the end we decided to create a synthetic connectivity matrix, based on some biological literature, so that we preserve the neuroanatomical inductive biases of our models.
We assumed the connection strengths between the above mentioned regions based on the following studies:
- Felleman, D. J., & Van Essen, D. C. (1991). Distributed hierarchical processing in the primate cerebral cortex. Cerebral cortex (New York, N.Y. : 1991), 1(1), 1–47. https://doi.org/10.1093/cercor/1.1.1-a
- Kaas, J. H. (2001). The organization of sensory cortex. Current Opinion in Neurobiology, 11(4), 498–504. https://doi.org/10.1016/S0959-4388(00)00240-3

2. Neural Network Architecture

- Implemented in PyTorch.
- One network per species.
- Early layers (V1, V2) are shared for both pathways. Afterwards the network splits into two streams: Ventral stream: V4 → IT for object classification, and Dorsal stream: MT → LIP for spatial regression.
- Layer outputs were scaled by connectivity strengths to mimic signal flow inside the brain between different regions. The weights were selected based on the calculated connectivity strengths between regions.
- We used ReLU activation and max pooling after each convolutional layer to introduce non-linearity, highlight key features, and reduce spatial dimensions.

3. Dataset and Training

- To train our models we used the Fashion MNIST dataset of 28×28 images with 10 classes.
- Training details:
Optimizer: Adam, learning rate = 0.001
Loss: CrossEntropy for ventral stream
Epochs: 5–10 depending on species model

Ventral stream is trained for object classification. The dorsal stream processes the spatial information, but we do not have corresponding spatial labels in Fashion MNIST, therefore we cannot compute a loss function for this stream. Its activations are still computed, and training only the ventral stream is sufficient for the representational similarity and connectivity analyses. 
   
4. Representational Similarity and Connectivity

- We extracted activations from all layers of the ventral stream (V1, V2, V4, IT) using 10 batches of test data.
- To investigate the representational similarity between the three models we used RSA (Spearman correlation) between representational dissimilarity matrices (RDMs) across all species and layers.
- To measure the functional connectivity before and after training,we calculated correlation between activations of each pair of layers.
- We used t-SNE to reduce high-dimensional activations to a lower dimension (2D) to visualize the representational topology for each layer and species.

## Results and Conclusions

- All networks successfully learned to classify Fashion MNIST images. Ventral stream performance (classification accuracy) improved with training, while dorsal stream regression output remained stable.

- RSA results:

Layer v1:
  human-marmoset: 0.997
  human-mouse: 0.987
  marmoset-mouse: 0.989

Layer v2:
  human-marmoset: 0.991
  human-mouse: 0.985
  marmoset-mouse: 0.990

Layer v4:
  human-marmoset: 0.984
  human-mouse: 0.980
  marmoset-mouse: 0.979

Layer it:
  human-marmoset: 0.956
  human-mouse: 0.934
  marmoset-mouse: 0.948

The RSA results show a clear hierarchical pattern of representational divergence across species. Early visual areas (V1, V2) show almost perfect alignment, which suggests that the species share low-level visual processing. However, as processing advances through V4 and IT, inter-species similarity gradually declines, from ≈ (0.97-0.99) to ≈ (0.93-0.97). This is consistent with increasing functional specialization in higher visual areas. This pattern matches what’s seen in primate brains - early visual areas work in almost the same way across species, while higher-level regions start to show more species-specific differences. Across all layers the most similar representations are for a human - marmoset species pair and least similar between human and mouse.

- As expected for untrained networks, the correlation between different layers is generally low (near 0) across all species, while the correlation of a layer with itself is 1. Interestingly, the only change we saw after training was between V1 and V4, where the correlation dropped. All other layer pairs stayed about the same (the results was rounded to 2 decimal points, so even if it shows 0, the change was probably near 0, not stayed completely the same). That result means that the training mainly changed how early and mid-level layers interact, making V4 less tied to basic visual features. That fits with what’s seen in real brains, where learning tends to affect higher visual areas more than the early ones. This trend is seen in all species, although in human and marmoset much more visible than in mouse.

- t-SNE results: Activations in V1 and V2 reflected broad, low-level features, leading to less structured clusters, whereas V4 and IT developed well-defined clusters, showing that complex representations are created in those layers. The structure differed for different species across all layers, which reflected how species-specific connectivity and training influenced the representational structure in each network.

## General Conclusions

- The use of anatomical connectivity in network design allowed us to create models reflecting species-specific visual processing characteristics.
- Higher-order layers (V4, IT) were influenced by both learning and species-specific connectivity, as showed by RSA and t-SNE analysis.

  ## Note
  To help with building the CNN model, we used the PyTorch documentation (https://docs.pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html). Additionally, in some sections we used ChatGPT to help with the code refactoring and debugging (prompt was "refactor this piece of code for optimality: {code_snippet}". 
