---
layout: single
title: Graphs
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Graphs
* **Graphs**
    * G = (V, E)
        * V: a nonempty set of vertices
        * E: a set of edges
    * edge는 1개 혹은 2개 vertices를 가짐: endpoints
    * edge: endpoints을 연결
    * Ex) V = {a, b, c, d}, E = { {a,b}, {c,a}, {b,c}, {b,d}, {d,c} }
* **Simple graph**
    * only one edge
* **Multigraphs**
    * multiple edges
    * multiplicity m: edge 갯수
    * no loop
* **Loop**
    * connect itself
* **Pseudograph**
    * multigraphs + include loops
* **Directed Graphs**
    * G = (V, E)
        * V: a nonempty set of vertices
        * E: a set of directed edges (ordered pair of vertices)
    * (𝑢, 𝑣): start at 𝑢 and end at 𝑣
        * 𝑢: initial vertex
        * 𝑣: terminal vertex
* **Simple directed graph**
    * no loops and no multiple edges
    * (b, c) ≠ (c, b)
* **Directed multigraph**
    * multiple directed edges
    * multiplicity m: directed edges 갯수

------------

# Graph Terminology 
* **adjacent** (or **neighbors**)
    * two vertices 𝑢, 𝑣 in an undirected graph 𝐺 
    * 𝑢 —— 𝑣
* **neighborhood**
    * the set of all neighbors a vertex 𝑣 of G = (V, E)
    * N(𝑣)
    * if A is a subset of V, N(A) = ⋃𝑣∈A 𝑁(𝑣) 
* **Degree** 
    * vertex에 연결되어 있는 edge 갯수 + loop(2개)
    * deg(𝑣)
* Theorem 1(**Handshaking Theorem**)
    * 2m = ∑v∈V deg(v)
    * m = |E|
* Theorem 2
    * undirected graph의 odd degree의 vertices의 갯수는 짝수
* **In-degree**, **Out-degree**
    * in-degree of a vertex 𝑣: deg-(𝑣)
        * 𝑣에서 끝나는 edge 개수
    * out-degree of vertex 𝑣: deg+(𝑣)
        * 𝑣에서 시작하는 edge 개수
    * loop는 in-degree, out-degree 둘 다 카운트
* Theorem 3
    * |E| =  ∑v∈V deg-(v) =  ∑v∈V deg+(v)

------------

# Special Types of graphs
* **Complete Graphs**
    * Kn (n vertices)
    * 모든 vertices와 neighborhood
* **Cycles**
    * Cn (n vertices, n≥ 3)
    * edges: {𝒗𝟏, 𝑣2}, {𝑣2, 𝑣3} , ⋯ , {𝑣n-1, 𝑣𝑛}, {𝑣𝑛, 𝒗𝟏}. 
* **Wheels**
    * Cn + 모든 vertices를 연결하는 vertex
* **n-Cubes**
    * 2^n vertices (n: bit strings of length)
* **Bipartite Graphs**
    * 인접한 vertex끼리 서로 다른 색으로 칠해서 모든 vertices을 두 가지 색으로만 칠할 수 있는 그래프.
* **Complete Bipartite Graphs**
    * Km,n
    * Bipartite Graphs G에서 V1 의 모든 노드들이 V2의 모든 노드들에 인접
* **Subgraph**
    * G =(V, E), H = (W, F), 𝑊 ⊂ 𝑉 and 𝐹 ⊂ 𝐸 
    * H는 G의 subgraph (𝐻 ≠ 𝐺)
* **Union of two simple graphs**
    * The union of G1 and G2: 𝐺1 ⋃ 𝐺2 
        * the simple graph with vertex set 𝑉1 ⋃ 𝑉2 and edge set 𝐸1 ⋃ 𝐸2 
