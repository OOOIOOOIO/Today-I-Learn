#	DFS(Depth-First-Search) 깊이 우선 탐색


## 그래프 탐색이란
>&nbsp;그래프의 탐색은 하나의 정점으로부터 시작하여 모든 정점을 차례대로 한 번씩 방문하는 것을 의미하며 그래프 탐색 방식으로는 DFS, BFS가 있다. 
예를 들어 특정 도시에서 다른 도시로의 이동 여부 판별 혹은 회로에서 단자와 단자의 연결 여부 확인 등에 사용된다.
 
## DFS 개념 
>&nbsp;루트 노드(혹은 임의의 노드)에서 다음 분기(branch)로 넘어가기 전에, 해당 분기(branch)를 완전 탐색하는 방법.
탐색 후에는 다시 원점으로 돌아가 다른 분기를 탐색한다.

## DFS 특징

- 자기 자신을 호출하는 순환 알고리즘의 형태를 지닌다.(재귀 or 스택(오버플로우 유의), 인접 행렬, 인접 리스트)

- DFS 알고리즘을 구현할 때 가장 큰 차이점은 그래프 탬색의 경우 어떤 노드를 방문했었는지 여부를 반드시 검사해야 한다는 것이다. 만약 검사를 하지 않을 경우 무한루프에 빠질 수 있다.

- 미로를 탐색할 때, 이어지는 길(해당 분기)을 따라 걸어가다 더 이상 갈 수 없게 되면 다시 가장 가까운 갈림길(새로운 분기)로  돌아와 다른 방향으로 탐색하는 것과 비슷하다고 생각하면 편하다.

- 모든 노드를 탐색, 방문하고자 할 때 DFS를 선택한다.

- BFS보다 더 간단하지만 검색 속도는 BFS에 비해 느리다.
 
<br>

```java
package algorithm;

import java.util.Iterator;
import java.util.LinkedList;
import java.util.Scanner;

// 방향 그래프 DFS
public class DFS {
	
//	static void DFS(int[] numbers, int idx, boolean[] visit) {
//		  visit[idx] = true;
//
//		  for(int i : numbers) {
//		     if(!visit[i])
//		       	  DFS(numbers, i, visit);
//		  }
//	}
	
	// 그래프를 만들어줄 클래스
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
		void DFS(int v) { // v를 시작노드로!
			boolean visited[] = new boolean[vCnt]; // 각 노드이 방문 여부를 저장하기 위해, vertex 수 만큼
			DFSUtil(v, visited);
		}
		
		// DFS에서 호출되는 함수
		void DFSUtil(int v, boolean visited[])  {
			// 현재 노드를 방문한 것으로 체크 (visited의 v번째 요소를 true로)
			visited[v] = true;
			System.out.println(v + " ");
			
			// 방문한 노드와 인접한 모든 노드를 가지고 온다
			Iterator<Integer> it = adj[v].iterator();
			Iterator<Integer> itt = adjj.get(v).iterator();
			
//			while (it.hasNext()) {
//				int n = it.next();
//				// 방문하지 않은 노드면 해당 노드를 다시 시작 노드로하여 DFSUtil을 호출
//				if (!visited[n])
//					DFSUtil(n, visited); // 재귀호출!
//			}
			
			while (itt.hasNext()) {
				int n = itt.next();
				// 방문하지 않은 노드면 해당 노드를 다시 시작 노드로하여 DFSUtil을 호출
				if (!visited[n])
					DFSUtil(n, visited); // 재귀호출!
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
	    graph.DFS(0);
    }
}
```

