---
layout: single
title: Discrete Probability2
toc: true
toc_sticky: true
categories: Discrete
published: true
---

# Bayes’ Theorem
* **Bayes’ Theorem**
    * <img width="374" alt="스크린샷 2022-11-15 오전 2 53 40" src="https://user-images.githubusercontent.com/63464299/201731530-bc39b7d6-0b0d-4ba5-a646-3a811b1bc6d1.png">
    * p(E)≠ 0 and p(F) ≠ 0 
* Generalized Bayes’ Theorem
    * 𝑝(𝐹j\|𝐸)= 𝑝(𝐸|𝐹j)𝑝(𝐹j) / ∑𝑝(𝐸|𝐹i)𝑝(𝐹i)
    * p(E)≠ 0 for i = 1, 2, ..., n
* Bayesian Spam Filters
    * B: set of spam messages
    * G: set of non-spam messages
    * w: particular word
    * nB(w), nG(w): the number of messages that it occurs in B and G
    * p(w): w가 포함된 스팸 메시지의 확률
        * p(w) = nB(w) / \|B\|
    * q(w): w가 포함된 스팸이 아닌 메시지의 확률
        * q(w) = nG(w) / \|G\|
    * S: the event that the message is spam
    * E: the event that the message contains w
    * p(S\|E) = p(E\|S)p(S) / p(E\|S)p(S) + p(E\|S-bar)p(S-bar)<br/>
      p(S\|E) = p(E\|S) / p(E\|S) + p(E\|S-bar) (p(S)=p(S-bar) = 1/2)<br/>
      r(w) = p(w) / (p(w) + q(w))
* Bayesian Spam Filters using Multiple Words
<img width="345" alt="스크린샷 2022-11-15 오전 2 51 45" src="https://user-images.githubusercontent.com/63464299/201731257-16f13d04-88e5-4ad9-941c-147554ca47cd.png">
