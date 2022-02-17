# BFS(Bread-First-Search) 너비 우선 탐색

## 그래프 탐색이란
>&nbsp;그래프의 탐색은 하나의 정점으로부터 시작하여 모든 정점을 차례대로 한 번씩 방문하는 것을 의미하며 그래프 탐색 방식으로는 DFS, BFS가 있다. 
예를 들어 특정 도시에서 다른 도시로의 이동 여부 판별 혹은 회로에서 단자와 단자의 연결 여부 확인 등에 사용된다.


## BFS 개념
>&nbsp;루트 노드(혹은 다른 임의의 노드)에서 시작한 인접 노드를 먼저 탐색하는 방법이다.
 
## BFS 특징

- DFS와 다르게 BFS는 재귀적으로 동작하지 않는다.

- BFS 알고리즘을 구현할 때 DFS와 마찬가지로 그래프의 탐색 경우 어떤 노드를 방문하였는지 여부를 반드시 검사해야한다. 만약 하지 않을 경우 무한루프에 빠질 수 있다.

- BFS는 방문한 노드들을 차례로 저장한 후 꺼낼 수 있는 "큐"를 사용한다. 선입선출의 원칙으로 탐색한다.

- 시작 정점으로부터 가까운 정점을 먼저 방문하고 멀리 떨어져 있는 정점을 나중에 방문하는 순회 방법이다.

- 두 노드 사이의 최단 경로 혹은 임의의 경로를 찾고 싶을 때 이 방법을 사용한다.
 
 
 <br>
 

```java
package algorithm;

import java.util.Iterator;
import java.util.LinkedList;
// import java.util.Queue;


// 방향 그래프 BFS
public class BFS {
	
//	static void BFS(int[] numbers, int start, boolean[] visit) {
//		Queue<Integer> queue = new LinkedList();
//		queue.add(start);
//		visit[start] = true;
//		
//		while(!queue.isEmpty()) {
//			int next = queue.poll();
//			
//			for(int i : numbers) {
//				if(!visit[i]) {
//					queue.add(i);
//					visit[i] = true;
//				}
//			}
//		}
//	}
	
	static class Graph {
		private int vCnt;
		private LinkedList<Integer> adj[]; // 링크드리스트의 배열
		private LinkedList<LinkedList<Integer>> adjj;
		
		// constructor
		Graph (int v) {
			vCnt = v;
			adj = new LinkedList[v];
			
			adjj = new LinkedList<>();
			
			// v개의 LinkedList 선언 및 생성
			for (int i = 0; i < v; ++i) {
				adj[i] = new LinkedList();
				
				adjj.add(new LinkedList<Integer>());
			}
		}
		
		// vertex 연결하기
		void addEdge (int v1, int v2) { // v번째 LinkedList 에 w를 삽입
			adj[v1].add(v2);
			
			adjj.get(v1).add(v2);
		}
		
		
		// DFS 함수
		void BFS(int s) {
			boolean visited[] = new boolean[vCnt]; // 각 노드이 방문 여부를 저장하기 위해
			LinkedList<Integer> queue = new LinkedList<Integer>();
			visited[s] = true;
			queue.add(s);
			
//			while (queue.size() != 0) {
//				// 방문한 노드를 큐에서 추출하고 값을 출력
//				s = queue.poll();
//				System.out.println(s + " ");
//				
//				// 방문한 노드와 인접한 모든 노드를 가져온다.
//				Iterator<Integer> i = adj[s].listIterator();
//				while (i.hasNext()) {
//					int n = i.next();
//					// 방문하지 않은 노드면 방문한 것으로 표시하고 큐에 삽입
//					if (!visited[n]) {
//						visited[n] = true;
//						queue.add(n);
//					}
//				}
//			}
			
			while (queue.size() != 0) {
				// 방문한 노드를 큐에서 추출하고 값을 출력
				s = queue.poll();
				System.out.println(s + " ");
				
				// 방문한 노드와 인접한 모든 노드를 가져온다.
				Iterator<Integer> it = adjj.get(s).iterator();
				while (it.hasNext()) {
					int n = it.next();
					// 방문하지 않은 노드면 방문한 것으로 표시하고 큐에 삽입
					if (!visited[n]) {
						visited[n] = true;
						queue.add(n);
					}
				}
			}
			
			
		}
	}
	
	public static void main(String[] args) {
		int vertices = 6;
		
	    Graph graph = new Graph(vertices);
	    
	    graph.addEdge(0, 1);
	    graph.addEdge(0, 2);
	    graph.addEdge(0, 3);
	    graph.addEdge(1, 2);
	    graph.addEdge(2, 4);
	    graph.BFS(0);

	}
}
```
  
