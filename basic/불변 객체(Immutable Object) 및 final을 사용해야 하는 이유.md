# 불변 객체(Immutable Object) 및 final을 사용해야 하는 이유

## 불변 객채(Immutable Object)란
> &nbsp;불변 객체란 객체 생성 이후 내부의 상태가 변하지 않는 객체이다. 불변 객체는 read-only 메소드만 제공하며 객체의 내부 상태를 제공하는 메서드를 제공하지 않거나 방어적 복사(defensive-copy)를 통해 제공한다. Java의 대표적인 불변 객체로는 String이 있다.
> &nbsp;Java에서는 배열이나 객체 등의 참조(Reference)를 전달한다. 그렇기 때문에 참조를 통해 값을 수정하면 내부의 상태가 변하기 때문에 내부를 복사하여 전달한다. 이를 방어적 복사(defensive-copy)라고 한다.

### String, toCharArray 방어적 복사
```java
public char[] toCharArray() {
    // Cannot use Arrays.copyOf because of class initialization order issues
    char result[] = new char[value.length];
    
    System.arraycopy(value, 0, result, 0, value.length);
    
    return result;
}
```

<br>
<hr>
<br>

## 불변 객체(Immutable Object) 및 final을 사용해야 하는 이유
- Thread-Safe하여 병렬 프로그래밍에 유용하며, 동기화를 고려하지 않아도 된다.
   - 
- 실패 원자적인(Failure Atomic) 메소드를 만들 수 있다.
- Cache나 Map 또는 Set 등의 요소로 활용하기에 더욱 적합하다.
- Side Effect를 피해 오류 가능성을 최소화할 수 있다.
- 다른 사람이 작성한 함수를 예측가능하며 안전하게 사용할 수 있다.
- 가비지 컬렉션의 성능을 높일 수 있다.




https://mangkyu.tistory.com/131
