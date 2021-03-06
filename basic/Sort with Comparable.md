# Sort with Comparable

- &nbsp;Comparator는 익명 클래스로 여러개를 생성할 수 있지만 Comparable같은 경우 implements를 한 후 compareTo 하나 밖에 구현할 수 없다.
그렇다보니, 보통 Comparable은 비교하고자 하는 가장 기본적인 설정(오름차순)으로 구현하는 경우가 많고, Comparator는 여러개를 생성할 수 있다보니
특별한 정렬을 하고싶을 때 많이 쓰인다.<br>
 
- &nbsp;Arrays.sort 와 Collections.sort는 Comparable과 Comparator를 기반으로 정렬을 해주기 때문에
사용자가 임의의 기준으로 정렬을 하기 위해선 메서드를 재정의해여 수정해야 한다.<br>

- public int compareTo(T o){ this - o }
   - return 값이 음수일 경우 : 두 원소의 위치를 교환한다. 현재 오름차순 상태
   - return 값이 양수일 경우 : 두 원소의 위치를 교환하지 않는다. 현재 내림차순 상태
   - return 값이 0일 경우 : 두 원소의 위치를 교환하지 않는다. 현재 값이 같은 상태

# 코드
```java
package util;

import java.util.Arrays;

class MyInteger implements Comparable<MyInteger> { // 인터페이스를 상속해서 사용할 경우 상속한 class에서 재정의한 compreTo로 sort가 진행된다.
	int value;
	
	public MyInteger(int value) {
		this.value = value;
	}
	
	@Override
	public int compareTo(MyInteger o) {
		// 오름차순
//		return this.value - o.value;
		
		// 내림차순
		return o.value - this.value;
	
	/* Arrays.sort / Collections.sort의 기준(오름차순이 기본) 
	 return이 음수일 경우 : 두 원소의 위치를 교환 안함(현재 오름차순)
	 return이 양수일 경우 : 두 원소의 위치를 교환 함(현재 내림차순)
	 --> 내림차순을 하고싶다면 return에 (this.value - o.value)*-1을 해주면 된다.
	 혹은 o.value - this.value 처럼 순서를 바꿔주면 된다.	
	 기준.compareTo(비교값) 이런 느낌 그래서 기준보다 크다면 오름차순이고 작다면 내림차순 상태일 것이다.*/
   
   }
}

// Comparable을 이용해 구현한 Arrays.sort
public class Comparable_Sort_O {

	public static void main(String[] args) {
		
//		인터페이스를 상속해서 사용할 경우 
		MyInteger[] arr = new MyInteger[10];
		
		// 객체 배열 초기화 (랜덤 값으로) 
		for(int i = 0; i < 10; i++) {
			arr[i] = new MyInteger((int)(Math.random() * 100));
		}
		
		// 정렬 이전
		System.out.print("정렬 전 : ");
		for(int i = 0; i < 10; i++) {
			System.out.print(arr[i].value + " ");
		}
		System.out.println();
		
    // 정렬하기
		Arrays.sort(arr);
        
		// 정렬 이후
		System.out.print("정렬 후 : ");
		for(int i = 0; i < 10; i++) {
			System.out.print(arr[i].value + " ");
		}
		System.out.println();
		
	}
}

/*
 
 <Comparator와 Comparable을 사용해 복합ㅈ거으로 구현하기>


 import java.util.Arrays;
import java.util.Comparator;
 
public class Test {
	
	public static void main(String[] args) {
		
		Student[] arr = new Student[9];
		
		arr[0] = new Student(3, 70);	// 3반 70점
		arr[1] = new Student(1, 70);	// 1반 70점
		arr[2] = new Student(1, 50);	// 1반 50점
		arr[3] = new Student(2, 60);	// 2반 60점
		arr[4] = new Student(2, 80);	// 2반 80점
		arr[5] = new Student(1, 30);	// 1반 30점
		arr[6] = new Student(2, 70);	// 2반 70점
		arr[7] = new Student(3, 90);	// 3반 90점
		arr[8] = new Student(3, 60);	// 3반 60점
		
		Student[] arr2 = arr.clone();	// 정렬 테스트를 위한 arr 객체 복사
		Student[] arr3 = arr.clone();	// 정렬 테스트를 위한 arr 객체 복사
		
		System.out.println("(c, s) -> (classNum, score)");
		// 정렬 이전
		System.out.print("정렬 전 : ");
		for(Student v : arr) {
			System.out.print(v);
		}
		System.out.println();
 
		Arrays.sort(arr);	// Comparable 사용
		
 
		System.out.print("\n학급 오름차순 정렬(같을 경우 성적 내림차순) : ");
		for(Student v : arr) {
			System.out.print(v);
		}
		System.out.println();
		
		
		
		Arrays.sort(arr2, comp1);	// Comparator 사용 
		
		System.out.print("\n학급 오름차순 정렬(같을 경우 성적 오름차순) : ");
		for(Student v : arr2) {
			System.out.print(v);
		}
		System.out.println();
	
		
		
		Arrays.sort(arr3, comp2);	// Comparator 사용
		
		System.out.print("\n성적 내림차순 정렬(같을 경우 학급 오름차순) : ");
		for(Student v : arr3) {
			System.out.print(v);
		}
		System.out.println();
		
	}
 
	
	static Comparator<Student> comp1 = new Comparator<Student>() {
		
		@Override
		public int compare(Student o1, Student o2) {
			
			// 만약 학급이 같다면 성적을 기준으로 "오름차순"으로 정렬한다.
			if(o1.classNum == o2.classNum) {
				return o1.score - o2.score;
			}
			return o1.classNum - o2.classNum;	// 학급 기준 오름차순으로 정렬한다.
		}
	};
	
	static Comparator<Student> comp2 = new Comparator<Student>() {
		
		@Override
		public int compare(Student o1, Student o2) {
			
			// 만약 성적이 같다면 학급을 "오름차순"으로 정렬한다.
			if(o1.score == o2.score) {
				return o1.classNum - o2.classNum;
			}
			return o2.score - o1.score;	// 성적을 내림차순으로 정렬한다.
		}
	};
}
 
 
class Student implements Comparable<Student> {
 
	int classNum;
	int score;
	
	public Student(int classNum, int score) {
		this.classNum = classNum;
		this.score = score;
	}
	
	@Override
	public int compareTo(Student o) {
		
		// 만약 학급이 같다면 성적을 기준으로 "내림차순"으로 정렬한다.
		if(this.classNum == o.classNum) {
			return o.score - this.score;
		}
		return this.classNum - o.classNum;	// 학급 기준 오름차순으로 정렬한다.
	}
	
	
	@Override
	public String toString() {
		return "("+classNum + ", " + score + ")  ";
	}
	
}
 */
 ```
