hashcode를 사용하는 HashSet, HashMap,HashTable 등은 객체를 논리적으로 같은지 비교할 때 아래 그림과 같은 과정을 거친다.
![image](https://user-images.githubusercontent.com/74396651/188268002-aadd5760-d4b4-47ce-a54a-4b8ec2c9e8a1.png)

1. hashCode 메서드의 리턴 값이 일치하는지 우선 확인하고
2. equals메서드의 리턴 값이 true여야 논리적으로 같은 객체라고 판단한다.

- String 클래스의 hashCode()는 같은 문자열에 대해 항상 동일한 HashCode를 반환한다.
- Object 클래스의 hashCode()는 객체의 주소로 해시코드를 만들어 내기 때문에 실행할 때마다 해시코드 값이 달라질수도 있다.
- equals의 반환값이 true라면 hashCode()를 호출해서 얻은 결과는 반드시 같아야 하지만
- 두 객체의 hashCode() 값이 같다고 해서 equals의 반환값이 true여야 하는 것은 아니다.
- equals의 반환값이 false라면 두 객체의 hashCode()의 반환값이 같은 경우여도 괜찮다. hashing을 사용하는 컬렉션의 성능을 향상시키긱 위해서는 서로 다른 값을 반환시키는 것이 좋다.
 중복되는 경우가 많아질수록 해싱을 사용하는 컬렉션의 검색속도가 떨어진다.
