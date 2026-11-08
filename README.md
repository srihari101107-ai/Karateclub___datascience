# Karateclub___datascience
# Modularity on the Karate Club Graph
### Recursive Spectral Community Detection from Scratch

**Course:** DSC212 – Graph Theory Module (Research Assignment)
**Author:** Sri Hari Venkatesh M | **Roll No.:** IMS25207

## Overview
This project implements Newman's **modularity-based spectral community detection**
from scratch and applies it to Zachary's Karate Club network (34 members, 78 edges).
The club split into two factions after a dispute between the instructor (Mr. Hi, node 0)
and the president (the Officer, node 33). The goal is to see whether a method that uses
only the graph structure can recover that real split.

**Method in short**
1. Build the modularity matrix `B = A - kkᵀ/2m`.
2. Take the leading eigenvector of `B` (Rayleigh–Ritz) and split nodes by its sign.
3. Recurse on each group while the leading eigenvalue stays positive and the true ΔQ > 0.
4. After each split, track degree, betweenness, closeness and clustering.

## Key Results
| Result | Value |
|---|---|
| First split | 16 + 18 members, Q = 0.3715 |
| Agreement with real factions | 33 / 34 members (97.1%), ARI 0.88, NMI 0.84 |
| Only misclassified node | Node 8 (sits on the boundary between the two sides) |
| Final partition | 5 communities, Q = 0.4094 |
| Newman's generalised matrix | 4 communities, Q = 0.3934 |
| Louvain (for comparison) | 4 communities, Q = 0.4188 |

**Findings**
- The spectral split scores a higher modularity than the real faction split (Q = 0.3582).
- Nodes **0, 33, 32** stay among the most central nodes at every iteration.
- Global bridges (e.g. node 0) lose betweenness when the graph is cut, while local brokers (e.g. nodes 31, 33) gain it.
- Maximising modularity is not the same as recovering the ground truth.

## What the Notebook Contains
| Section | Topic |
|---|---|
| 1–2 | Setup, modularity matrix, cut size vs. modularity |
| 3–4 | Null model simulation, numerical checks of properties of `B` |
| 5–6 | Spectral bisection, exactness of ΔQ |
| 7–8 | Recursive algorithm, visualisation after every split |
| 9 | Evaluation vs. ground truth, greedy modularity and Louvain |
| 10–12 | Node metrics, their evolution, and community-level analysis |
| 13–14 | Vertex-move refinement extension, discussion |
| 15–16 | Exam Q&A, references |

## How to Run
Open `Karate_Modularity.ipynb` in Google Colab (or Jupyter) and choose *Run all*.
Requires only `numpy`, `networkx`, `matplotlib` and `pandas`.
Figures are saved as PNG files next to the notebook.

## References
- M. E. J. Newman (2006). *Modularity and community structure in networks.* PNAS 103(23).
- M. E. J. Newman (2006). *Finding community structure in networks using the eigenvectors of matrices.* Phys. Rev. E 74, 036104.
- W. W. Zachary (1977). *An information flow model for conflict and fission in small groups.* J. Anthropological Research 33(4).
