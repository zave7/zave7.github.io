---
title: 선형대수학 - 선형방정식
categories: linear-algebra
tags: 
  - Linear
  - Algebra
  - 선형대수학
  - 선형방정식
use_math: true
---
### 1) Linear equaiton

아래와 같이 표현되는 것이 linear equation 이다.

$$
a_{1}x_{1}+a_{1}x_{1}+a_{1}x_{1}+•••+a_{n}x_{n} = b
$$

x변수에 곱해지는 a들을 `coefficients` 라고 한다.

a변수들과 b는 `real or complex numbers(실수 혹은 허수)` 가 올 수 있다.

- linear equation이 아닌 예
    - $4x_{1}-5x_{2}=x_{1}x_{2}$ `우변 때문에 Linear equation이 아니다`
    - $x_{2}=\sqrt{x_{1}}-6$ $`\sqrt{x_{2}}$ 때문에 linear equation이 아니다`

### 2) A system of linear equations

: A collection of one or more linear equations.

아래와 같이 linear equation이 1개 이상의 집합이 존재할 경우 `system of linear equtions` 라고 한다.

$$
\Biggl\{
\begin{gather*} 
x_{1}-2x_{2}=-1\\
-x+3x_{2}=3
\end{gather*}
$$

### 3) Solution set

: The set of all possible solutions of the linear system.

linear system에서 가능한 해의 집합을 solution set이라고 한다.

- equivalent : Two linear systems are called equivalent if they have the same solution set
    
    만약 두 행렬의 solution set이 같다면 equivalent 하다라고 표현한다.
    

### 4) inconsistent, consistent

: A system of linear equations has either

system of linear equations는 다음 중 어느 하나를 만족한다.

1. no solution
2. exactly one solution
3. infinitely many solutions

### 5) Matrix notation

행렬의 표기는 아래와 같이 한다.

$$
\begin{gather*} 
x_{1}-2x_{2}+x_{3}=0\\
2x_{2}-8x_{3}=8\\
-4x_{1}+5x_{2}+9x_{3}=-9
\end{gather*}
$$

- coefficient matrix

$$
\begin{bmatrix}
1 & -2 & 1\\
0 & 2 & 8\\
-4 & 5 & 9
\end{bmatrix}

$$

- augmented matrix

: 가장 오른쪽에 

$$
\begin{bmatrix}
1 & -2 & 1 & 0\\
0 & 2 & 8 & 8\\
-4 & 5 & 9 & -9
\end{bmatrix}
$$

### 6) Elementary row operations

- replacement : 특정 row에 숫자를 곱하거나 나누어서 다른 행에 더하는 연산
- interchange : 행의 순서를 바꾸는 연산
- scaling : 특정 row에 숫자를 곱하거나 나누는 연산

⭐️ row equivalent

: row operation을 통해 같게 만들어 지는 두 행렬의 관계

`We say two matrixes are ‘row equivalent’ if there is a sequence of elementary row operations that transforms one matrix into the other.`

⭐️ 만약 두 Linear systems의 augmented matrixes가 row equivalent 하다면 두 시스템은 같은 solution set을 가진 것이다.

`If the augmented matrixes of two linear systems are row equivalent, then the two systems have the same solution set.`