# Comparing Performances of Classic Dijkstra vs Dijkstra with Min-Heap

**Authors:**  
Luisa M. G. Mathias  
Viviane Stephane P. Novo  

**Course:**  
Algorithms and Data Structures II (DCA3702)  
Computer Engineering – Universidade Federal do Rio Grande do Norte (UFRN)

---

## Objective

This project compares the **performance** and **carbon footprint** of two implementations of the Dijkstra algorithm for computing shortest paths in **weighted directed graphs**:

- **Classic Dijkstra:** complexity **O(V² + E)**  
- **Dijkstra with Min-Heap:** complexity **O((V + E) log V)**  

The experiments follow reproducible research guidelines and use **CodeCarbon** to estimate CO₂ emissions from computational usage.

---

## Problem Description

The goal is to analyze performance and environmental impact when processing **graphs of varying sizes**, measuring how algorithmic complexity translates into runtime and energy consumption.  

We used **NetworkX** to generate connected graphs and **CodeCarbon** to estimate energy-related emissions.

---

### Experiment Workflow

1. **Graph Generation:**  
   - Created using `nx.gnp_random_graph(n, p)` with random **positive weights (1–10)**.  
   - Connectivity ensured via the graph’s **giant component**.

2. **Parameters:**
   - **Graph sizes**: `[100, 500, 1,000, 5,000, 10,000, 50,000, 100,000]`
   - **Repetitions:** 15–20 per graph size
   - **Random Sources:** 5 random starting nodes per test
   - **Fixed Seeds:** for reproducibility

3. **Metrics Collected:**
   - **Execution Time (s)**
   - **Estimated CO₂ emissions (kg)** via CodeCarbon
   - **Statistical Measures:** mean and standard deviation

---

## Experimental Setup

| Item              | Value |
|--------------------|-------|
| **Graph sizes**    | 100 – 100,000 nodes |
| **Repetitions**    | 15–20 |
| **Graph Generator**| `nx.gnp_random_graph(n, p)` |
| **Weights**        | 1 to 10 |
| **Connectivity**   | Giant component check |
| **Fixed Seeds**    | For NumPy & random |
| **Libraries**      | NetworkX, CodeCarbon, NumPy, Matplotlib, tqdm |
| **Python Version** | 3.10+ |

---

## Expected Results

| Situation | Classic Dijkstra | Min-Heap Dijkstra |
|------------|------------------|-------------------|
| **Sparse Graphs** | Becomes very slow (O(V²)) | Much faster (O(E log V)) |
| **Dense Graphs** | Similar timing | Slight heap overhead |
| **Scalability** | Up to ≈10,000 nodes | Beyond 100,000 nodes efficiently |
| **CO₂ Footprint** | Higher (longer CPU usage) | Lower (less execution time) |

---

## Methodology Summary

- **Repetitions** and **averaging** ensure statistically sound results.  
- **Emissions measured** using CodeCarbon, based on CPU time and energy consumption models.  
- All **parameters** and **random seeds** are fixed for reproducibility.  
- **Visualization** with Matplotlib for runtime and emissions scaling comparison.

---

## Experimental Results

> *(Fill in after running final experiments — you can include your results tables and interpretations below.)*

### Performance Comparison
| Graph Size | Classic Dijkstra (s) | Min-Heap Dijkstra (s) | Speedup Factor |
|-------------|----------------------|------------------------|----------------|
| 100 | ... | ... | ... |
| 1,000 | ... | ... | ... |
| 10,000 | ... | ... | ... |
| 100,000 | ... | ... | ... |

### Carbon Footprint
| Graph Size | Classic Dijkstra (kg CO₂) | Min-Heap Dijkstra (kg CO₂) | Reduction (%) |
|-------------|----------------------------|-----------------------------|----------------|
| 100 | ... | ... | ... |
| 100,000 | ... | ... | ... |

**Observations:**
- Runtime and emissions scale nonlinearly with graph size.  
- Min-Heap Dijkstra is notably more efficient for larger graphs, confirming the expected theoretical behavior.  
- The CO₂ reduction maintains proportionality to the runtime decrease.

---

## Visualization

Below is an example of how you can visualize your results directly in the notebook or script:

```python
plt.figure(figsize=(8, 4))
for alg in ['classico', 'heap', 'networkx']:
    sub = agg[agg.algoritmo == alg]
    plt.errorbar(sub['n'], sub['tempo_medio'],
                 yerr=sub['tempo_std'], label=alg, marker='o')
plt.xscale('log')
plt.yscale('log')
plt.xlabel('Número de nós')
plt.ylabel('Tempo (s) – média ± desvio')
plt.legend()
plt.tight_layout()
plt.savefig('tempo.png')
plt.show()

plt.figure(figsize=(8, 4))
for alg in ['classico', 'heap', 'networkx']:
    sub = agg[agg.algoritmo == alg]
    plt.errorbar(sub['n'], sub['co2_medio'],
                 yerr=sub['co2_std'], label=alg, marker='o')
plt.xscale('log')
plt.yscale('log')
plt.xlabel('Número de nós')
plt.ylabel('CO₂ (kg) – média ± desvio')
plt.legend()
plt.tight_layout()
plt.savefig('co2.png')
plt.show()
```

![Execution Time Comparison](https://github.com/lumathias/Dijkstra_performance/issues/1#issue-3563903792)

![CO2 Emissions Comparison](https://github.com/lumathias/Dijkstra_performance/issues/1#issuecomment-3459195598)


## How to Run

```bash
# Clone the repository
git clone https://github.com/SEU-USUARIO/dijkstra-comparativo.git
cd dijkstra-comparativo

# (Optional) Create and activate a virtual environment
python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate         # Windows

# Install dependencies
pip install -r requirements.txt

# Run the notebook
jupyter notebook dijkstra_experiments.ipynb
```

---

## Video Presentation

[🔗 **Watch the project demonstration video**](#)  
*(Insert your video link here once available)*

---

## References

- NetworkX Documentation: [https://networkx.org/documentation/stable/](https://networkx.org/documentation/stable/)  
- CodeCarbon Documentation: [https://mlco2.github.io/codecarbon/](https://mlco2.github.io/codecarbon/)  
- Dijkstra, E. W. (1959). *A note on two problems in connexion with graphs*. Numerische Mathematik, 1, 269–271.

