# 이분 그래프(Bipartite Graph)

- 인접한 정점끼리 서로 다른 색으로 칠해서 모든 정점을 두 가지 색으로만 칠할 수 있는 그래프

- 즉, 그래프의 모든 정점이 두 그룹으로 나눠지고 서로 다른 그룹의 정점이 간선으로 연결되어져 있는 그래프를 이분 그래프라고 한다.( 인접하지 않다라는 건 ㅁ-ㅇ-ㅁ-ㅇ 이런 느낌)

<br>

![image](https://user-images.githubusercontent.com/74396651/161661154-c89d37f4-325b-4463-8a97-95bd78e14335.png)

<br>

![image](https://user-images.githubusercontent.com/74396651/161659484-a129eeaf-036b-48a9-8fcd-32fede771a07.png)

<br>



## 구분하는 법

- 서로 인접한 정점이 같은 색이면 이분 그래프가 아니다.
   1. BFS, DFS로 탐색하면서 정점을 방문할 때마다 두 가지 색 중 하나를 칠한다.
   2. 다음 정점을 방문하면서 자신과 인접한 정점은 자신과 다른 색으로 칠한다.
   3. 탐색을 진행할 때 자신과 인접한 정점의 색이 자신과 동일하면 이분 그래프가 아니다.
      - BFS의 경우 정점을 방문하다 만약 같은 레벨에서 정점을 다른 색으로 칠해야 한다면 무조건 이분 그래프가 아니다.
   5. 모든 정점을 다 방문하였는데 위와 같은 경우가 없다면 이분 그래프가 아니다. 

- 이때 주의할 점은 연결 그래프와 비연결 그래프 둘 다 고려해야한다는 것이다. 또한 간선으로 연결되어 있지 않고 정점만 있을 경우도 이분 그래프이다.
   - 비연결 그래프인 경우 모든 정점에 대해 확인하는 작업이 필요하다.   
```java

public class Bipartite_Graph_이분그래프_흑백 {

	
	static ArrayList<Integer>[] graph;
	static int[] color;
	static int V, E;
	static StringBuilder sb = new StringBuilder();
	
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = null;
		
		// 테스트 케이스
		int K = Integer.parseInt(br.readLine());
		
		while(K-- > 0) {
			st = new StringTokenizer(br.readLine());
			// 정점의 개수
			V = Integer.parseInt(st.nextToken());
			// 간선의 개수
			E = Integer.parseInt(st.nextToken());
			
			
			// 선언
			graph = new ArrayList[V+1];
			color = new int[V+1];
			
			// 생성
			for(int i = 1; i <= V; i++) {
				graph[i] = new ArrayList<Integer>();
			}
			
			// 연결
			for(int i = 0; i < E; i++) {
				st = new StringTokenizer(br.readLine());
				int v1 = Integer.parseInt(st.nextToken());
				int v2 = Integer.parseInt(st.nextToken());
				graph[v1].add(v2);
				graph[v2].add(v1);
				
			}
			
			if(bfs(1)) {
				sb.append("YES").append("\n");
			}
			
			
		}
		System.out.println(sb);
	}
	
	static boolean bfs(int start) {
		Queue<Integer> q = new LinkedList<>();
		
		// 모든 노드 탐색
		for(int i = 1; i <= V; i++) {
			
			// 시작(root)부터 1로 만들어 준다.
			// 순회를 시작하는 노드를 1로 만들어 줬으니 그 다음 노드는 1이 아닌 다른 수여야 한다.
			if(color[i] == 0) {
//				System.out.println("여기여기 모여라" + " " + i);
				color[i] = 1;
				q.add(i);
			}
		
			while(!q.isEmpty()) {
				
				int pos = q.poll();
				
				for(int next : graph[pos]) {
					
//					color[pos] = 1;
					
                    if(color[next] == color[pos]) {
                    	sb.append("NO").append("\n");
						return false;	
					}
                    
					if(color[next] == 0) {
//						System.out.println("여기로 들어왔나" + " " + next);
						q.add(next);
						
						if(color[pos] == 1) {
							color[next] = -1;
						}else {
							color[next] = 1;
						}
					}
				}
			}
		}
		
		return true;
	}
	
	
}


```
