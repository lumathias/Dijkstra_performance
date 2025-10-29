# Comparing Performances of Classic Dijkstra vs Dijkstra with Min-Heap

**Authors:**  
Luisa M. G. Mathias  
Viviane Stephane P. Novo  

**Course:**  
Algorithms and Data Structures II (DCA3702)  
Computer Engineering – Universidade Federal do Rio Grande do Norte (UFRN)

---

## Objective

The central goal of this project is to **compare and quantify the performance and environmental impact differences** between two approaches of **Dijkstra’s Shortest Path Algorithm**:

1. **Classic Dijkstra** (linear search–based implementation)  
2. **Optimized Dijkstra with Min-Heap** (priority queue–based implementation)

The analysis aims to **validate theoretical complexity gains** and **correlate them with the carbon footprint ($\text{CO}_2$)** emitted during execution.
The experiments follow reproducible research guidelines and use **CodeCarbon** to estimate CO₂ emissions from computational usage.
 
---

## Problem Description

The goal is to analyze performance and environmental impact when processing **graphs of varying sizes**, measuring how algorithmic complexity translates into runtime and energy consumption.  

We used **NetworkX** to generate connected graphs and **CodeCarbon** to estimate energy-related emissions.

---
## Methodology and Experimental Setup

To ensure **reproducibility**, the experiment followed the process below.

### 🔹 Data Generation

- **Graphs:** Directed, strongly connected, and weighted graphs (edge weights ∈ [1, 10]) were generated using **NetworkX**.  
- **Graph Sizes:** Varied from **100 to 50,000 nodes**.  
- **Sampling:** For each graph size, **15 repetitions** were performed, with **5 random source nodes** per repetition — totaling **75 runs per algorithm per size**.  
- **Reproducibility:** A fixed random seed (`SEED = 42`) was used for both graph generation and node selection.

### 🔹 Measurement and Comparison

**Performance Metrics**
- **Execution Time (s):** 3h43min Measured with system wall time.  

**Algorithms Tested**
- `classic`: Implementation with complexity $O(V^2 + E)$.  
- `heap`: Implementation with complexity $O((V + E)\log V)$.  
- `networkx`: Reference implementation from **NetworkX**.

**Statistical Analysis**
- Runs were compared using the **mean and standard deviation** of results for consistency and statistical rigor.

---

## Experimental Configuration

| Parameter | Value |
|------------|-------|
| **Graph Sizes** | 100 to 50,000 nodes |
| **Repetitions** | 15 per graph size, 5 random sources (75 runs total) |
| **Graph Generator** | `nx.gnp_random_graph(n, p)` |
| **Weights** | Integers from 1 to 10 |
| **Connectivity** | Strongly connected component |
| **Random Seed** | `SEED = 42` |
| **Libraries** | NetworkX, CodeCarbon, NumPy, Matplotlib, tqdm |
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

### Performance Comparison

| Graph Size | Classic Dijkstra (s) | Min-Heap Dijkstra (s) | Speedup Factor |
|:----------:|:--------------------:|:---------------------:|:--------------:|
| **100**    | 0.000038             | 0.000243              | **0.16x** (slower) |
| **500**    | 0.018321             | 0.005475              | **3.35x**      |
| **1,000**  | 0.068125             | 0.017218              | **3.96x**      |
| **5,000**  | 1.253174             | 0.129223              | **9.70x**      |
| **10,000** | 5.659204             | 0.718862              | **7.87x**      |
| **50,000** | 135.300812           | 0.908809              | **148.88x**    |

### Carbon Footprint Comparison

| Graph Size | Classic Dijkstra (kg CO₂) | Min-Heap Dijkstra (kg CO₂) | Reduction (%) |
|:----------:|:-------------------------:|:--------------------------:|:-------------:|
| **100**    | 2.08E-08                  | 2.80E-08                   | **-34.6%** (more) |
| **500**    | 1.88E-07                  | 6.93E-08                   | **63.1%**     |
| **1,000**  | 6.41E-07                  | 1.84E-07                   | **71.3%**     |
| **5,000**  | 1.16E-05                  | 1.23E-06                   | **89.4%**     |
| **10,000** | 5.22E-05                  | 6.75E-06                   | **87.1%**     |
| **50,000** | 0.001264                  | 8.44E-06                   | **99.3%**     |

**Observations:**
- Runtime and emissions scale nonlinearly with graph size.  
- Min-Heap Dijkstra is notably more efficient for larger graphs, confirming the expected theoretical behavior.  
- The CO₂ reduction maintains proportionality to the runtime decrease.

---

## Visualization

Below is an example of how the comparative charts were generated using Matplotlib, followed by the images:

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

---

##  Results Analysis

The following results, plotted on **log-log scale**, demonstrate the relationship between algorithmic complexity, execution performance, and energy consumption.

### Execution Time (Time vs. Number of Nodes)
- **Complexity Validation:** The **Classic** algorithm (blue curve) exhibits steep growth, confirming the expected **quadratic time complexity (O(V²))**.  
- **Optimization Effect:** The **Min-Heap (orange)** and **NetworkX (green)** curves show a much smoother, near-log-linear growth pattern. The optimized version outperforms the classic one starting from **≈ 500 nodes**.  
- **Reference Consistency:** The `networkx` implementation follows the same asymptotic trend as the Min-Heap version, serving as a reliable reference benchmark.

### Carbon Footprint ($\text{CO}_2$ vs. Number of Nodes)
- **Direct Correlation:** The $\text{CO}_2$ emission curve mirrors the execution time plot, confirming that carbon footprint is **directly proportional to computational time**.  
- **Environmental Impact:** The **Classic** version consumes **orders of magnitude more $\text{CO}_2$** for larger graphs (e.g., 10⁴ nodes) than the **Min-Heap** version.  
- **Practical Conclusion:** Algorithmic optimization is not only a performance improvement but also an effective **strategy for reducing energy consumption and environmental impact at scale**.

---


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

[ **Watch the project demonstration video**](https://drive.google.com/file/d/1haTP8D9C3BCB49H6qI6PMkuzG9C6LOBX/view?usp=drive_link)  

---

## References

- NetworkX Documentation: [https://networkx.org/documentation/stable/](https://networkx.org/documentation/stable/)  
- CodeCarbon Documentation: [https://mlco2.github.io/codecarbon/](https://mlco2.github.io/codecarbon/)  
- Dijkstra, E. W. (1959). *A note on two problems in connexion with graphs*. Numerische Mathematik, 1, 269–271.

---




