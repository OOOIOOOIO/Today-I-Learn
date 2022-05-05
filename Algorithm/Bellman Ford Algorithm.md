

```java
package algorithm_개념;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Bellman_Ford_Algorithm {
	
	static class Edge{
		int node_1;
		int node_2;
		int cost;
		
		public Edge(int node_1, int node_2, int cost) {
			this.node_1 = node_1;
			this.node_2 = node_2;
			this.cost = cost;
		}
	}
	
	static StringBuilder sb = new StringBuilder();
	static long[] dp;
	static ArrayList<Edge> graph ;
	static int N, M;
	static final int INF = Integer.MAX_VALUE;
	
	
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = null;
		
		st = new StringTokenizer(br.readLine());
		// 도시
		N = Integer.parseInt(st.nextToken());
		// 버스
		M = Integer.parseInt(st.nextToken());
		
		// 선언
		dp = new long[N+1];
		graph = new ArrayList<Edge>(); 
		
		Arrays.fill(dp, INF);
		
		// 연결
		for(int i = 0; i < M; i++) {
			st = new StringTokenizer(br.readLine());
			int v1  = Integer.parseInt(st.nextToken());
			int v2  = Integer.parseInt(st.nextToken());
			int cost  = Integer.parseInt(st.nextToken());
			
			graph.add(new Edge(v1, v2, cost));
			
		}
	
		for(int i = 1; i <= N; i++) {
			System.out.println(dp[i] == INF ? "INF" : dp[i]);
		}
		
	}
	
	static void bellmanFord(int start) {
		
		dp[start] = 0;
		
		// n번 순환할 경우 음의 사이클 체크, n-1번일 경우 체크 안함
		for(int i = 1; i <= N; i++) {
			
			// 다익스트라처럼 현재 노드와 연결된 간선이 아니라,
			// 그냥 모든 간선을 확인한다.
			for(int j = 0; j < M; j++ ) {
				int curr = graph.get(j).node_1;
				int next = graph.get(j).node_2;
				int cost = graph.get(j).cost;
				
				// 동떨어진 노드?
				if(dp[curr] == INF) continue;
				
				// 최단거리 갱신해주기
				if(dp[next] > (dp[curr] + cost)) {
					// 음수 사이클 확인하기
					if(i == N) {
						return;
//						return true;
					}
					dp[next] = dp[curr] + cost;
				}
			}
		}
		
		
//		return false;
	}
	
}





```
