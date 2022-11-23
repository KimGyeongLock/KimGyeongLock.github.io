---
layout: single
title: Relations
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Relations and Their Properties
* **Binary Relations**
    * a subset R ⊆ A × B
* Binary Relations on a Set
    * a subset of A × A or a relation from A to A
    * A × A의 elements 갯수 = **n^2**
    * A × A의 subset 갯수 = **2^(n^2)** = relations 갯수
* **Reflexive Relations**
    * R is **reflexive** ↔︎ (a, a) ∈ R for every element a ∈ A
    * **∀𝑥\[𝑥 ∈ 𝐴 → (𝑥, 𝑥) ∈ 𝑅\] **
    * If A = ∅ then the empty relation is reflexive vacuously. 
* **Symmetric Relations**
    * R is **symmetric** ↔︎ (b, a) ∈ R whenever (a, b) ∈ R for all a, b ∈ A
    * **∀𝑥∀𝑦\[𝑥, 𝑦 ∈ 𝐴 → ((𝑥, 𝑦) ∈ 𝑅 → (𝑦, 𝑥) ∈ 𝑅)\]**
* **Antisymmetric Relations**
    * R is **antisymmetric** ↔︎ for all a, b ∈ 𝐴 **if (a, b) ∈ 𝑅 and (𝑏, 𝑎)∈ 𝑅, then 𝑎 = 𝑏**
    * **∀𝑥∀𝑦 \[𝑥, 𝑦 ∈ 𝐴 → ((𝑥, 𝑦) ∈ 𝑅 ∧ (𝑦, 𝑥) ∈ 𝑅) → 𝑥 = 𝑦)\]**
    * ((𝑥, 𝑦) ∈ 𝑅 ∧ (𝑦, 𝑥) ∈ 𝑅) = True, (x=y) = True -> Antisymmetric
    * ((𝑥, 𝑦) ∈ 𝑅 ∧ (𝑦, 𝑥) ∈ 𝑅) = False, (x=y) = anything -> Antisymmetric
        * Ex) 𝑅 = {(𝑎, 𝑏) | 𝑎 > 𝑏} (**trivially**)
    * ((𝑥, 𝑦) ∈ 𝑅 ∧ (𝑦, 𝑥) ∈ 𝑅) = True, (x=y) = False -> Not Antisymmetric
* **Transitive Relations**
    * R is **transitive** → (a, b) ∈ 𝑅 and (b, c) ∈ 𝑅, then (a, c) ∈ 𝑅, for all 𝑎,𝑏,𝑐 ∈ 𝐴.
    * **∀𝑥∀𝑦∀𝑧\[𝑥, 𝑦, 𝑧 ∈ 𝐴 → (((𝑥, 𝑦) ∈ 𝑅 ∧ (𝑦, 𝑧) ∈ 𝑅) → (𝑥, 𝑧) ∈ 𝑅)\]**
    * ((𝑥, 𝑦) ∈ 𝑅 ∧ (𝑦, 𝑧) ∈ 𝑅) = True, (a, c) ∈ 𝑅 = True -> transitive
    * ((𝑥, 𝑦) ∈ 𝑅 ∧ (𝑦, 𝑧) ∈ 𝑅) = False, (a, c) ∈ 𝑅 = anything -> transitive
    * ((𝑥, 𝑦) ∈ 𝑅 ∧ (𝑦, 𝑧) ∈ 𝑅) = True, (a, c) ∈ 𝑅 = False -> Not transitive
* Combining Relations
    * 𝑅1 ∪ 𝑅2 
    * 𝑅1 ∩ 𝑅2
    * 𝑅1 − 𝑅2
    * 𝑅2 − 𝑅1. 
* Composition
    * R1: a relation from a set A to a set B
    * R2: a relation from a set B to a set C
    * **R2 ∘ R1**: the composition of R2 with R1, relation from A to C 
* Powers of a Relation
    * Basis Step: R^1 = R
    * Inductive Step: R^(n+1) = R^n ∘ R

----------------

# Representing Relations
* Using Matrices
    * zero-one matrix
    * mij = 1 if (ai, bj) ∈ R, mij = 0 if (ai, bj) ∉ R
* Matrices of Relations on Sets
    * reflexive relation
        * mkk = 1 (diagonal)
    * symmetric relation
        * mij = mji
    * antisymmetric relation
        * mij = 0 or mji = 0 when i≠j
* Using Digraphs
    * (a, b)
        * a: initial vertex
        * b: terminal vertex
    * **Reflexivity**
        * 모든 vertices에 loop가 필요
    * **Symmetry**
        * (x, y): edge -> (y, x): edge (왕복)
    * **Antisymmetry**
        * (x, y) with x ≠ y: edge -> (y, x): not edge 
    * **Transitivity**
        * (x, y): edge, (y, z): edge -> (x, z): edge (삼각형) 
