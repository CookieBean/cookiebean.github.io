---
title: Single Quantum Gate
author: CookieBean
date: 2025-03-11 15:33:00 +0800
categories: [Blogging, QuantumComputing]
tags: [quantum_computing, quantum_informatics, quantum_gate]
pin: false
math: true
mermaid: false
---

![Desktop Mode](../assets/img/qc/1.3/thumbnail.jpg)
_Image from Bailey Zindel https://unsplash.com/ko/@baileyzindel_

## Quantum Gates

고전컴퓨터가 Wire와 Gate들로 이루어 진것처럼, Quantum Informatics를 위해서는 당연히 Qubit들을 Input으로 받는 Gate들이 필요하다. 하지만 이러한 양자컴퓨터의 게이터들은 고전적으로 알려진 법칙 (가령 **NAND Gate로 모든 Gate들을 만들어낼 수 있다**) 등이 성립하지 않는 등 일부분 차이가 있다. 본 글에서는 다양한 양자컴퓨터의 게이트들을 알아보기 전에 Single Qubit에 적용되는 게이트들부터 소개하려고 한다.

## Not Gate - $X$

고전컴퓨터의 Not 게이트는 아주 간단한 형태로 표현된다. 아래 그림은 고전컴퓨터에서의 Not 게이트의 회로표현이다.

![Desktop Mode](../assets/img/qc/1.3/not.png)
_https://en.wikipedia.org/wiki/Inverter_(logic_gate)_

Wire A에 들어오는 값이 0이라면 1을 내뱉고, 1이라면 0을 내뱉는 아주 단순한 게이트이다. 한편 고전컴퓨터에서 A는 0 또는 1의 값만 가질 수 있기에 모든 Input의 경우에 대해서 Output을 명시하는게 가능하다. 이러한 표현법을 진리표라고 부르고, Not의 진리표는 아래처럼 쓸 수 있다.

| Input | Output | 
| :---- | :----- |
| 0     | 1      |
| 1     | 0      |
_Truth Table of Not Gate_

한편 양자컴퓨터는 $\ket{0}$이나 $\ket{1}$만 존재하는 상태보다 이 둘이 적당히 중첩된 $\alpha\ket{0} + \beta\ket{1}$과 같은 상태로 존재하기 마련이다. 따라서 Input이 0혹은 1이 아닌 경우에는 어떻게 동작해야 하는지 고민이 필요하다. 이러한 고민을 보다 간편하게 해결하기 위해 회로를 수학적으로 접근해보자. 

사실 모든 고전컴퓨터의 게이트는 하나의 행렬로 표현할 수 있다. 가령 위의 Not Gate의 경우, Input으로 들어오는 Wire A는 두 가지의 가능한 경우, 0 혹은 1이 있다. **Linear Algebraic**하게 이를 바라보아 $\begin{bmatrix}1 \\ 0\end{bmatrix}$과 $\begin{bmatrix}0 \\ 1\end{bmatrix}$로 표현해보자. 이때 Not Gate는

$$
\begin{equation}
  X \equiv
  \begin{bmatrix}
    0 & 1 \\
    1 & 0 \\
  \end{bmatrix}
\end{equation}
$$

로 쓸 수 있다.

> 사실상 행렬표현이 진리표와 동일한건 Input을 저렇게 정의했기에 당연한 수순이다.
{: .prompt-tip}

이렇게 쓰고나면, 고전컴퓨터의 NOT 게이트가 양자컴퓨터에서 어떻게 확장될지는 보다 자명하게 느껴진다. Input으로 들어오는 Qubit의 상태를 위와 동일하게 아래처럼 쓸 수 있다.

$$
\begin{equation}
  \ket{\psi} = \alpha\ket{0} + \beta\ket{1} = 
  \begin{bmatrix}
    \alpha \\
    \beta
  \end{bmatrix}
\end{equation}
$$

이제 이 Qubit를 $(1)$에 표현된 고전 NOT Gate에(그런 Gate가 있다고 생각하고) 통과시키면

$$
\begin{equation}
  \begin{bmatrix}
    \beta \\
    \alpha
  \end{bmatrix}
   = 
  \begin{bmatrix}
    0 & 1 \\
    1 & 0
  \end{bmatrix}
  \begin{bmatrix}
    \alpha \\
    \beta
  \end{bmatrix}
\end{equation}
$$

