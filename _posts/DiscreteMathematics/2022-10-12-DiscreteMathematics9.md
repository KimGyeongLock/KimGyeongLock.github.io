Induction

# Principle of Mathematical Induction
* **P(n) is true for all positive integers n** 증명
    * **Basis Step**
        * **P(1) is true** 증명
    * **Inductive Step**
        * **P(k) → P(k+1) is true for all positive integers k** 증명
        * P(k) : inductive hypothesis

# Proving a summation formula by Mathematical Induction
* Mathematical induction (the rule of inference)
    * ( P(1) ∧ ∀k(P(k) → P(k+1) ) → ∀nP(n)
    * U = the set of positive integers
* Strong Induction
    * ( (P(1) ∧ P(2) ∧ … ∧ P(k)) → P(k+1) ) → ∀nP(n)
    * U = the set of positive integers

# SOME USEFUL SUMMATION FORMULAE 

* ∑i = n(n+1) / 2
* ∑i^2 = n(n+1)(2n+1) / 6
* ∑i^3 = n^2(n+1)^2 / 4

* ∑i = n(n+1) / 2
* Basis Step : P(1) = 1(1+1)/2 = 1 (true)
* Inductive Step: P(k) -> P(k+1)
    * P(k+1) = 1+2+…+k+(k+1) = k(k+1)/2 + (k+1) = k(k+1) + 2(k+1) / 2 = (k+1)(k+2)/2

# Conjecturing a formula

* 1=1, 1+3=4, 1+3+5=9, 1+3+5+7=16, 1+3+5+7+9=25
* Conjecture(추측)
    * 1+3+5+…+(2n-1) = n^2
* Basis Step: P(1) = 1^2 = 1 (true)
* Inductive Step: P(k) -> P(k+1)
    * Inductive Hypothesis: P(k) = 1+3+5+…+(2k-1) = k^2
    * P(k+1) = 1+3+5+…+(2k-1)+(2k+1) = k^2 + (2k+1)  = k^2 + 2k + 1 = (k+1)^2

# Proving Inequalities
* P(n): n < 2^n
* Basis Step: P(1) = 1 < 2^1 = 2 (true)
* Inductive Step: P(k) -> P(k+1)
    * P(k+1): k+1 < 2^k + 1 < 2^k + 2 < 2^k + 2^k = 2x2^k = 2^(k+1)
