# Graph -인접 행렬

```java
package algorithm;

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
public class 그래프_인접행렬 {

	public static void main(String[] args) {
		
//														<인접 행렬을 이용한 방향성 그래프>
		Scanner sc = new Scanner(System.in);
		
		// vertex(꼭지점)의 개수
		int vCnt = sc.nextInt();
		
		// edge(간선)의 개수
		int eCnt = sc.nextInt();
		
		// vertex는 1부터 시작하니까 크기+1 해주기
		int[][] adMatrix = new int[vCnt+1][vCnt+1];
		
		// edge로 연결되었다는 정보 저장
		for(int i = 0; i < eCnt; i++) {
			int vertex1 = sc.nextInt();
			int vertex2 = sc.nextInt();
			
			adMatrix[vertex1][vertex2] = 1;
		}
		
		// 0행 0 열 없애고 출력  
		for(int i = 1; i <= vCnt; i++) {
			System.out.print("[ " + i + "] - ");
			for(int j = 1; j <= vCnt; j++) {
				System.out.print(adMatrix[i][j] + " ");
			}
			System.out.println();
		}
		
	
		
//====================================================================================================================================================
		
//														<인접 행렬을 이용한 비방향성 그래프>
		
		Scanner sc2 = new Scanner(System.in);
		
		// vertex(꼭지점)의 개수
		int vCnt2 = sc2.nextInt();
		
		// edge(간선)의 개수
		int eCnt2 = sc2.nextInt();
		
		// vertex는 1부터 시작하니까 크기+1 해주기
		int[][] adMatrix2 = new int[vCnt2+1][vCnt2+1];
		
		// edge로 연결되었다는 정보 저장
		for(int i = 0; i < eCnt2; i++) {
			int vertex1 = sc2.nextInt();
			int vertex2 = sc2.nextInt();
			
			// 양방향으로 연결
			adMatrix2[vertex1][vertex2] = 1;
			adMatrix2[vertex2][vertex1] = 1;
		}
		
		// 0행 0 열 없애고 출력  
		for(int i = 1; i <= vCnt2; i++) {
			System.out.print("[ " + i + "] - ");
			for(int j = 1; j <= vCnt2; j++) {
				System.out.print(adMatrix2[i][j] + " ");
			}
			System.out.println();
		}
		sc.close();
		sc2.close();
	}
}

```
