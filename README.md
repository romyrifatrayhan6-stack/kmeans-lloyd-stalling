# kmeans-lloyd-stalling
Code annex and documentation for the 2026 thesis: 'Understanding Why Lloyd's Algorithm in K-Means Clustering Frequently Stalls at Suboptimal Cluster Solutions.' It explores algorithmic stalling via a practical case study, analyzing 162k+ retail transactions from a major EU supermarket chain in Poland using 1,000 Monte Carlo replications

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
