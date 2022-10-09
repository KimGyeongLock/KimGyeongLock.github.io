---
layout: single
title: Ch 3. Arithmetic for computers - (4)
toc: true
toc_sticky: true
categories: Structure
published: true
---

# 4. Floating point number arithmetic

## Normalized Scientific Notation
* Scientific notation
	<br/> coefficient X (base number)^exponent
    * coefficient: 0~9까지의 한 자리 숫자
        * Ex) 7.15576 x 10^4, 0.314 x 10^1
* Normalized scientific notation
	<br/> 1 ≤ coefficient ≤ 10
    * 0.314 x 10^1 (X)
    * Binary number의 경우
        * 1.yyyy… x 2^z
        * 소수점 앞 1만 올수 있음 (0은 못옴)
* Representation: **Normalized scientific notation**
    * sign, exponent, significand : (-1)^sign x significand x 2^exponent
    * sign
        * if sign = 0, Positive floating number
        * if sign = 1, Negative floating number
    * exponent
        * bit가 커지면 훨씬 더 큰 수를 표현 (range 증가)
    * significand 
        * bit가 커지면 정확성이 올라감 
* IEEE 754 floating point standard
    * single precision (32bits)
        * float
        * sign: 1 bit
        * exponent: 8 bit
        * fraction 23 bit
            * 10진수로 6자릿수
    * double precision (64bits)
        * double
        * sign: 1 bit
        * exponent: 11 bit
        * fraction 52 bit
            * 10진수로 16자릿수

## IEEE 754 floating-point standard
Binary number의 경우
* fraction의 1 bit은 암시적으로 확정 (0은 올 수 없으니)
* Exponent: **biased** 사용
    * single precision: bias of **127**
    * double precision: bias of **1023**
    * all 0s: smallest exponent
        * exponent value = 0 - 127 = -127
    * all 1s: largest exponent
        * exponent value = 255 - 127 = 128
* (-1)^sign X (1 + fraction) X 2^(exponent - bias)


## Precision Range
* Exponent: all 0s와 all 1s 는 다른 목적으로 사용
* Smallest value
    * Exponent: 000…001
        * 1 - 127(1023) = -126(-1022)
    * Fraction: 000..00
        * 1 + fraction(0) = 1.0
    * ±1.0 × 2^-126(-1022)(2) or ±1.2(2.2) × 10^-38(-308)(10)
* Largest value
    * Exponent: 111…110
        * 254(2046) - 127(1023) = 127(1023)
    * Fraction: 111..11
        * 1 + fraction(1) = 2.0
    * **±2.0 × 2^127(1023)**(2) or ±3.4(1.8) × 10^38(308)(10)


## Floating Point Complexities
* exponent: all 0s, fraction: all 0s, sign = 0
    * 1.0 x 2^-127 (X)  **0** (O)
* exponent 범위를 벗어나게 되면 **underflow** 발생
    * 보다 정확성이 더 요구 되는 부분
    * 0.5 x 2^-129


## Denormalized Numbers
* **Exponent: all 0s**: hidden bit = 0
    * x = (-1)^S x (**0** + fraction) x 2^-Bias
    * normalized number 보다 더 작은 숫자를 표현 할 수 있음 underflow 내 숫자
* **Exponent: all 0s**, Fraction: all 0s
    * x = (-1)^S x (0 + 0) x 2^-Bias = ±0.0
    * if sign = 0 positive 0
    * if sign = 1 negative 0

## Infinities and NaNs
* **Exponent: all 1s**, Fraction: all 0s
    * ± ∞
* **Exponent: all 1s**, Fraction: Not all 0s
    * Not-a-Number (NaN)
    * 0.0 / 0.0


