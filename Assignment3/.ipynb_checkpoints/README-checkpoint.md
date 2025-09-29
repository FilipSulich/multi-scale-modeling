# Assignment 3

This repository contains the Jupyter Notebook **`Assignment3.ipynb`**.

---

## Requirements

- Python 3.8 or higher  
- Jupyter Notebook or JupyterLab  
---

## How to Run

1. Clone or download this repository.  
2. Open a terminal and start Jupyter Notebook:
   ```bash
   jupyter notebook
3. Open the **`Assignment3.ipynb`** file.
4. Run all cells in order. If you encounter issues, try “Kernel -> Restart & Run All”.

## Answers to questions

# Which mutation is most dangerous and why? Provide quantitative evidence.

Based on strictly the simulation results, mutations A, B and C are equally dangerous. That is because all three surpress p53 activity, which is the tumor suppressor protein. Without p53 cells can keep dividing (apoptosis doesn't happen) even when DNA is damaged, which makes them much more likely to become cancerous. All three mutations have 2 attractors, both reached by 128 states. Attractor 2 (Growth ON, Death OFF, p53 OFF, DNA Damage ON), which is reached by 50% of the states, represents a cancerous-like state, as it promotes the cell growth and spreading of damaged DNA.

However, if we were to interpret those mutations from a biological point of view, mutation A would be the most dangerous. That is because it's a complete p53 knockout, which leads to an irreversible loss of a central tumor suppressor. In mutations B and C, p53 is not knocked out completely, so technically p53 pathway can be reactivated. In mutation B, MYC, which is a strong growth promoter, is permanently switched on and can override p53, which is responsible for stopping the uncontrollable growth. In mutation C, MDM2 is overexpressed and suppresses p53, so the cell's safety mechanism responding to DNA damage is turned off. However, in both B and C, p53 itself is not deleted, just temporarily overriden, so the danger, while still being high, is not completely irreversible. 

# Explain the role of feedback loops (e.g., MYC → MDM2 → p53)

Feedback loops are regulatory mechanisms, where a system's output affects its input, regulating processes like growth, death or stress responses. 
The main feedback loop (MYC → MDM2 → p53) is a negative feedback loop, which means that the output of the loop reduces the activity of the system. 
This loop's purpose is to stabilize p53 activity and prevent uncontrollable growth.

It works as follows. MYC activates MDM2 (whenever MYC is active, MDM2 levels go up). MDM2 inhibits p53 (when MDM2 is ON, p53 cannot accumulate effectively). p53 controls p21 and apoptosis. If p53 is ON and DNA damage is detected, it can activate p21 (cell-cycle arrest) or trigger apoptosis.
However, when rewired by mutations (such as p53 knockout, MYC amplification or MDM2 overexpression) - they feedback loops create stable attractors where the cell ignores DNA damage and proliferates indefinitely. In this case, if p53 is OFF, these safeguards are gone, which leads to uncontrolled cell growth, even when DNA is damaged, which is a cancer-like state. 

# What are the limitations of this Boolean network model? Discuss 3 specific limitations.

The first limitation of this Boolean network model is oversimplification. In our model the node is either ON (1) or OFF (0). In reality, proteins like p53, MYC, or MDM2 can vary continuously and small changes can affect how the cell behaves. The model doesn’t capture these gradual effects or random fluctuations.

The second limitations comes from the fact that the model doesn't include the real timing of events. It updates all nodes step by step, without considering how fast reactions happen in real cells. This means it shows only the final outcomes (attractors) and can miss important temporary responses, like p53 pulses that decide whether a cell repairs itself or dies.

The third limitation is the small size of the network. Because the model only has 8 nodes, it leaves out other important regulators of the p53/MYC system. Because of that, the model can overestimate the dominance of single mutations (like MYC amplification), because it ignores backup mechanisms the cell might have. 

Despite these limitations, Boolean networks are still very useful, because they allow us to simplify complex biological systems, identify key regulatory interactions and explore possible stable outcomes (attractors).