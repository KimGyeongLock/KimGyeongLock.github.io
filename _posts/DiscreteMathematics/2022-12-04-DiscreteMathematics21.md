---
layout: single
title: Graphs2
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Representing Graphs
* **Adjacency Lists**
    * **no multiple edges** graph를 표현
    * 각 vertex에 **인접**한 vertices specify
    * **sparse graph**: edge가 적은 graph
* **Adjacency Matrices**
    * **no loop and multiple edges**
        * 𝑛 × 𝑛 zero-one matrix 
        * vi와 vj가 **인접하면 1**, 인접하지 않으면 0
        * loop가 없으면, 대각선은 모두 0
        * undirected graph: **symmetric**
        * **dense graph**: edge가 많은 graph
    * **loop and multiple edges**
        * (i, j)번째 entry = edges의 갯수
    * **directed graphs**
        * vi에서 vj가 **edge**이면 (i,j) = 1
        * **not symmetric**
        * aij = vi, vj에 연결되어 있는 edges 갯수
* **Incidence Matrices**
    * **undirected** graph
    * 𝑛 × 𝑚 matrix M = \[mij\]
    * edge ej가 vi에 의해 발생했을 때 mij = 1

---------------

# Graph Isomorphism
* simple graph G1 = (V1, E1), G2 = (V2, E2)
* **one-to-one** and **onto function** from V1 to V2
* a와 b가 G1에서 인접 ↔︎ G2에서 f(a), f(b)는 인접
* not isomorphic: nonisomophic
* isomorphic한지 확인 방법
	1. number of vertices and edges 확인
	2. degree 갯수 확인
	3. 인접하는 degree 개수 확인

---------------

# Connectivity
## Term
* **Path**
    * sequence of edges
* path of **length** n
    * a sequence of n edges
* **circuit**
    * 시작과 끝이 같은 vertex
    * length n > 0
* **pass through** the vertices
* **traverse** the edges
* **simple** path or circuit
    * 한번 이상 같은 edge를 포함X
* Counting Paths
    * adjacency matrix 사용


## Connectedness
* Connectedness in **Undirected** Graphs
    * 모든 vertices의 짝 사이에 path가 존재
    * disconnected : vertices나 edges, both 제거
* **Connected Components**
    * disconnected graph
        * two or more connected components (disjoint)
        * components의 union = graph
* Connectedness in **Directed** Graphs
    * **Strongly connected**
        * a에서 b까지의 path, b에서 a까지의 path가 둘다 있는 경우
    * **Weakly connected**
        * undirected graph였으면 모든 두 vertices 사이에 path 존재
* **Strongly Connected Components**
    * maximal strongly connected subgraphs
    * 더 큰 strongly connected subgraphs가 붙어 있으면 안됨

---------------

# Euler Graphs
* **Euler circuit**
    * **모든 edge를 포함**하는 simple circuit
    * simple circuit: **한번 이상 같은 edge 포함x**
    * deg(initial vertex) : even degree
    * other vertex: even degree
* **Euler path**
    * **모든 edge를 포함**하는 simple path
    * simple path: **한번 이상 같은 edge 포함x**
    * initial vertex, final vertex : odd degree = **two vertices of odd degree**
    * other vertex: even degree

---------------

# Hamiltonian Graphs
* **Hamilton circuit**
    * **모든 vertex를 한번만** pass through 하는 simple circuit
* **Hamilton path**
    * **모든 vertex를 한번만** pass through 하는 simple path
* **Dirac’s Theorem**
    * Hamilton circuit
        * 모든 vertex의 degree ≥ 𝑛/2 인 3개 이상 vertices를 가진 simple graph
        * n: vertex 갯수
* **Ore’s Theorem** 
    * Hamilton circuit
        * 인접하지 않은 vertices의 모든 쌍에 대해 deg(u) + deg(v) ≥ n과 같은 3개 이상 vertices를 가진 simple graph
