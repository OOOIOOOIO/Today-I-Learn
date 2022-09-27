# 자료형의 범위 
int : -2,147,483,648 ~ 2,147,483,647

long : -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807

BigInteger : 문자열 형태로 이루어져 있어 숫자의 범위가 무한

```java
package 수학;

import java.math.BigInteger;

public class 조합_2407 {
	public static void main(String[] args){
		
		
		BigInteger n1 = BigInteger.ONE; // 하나만
		BigInteger n2 = BigInteger.ONE;
		
    /*
      (nCm 구하는 법 - 100C6) 100P6 / 6! 구하는 법 (nCm 구하는 법)
      100!만 되도 long 타입으로는 감당하기 힘들다.
      따라서 BigInteger를 통해 큰 수를 구해야 한다! 더 큰 값,소수점, 미세한 숫자의 변동을 
      구하고 싶다면 BigDecimal을 통해 사용한다!
    */
		for(int i = 0; i < 6; i++) {
			n1 = n1.multiply(new BigInteger(String.valueOf(100-i)));
			n2 = n2.multiply(new BigInteger(String.valueOf(i + 1)));
		
		}

		BigInteger result = n1.divide(n2);
		System.out.println(result);
    
    /*
      계산
    */
    BigInteger bigNumber1 = new BigInteger("100000");
    BigInteger bigNumber2 = new BigInteger("10000");

    System.out.println("덧셈(+) :" +bigNumber1.add(bigNumber2));
    System.out.println("뺄셈(-) :" +bigNumber1.subtract(bigNumber2));
    System.out.println("곱셈(*) :" +bigNumber1.multiply(bigNumber2));
    System.out.println("나눗셈(/) :" +bigNumber1.divide(bigNumber2));
    System.out.println("나머지(%) :" +bigNumber1.remainder(bigNumber2));
    
    /*
     형 변환
    */
    BigInteger bigNumber = BigInteger.valueOf(100000); //int -> BigIntger

    int int_bigNum = bigNumber.intValue(); //BigIntger -> int
    long long_bigNum = bigNumber.longValue(); //BigIntger -> long
    float float_bigNum = bigNumber.floatValue(); //BigIntger -> float
    double double_bigNum = bigNumber.doubleValue(); //BigIntger -> double
    String String_bigNum = bigNumber.toString(); //BigIntger -> String
		
    /*
      비교
     */
     
     BigInteger bigNumber1 = new BigInteger("100000");
     BigInteger bigNumber2 = new BigInteger("1000000");

     //두 수 비교 compareTo 맞으면 0   틀리면 -1
     int compare = bigNumber1.compareTo(bigNumber2);
     System.out.println(compare);
	}
}

```
