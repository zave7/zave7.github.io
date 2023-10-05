---
title: 선형대수학 - 사다리꼴행렬
categories: Linear-Algebra
tags: 
  - Linear
  - Algebra
  - 선형대수학
  - 선형방정식
  - Echelon
use_math: true
---

# 2. Row Reduction and Echelon Forms

### 1) A nonzero row or column

: 0이 아닌 원소가 존재하는 행 또는 열

- **nonzero row**

$$
\begin{bmatrix}
0 & 0 & 0 & 3 & 0 & 0
\end{bmatrix}
$$

- **nonzero column**

$$
\begin{bmatrix}
0\\
0\\
0\\
3\\
0\\
0
\end{bmatrix}
$$

### 2) A Leading entry of row

: the leftmost nonzero entry / 0이 아닌 가장 왼쪽의 원소

$$
\begin{bmatrix}
1 & -2 & 1 & 0\\
0 & 2 & -8 & 8\\
0 & 0 & 0 & 77
\end{bmatrix}
$$

**nonzero entry**

- 1 row → 1
- 2 row → 2
- 3 row → 77

### 3) Echelon form

1. 모든 nonzero rows는 모든 zero 행보다 `위에` 있다.
2. 각 행의 `Leading entry(선행 원소)`는 바로 위 행의 leading entry 가 있는 열 `오른쪽`에 있다.
- `All nonzero rows are above any rows of all zeros.`
- `Each leading entry of a row is in a column to the right of the leading entry of the row above it.`

$$
\begin{bmatrix}
● & * & * & *\\
0 & ● & * & *\\
0 & 0 & 0 & 0\\
0 & 0 & 0 & 0\\
\end{bmatrix}
$$

$$
\begin{bmatrix}
● & * & * & * & * & * & *\\
0 & 0 & ● & * & * & * & *\\
0 & 0 & 0 & 0 & ● & * & *\\
0 & 0 & 0 & 0 & 0 & ● & *\\
\end{bmatrix}
$$

### 4) Reduced echelon form

1. 각각의 nonzero 행에서 leading entry 는 1이다.
2. 값이 1인 각각의 leading entry는 해당 컬럼에서 유일한 nonzero entry이다.
- `The leading entry in each nonzero row is 1.`
- `Each leading 1 is the only nonzero entry in its column.`

**pivot position**

$$
\begin{bmatrix}
1 & * & * & * & * & * & *\\
0 & 0 & 1 & * & * & * & *\\
0 & 0 & 0 & 0 & 1 & * & *\\
0 & 0 & 0 & 0 & 0 & 1 & *\\
\end{bmatrix}
$$

- row 1 → (1, 1)
- row 2 → (2, 3)
- row 3 → (3, 7)
- row 4 → (4, 8)

<aside>
💡 [ Theorem 1 ]
- Uniqueness of the Reduced Echelon Form

각 행렬은 하나의 감소된 각 행렬에 대해 row equivalent 하다.
다시말해 각각의 행렬은 1개의 reduced echelon form 만을 가진다.
`Each matrix is row equivalent to one and only one reduced echelon matrix.`

</aside>

### 5) Row reduction algorithm

- Step 1
    - 맨 왼쪽 nonzero column부터 시작한다
    `begin with the leftmost nonzero column`
- Step 2
    - nonzero entry를 찾고 interchange 연산을 한다
    `select a nonzero entry in the pivot column as a pivot. If necessary, interchange rows to move this entry into the pivot position`
- Step 3
    - row replacement 연산을 통해 pivot 아래를 모두 zero로 만든다
        
        `row replacement to create zeros in all positions below the pivot`
        
    - 행렬 왼쪽의 `~` 는 row equivalent 하다는 뜻이다
- Step 4
    - Step 1-3 를 반복한다.
    `apply steps 1-3 to the submatrix that remain`
- Forward phase
    - 여기까지 과정을 foward phase 라고 한다
    `The combination of step 1-4 is called forward phase echelon form`
    - forward phase 를 통해 echelon form을 만든다
- Step 5
    - pivot 위를 모두 zero로 만든다
    `Beginning with the rightmost pivot and working upward and to the left, create zeros above each pivot. If a pivot is not 1, make it 1 by a scaling operation`
- Backward phase
    - Step 5 과정을 Backward phase 라고 한다
    `Step 5 is called backward phase reduced echelon form`
    - backward phase를 통해 reduced echelon form을 만든다

### 6) Solution of linear systems

$$
\begin{bmatrix}
1 & 0 & -5 & 1\\
0 & 1 & 1 & 4\\
0 & 0 & 0 & 0
\end{bmatrix}
$$

