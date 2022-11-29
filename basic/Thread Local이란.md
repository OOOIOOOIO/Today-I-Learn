# Thread Local
> &nbsp;쓰레드 로컬은 해당 쓰레드만 접근할 수 있는 특별한 저장소를 말한다. 쉽게 이야기해서 물건 보관 창구를 떠올리면 된다. 여러 사람이 같은 물건 보관 창구를 사용하더라도 창구 직원은 사용자를 인식해서 사용자별로 확실하게 물건을 구분해준다. 사용자A, 사용자B(Thread) 모두 창구 직원을 통해 물건을 보관하고 꺼낸다. 이때 창구 직원은 사용자에 따라 보관한 물건(Thraed Local)을 구분해준다. <br><br> &nbsp; 만약 사용자 A가 보관한 짐을 꺼낼 때 사용자 B의 짐이 꺼내졌을 경우 동시성 문제가 발생한 것이다. 여러 쓰레드(사용자)가 동시에 같은 인스턴스의 필드 값(보관함)을 변경하면서 발생하는 문제이다. 
이런 동시성 문제는 여러 쓰레드가 같은 인스턴스의 필드에 접근해야 하기 때문에 트래픽이 적은 상황에서는 확률상 잘 나타나지 않고, 트래픽이 많아질수록 자주 발생한다.<br><br> &nbsp;이런 동시성 문제는 지역 변수에서는 발생하지 않는다. 지역 변수는 쓰레드마다 각각 다른 메모리 영역에 할당되기 때문이다. 동시성 문제가 발생하는 곳은 인스턴스 필드(주로 싱글톤에서 자주 발생), 또는 static 같은 공용 필드에 접근할 때 발생한다. 이를 해결하기 위해 사용하는 것이 바로 쓰레드 로컬이다. <br><br> &nbsp;동시성 문제는 값을 읽기만 하면 발생하지 않는다. 어디선가 값을 변경하기 때문에 발생한다.

<br>
<hr>
<br>

## 변수를 공유하는 법
- 객체는 Heap 또는 Stack 메모리 영역에 배치시킬 수 있다. Heap 영역은 일반적으로 모든 Thread에서 접근할 수 있으며, Stack 영역은 Thread 당 하나씩 만들어지는 메모리 영역으로 Thread 간 접근이 불가능한 것으로 알려져 있다.

![image](https://user-images.githubusercontent.com/74396651/204572869-dd863705-de8f-47a7-a32b-f60cd7c5c556.png)

![image](https://user-images.githubusercontent.com/74396651/204573079-d93a34e1-45aa-4d43-99f5-b308be79f064.png)

![image](https://user-images.githubusercontent.com/74396651/204573129-550f52ff-f842-4520-8c8b-42e4691cfae6.png)

![image](https://user-images.githubusercontent.com/74396651/204573208-6b783907-0399-49bd-83b2-897798b6c1d3.png)

![image](https://user-images.githubusercontent.com/74396651/204573293-260e32ba-81c3-489e-b312-6c48740454b6.png)

![image](https://user-images.githubusercontent.com/74396651/204573447-f50cb139-9220-4b71-90e4-4962a4bdcfb3.png)


<br>
<hr>
<br>
사진 참조 : https://sabarada.tistory.com/m/163


