Project developed by Luisa M. G. Mathias and Viviane Stephane P. Novo Related to the second unit of the subject: Algorithms and Data Structures II - DCA3702 of the Computer Engineering course at UFRN
# Comparing Performances of Classic Dijkstra versus Dijkstra with Min-Heap

## Objective

This project compares the performance and carbon footprint of two implementations of the **Dijkstra algorithm** for calculating minimum paths in weighted and directed graphs:

-  **Classic Dijkstra:** complexity `O(V² + E)`  
-  **Min-Heap Dijkstra:** complexity `O((V + E) log V)`

The experiment measures the **execution time** and **estimated CO₂ emissions** (through CodeCarbon) for each algorithm, following scientific guidelines for reproducibility and statistical analysis.

---

## Problem Description

1. **Generating weighted and connected graphs** with [NetworkX](https://networkx.org/) in different sizes (up to 100,000 nodes).   
2. **Selecting 5 random 5 nodes** and calculating the shortest path from these nodes to all others using: 
   - Classic Dijkstra (`O(V²)` version)  
   - Dijkstra with Min-Heap (`O((V + E) log V`) version)
   - *NetworkX* reference algorithm (`nx.single_source_dijkstra_path_length`)
3. **Repeating 15–20 times** per graph size, with new initial nodes each round.
4. **Metrics collection:**
   - Total execution time (seconds)
   - Estimated CO₂ emissions (kilograms)
5. **Statistical calculation** of means and standard deviations.  
6. **Generating comparative graphs** of time and emissions.

---

## Experimental Setup

| Item | Value |
|------|--------|
| **Graph sizes** | `[100, 500, 1,000, 5,000, 10,000, 50,000, 100,000]` |
| **Repetitions** | 15–20 per size |
| **Fixed seeds** | For `numpy` and `random` |
| **Graph generator** | `nx.gnp_random_graph(n, p)` with positive weights (1–10) |
| **Assurance** | Connectivity using giant component |
| **Metrics** | Average time, standard deviation, average CO₂ |

---

## Expected Results

| Situation | Classic Dijkstra | Min-Heap Dijkstra |
|-----------|------------------|------------------|
| **Sparse graph** | Increasing slowness `O(V²)` | Far more efficient `O(E log V)` |
| **Dense graph** | Similar performance | Slight heap overhead |
| **Scalability** | Up to ~10,000 nodes | Up to 100,000+ nodes |
| **CO₂ footprint** | Increased energy consumption | Lower emissions (lower CPU time) |

---

## Technology Stack

- [Python 3.10+](https://www.python.org/)
- [NetworkX](https://networkx.org/)
- [CodeCarbon](https://mlco2.github.io/codecarbon/)
- [NumPy](https://numpy.org/)
- [Matplotlib](https://matplotlib.org/)
- [tqdm](https://tqdm.github.io/) (progress bar)

---

## How to Run It:

```bash
# Clone the repository
git clone https://github.com/SEU-USUARIO/dijkstra-comparativo.git
cd dijkstra-comparativo

# Create and activate a virtual environment (optional)
python -m venv venv
source venv/bin/activate     # Linux/Mac
venv\Scripts\activate        # Windows

# Install dependencies
pip install -r requirements.txt

# Run the notebook or main script
jupyter notebook dijkstra_experiments.ipynb