$$
\begin{align*}
x_{1}-5x_{3}=1\\
x_{2}+x_{3}=4\\
0=0
\end{align*}\quad

\begin{bmatrix}
6\\
3\\
1\\
\end{bmatrix}

\begin{bmatrix}
-9\\
6\\
-2\\
\end{bmatrix}
●●●
$$

- basic variables(leading variables) : `x1, x2`
    
    무한한 해를 가졌을 경우 변수는 basic과 free로 나뉜다. pivot 값이 1인 변수가 basic이 되고, 나머지 변수는 free 변수가 된다.
    

- 아래 같이 표현된 솔루션을 `general solution`이라고 한다.

$$
\Biggl\{\quad
\begin{gather*}
x_{1}=1+5x_{3}\\
x_{2}=4-x_{3}\\
x_{3}\text{ is free}
\end{gather*}
$$

Example. find the general solution of the following augmented matrix

$$
\begin{bmatrix}
1 & 5 & -1 & 2 & 4\\
0 & 2 & 3 & 2 & 1\\
0 & 0 & 3 & 5 & 7
\end{bmatrix}
$$

$$
(1)\quad\sim
\begin{bmatrix}
1 & 5 & -1 & 2 & 4\\
0 & 1 & \frac{3}{2} & 1 & \frac{1}{2}\\
0 & 0 & 3 & 5 & 7
\end{bmatrix}
$$

$$
(2)\quad\sim
\begin{bmatrix}
1 & 0 & \left ( - \frac{17}{2} \right ) & -3 & \frac{3}{2}\\
0 & 1 & \frac{3}{2} & 1 & \frac{1}{2}\\
0 & 0 & 3 & 5 & 7
\end{bmatrix}
$$

$$
(3)\quad\sim
\begin{bmatrix}
1 & 0 & \left ( - \frac{17}{2} \right ) & -3 & \frac{3}{2}\\
0 & 1 & \frac{3}{2} & 1 & \frac{1}{2}\\
0 & 0 & 1 & \frac{5}{3} & \frac{7}{3}
\end{bmatrix}
$$

$$
(4)\quad\sim
\begin{bmatrix}
1 & 0 & \left ( - \frac{17}{2} \right ) & -3 & \frac{3}{2}\\
0 & 1 & 0 & \left ( - \frac{3}{2} \right ) & -2\\
0 & 0 & 1 & \frac{5}{3} & \frac{7}{3}
\end{bmatrix}
$$

$$
(5)\quad\sim
\begin{bmatrix}
1 & 0 & 0 & \left ( - \frac{103}{6} \right ) & \left ( - \frac{110}{6} \right )\\
0 & 1 & 0 & \left ( - \frac{3}{2} \right ) & -2\\
0 & 0 & 1 & \frac{5}{3} & \frac{7}{3}
\end{bmatrix}
$$

$$
\begin{align*}
x_{1} - \frac{103}{6}x_{4} = -\frac{110}{6}\\
x_{2} - \frac{3}{2}x_{4} = -2{3}\\
x_{3} +\frac{5}{3}x_{4} = \frac{7}{3}
\end{align*}
$$

$$
\left\{
\begin{gather*}
x_{1} = \frac{103}{6}x_{4}-\frac{110}{6}\\
x_{2} = \frac{3}{2}x_{4}-2{3}\\
x_{3} = -\frac{5}{3}x_{4}+\frac{7}{3}\\
x_{4} \text{ is free }
\end{gather*}
\right\}
$$

<aside>
💡 [Theorem 2]
- Existence and Uniqueness Theorem

$$
\begin{bmatrix}
1 & 6 & 2 & -5 & -2 & -4\\
0 & 0 & 2 & -8 & -1 & 3\\
0 & 0 & 0 & 0 & 0 & 7
\end{bmatrix}
\quad\quad
0 = 7?
$$

- augmented matrix에 row reduction을 통해서 구한 reduced echelon form에서 맨 오른쪽 컬럼이 pivot 컬럼이 아닌 경우에만 해가 존재한다.
- consistent 한 linear system의 경우 free variable이 없을 경우에 unique solution 을 가지고, 1개 이상의 free variable이 존재할 경우에는 무한히 많은 해를 가진다.

```Plain text
A linear system is `consistent` if and only if the rightmost column of the augmented matrix is not a pivot column - that is, if and only an `echelon form` of the `augmented matrix` has no row of the forms

$`[0\quad・・・\quad0\quad b]\quad \text{with b is nonzero}`$

If a linear system is consistent, then the solution set contains either (i) a `unique` solution, when there are `no free` variables, or (ii) `infinitely` many solutions, then there is `at least one free` variables.
```


</aside>