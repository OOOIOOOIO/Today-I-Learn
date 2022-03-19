# Backtracking(백트래킹)

<br>

![image](https://user-images.githubusercontent.com/74396651/159123806-0481bda0-3a90-459c-b382-97ab0f5ca966.png)


<br>

## 개념

- 해를 찾는 도중 해가 아니라면, 되돌아가 다시 해를 찾아가는 기법이다. 최적화 문제와 결정 문제를 푸는 방법이 된다.

- 모든 가능한 경우의 수 중에서 특정한 조건을 만족하는 경우만 살펴보는 방법이다. 즉 답이 될만한지 판단하고 그렇지 않으면 그 부분까지 탐색하는 것을 하지 않고 가지치기 하는 것이다.

- 완전탐색인 DFS의 비효율적인 경로를 차단하고 목표지점에 도달할 수 있는 가능성 있는 루트를 검사하는 방법이다.

<br>

## 유망성 판단

- 어던 노드의 유망성, 즉 해가 될만한지 판단한 후 유망하지 않다고 결정되면 그 노드의 이전(부모)로 돌아가(Backtracking) 다음 자식 노드를 탐색한다.

- 해가 될 가능성이 있다면 유망하다(promising)고 하며, 유망하지 않은 노드에 가지 않는 것을 가지치기(pruning)한다고 한다.

<br>

<hr>

# 백트래킹 안에 dfs와 bfs 같은 순환 알고리즘이 있는 것이다. 그리고 dfs와 bfs를 꼭 graph, tree와 연결지어 노드만 생각하지 말자!

<br>

```java
package 백트래킹;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

import org.omg.PortableInterceptor.SYSTEM_EXCEPTION;

public class N과M_1_15649 {
	static boolean[] visited;
	static int[] arr;
	static int N, M;
	static StringBuilder sb = new StringBuilder();
	
	static void dfs(int depth) {

		// 재귀의 깊이가 M과 같아지면 탐색과정에서 탐색을 끝내고 담았던 배열을 출력
		if(depth == M) {
			for(int val : arr) {
				sb.append(val).append(" ");
			}
			sb.append("\n");
			return;
		}
		
		// for문을 돌면서  arr을 채워준다 
		for(int i = 0; i < N; i++) {
			// 만약 해당 노드(값)을 방문하지 않았다면
			if(!(visited[i])) {
				visited[i] = true;	// 해당 노드를 방문 상태로 변경
				arr[depth] = i + 1; // 해당 깊이를 index로 하여 i+1 값 저장
				dfs(depth + 1); // 다음 자식 노드 방문을 위해 depth를 1 증가시키면서 재귀 호출
				
				// i  = ?에 대한 재귀를 한바퀴 돌고 오면 자식 노드 방문이 끝나고 돌아오면 방문한 노드를 방문하지 않은 상태로 변경
				visited[i] = false;
			}
		}
		
		
//		return;
		
//		visited[1] = true;
//		
//		for(int item : arr) {
//			if(!(visited[item])){
//				dfs();
//			}
//		}
		
	}
	
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		
		// 수열의 수
		arr = new int[M];
		visited = new boolean[N];
		
		dfs(0);
		System.out.println(sb);
	}
}	

```
