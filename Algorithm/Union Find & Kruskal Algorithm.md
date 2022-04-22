# 유니온(Union Find)

- 유니온 파인드 알고리즘은 "합집합 찾기" 알고리즘으로 변역할 수 있다.
- 상호 배타적 집합(Disjoint-set)이라고도 한다.
- 여러 노드가 존재할 때, 두 개의 노드를 선택해서 현재 두 노드가 같은 그래프에 속하는지 판별하는 알고리즘이다.
- 두 가지 연산으로 이루어져 있다.
   - find : x가 어떤 집합에 포함되어 있는지 찾는 연산
   - union : x와 y가 포함되어 있는 집합을 합치는 연산, 일반적으로 부모를 합칠 때 더 작은 값의 부모로 합친다.


# 유니온 파인드 

```java
package algorithm_개념;

public class Union_Find {
    public static int[] parent = new int[1000001];
	
  
    public static void main(String[] args) {
    	
        // parent[현재노드] = 부모노드
        for(int i = 1; i <= 8; i++) {
            parent[i] = i;
        }
        
        union(1, 2);
        union(2, 3);
        
        System.out.println("1과 3은 연결되어 있나요? " + isSameParent(1,3));
    }	
    
    // 현재 노드의 부모 찾기
    public static int find(int x) {
        // x(현재 노드) == parent[x](부모)라면 현재 x는 그 집합의 부모이다.
        if(x == parent[x]) return x;
        
        // dp처럼 타고 타고 가면서 부모 구하기
        else return parent[x] = find(parent[x]);
	}
	
      // 노드 합치기(연결하기)
    public static void union(int x, int y) {
    	// find를 통해 현재 노드의 부모를 찾는다.
        x = find(x);
        y = find(y);
        
        // 같은 부모를 가지고 있지 않을 때
        if(x != y) {
        	// 더 작은 값으로 부모를 설정해준다.
        	if(y > x) parent[y] = x;
        	
        	else parent[x] = y;
        }
    }
    
    //같은 부모 노드를 가지는지 확인
    public static boolean isSameParent(int x, int y) {
        // 같은 부모인지 찾는다
    	x = find(x);
        y = find(y);
        
        if(x == y) return true;
        
        else return false;
    }
	    
}
```


















