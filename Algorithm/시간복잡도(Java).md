# 시간 복잡도

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/57427581-33bf-449d-ab71-956cc7b4a204)


- 1초는 약 1억(10^8, int형이 2*10^9)


![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/bd7cba71-748c-42b2-8723-d2bb323a18b1)


# 공간 복잡도

- 코딩 테스트에서 보통 메모리 사용량을 128~512MB 정도로 제한한다. 즉, 일반적인 경우 데이터의 개수가 1,000만 단위가 넘지 않도록 알고리즘을 설계해야한다.

![image](https://github.com/OOOIOOOIO/Today-I-Learn/assets/74396651/7a15b84b-bc97-4701-b8ed-a9b3328b470e)


[자바 컬렉션 시간복잡도](https://www.grepiu.com/post/9)


# 알고리즘 별 시간복잡도
- BFS
  - 인접행렬 : O(V^2)
  - 인접리스트 : O(V+E)
- DFS
  - 인접행렬 : O(V^2)
  - 인접리스트 : O(V+E)
- 다익스트라
  - 우선순위큐 : O(ElogV)
- 벨만포드
  - O(VE)
- 플로이드워셜
  - O(V^3)
- 크루스칼(간선의 수가 적을 경우, Sparse Graph)
  - O(ElogE)
- 프림(간선의 수가 많을 경우, Dense Graph)
  - O(ELogV)
