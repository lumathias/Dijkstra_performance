Project developed by Luisa M. G. Mathias and Viviane Stephane P. Novo Related to the second unit of the subject: Algorithms and Data Structures II - DCA3702 of the Computer Engineering course at UFRN
# Comparing Performances of Classic Dijkstra versus Dijkstra with Min-Heap

## Objective

This project compares the performance and carbon footprint of two implementations of the **Dijkstra algorithm** for calculating minimum paths in weighted and directed graphs:

-  **Classic Dijkstra:** complexity `O(V² + E)`  
-  **Min-Heap Dijkstra:** complexity `O((V + E) log V)`

The experiment measures the **execution time** and **estimated CO₂ emissions** (through CodeCarbon) for each algorithm, following scientific guidelines for reproducibility and statistical analysis.

---

## Descrição do Problema

1. **Geração de grafos ponderados e conectados** com [NetworkX](https://networkx.org/) em diferentes tamanhos (até 100 000 nós).  
2. **Seleção de 5 nós aleatórios** e cálculo do menor caminho desses nós até todos os outros utilizando:
   - Dijkstra Clássico (versão `O(V²)`)
   - Dijkstra com Min-Heap (versão `O((V + E) log V)`)
   - Algoritmo de referência do *NetworkX* (`nx.single_source_dijkstra_path_length`)
3. **Repetição de 15 – 20 vezes** por tamanho do grafo, com novos nós iniciais a cada rodada.  
4. **Coleta de métricas:**  
   - Tempo total de execução (segundos)  
   - Emissões estimadas de CO₂ (kilogramas)  
5. **Cálculo estatístico** de médias e desvios-padrão.  
6. **Geração de gráficos comparativos** de tempo e emissões.

---

## Configuração Experimental

| Item | Valor |
|------|--------|
| **Tamanhos de grafos** | `[100, 500, 1 000, 5 000, 10 000, 50 000, 100 000]` |
| **Repetições** | 15 – 20 por tamanho |
| **Seeds fixas** | Para `numpy` e `random` |
| **Geração de grafos** | `nx.gnp_random_graph(n, p)` com pesos positivos (1 – 10) |
| **Garantia** | Conectividade usando componente gigante |
| **Métricas** | Tempo médio, desvio padrão, CO₂ médio |

---

## Resultados Esperados

| Situação | Dijkstra Clássico | Dijkstra Min-Heap |
|-----------|------------------|------------------|
| **Grafo esparso** | Lentidão crescente `O(V²)` | Muito mais eficiente `O(E log V)` |
| **Grafo denso** | Desempenho semelhante | Leve sobrecarga do heap |
| **Escalabilidade** | Até ~10 000 nós | Até 100 000+ nós |
| **Pegada de CO₂** | Maior consumo energético | Menor emissão (menor tempo de CPU) |

---

## Stack Tecnológica

- [Python 3.10+](https://www.python.org/)
- [NetworkX](https://networkx.org/)
- [CodeCarbon](https://mlco2.github.io/codecarbon/)
- [NumPy](https://numpy.org/)
- [Matplotlib](https://matplotlib.org/)
- [tqdm](https://tqdm.github.io/) (para barra de progresso)

---

## Como Executar

```bash
# Clone o repositório
git clone https://github.com/SEU-USUARIO/dijkstra-comparativo.git
cd dijkstra-comparativo

# Crie e ative um ambiente virtual (opcional)
python -m venv venv
source venv/bin/activate     # Linux/Mac
venv\Scripts\activate        # Windows

# Instale as dependências
pip install -r requirements.txt

# Execute o notebook ou script principal
jupyter notebook dijkstra_experimentos.ipynb
