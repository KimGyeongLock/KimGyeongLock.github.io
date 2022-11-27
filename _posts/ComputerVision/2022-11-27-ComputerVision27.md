---
layout: single
title: Image Compression
toc: true
toc_sticky: true
categories: Vision
published: true
---

# Introduction
* Data compression
    * Process of reducing the amount of data required to represent a given quantity of information
* During image compression, there may exist information loss
    * MSE
      <img width="258" alt="스크린샷 2022-11-27 오후 2 28 51" src="https://user-images.githubusercontent.com/63464299/204122205-423ed11c-3616-48c1-9d39-d02da3ab7515.png">
    * PSNR
      <img width="237" alt="스크린샷 2022-11-27 오후 2 29 27" src="https://user-images.githubusercontent.com/63464299/204122217-2fa9b6e8-0127-4c50-9cea-eb2d470c39e6.png">
        * the higher the better
        * 값이 낮을수록 blur 처리가 됨
* Video codec
    * Codec은 coder(compress image or video)/decoder(decompress image or video)의 합성어
    * Compression Codec
        * lossy codecs
        * lossless codecs

----------

# Basic compression methods
* Run-length coding
    * consequative same pixel value -> one pixel value
    * lossless codecs
* Golomb coding
    * currently use in MP4, MPEG4
    * 10 possible cases - 4bits(2^4=16)
    * all 0s - 1bit
    * There should be lots of zeros
    * lossless codecs
* Transform coding
    * Compress
        * input image(M×N) -> Construct n×n subimages -> Forward transform -> Quantizer -> Symbol encoder -> Compressed image
    * Decompress
        * Compressed image -> Symbol decoder -> Inverse transform -> Merge n×n subimages -> Decompressed image
* DCT(Discrete Cosine Transformation)
    * 다양한 크기와 주파수의 sinusoids의 합으로 이미지 표현
    * 이미지를 다른 중요한 부분으로 분리하는데 도움 (이미지의 시각적 품질)
        * Ex) JPEG
    * Distribution of coefficients in DCT
      <img width="444" alt="스크린샷 2022-11-27 오후 2 55 44" src="https://user-images.githubusercontent.com/63464299/204122225-5383ceb4-2a55-44d8-8d95-d2fdc045bf3c.png">

* Intra prediction
* Inter prediction(motion compensation)
    * Currently, Block Matching Algorithm is used for motion estimation
    * It is not exactly the motion
* Forward/Backward prediction

----------

# Quantization
* 정수의 정밀도를 줄임으로써 정수 값을 저장하는 데 필요한 비트 수를 줄이는 과정
* DCT 계수의 매트릭스를 감안할 때, 일반적으로 DC 계수에서 멀어지면서 계수의 정밀도를 점점 더 낮출 수 있다.
* Quantization Process
    * DCT(i,j) / Quantum(i,j) (Quantized value(i,j),반올림)
    * low-frequency elements: 소량으로만 수정
    * high-frequency areas: 대부분 0으로 감소
    * 중요하지 않은 데이터는 폐기, 이미지 정보는 압축
