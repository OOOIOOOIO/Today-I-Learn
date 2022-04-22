# Kruskal Algorithm
- 크루스칼 알고리즘은 그래프에서 최소 비용 신장 부분 트리(Minimum Spanning Tree(MST))를 찾는 알고리즘이다.
- 크루스칼 알고리즘은 그리디한 선택을 바탕으로 전개해 나간다.
   - 주어진 그래프의 모든 간선에 대해서, 간선의 연결비용을 낮은 순으로 오름 차순 정렬한다.
   - 정렬된 간선 순서대로 선택하면서, 간선의 양 끝 정점을 Union한다. 단, 이때 선택된 두 정점이 같은 집합에 속해있다면 사이클(cycle)이 있다고 판단해 포함시키지 않는다.
   - 사이클이 생긴다는 것은 간선의 양 끝 정점이 서로 같은 부모인 것을 뜻한다.
   - 이를 반복하며 최종 선택된 간선을 연결한 것이 Minimum Spanning Tree(MST)이다.

- 크루스칼 알고리즘은 서로소 집합에 대한 개념만 명확히 알고 있다면 매커니즘은 어렵지 않다.

```java
package algorithm_개념;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Scanner;
import java.util.StringTokenizer;
/*
6 9
1 2 7
1 3 11
1 6 5
2 4 6
2 3 3
3 4 10
3 5 15
4 5 7
5 6 9 
 */
public class Kruscal_Alrorithm_최소스패닝트리_MST {


	static class Edge implements Comparable<Edge> {
	    int v1;
	    int v2;
	    int cost;
	    
	    Edge(int v1, int v2, int cost) {
	        this.v1 = v1;
	        this.v2 = v2;
	        this.cost = cost;
	    }
	    @Override
	    public int compareTo(Edge o) {
	        if(this.cost < o.cost)
	            return -1;
	        else if(this.cost == o.cost)
	            return 0;
	        else
	            return 1;
	    }
	}
	
    static int[] parent; // 부모를 담을 배열
    static ArrayList<Edge> edgeList; 
	
   
    public static void main(String[] args) throws IOException {
    	BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    	StringTokenizer st = new StringTokenizer(br.readLine());
    	
    	// 노드, 간선
        int v = Integer.parseInt(st.nextToken());
        int e = Integer.parseInt(st.nextToken());
		
        // 선언
        edgeList = new ArrayList<Edge>();
        parent = new int[v+1];
        
        // 연결
        for(int i = 0; i < e; i++) {
        	st = new StringTokenizer(br.readLine());
            int v1 = Integer.parseInt(st.nextToken());
            int v2 = Integer.parseInt(st.nextToken());
            int cost = Integer.parseInt(st.nextToken());
            
            edgeList.add(new Edge(v1,v2,cost));
        }
		
        // 각 노드를 서로소 집합으로 초기화
        // parent[현재노드] = 부모노드
        for(int i = 1; i <= v; i++) {
            parent[i] = i;
        }
		
        // 가중치 정렬하기, 정렬 기준은 class 혹은 sort 메서드 내애 선언
        Collections.sort(edgeList);
		
        // 최소 가중치로 연결한 합
        int sum = 0;
        
        for(int i = 0; i < edgeList.size(); i++) {
            Edge edge = edgeList.get(i);
            
            if(!(isSameParent(edge.v1, edge.v2))) {
                sum += edge.cost;
                union(edge.v1, edge.v2);
            }
        }
		
        System.out.println(sum);
    }	
    
    // union, find, isSameParent는 Union Find와 동일하다.
    public static void union(int x, int y) {
        x = find(x);
        y = find(y);
        
        if(x != y) {
        	
        	if(y > x) parent[y] = x;
        	
        	else parent[x] = y;
        	
        }
    }
	
    public static int find(int x) {
        if(parent[x] == x) {
            return x;
        }
        
        return parent[x] = find(parent[x]);
    }
    public static boolean isSameParent(int x, int y) {
        x = find(x);
        y = find(y);
        if(x == y) return true;
        else return false;
    }
}
```
