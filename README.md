# kmeans-lloyd-stalling
'Understanding Why Lloyd's Algorithm in K-Means Clustering Frequently Stalls at Suboptimal Cluster Solutions.' It explores algorithmic stalling via a practical case study, analyzing 162k+ retail transactions from a major EU supermarket chain in Poland using 1,000 Monte Carlo replications

Overview: 
Briefly state that this project is a Monte Carlo simulation analyzing why K-Means clustering stalls at suboptimal solutions, using 162,926 point-of-sale transactions from a Polish supermarket. 

Key Innovations: Highlight your custom convergence metric, Mean Centroid Displacement (MCD), and the dimensionless "Lloyd Bias" framework. 

Major Findings: Clearly state your most striking results. Note that Lloyd's algorithm stalls in 99.9% of individual runs at $k=7$. Mention that K-Means++ reduces displacement variance by 2-6% but only reduces the stall probability by a mere 0.1%.

Business Impact: Explain that standard single-iteration K-Means can cause 25% to 40% of customers to be placed into different segments just by changing the random seed.  

Reproducibility: Explicitly mention that the code uses deterministic random seeds (0 to 999) to guarantee the full reproduction of the 440,000 algorithm executions

```markdown
# Understanding Why Lloyd's Algorithm Stalls in K-Means Clustering

![Python Version](https://img.shields.io/badge/python-3.11-blue.svg)
![NumPy](https://img.shields.io/badge/numpy-2.0.2-blue.svg)
![Pandas](https://img.shields.io/badge/pandas-2.2%2B-blue.svg)
![Status](https://img.shields.io/badge/status-Completed-success.svg)

**Author:** Rifat Rayhan Romy  
**Institution:** Bucharest University of Economic Studies (FABIZ)  
**Supervisor:** Professor Adriana Mihnea  
**Year:** 2026  

## 📖 Abstract & Overview
This repository contains the code, data annex, and documentation for the thesis: **"Understanding Why Lloyd's Algorithm in K-Means Clustering Frequently Stalls at Suboptimal Cluster Solutions: A Case Study in Customer Segmentation."**

Lloyd's algorithm, the fundamental iterative process driving most practical K-Means implementations, frequently suffers from *algorithmic stalling*. It inevitably terminates and appears to converge successfully; however, because it minimizes a non-convex criterion, it frequently stalls at suboptimal partitions (local minima) without indicating failure. This project explores the scope of this phenomenon and its implications for business analytics through a robust case study analyzing retail transactions.

## 📂 Repository Structure

```text
├── docs/
│   ├── Analytics_ROMY_RIFAT_RAYHAN.pdf     # Full thesis (Theory, Methodology, Results)
│   └── Code_Annex.html                     # Exported HTML notebook with execution outputs
├── notebooks/
│   └── Lloyd_KMeans_Poland_POS_v3.ipynb    # Main experimental implementation
├── data/
│   └── .gitkeep                            # Directory for local datasets (ignored by git)
├── .gitignore
└── README.md

```

## 📊 Dataset Context

The research utilizes real-world retail data to test algorithmic performance:

* **Source:** Antczak & Weron (2019), MDPI Data 4(2), 67
* **Context:** A major EU supermarket chain in Southern Poland
* **Volume:** 162,926 cleaned transactions
* **Periods Covered:** Dec 2017 | Feb 2019 | Mar–Apr 2019
* **Features:** 10 engineered transaction-level features (z-score normalized)


## 🔬 Experimental Configuration

The experiments were rigorously designed to produce publication-grade results using 1,000 Monte Carlo replications per condition.

| Parameter | Specification |
| --- | --- |
| **Primary Algorithm** | Custom Lloyd's algorithm, random initialization, `n_init=1` |
| **Benchmark Algorithm** | `sklearn.cluster.KMeans` (K-Means++), `n_init=1` |
| **Tested *k* Range** | *k* ∈ {2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12} |
| **GDB Blocks** | 10 blocks (300 transactions each, *K_TRUE* = 7 Gaussian clusters) |
| **Monte Carlo Replications** | 1,000 per condition (Algorithm × *k* × Block) |
| **Total Executions** | 440,000 |
| **Convergence Threshold** | Mean Centroid Distance (MCD) < 10⁻⁴ |
| **Max Iterations** | 150 per run |

## 🚀 Setup & Execution

The primary notebook (`Lloyd_KMeans_Poland_POS_v3.ipynb`) is structured in twelve sections documenting the design rationale and code outputs.

**Dependencies:**

```bash
pip install numpy pandas scikit-learn joblib jupyter

```

**Running the Code:**

1. Clone this repository.
2. Ensure you have the dataset in the `data/` folder (or adjust the path in the notebook).
3. The custom `run_lloyd()` implementation is intentionally unoptimized to allow for transparent MCD tracking.
4. **HPC / Parallel Execution:** Due to the 440,000 total executions, the notebook utilizes `joblib` for parallelization.
```python
from joblib import Parallel, delayed
reps = Parallel(n_jobs=-1)(
    delayed(run_lloyd)(X, k, LLOYD_INIT, rep, MAX_ITER)
    for rep in range(N_MONTE)
)

```



If you only wish to view the results and code without executing the heavy 1,000-replication Monte Carlo simulation, please open `docs/Code_Annex.html` in your web browser.

## 📄 License & Citation

If you use this code or methodology in your own work, please cite the original thesis.

```bibtex

  author       = {Rifat Rayhan Romy},
  title        = {Understanding Why Lloyd's Algorithm in K-Means Clustering Frequently Stalls at Suboptimal Cluster Solutions: A Case Study in Customer Segmentation},
  school       = {Bucharest University of Economic Studies (FABIZ)},
  year         = {2026},
  
}

```

```

```
