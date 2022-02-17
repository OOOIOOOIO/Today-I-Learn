# Graph-인접 리스트

```java
package algorithm;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.Scanner;

/*
	<인접 리스트 / 행렬 결정하기>
	
정점 u-v 간 간선 여부 확인
- 인접 리스트는 list[u]의 처음부터 읽어 나가면서 각 원소를 일일이 확인한다.
- 인접 행렬은 정접 u, v가 주어졌을 때, 단 한 번 배열에 접근해 연결 여부를 확인한다.


공간 복잡도
- 인접 리스트 : 정점의 개수 V와 실제 간선의 개수 E에 좌우된다(E + V). 만약 간선의 개수가 V에 수렴한다면 인접행렬과 비슷한 공간 복잡도를 가진다.
- 인접 행렬 : V * V 개수 만큼 공간이 필요하다.

따라서 간선의 수가 V에 비해 적은 그래프를 희소 그래프라고 하며 인접 리스트를 사용하고 간선의 수가 V에 비례하는 그래프를 밀접 그래프라고 하며 인접 행렬을 사용한다.
*/

public class 그래프_인접리스트 {

	public static void main(String[] args) {
//																<인접 리스트를 이용한 방향성 그래프>
		Scanner sc = new Scanner(System.in);
		
		// vertex(꼭지점)의 개수
		int vCnt = sc.nextInt();
		
		// edge(간선)의 개수
		int eCnt = sc.nextInt();
		
		// ArrayList 안에 ArrayList 선언. 이런식으로도 할 수 있구나~~~
		ArrayList<ArrayList<Integer>> list = new ArrayList<>();
		
		// vertex는 1부터 시작하니까 0번쨰 index 미리 채워넣기
		list.add(new ArrayList<Integer>());
		
		// vertex 만들어주기
		for(int i = 0; i < vCnt; i++) {
			list.add(new ArrayList<Integer>());
		}
		
		// edge로 vertex 연결해주기
		for(int i = 0; i < eCnt; i++) {
			int vertex1, vertex2;
			vertex1 = sc.nextInt();
			vertex2 = sc.nextInt();
			
			// vertex1번 노드에 vertex2번 노드를 연결 마치(그래프엔 없지만 마치 부모 - 자식 처럼)
			list.get(vertex1).add(vertex2);
		}
		
		for(int i = 1; i <= vCnt; i++) {
			Iterator<Integer> iter = list.get(i).iterator();
				System.out.print("[ " + i + "] - ");
			while(iter.hasNext()) {
				System.out.print(iter.next() + " ");
			}
			System.out.println();
		}
		
//====================================================================================================================================================
		
//																<인접리스트를 이용한 비방향성 그래프>
		
		Scanner sc2 = new Scanner(System.in);
		
		// vertex(꼭지점)의 개수
		int vCnt2 = sc2.nextInt();
		
		// edge(간선)의 개수
		int eCnt2 = sc2.nextInt();
		
		ArrayList<ArrayList<Integer>> list2 = new ArrayList<>();
		
		// vertex는 1부터 시작하니까 0번쨰 index 미리 채워넣기
		list2.add(new ArrayList<Integer>());
		
		// vertex 만들어주기
		for(int i = 0; i < vCnt2; i++) {
			list2.add(new ArrayList<Integer>());
		}
		
		// edge로 vertex 연결해주기
		for(int i = 0; i < eCnt2; i++) {
			int vertex1, vertex2;
			vertex1 = sc2.nextInt();
			vertex2 = sc2.nextInt();
			
			// vertex1번 노드와 vertex2번 노드를 양방향으로 연결 
			list2.get(vertex1).add(vertex2);
			list2.get(vertex2).add(vertex1);
		}
		
		for(int i = 1; i <= vCnt2; i++) {
			Iterator<Integer> iter = list2.get(i).iterator();
			System.out.print("[ " + i + "] - ");
			while(iter.hasNext()) {
				System.out.print(iter.next() + " ");
			}
			System.out.println();
		}		
		
		sc.close();
		sc2.close();
	}
}


```
