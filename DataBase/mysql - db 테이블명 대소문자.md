# Table doesn't exist 에러
> 분명 테이블은 만들었는데 오류가 뜬다. MySQL 8.0 버전부터 DB 파라미터의 lower_case_table_names 속성의 기본값이 0으로 지정된다.

```
show variables like 'lower_case_table_names';
```

- 값이 0이라면 테이블명의 대소문자를 구별한다
- 값이 1이라면 테이블명의 대소문자를 구별하지 않는다.


## 해결법
> 속성값을 1로 바꾸거나 테이블명의 대소문자를 맞춰주면 된다
