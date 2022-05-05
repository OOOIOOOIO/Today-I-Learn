# Dijkstra Algorithm(다익스트라 알고리즘)

## 개념

- 다익스트라 알고리즘은 "음의 가중치"가 없는 그래프의 한 노드에서 각 모든 노드까지의 최단거리를 구하는 알고리즘이다.

- 초기 모델은 O(V^2)의 시간복잡도를 가졌다. 이후 우선순위 큐 등을 이용한 고안된 알고리즘이 탄생하였고, 현재는 O((V+E)log V)의 시복잡도를 가지고 있다.
만일 연결 그래프라면 O(Elog V)까지 시간 복잡도를 줄일 수 있다. 일반적으로는 그래프가 희소 그래프인 경우에 우선순위 큐를 이용하는 것 이 낫다.
   - 연결 그래프 : 모든 두 꼭짓점 사이에 경로가 존재하는 그래프
   - 희소 그래프 : 밀집 그래프의 반대. 밀집 그래프란 간선의 수가 최대에 가까운 그래프를 말한다. 보통 간선의 총 개수가 정점의 개수^2과 근사하다면 밀집 그래프이다.
   

## 매커니즘

- 다익스트라 알고리즘은 기본적으로 그리디 알고리즘이자 다이나믹 프로그래밍 기법을 사용한 알고리즘이다.
- 다익스트라 알고리즘은 기본적으로 아래 두 단계를 반복하여 임의의 노드에서 각 모든 노드까지의 최단거리를 구하며 기본적인 뼈대는 BFS이다. 임의의 노드에서 다른 노드로 가는 값을 비용이라고 한다.

- 방문하지 않은 노드 중에서 가장 비용이 적은 노드를 선택한다.(그리디 알고리즘)
- 해당 노드로부터 갈 수 있는 노드들의 비용을 갱신한다.(다이나믹 프로그래밍)

   <img style="width:800px; height:500px;" src="https://user-images.githubusercontent.com/74396651/163569872-95639e4d-abc5-4b2b-a9c2-e7fdac83381f.png"/>

```java
package algorithm_구현;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.LinkedList;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.StringTokenizer;
/*
<input>
5 6
1
5 1 1
1 2 2
1 3 3
2 3 4
2 4 5
3 4 6
*/
public class 최단경로_다익스트라_우선순위큐_1753 {
	
	static class Node{
		int nodeNum;
		int cost;
		Node next;
		
		public Node(int nodeNum, int cost) {
			this.nodeNum = nodeNum;
			this.cost = cost;
		}
	}
	
	
//	static ArrayList<Node>[] graph; 이런 경우는 특정 노드를 구하지 않고 모든 노드를 순환할 때 사용하면 좋다
	
	static ArrayList<ArrayList<Node>> graph;
	static int[] dp;
	static int V;
	static StringBuilder sb = new StringBuilder();
	
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = null;
		
		// 노드, 간선 개수
		st = new StringTokenizer(br.readLine());
		V = Integer.parseInt(st.nextToken());
		int E = Integer.parseInt(st.nextToken());
		
		// graph 생성
		graph = new ArrayList<ArrayList<Node>>();
		
		
		// 시작노드
		int start = Integer.parseInt(br.readLine());
		
		
		// 노드 생성(1번부터 시작하므로 +1)
		for(int i = 0; i <= V; i++) {
			graph.add(new ArrayList<>());
		}
		
		// 최단거리를 저장할 배열을 생성한다.
		dp = new int[V+1];
		
		
		// 연결
		for(int i = 0; i < E; i++) {
			st = new StringTokenizer(br.readLine());
			int v1 = Integer.parseInt(st.nextToken());
			int v2 = Integer.parseInt(st.nextToken());
			int cost = Integer.parseInt(st.nextToken());
			
			// v1 --> v2 연
			graph.get(v1).add(new Node(v2, cost));
			
		}
		
		// 다익스트라는 초깃값을 무한대로 설정한다.(여기선 정수 최댓값)
		for(int i = 0; i <= V; i++) {
			dp[i] = Integer.MAX_VALUE;
		}
		
		
		dijkstra(start, V);
		
		for(int i = 1; i <= V; i++) {
			System.out.println(dp[i]);
		}
	}
	

	
	static void dijkstra(int start, int target) {
		Queue<Node> queue = new PriorityQueue<Node>(new Comparator<Node>() {
			public int compare(Node o1, Node o2) {
				return o1.cost - o2.cost;
			};
		});
		
		// 시작 노드 
		queue.offer(new Node(start, 0));
		
		// 시작노드의 가중치를 먼저 설정한다. 시작노드부터 시작노드이므로 가중치가 0이다.
		dp[start] = 0;
		
		
		while(!(queue.isEmpty())) {
			
			// 현재 노드 번호 -> item(연결되어있는 노드들)
			Node curr = queue.poll();
			
			// 시작노드가 목표노드인 경우 탈출
			if(curr.nodeNum == target) {
				sb.append(dp[curr.nodeNum]);
				return;
			}
			
			// curr은 현재 최소 비용을 갖고 있는 노드이다. 즉 해당 노드의 비용보다 dp에 저장되어 있는 최단거리가 더 짧다면 
			// 현재 노드는 고려할 필요가 없으므로 continue를 해준다.
			if(dp[curr.nodeNum] < curr.cost) {
				continue;
			}
			
			// 현재노드와 연결되어 있는 노드의 수 만큼
			for(int i = 0; i < graph.get(curr.nodeNum).size(); i++) {
				Node next = graph.get(curr.nodeNum).get(i);
				
				if(dp[next.nodeNum] > curr.cost + next.cost) {
					dp[next.nodeNum] = curr.cost + next.cost;
					
					// 현재 노드까지의 거리를  cost로 넘겨준다					
					queue.offer(new Node(next.nodeNum, dp[next.nodeNum]));
				}
			}
		}
	}
	
	
	
	
	
}


```