를 얻는다. 즉, $\beta\ket{0} + \alpha\ket{1}$을 얻는 셈이다. 이게 바로 양자컴퓨터에서의 Not Gate이며 이 Gate는 실제로 존재한다. 왜 Not Gate가 이렇게 고전컴퓨터처럼 예쁘게 작동하는지는 양자역학에서 그 이유를 찾을 수 있다. 물론 이 글을 쓰고있는 본인도 이에 대해서는 잘 알고있지 않으며, linear이 아니라 non-linear하게 이들이 동작할 경우 몹시 이상한 결과들(시간여행, 빛 보다 빠른 정보전달, 열역학 제 2법칙 위배 등)이 도출된다는것만 알고있으면 된다.

한편 이 양자컴퓨터의 게이트에는 특별한 특징이 있는데, 그건 바로 게이트를 행렬로 표현했을때 Unitary라는 것이다. 아래는 이에 대한 증명이다.

> Unitary Matrix는 자신과 Hermitian transpose를 곱한 행렬이 항등행렬인 행렬이다. 이와 관련한 자세한 성질은 [여기](https://en.wikipedia.org/wiki/Unitary_matrix)를 참조하라
{: .prompt-tip}

<div class="box">
<strong>Thm.</strong> 
모든 양자컴퓨터 게이트는 Unitary이다.
</div>

<blockquote>

pf) Qbit가 가지는 중요한 특징 중 하나는 바로 각 상태마다 계수의 크기 제곱이 확률이기에 이들을 전부 합치면 1이라는 점이다. 즉, 다시말해 Qbit의 각 상태가 벡터공간의 basis라고 생각하면 이 벡터의 크기는 1이다. 따라서, $n$개 Qbit의 상태를 아래와 같이 표현할 수 있다.

$$
\begin{equation}
  \ket{\psi} =
  \begin{bmatrix}
    a_1 \\ a_2 \\ \vdots \\ a_{2^n} 
  \end{bmatrix}
\end{equation}
$$

$$
\begin{equation}
  \vert\psi\vert^2 = 
  \sum_{i} |a_i|^2 = 1
\end{equation}
$$

그런데, 이 제한조건$(5)$는 Gate를 통과한 이후에도 여전히 적용되어야 하므로 게이트 $A$에 대해 아래가 성질이 만족되어야 한다.

$$
\begin{equation}
  \vert G\psi\vert^2 = \braket{G\psi \vert G\psi} = 1
\end{equation}
$$

한편 Unitary Matrix의 정의에 의해

$$
\begin{equation}
  \braket{G\psi \vert G\psi} = \braket{\psi \vert G^\dagger G \psi} = \braket{\psi \vert G^\dagger G \vert \psi} = 1
\end{equation}
$$

가 성립한다. 여기서 $G^\dagger G$를 $\mathbb{C}^{2^n} \rightarrow \mathbb{C}^{2^n}$인 선형연산자 $T$로 보면

$$
\begin{equation}
  \forall \psi \in \mathbb{C}^{2^n}, T(\psi) = \psi
\end{equation}
$$

가 성립한다. 이러한 선형연산자는 항등연산자로 유일하기에 $G^\dagger G = I = G G^\dagger$가 성립한다. 따라서. G는 Unitary Matrix이다.

</blockquote>

놀라운 사실은 이 Unitary Matrix조건은 Quantum Gate가 되기 위한 충분조건도 된다! 이는 추후 글에서 다룰 계획이다.

## Z Gate - $Z$

단일 비트를 받는 게이트가 Not Gate로 하나였던 고전컴퓨터와 달리 양자컴퓨터는 여러개의 Single Bit Gate가 있다. $Z$ Gate도 그 중에 하나이며, 이 게이트는 추후에 직접 사용하는 시점에서 더 자세히 설명하겠다.

$$
\begin{equation}
  Z \equiv
  \begin{bmatrix}
    1 & 0 \\
    0 & -1
  \end{bmatrix}
\end{equation}
$$

역시 $Z^\dagger Z = Z Z^\dagger = I$임이 성립함은 쉽게 확인할 수 있다.

## 아다마르 게이트 - $H$

단일 Qbit 게이트 중에서 가장 중요한 역할을 맡는 Hadamard Gate $H$이다. 먼저 생김새를 보면

$$
\begin{equation}
  H \equiv
  \frac{1}{\sqrt{2}}
  \begin{bmatrix}
    1 & 1 \\
    1 & -1
  \end{bmatrix}
\end{equation}
$$

와 같이 생겼는데, $X$ 게이트나 $Z$ 게이트에서는 볼 수 없는 *중첩*이 일어난다는 점이 특징이다. 당연히 $H^\dagger H = H H^\dagger = I$가 만족됨은 간단한 계산으로 살펴볼 수 있다. 그리고 Linear Algebra에 관심있는 사람이라면 이 $H$ 게이트가 사실상 회전변환과 동일하게 생겼다는점을 이해할 수 있다. 
