---
layout: post
title:  "Discrete probability distribution"
date:   2019-10-20
---

## 이산확률변수


* 이글은 확률의 입문 제 9판 (Sheldon Ross 지음)을 참고하였습니다.

## 1. 확률변수란?
확률변수란, 표본공간에서 정의된 실수값 함수이다.
예를 들어 2개의 주사위를 던지는 경우 주사위의 합이 5인 경우를 센다면 

**주사위의 합 : 확률변수**
실제의 결과 : (1, 6) / (2, 5) / (3, 4) .. etc

일 것이다.

결국 우리는 주사위의 합에만 관심이 있고, 두 주사위의 각 값에 대해서는 실제로는 관심을 갖지 않는다.
관심의 대상이 되는 양인 주사위의 합이 **확률변수(Random Variable)**가 된다.

확률변수의 값은 실험의 결과에 의해 결정되기 때문에 확률변수의 가능한 값에 확률을 부여할 수 있다.
ex) 주사위를 1번 던졌을 때 2가 나올 확률 $$$[X=2] = {1\over6}$$$

우리가 확률변수를 문제에서 본다면,

**(1) 확률변수의 정의를 정의하고 $$$X$$$
(2) 확률변수가 가질 수 있는 범위를 정의해야 한다. $$$ [X = 1, 2, .. n]$$$
(3) 확률변수의 각 확률을 구한다. $$$ Pr[X = i]$$$
(4) 마지막으로 확률변수의 각 확률의 합이 1인지 확인해야 한다. $$$  \sum_i Pr[X = i]=1$$$**

## 2. 누적분포함수

확률변수 X에 대해
$$
F(x) = P[X=x],  {-\infty< x <\infty}
$$
로 정의된 함수 F를 **X의 누적분포함수(cumulative distribution function) 또는 간단히 분포함수(distribution function)**라 한다.
분포함수는 **모든 실숫값 x에 대해 확률변수가 x이하일 확률**을 나타낸다.

## 3. 확률질량함수

**이산확률변수(discrete random variable)란, 셀 수 있는 값들을 갖는 확률변수이다.**
이산확률변수 X에 대해서 **확률질량함수(probability mass function)** 즉, **p(a)**를 다음과 같이 정의한다.

$$
p(a) = P[X = a]
$$
즉, **확률변수가 a를 가질 확률이 확률질량함수(pmf라 통칭하자)**인 것이다.

이산확률변수인 확률질량함수는 이러한 성질을 가진다.
$$
p(a)>= 0
$$
$$
\sum_{i=1}^{\infty}p(x_i) = 1
$$
각 확률질량함수의 값은 0보다 크거나 0일 수 있고, 모든 확률질량함수를 더하면 1이다.(모든 확률의 합이므로)
확률질량함수의 합이 결국에 누적분포함수가 되므로 다음과 같이 나타낼 수 있다.
$$
F(a) = \sum_{x\leq a}p(x)
$$
a보다 작거나 같은 확률질량함수를 모두 합하면 누적분포함수가 된다.

## 4. 이산확률변수의 기댓값

이산확률변수 $$$p(x)$$$의 기댓값은 다음과 같이 정의한다.
$$
E[X] = \sum_{x:p(x)>0} xp(x)
$$

즉, $$$X$$$가 택할 수 있는 가능한 값($$$x$$$)에 각각 그 값을 택할 확률( $$$p(x)$$$ )이 가중된 가중평균이다.
확률변수 $$$X$$$가 가질 수 있는 값 각각에 나타날 확률 $$$p(x)$$$을 곱하여 평균을 구한다. 

## 5. 이산확률변수의 함수의 기댓값

그렇다면, $$$E[X^2]$$$를 구하고 싶다면, 어떻게 해야 할까?
**방법은 $$$X^2$$$를 $$$Y$$$라고 취급한 뒤, $$$E[Y]$$$를 구하는 것이다.**

**$$$X$$$가 택할 수 있는 가능한 값이 $$$X^2$$$로 각각 변한다고 해도, 그 값을 택할 확률( $$$p(x)$$$ )은 변하지 않기 때문이다.**

예를 들어보면, $$$X$$$가 $$$ -1,0, 1$$$의 값을 가지는 확률변수로 대응되는 각 확률이 
$$P[X= -1] = 0.2
$$
$$
P[X= 0] = 0.5
$$
$$
P[X= 1] = 0.3
$$
이면, $$$ X^2$$$의 확률질량함수는 
$$P[X= (-1)^2] = 0.2
$$
$$
P[X= (1)^2] = 0.3 
$$
$$
P[X^2 = 1] = 0.2 + 0.3 = 0.5
$$
$$
P[X^2 = 0] = 0.5
$$
$$
E[X^2] = 1 * 0.5 + 0 * 0.5 = 0.5
$$
이다. 

$$$Y$$$를 $$$g(x)$$$라고 하자. 그렇다면
$$E[g(X)] = \sum_{i} g(x_i)p(x)
$$
으로 계산한다고 말할 수 있다.

## 5. 여러가지 이산확률변수

 이제 여러가지 이산확률변수의 범위와 특징, 평균, 분산을 배워보자.

