# Dynamic Programming(동적 계획법) 
> &nbsp;동적 계획법이란 메모리를 적절히 사용하여 수행 시간의 효율성을 비약적으로 향상시키는 방법이다. 
> 또한 특정 범위까지의 최적해를 구하기 위해 이전에 구한 최적해를 기반으로 규칙성을 파악하여 다음 값을 구하는 것이라고 생각할 수 있다.

## Dynamic Programming의 속성
- Overlapping Subproblem(부분 문제가 겹칠 경우)
   - 이전에 구한 최적해(부분 문제)를 기반으로 다음 문제의 최적해(전체 문제)를 구할 수 있는 구조여야 한다. 
   따라서 부분 문제가 전체 문제의 최적해라고 보장되어 있는 구조여야한다.
   - 이러한 구조를 갖는 경우는 대표적으로 "경유지를 거쳐 목적지로 가는 문제"가 있다.
  
- Optimal Substructure(최적 부분 구조일 경우)
   - 부분 문제들이 반복되는 경향이 존재한다는 의미이다. 부분 문제를 나누어 가는 과정에서 
   하위 문제와 상위 문제의 관계가 반복되는 경향이 존재한다는 것이다.
   - 
## 접근 방법

### Top_Down
- 재귀를 이용하는 방식
- 전체 문제부터 시작하여 가장 작은 문제(기저 문제)까지 호출한 뒤 거꾸로 다시 올라오는 방식이다. 올라오면서 해결한 값을 
Memoization(저장)하며 값을 재활용해 문제를 해결하는 구현 방식이다. 
- Memoization : 반복되는 결과를 메모리에 저장하여 호출 되었을 때 한 번 더 계산하지 않고 메모리에서 꺼내와 재활용하는 것

### Bottom_Up
- 반복문을 이용하는 방식
- 가장 작은 문제(기저 문제)부터 시작하여 그 값들을 Tabulation(도표화)하고 값을 재활용해 다음 문제를 순차적으로 해결하면서 전체 문제까지 
해결하는 방식이다. 
- Tabulation

## Dynamic Programming 유형
- Coin Change Problem
- KnapSack
- LCS
- LIS
- Edit Distance
- Matrix Chain Multiplication

## Dynamic Programming을 이해하기
> &nbsp;동적 계획법을 이해할 때 가장 많이 이용되는 문제는 바로 피보나치 수열을 구하는 문제이다.<br>
>
>![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd6z5a1%2Fbtq9jvKjuFd%2FSt63lOH2izftq9Wgij1kC1%2Fimg.png)<br>

## 기본 재귀 호출을 이용한 피보나치 수열 O(2^N)
```java

public class Dynamic_Programming {
	static int Fibo(int n) {
		if(n == 1 || n == 2) {
			return 1;
		}
		else {
			return Fibo(n-1) + Fibo(n-2);
		}
	}
	
	public static void main(String[] args) {
		System.out.println("피보나치 수열 : "+ Fibo(10));
		
	}
}
```

<br>

## Top-Down 방식 O(N)
```java

public class Dynamic_Programming {
	// static int[] dp; 이렇게 해주고 main 초기화 해줘도 된다.
	
	static int Fibo(int[] dp, int n) {
		if(n == 1 || n == 2) {
			return 1;
		}
		else if(dp[n] != 0) {
			return dp[n];
		}
		else {
			return dp[n] = Fibo(dp, n-1) + Fibo(dp, n-2);
		}
	}
	
	public static void main(String[] args) {
		// Memorization할 배열의 길이는 구할 피보나치 수+1 이다. 0번째 index는 그냥 0으로 무시한다.
		int[] dp = new int[10+1];
		System.out.println("피보나치 수열 : "+ Fibo(dp, 10));
		
	}
}
```

<br>

## Bottom-Up 방식 O(N)
```java
public class Dynamic_Programming {
	// static int[] dp; 이렇게 해주고 main 초기화 해줘도 된다.
	
	static int Fibo(int[] dp, int n) {
		for(int i = 1; i <= n; i++) {
			if(i == 1 || i == 2) {
				dp[i] = 1;
			}
			else {
				dp[i] = dp[i-1] + dp[i-2];
			}
		}
		return dp[n];
	}
	
	public static void main(String[] args) {
		// Memorization할 배열의 길이는 구할 피보나치 수+1 이다. 0번째 index는 그냥 0으로 무시한다.
		int[] dp = new int[10+1];
		System.out.println("피보나치 수열 : "+ Fibo(dp, 10));

	}
}
```
<br>

### 어떻게 접근하면 좋을지
- 전체를 어떻게 부분으로 나눌 것인가, 해당 부분의 최적해들을 어떻게 정의하고 저장할 것인가를 생각해본다.
- 부분 문제들의 연관성, 규칙성을 생각해보며 점화식을 도출한다. 최단 경로를 예로 들면 dp[n] = dp[n-1] + (n-1에서 n으로 가는 최단거리) 이런 식으로 말이다.
- 점화식을 바탕으로 dp 테이블을 갱신하면서 최종 문제를 해결한다.


# VS 분할 정복 알고리즘
> &nbsp;동적 계획법과 분할 정복 알고리즘 모두 전체 문제를 부분 문제로 나누어 생각한다느 점에서 동일하다고 느낄 수 있다.
> 하지만 이를 구분하는 법은 생각보다 쉽다. 바로 동적 계획법은 부분 문제들 사이의 연관성이 존재하고, 분할 정복은 부분 문제들
> 사이에 연관성이 존재하지 않는다는 것이다.
