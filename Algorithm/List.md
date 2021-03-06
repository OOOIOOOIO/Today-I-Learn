 # Collection FrameWork
 
- Java에서는 Collection이란 데이터의 집합, 그룹을 의미하며 JCF(Java Collection FrameWork)는 이러한 데이터 자료구조인 컬렉션과
이를 구현하는 클래스를 정의하는 인터페이스를 제공한다.

- Collection 인터페이스는 List, Set, Queue로 크게 3가지 상위 인터페이스로 분류할 수 있다. 그리고 Map같은 경우
Collection 인터페이스를 상속받고 있지 않지만 Collection Framework로 분류된다.

----------------------------------------------------------
## <List 인터페이스>

- List 인터페이스의 특징은 순서가 있는 데이터의 집합으로 데이터의 중복을 허용한다는 점이다. List 인터페이스를 구현하는 클래스로는
ArrayList, LinkedList, Vector가 있다.


### List 인터페이스를 구현한 클래스

- ArrayList : 단방향 포인터 구조로 각 데이터에 대한 인덱스를 가지고 있어 조회 기능에 뛰아난 성능을 보인다

- LinkedList : 양방향 포인터 구조로 데이터의 삽입, 삭제가 빈번할 경우 뛰어난 성능을 보인다. 스택, 큐, 양방향 큐 등을 만드는 용도로 쓰인다.

- Vector : 과거에 대용량 처리를 위해 사용하였으며 내ㅁ부에 자동으로 동괴화처리(대기)가 일어나 비교적 성능이 좋지 않고 무거워 요즘은 잘 쓰이지 않는다.


-----------------------------------------------------
  

## ArrayList 메소드 --> LinkedList도 비슷하지만 쓰임새가 다르다

 모두 자동으로 저장된다. 왜? 파라미터로 리스트(주소값)을 주었으니까.
- value == Obj o

> .add(Obj o) : return type --> boolean	   
> O(n) - 추가
 
>.add(int index, Obj o) : return type --> void       
> O(n) - 특정 인덱스에 삽입

>.set(int index, Obj o) : return type --> integer(pop된 값)     
> O(1) - 수정

>.remove(int index) : return --> integer							
> O(1) - 삭제

>.remove(Obj o) : index와 Obj가 둘 다 있어서 Integer(10) 이런식으로 넣어줘야 한다. return type --> boolean       
>O(n) - 삭제    

  
>.get(int index) : .size() return type --> integer     
>O(1) - 탐색

>.contains(Obj o) : return type --> boolean							  
> O(n) - 값이 있는지 확인

>.indexOf(Obj o) : return --> int / 없다면 -1 return					  
> O(n) - 인덱스 추출

>.lastIndexOf(Obj o) : return --> int / 없다면 -1 return				  
> O(n) - 인덱스 추출

>.size() : return type --> int    
>O(1) - 배열 크기

>.isEmpty() : return type --> boolean    
> O(1) - 비어있는지

>.clone() : return type --> Object   
> O(n) - 복사(객체만, 요소는 X

>.clear() : return type --> void     
>O(n) - 전체 삭제(empty 됨)

>.equals(ArrayList) : return type --> boolean


#### 자주 쓰는 표현들

인덱스로 삭제
arr.remove(arr.indexOf(value));

값으로 삭제
arr.remove(arr.get(int index)); 

arr.remove(arr.get(arr.indexOf(value)));

비어있는지 
if(arr.isEmpty()){
}

---------------------------------------------
### 간단하게 ArrayList와 LinkedList 사용해보기

```java
public class List_Study {
 public static void main(String[] args) {
  // ArrayList

  ArrayList<Integer> arr = new ArrayList<>();

  arr.add(10);
  arr.add(20);
  arr.add(30);
  arr.add(40);
  arr.add(50);
  arr.add(60);
  arr.add(null);
  arr.add(null);
  arr.add(null);

  System.out.println(arr.get(3));

  arr.remove(arr.get(3));
  arr.remove(arr.indexOf(10));

  System.out.println(arr);

  Collections.fill(arr, 1);

  System.out.println("fill 사용 : " +arr);

  // LinkedList

  LinkedList<Integer> list = new LinkedList<>();
  list.add(10);
  list.add(20);
  list.add(30);
  list.add(40);
  list.add(50);
  list.add(60);

  System.out.println(list.get(3));

  list.remove(list.get(3));

  System.out.println(list);


 }
}
```