### 5-1. 베르누이 확률변수

(1) 확률변수의 정의 : 결과가 '성공' 또는 '실패'로 분류될 수 있는 시행이나 실험. 
(2) 확률변수가 가질 수 있는 범위 : $$$ [X = 0, 1]$$$
(3) 확률변수의 각 확률 :
$$p(x) = p^x(1-p)^{1-x}$$
$$ Pr[X = 0] = 1 - p$$
$$ P[X=1] = p$$

(4) 마지막으로 확률변수의 각 확률의 합이 1인지 확인 : $$$  \sum_i Pr[X = 0, 1]=p + (1 - p)=1$$$
(5) 평균 : $$$E[X] = p $$$
(6) 분산 : $$$Var[X] = p(1-p)$$$

### 5-2. 이항확률변수

(1) 확률변수의 정의 : 베르누이 시행을 n번 독립적으로 시행하여 발생한 성공의 횟수
(2) 확률변수가 가질 수 있는 범위 : $$$ [X = 0, 1, ... n]$$$
(3) 확률변수의 각 확률 :
$$p(i) = \binom{n}{i}p^i(1-p)^{n-i}$$


(4) 마지막으로 확률변수의 각 확률의 합이 1인지 확인 : $$$  \sum_i Pr[X = 0, 1,..n]=\sum_{i=0}^{n}\binom{n}{i}p^i(1-p)^{n-i}=[p + (1-p)]^n=1$$$

why?) 이항정리에 의해서 $$$\sum_{k=0}^{n}\binom{n}{k}x^k(y)^{n-k} = (x + y)^n $$$
(5) 평균 : $$$E[X] = np $$$
(6) 분산 : $$$Var[X] = np(1-p)$$$

### 5-3. 푸아송 확률변수

(1) 확률변수의 정의 : 짧은 구간에서 발생하는 사건의 갯수(n이 크고, p가 작을 때 이항 확률변수의 근사)
(2) 확률변수가 가질 수 있는 범위 : $$$ [i = 0, 1, ... ]$$$
(3) 확률변수의 각 확률 :
$$p(i) = e^{-\lambda}{\lambda^{i}\over i!}$$
$$
i = 0, 1, 2...\infty
$$

(4) 마지막으로 확률변수의 각 확률의 합이 1인지 확인 : $$$  \sum_i Pr[X = 0, 1,..\infty]=1$$$
(5) 평균 : $$$E[X] = np = \lambda $$$
(6) 분산 : $$$Var[X] = np(1-p) = \lambda$$$ (why? $$$(1-p)$$$가 충분히 작기 때문에)

### 5-4. 기하 확률변수

(1) 확률변수의 정의 : 성공확률이 $$$p$$$, $$$0 < p < 1$$$인 독립시행에서 최초로 성공할 때까지 필요한 시행횟수
(2) 확률변수가 가질 수 있는 범위 : $$$ [n = 1, 2...\infty ]$$$
(3) 확률변수의 각 확률 :
$$P[X=n]= p(n) = (1-p)^{n-1}p$$
$$
n = 1, 2...\infty
$$

(4) 마지막으로 확률변수의 각 확률의 합이 1인지 확인 : 
$$$  \sum_{n = 1}^{\infty} Pr[X = n]= p\sum_{n = 1}^{\infty}(1-p)^{n-1}={p \over {1 - (1 -p)}}=1$$$
(5) 평균 : $$$E[X] = {1 \over p} $$$
(6) 분산 : $$$Var[X] = {1-p \over p}$$$

### 5-5. 음이항 확률변수

(1) 확률변수의 정의 : 성공확률이 $$$p$$$, $$$0 < p < 1$$$인 독립시행을 n번 하여 총 r번 성공할 때까지 필요한 시행횟수
(2) 확률변수가 가질 수 있는 범위 : $$$ [n = r, r +1, ..\infty ]$$$
(3) 확률변수의 각 확률 :
$$P[X=n]= p(n) =\binom{n-1}{r-1} p^r(1-p)^{n-r}$$
$$
n = r, r+1...\infty
$$

(4) 마지막으로 확률변수의 각 확률의 합이 1인지 확인 : 
$$$  \sum_{n = r}^{\infty} Pr[X = n]= \sum_{n = r}^{\infty}\binom{n-1}{r-1} p^r(1-p)^{n-r}=1$$$
why? ) $$$r$$$번 성공하기 위해 필요한 시행횟수는 첫번째 성공할 때까지 필요한 시행횟수 + 두번째 성공할 때까지 추가된 시행횟수 +... $$$r$$$번째 성공할 때까지 추가된 시행횟수와 같다. 그러므로 (4) 의 값은 유한이고 확률을 모두 더하면 1이 된다.

(5) 평균 : $$$E[X] = {r \over p} $$$
(6) 분산 : $$$Var[X] = {(1-p)r \over p^2}$$$


- - -


다른 이항확률변수도 있지만, 이 포스트에서는 음이항 확률변수까지 다루기로 한다.
확률변수는 확률변수의 범위가 유한한지, 무한한지에 따라서 나뉜다고 배웠었다.
다음에는 무한한 확률변수를 가지는 연속확률변수를 알아보자.
