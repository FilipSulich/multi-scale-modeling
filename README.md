# KEN3170 — Multi-Scale Modeling of Biological Systems (Maastricht University)

This repository contains assignments for the KEN3170 course: Multi-Scale Modeling of Biological Systems at Maastricht University.

Each assignment lives in its own folder and includes:
- A Jupyter Notebook (`.ipynb`) with the assignment instructions and code.
- Any relevant data files required to complete and run the notebook.

To inspect the assignment, open its Jupyter Notebook and run it.

---

## Repository Structure

A typical layout looks like this:
```
multi-scale-modeling/
├─ Assignment1/
│  ├─ data/                # Input data files specific to this assignment
│  └─ Assignment1.ipynb  # Main notebook for the assignment
├─ Assignment2/
│  ├─ data/
│  └─ Assignment2.ipynb
└─ README.md
```

Naming convention:
- Folders: `AssignmentXX` (e.g., `Assignment1`, `Assignment2`)
- Notebook: `AssignmentXX.ipynb` inside the corresponding folder

---

## Getting Started

### Prerequisites
- Python 3.9+ (recommended)
- JupyterLab or Jupyter Notebook
- Optionally, a virtual environment (conda or venv)

### 1) Clone the repository
```bash
git clone https://github.com/FilipSulich/multi-scale-modeling.git
cd multi-scale-modeling
```

### 2) Set up an environment (optional but recommended)

Using conda:
```bash
conda create -n msm-env python=3.10 -y
conda activate msm-env
pip install jupyterlab
```

Using venv:
```bash
python -m venv .venv
# On macOS/Linux:
source .venv/bin/activate
# On Windows PowerShell:
.venv\Scripts\Activate.ps1
pip install jupyterlab
```

If an assignment requires extra packages, install them as you go (you can also use pip inside notebooks):
```python
# In a notebook cell:
%pip install <package-name>
```

### 3) Launch Jupyter
```bash
jupyter lab
# or
jupyter notebook
```

### 4) Open and run an assignment
- In the Jupyter interface, navigate to the desired `AssignmentXX` folder.
- Open the corresponding `AssignmentXX.ipynb`.
- Run all cells in order. If you encounter issues, try “Kernel -> Restart & Run All”.
