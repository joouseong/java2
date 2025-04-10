# 주우성 202230236

## 4월 10일(6주차)
### 클래스와 객체
세상 모든 것이 객체다
* 실 세계 객체의 특징
  - 객체마다 고유한 특성(state)와 행동(behavior)를 가짐
  - 다른 객체들과 정보를 주고 받는 등, 상호작용 하면서 살아감
* 컴퓨터 프로그램에서 객체 사례
  - 테트리스 게임의 각 블록들
  - 한글 프로그램의 메뉴나 버튼들

자바의 객체 지향 특성: 캡슐화
* 캡슐화: 객체를 캡슐로 싸서 내부를 볼 수 없게 하는 것
  - 객체의 가장 본질적인 특징
  - 외부의 접근으로부터 객체 보호
* 자바의 캡슐화
  - 클래스(class): 객체 모양을 선언한 틀(캡슐화하는 틀)
  - 객체: 생성된 실체(instance): 클래스 내에 메소드와 필드 구현

자바의 객체 지향 특성: 상속
* 상속
  - 상위 객체의 속성이 하위 객체에 물려 줌
  - 하위 객체가 상위 객체의 속성을 모두 가지는 관계
* 실세계의 상속 사례
  - 나무는 식물의 속성과 생물의 속성을 모두 가짐
  - 사람은 생물의 속성은 가지지만 식물의 속성은 가지고 있지 않음
* 자바의 상속
  - 상위 클래스의 멤버를 하위 클래스가 물려받음
  - 상위 클래스: 슈퍼 클래스
  - 하위 클래스: 서브 클래스, 슈퍼 클래스 코드의 재사용, 새로운 특성 추가 가능

자바의 객체 지향 특성: 다형성
* 다형성
  - 같은 이름의 메소드가 클래스 혹은 객체에 따라 다르게 구현되는 것
* 다형성 사례
  - 메소드 오버로딩: 한 클래스 내에서 같은 이름이지만 다르게 작동하는 여러 메소드
  - 메소드 오버라이딩: 슈퍼 클래스의 메소드를 동일한 이름으로 서브 클래스마다 다르게 구현

객체 지향 언어의 목적
1. 소프트웨어의 생산성 향상
  * 컴퓨터 산업 발전에 따라 소프트웨어의 생명 주기(life cycle) 단축
    - 소프트웨어를 빠른 속도로 생산할 필요성 증대

  * 객체 지향 언어
    - 상속, 다형성, 객체, 캡슐화 등 소프트웨어 재사용을 위한 여러 장치 내장
    - 소프트웨어 재사용과 부분 수정 빠름
    - 소프트웨어를 다시 만드는 부담 대폭 줄임
    - 소프트웨어 생산성 향상
2. 실세계에 대한 쉬운 모델링
  * 초기 프로그래밍
    - 수학 계산/통계 처리를 하는 등 처리 과정, 계산 절차 중요
  * 현대 프로그래밍
    - 컴퓨터가 산업 전반에 활용
    - 실세계에서 발생하는 일을 프로그래밍
    - 실세계에서는 절차나 과정보다 물체(객체)들의 상호 작용으로 묘사하는 것이 용이
  * 객체 지향 언어
    - 실세계의 일을 보다 쉽게 프로그래밍하기 위한 객체 중심적 언어

절차 지향 프로그래밍과 객체 지향 프로그래밍
* 절차 지향 프로그래밍
  - 작업 순서를 표현하는 컴퓨터 명령 집합
  - 함수들의 집합으로 프로그램 작성
* 객체 지향 프로그래밍
  - 컴퓨터가 수행하는 작업을 객체들 간의 상호 작용으로 표현
  - 클래스 혹은 객체들의 집합으로 프로그램 작성

클래스와 객체
* 클래스: 객체의 속성(state)와 행위(behavior) 선언, 객체의 설계도 혹은 틀
* 객체: 클래스의 틀로 찍어낸 실체
  - 프로그램 실행 중에 생성되는 실체
  - 메모리 공간을 갖는 구체적인 실체
  - 인스턴스(instance)라고도 부름
* 사례
  - 클래스: 소나타자동차, 객체: 출고된 실제 소나타 100대
  - 클래스: 벽시계,       객체: 우리집 벽에 걸린 벽시계들
  - 클래스: 책상,         객체: 우리가 사용중인 실제 책상들

자바 클래스 구성
* 클래스
  - class 키워드로 선언
  - 멤버: 클래스 구성 요소, 필드(멤버 변수)와 메소드(멤버 함수)
  - 클래스에 대한 public 접근 지정: 다른 모든 클래스에서 클래스 사용 허락
  - 멤버에 대한 public 접근 지정: 다른 모든 클래스에게 멤버 접근 허용

``` java
public class ex4_1 {
    int radius; // 원의 반지름 필드
    String name; // 원의 이름 필드

    public double getArea() { //멤버 메소드
        return 3.14*radius* radius;
    }

    public static void main(String[] args) {
        ex4_1 pizza; //객체에 대한 레퍼런스 변수 pizza 선언
        pizza = new ex4_1(); // Circle 객체 생성
        pizza.radius = 10; // 피자의 반지름을 10으로 설정
        pizza.name = "자바피자"; // 피자의 이름 설정
        double area = pizza.getArea(); // 피자의 면적 알아내기
        System.out.println(pizza.name + "의 면적은 " + area);

        ex4_1 donut = new ex4_1(); // Circle 객체 생성
        donut.radius = 2; // 도넛의 반지름을 2로 설정
        donut.name = "자바도넛"; // 도넛의 이름을 설정
        area = donut.getArea(); // 도넛의 면적 알아내기
        System.out.println(donut.name + "의 면적은 " + area);
    }
}
결과: 자바피자의 면적은 314.0
자바도넛의 면적은 12.56
```





---
## 4월 3일(5주차)
### 반복문
* 자바 반복문 - for 문, while 문, do-whlie 문

for 문
* for 문을 이용하여 1부터 10까지 합 출력하기
``` java
public class ex3_1 {
    public static void main(String[] args) {
        int i, sum = 0;

        for (i=1; i<=10; i++){
            sum += i;
            System.out.print(i);

            if (i <= 9)
                System.out.print("+");
            else {
                System.out.print("=");
                System.out.print(sum);
            }
        }
    }
}

결과: 1+2+3+4+5+6+7+8+9+10=55
```

while 문
* while 문의 구성과 코드 사례: 조건식이 '참'인 동안 반복 실행
* for 문과 while 문의 차이: for문은 반복되는 수가 정확히 지정됨 그러나 while 문은 횟수가 정해지지 않은 반복문을 위해 만들어짐(예: 끝났다는 신호가 왔을 때)
* while 문을 이용하여 입력된 정수의 평균 구하기
``` java
import java.util.Scanner;
public class ex3_2 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int count=0, n=0;
        double sum=0;

        System.out.println("정수를 입력하고 마지막에 0을 입력하세요.");
        while((n=scanner.nextInt()) != 0){  //0이 입력되면 while 문 벗어남
            sum=sum+n;
            count++;
        }
        System.out.print("수의 개수는 " + count + "개이며 ");
        System.out.println("평균은 " + sum/count + "입니다.");
        scanner.close();
    }
}

결과: 정수를 입력하고 마지막에 0을 입력하세요.
10 30 -20 40 0
수의 개수는 4개이며 평균은 15.0 입니다.
```

do-while 문
* do-while 문의 구성과 코드 사례: 조건식이 '참'인 동안 반복 실행. 작업문은 한 번 반드시 실행
* do-while 문을 이용하여 'a' 에서 'z' 가지 출력하기
``` java
public class ex3_3 {
    public static void main(String[] args) {
        char a = 'a';

        do{
            System.out.print(a); // 문자 출력
            a = (char) (a+1);    // 알파벳의 경우 1을 더하면 다음 문자의 코드 값
        } while (a <= 'z');
    }
}

결과: abcdefghijklmnopqrstuvwxyz
```

중첩 반복
* 반복문이 다른 반복문을 내포하는 구조
* for 문안에 for 문이나 while 문을 둘 수도 있고, while 문 안에 for, while, do-while 문을 둘 수 도 있음
* 반복은 몇 번이고 중첩 가능하지만, 너무 많은 중첩 반복은 프로그램 구조를 복잡하게 하므로 2중 또는 3중 반복 정도가 적당함
* 2중 중첩을 이용한 구구단 출력하기
``` java
public class ex3_4 {
    public static void main(String[] args) {
        for (int i=1; i<10; i++){  // 단에 대한 반복
            for (int j=1; j<10; j++) {  // 각 단의 곱셈
                System.out.print(j + "*" + i + "=" + j*i);  // 구구셈 출력
                System.out.print('\t');  // 하나씩 탭으로 띄기
            }
            System.out.println(); // 한 단이 끝나면 다음 줄로 커서 이동
        }
    }
}
```
### continue문과 break문
continue 문
* 반복문을 빠져 나가지 않고, 다음 반복으로 제어 변경
* 반복문에서 continue; 문에 의한 분기한다
* continue 문을 이용하여 양수 합 구하기
``` java
import java.util.Scanner;
public class ex3_5 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("정수를 5개 입력하세요.");
        int sum=0;
        for(int i=0; i<5; i++){
            int n=scanner.nextInt();
            if(n<=0) continue;
            else sum += n;
        }
        System.out.println("양수의 합은 " + sum);

        scanner.close();
    }
}
결과: 정수를 5개 입력하세요.
5
-2
6
10
-4
양수의 합은 21
```
break 문
* 반복문 하나를 즉식 벗어날 때 사용. 하나의 반복문만 벗어남.
* 중첩 반복의 경우 안쪽 반복문의 break 문이 실행되면 안쪽 반복문만 벗어남.
* break 문을 이용하여 while 문 벗어나기
``` java
import java.util.Scanner;
public class ex3_6 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("exit을 입력하면 종료됩니다");
        while(true) {
            System.out.print(">>");
            String text = scanner.nextLine();
            if(text.equals("exit"))
                break;
        }
        System.out.println("종료합니다...");

        scanner.close();
    }
}
결과: exit을 입력하면 종료됩니다.
>> edit
>> exit
종료합니다...
```

### 자바의 배열
자바 배열(array)
* 인덱스와 인덱스에 대응하는 데이터들로 이루어진 자료 구조로 한 번에 많은 메모리 공간 선언
* 같은 타입의 데이터들이 순차적으로 저장되는 공간으로 인덱스를 이용하여 원소 데이터 접근
* 반복문을 이용하여 처리하기에 적합한 자료구조
* 배열 인덱스: 0 부터 시작

배열 선언과 생성
1. 배열에 대한 레퍼런스 변수 선언
  - 배열 타입-배열에 대한 레퍼런스 변수-배열 선언(int intArray [];)
2. 배열 생성
  - 배열에 대한 레퍼런스 변수=배열생성-타입-원소 개수(intArray = new int [5];)

배열 선언 및 생성 디테일
* 배열은 선언과 생성의 두 단계 필요: 선언과 동시에 생성할 수 있음
* 배열 선언: 배열의 이름 선언(배열 레퍼런스 변수 선언)
  - int intArray[]; 또는 int[] intArray;
* 배열 생성: 배열 공간 할당 받는 과정
  - intArray = new int[5]; 또는 int intArray[] = new int[5];
* 배열 초기화: 배열 생성과 값 초기화
  - int intArray[] = {4,3,2,1,0}; // 5개의 정수 배열 생성 및 값 초기화
  - double doubleArray[] = {0.1, 0.2, 0.3, 0.4}; // 5개의 실ㅅ수 배열 생성 및 값 초기화

배열 인덱스와 배열 원소 접근
* 배열의 인덱스는 0부터, 크기 1부터
* 인덱스로 음수 사용 불가
* 반드시 배열 생성 후 접근

레퍼런스 치환과 배열 공유
* 레퍼런스 치환으로 두 레퍼런스가 하나의 배열 공유
  - int intArray[] = new int[5];
  - int myArray[] = intArray;

* 양수 5개를 입력받아 배열에 저장하고 제일 큰 수를 출력
``` java
import java.util.Scanner;
public class ex3_7 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int intArray[];
        intArray = new int[5];
        // 선언과 생성을 한 줄에 할 수 있다
        // int intArray[] = new int[5];

        int max = 0; //현재 가장 큰 수
        System.out.println("양수 5개를 입력하세요.");

        for (int i=0; i<5; i++) {
            intArray[i] = scanner.nextInt();
            if(intArray[i] > max)
                max = intArray[i];
        }
        System.out.print("가장 큰 수는 " + max + "입니다.");

        scanner.close();
    }
}
결과: 양수 5개를 입력하세요.
1 39 78 100 99
가장 큰 수는 100입니다.
```

배열의 크기, length 필드
* 자바의 배열은 객체로 처리
* 배열의 크기는 배열 객체의 length 필드에 저장
* length 필드를 이용하여 배열의 모든 값을 출력하는 사례
  - for(int i=0; i<intArray.length; i++>) //intArray 배열 크기만큼 루프를 돈다
  - System.out.println(intArray[i];)
* 배열의 length 필드를 이용하여 배열 크기만큼 정수를 입력 받고 평균을 출력

함수 호출 시 배열 전달 비교: C/C++ vs 자바
* 자바가 C/C++에 비해 배열을 다루기 10배 편한 구조
* C/C++의 경우 배열과 크기를 각각 전달 받음
* 자바의 경우 배열만 전달받음

배열과 for-each 문
* for-each 문: 배열이나 나열(enumeration)의 원소를 순차 접근하는데 유용한 for 문

### 다차원 배열
2차원 배열
* 2차원 배열 선언
  - int intArray[][]; 또는 int[][] intArray;
* 2차원 배열 생성
  - intArray = new int[2][5];
  - int intAray[] = new int[2][5]; //배열 선언과 생성 동시
* 2차원 배열의 length 필드
  - i.length -> 2차원 배열의 행의 개수로, 2
  - i[n].length -> n번째 행의 열의 개수
  - i[1].length -> 1번째 행의 열의 개수, 5

2차원 배열의 초기화
* 배열의 선언과 동시에 초기화
  - int intArray[][] = {{0,1,2}, {3,4,5}, {6,7,8}};

### 메소드의 배열 리턴
* 배열의 레퍼런스만 리턴되며, 배열 전체가 리턴되는 것이 아님
* 메소드의 리턴 타입
  - 리턴하는 배열 타입과 리턴 받는 배열 타입 일치
  - 리턴 타입에 배열의 크기를지정하지 않음

### 자바의 예외 처리
* 예외(Exception): 실행 중 오동작이나 결과에 악영향을 미치는 예상치 못한 상황 발생 -> 자바에서는 실행 중 발생하는 에러를 예외로 처리
* 실행 중 예외가 발생하면: 자바 플랫폼은 응용프로그램이 예외를 처리하도록 호출 -> 응용프로그램이 예외를 처리하지 않으면 프로그램 강제 종료 시킴
* [예외 발생 경우]
  - 정수를 0으로 나누는 경우
  - 배열의 크기보다 큰 인덱스로 배열의 원소를 접근하는 경우
  - 정수를 읽는 코드가 실행되고 있을 때 사용자가 문자를 입력한 경우
* 0으로 나누기 시 예외 발생으로 강제 종료되는 경우
``` java
import java.util.Scanner;
public class ex3_12 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int dividend; //나뉨수
        int divisor; //나눔수

        System.out.print("나뉨수를 입력하시오: ");
        dividend = scanner.nextInt(); //나뉨수 입력
        System.out.print("나눗수를 입력하시오: ");
        divisor = scanner.nextInt(); //나눔수 입력
        System.out.println(dividend+"를 " + divisor + "로 나누면 몫은 " + dividend/divisor + "입니다.");
    scanner.close();
    }
}
결과:나뉨수를 입력하시오: 100
나눗수를 입력하시오: 0
Exception in thread "main" java.lang.ArithmeticException: / by zero
        at ex3_12.main(ex3_12.java:12)
```

자바의 예외 처리, try-catch-fianlly 문
* 예외 처리: 발생한 예외에 대해 개발자가 작성한 프로그램 코드에서 대응하는 것
* try-catch-finally문 사용. finally 블록은 생략 가능
  - try {
        예외가 발생할 가능성이 있는 실행문
  }
  - catch(처리할 예외 타입 선언){
      예외 처리문
  }
  - finally {
        예외 발생 여부와 상관없이 무조건 실행되는 문장
  }

``` java
import java.util.Scanner;
public class ex3_13 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int dividend;
        int divisor;

        System.out.print("나뉨수를 입력하시오:");
        dividend = scanner.nextInt();
        System.out.print("나눗수를 입력하시오:");
        divisor = scanner.nextInt();
        try{
            System.out.println(dividend + "를" + divisor + "로 나누면 몫은 " + dividend/divisor + "입니다.");
        }
        catch(ArithmeticException e){
            System.out.println("0으로 나눌 수 없습니다!");
        }
        finally {
            scanner.close();
        }
        


    }
}
결과: 나뉨수를 입력하시오:100
나눗수를 입력하시오:0
0으로 나눌 수 없습니다!
```
``` java
import java.util.Scanner;
import java.util.InputMismatchException;
public class ex3_14 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("정수를 3개 입력하세요:");
        int sum = 0, n = 0;
        for(int i=0; i<33; i++){
            System.out.print(i+">>");
            try{
                n = scanner.nextInt();
            }
            catch(InputMismatchException e) {
                System.out.println("정수가 아닙니다. 다시 입력하세요!");
                scanner.next();
                i--;
                continue;
            }
            sum += n;
        }
        System.out.println("합은 " + sum);
        scanner.close();
    }
}


```



---
## 3월 27일(4주차)

### 자바의 특징
가비지 컬렉션
* 자바 언어는 메모리 할당 기능은 있어도 메모리 반환 기능 없음
* 사용하지 않는 메모리는 JVM에 의해 자동 반환 - 가비지 컬렉션

실시간 응용프로그램에 부적합
* 실행 도중 예측할 수 없는 시점에 가비지 컬렉션 실행 때문
* 응용프로그램의 일시적 중단 발생

자바 프로그램은 안전
* 타임 체크 엄격
* 물리적 주소 ???를 사용하는 포인터 개념 없음

프로그램 작성 쉬움
* 포인터 개념이 없음. 동작 메모리 반환 하지 않음. 다양한 라이브러리 지원

실행 속도 개선을 위한 JIT 컴파일러 사용
* 자바는 바이트 코드를 인터프리터 방식으로 실행
* 기계어가 실행되는 것보다 느림
* JIT컴파일 기법으로 실행 속도 개선
* JIT 컴파일 - 실행 중에 바이트 코드를 컴파일하여 기계어를 실행하는 기법

### 소스 코드, 바이트 코드, 기계어
1. 소스코드(source code)
* 우리가 작성하는 Java 코드(.Java 파일)
* 사람이 읽을 수 있는 고수준 언어(하이레벨랭귀지)

2. 바이트 코드(.class 파일)
* Java 컴파일러(Javac)가 소스코드를 변환한 중간 코드
* CPU가 직접 실행할 수 없음 -> JVM이 실행해야 함
* 기계어와 다르게 플랫폼 독립적
* 바이트 코드는 JVM이 해석(인터프리터)하거나, JIT 컴파일러가 기계어로 변환 실행 됨

3. 기계어(Machine Code)
* CPU가 직접 실행할 수 있는 0과 1의 이진 코드
* 운영체제(OS)와 CPU 아키텍쳐(intel, ARM 등)에 따라 다름
* 16진수 형태의 기계어

바이트코드와 기계어의 차이점
* 바이트 코드는 JVM이 실행하는 중간 코드 -> 운영체제와 CPU에 관계없이 사용 가능
* 기계어는 CPU가 직접 실행하는 코드 -> 특정 하드웨어에 종속됨

### 자바 기본 프로그래밍

식별자(identifier) - 명명 규칙(Naming Convention)
* 식별자: 클래스, 변수, 상수, 메소드 등에 붙이는 이름
* '@', '#', '!'와 같은 특수문자, 공백 또는 탭은 식별자로 사용불가 '_', '$'는 사용 가능
* 유니코드 문자 사용 가능, 한글 사용 가능 but 한글은 사용 X
* 자바 언어의 키워드는 식별자로 사용 불가
* 식별자의 첫 번째 문자로 숫자는 사용 불가
* '_' 또는 '$'를 식별자 첫 번째 문자로 사용할 수 있으나 일반적으로 잘 사용하지 않는다
* 불린  리터럴(true, faluse)와 널 리터럴(null)은 식별자로 사용 불가
* 길이 제한 없음
* 대소문자 구별: barChart 와 barchart 는 다른 식별자

Java의 데이터 타입
* 기본 자료형(Primitive Type) 8개
* 기본 타입의 크기는 CPU나 운영체제에 따라 변하지 않음
* 레퍼런스형 1개이며 용도는 다음 3가지: 포인터와 유사한 개념이지만 메모리 주소는 아님
  1. 클래스에 대한 레퍼런스
  2. 인터페이스에 대한 레퍼런스
  3. 배열에 대한 레퍼런스
* 문자열은 기본 타입이 아님. String 클래스로 문자열 표현
* 문자열 리터럴: "JDK", "한글"
  1. 리터럴 이란 소스코드 중 특정한 자료형의 값을 의미
* 문자열이나 문자열과 다른 자료형의 리터럴을 + 연산을 할 경우 결과는 문자열로 변환

참조 자료형(REference Type)
* 포인터는 임의의 메모리 주소를 저장 하는 반면, 참조 자료형은 주소를 지정할 수 없음
* 직접 주소를 갖고 있지는 않지만, JVM이 해당 주소로 안내해 주게 됨
* 객체를 잠조하는 변수 유형으로, 힙(Heap) 영역에 저장된 객체의 메모리 주소를 가리킴
* 기본 자료형은 스택(Stack) 영역에 저장됨
* New 키워드로 객체(인스턴스)를 생성하는 것이 바로 참조 자료형을 선언하는 것
* 이렇게 선언된 참조 자료형은 JVM이 대신 객체의 주소를 저장
* 배열, 인터페이스 혹은 열거형도 객체이기 때문에 참조 자료형임
* 객체를 참조하지 않을 때 null 값을 가질 수 있음
* 같은 객체를 여러 변수가 참조할 수 있고, ==연산자로 객체의 주소 비교 할 수도 있음
* 일반적으로 '레퍼런스'라고 부르면 되지만, 레퍼런스형, 레퍼런스 자료형, 참조형,  참조자료형, 레퍼런스 변수, 참조 변수 등 다양하게 사용

Java는 왜 참조 자료형을 사용할까?
* 메모리 설정 자율성
1. 포인터는 개발자가 임의로 메모리 값을 설정하고 해당 메모리에 직접 접근이 가능하기에 참조 자료형에 비해 상대적으로 메모리 설정 자율성이 높음
* 메모리 관리 편의성
1. 자바는 참조 자료형을 사용하는 대신 Garbage Collector를 사용하여 개발자 대신 참조되지 않는 메모리는 자동으로 해제하여 메모리를 효율적으로 관리함
* 안전성
1. JVM과 GC를 통해 스스로 메모리 관리를 하고 개발자가 직접적으로 메모리에 접근하는 것을 막아 이러한 오류를 방지함
* 성능


메모리의 구조
* 힙(Heap - FIFO) 영역은 프로그래머가 직접 공간을 할당, 해제하는 메모리 공간으로 Java의 경우 JVM이 담당
* 스택(Stack - LIFO) 영역은 프로그램이 자동으로 사용하는 임시 메모리 영역
* 힙이 스택을 침범하는 경우를 힙 오버 플로우라 하고, 스택이 힙을 침범하는 경우를 스택 오버 플로우라고 함

변수의 선언
* 변수: 프로그램 실행 중에 값을 임시로 저장하기 위한 메모리의 공간으로 프로그램 수행 중 변경될 수 있음
* 변수 선언: 데이터 타입에서 정한 크기의 메모리를 할당

상수 선언
* final 키워드 사용
* 선언할 때 초기값 지정
* 실행 중 값의 변경은 불가능

var 키워드
* Java 10부터 도입 됨
* var 키워드는 타입을 생략하고 변수 선언을 할 수 있음
* 컴파일러가 추론하여 변수 타입을 결정
* 변수 선언할 때 초기값이 주어지지 않으면 컴파일 오류가 발생
* var은 지역 변수 선언에만 사용이 가능하고 클래스 필드에서는 사용할 수 없음
  1. 지역 변수: 메소드 내부에 선언되는 변수
  2. 클래스 필드: 클래스 내부에 선언되는 변수. 객체가 생성될 때 함께 만들어지는 변수

  다음과 같이 사용하는 것이 좋다
  * 기본적으로는 명시적 자료형(int, String, double 등)을 사용하는 것이 좋음
  * 가독성이 유지될 수 있는 경우에 한해서 var를 적절히 활용하는 것이 좋음
  * 특히 상수를 적극적으로 활용해서 코드의 안정성을 높이는 것이 중요

변수, 리터럴, 상수 사용하기
* 원의 면적을 계산하여 출력하는 프로그램을 작성하라
```java
public class ex2_3 {
    public static void main(String[] args) {
        final double PI = 3.14;
        double radius = 10.2;
        double circleArea = radius * radius * PI;

        System.out.print("반지름 " + radius + ", ");
        System.out.println("원의 면적 = " + circleArea);
    }
}

결과: 반지름 10.2, 원의 면적 = 326.68559999999997
```

System.out.print의 종류
* System.out.print()
  - 기본 출력문으로 줄 바꿈을 하지 않고 한 줄로 출력됨
  - 줄 바꿈을 하려면 개행 문자 \n (new line)을 넣어야 함
* System.out.println()
  - 출력 후 자동으로 줄 바꿈(개행)을 실행
* System.out.printf()
  - 서식(%d, %o,%x, %f, %c 등) 을 사용하여 표현할때 사용

타입 변환
* 특정 데이터 타입의 값을 다른 데이터 타입의 값으로 변환
* 자동 타입 변환
  - 컴파일러에 의해 원래의 타입보다 큰 타입으로 자동 변한
  - 치환문(=)이나 수식 내에서 타입이 일치하지 않을 때
* 강제 타입 변환
  - 개발자의 의도적 타입 변환
  - () 안에 개발자가 명시적으로 타입 변환 지정
  - 강제 변환은 값 손실 우려

  큰 데이터 타입에서 작은 데이터 타입으로는 변환되지 않음
  int -> byte 등은 오류가 발생


자바의 키 입력: System.in VS Scanner
* System.in
  - 키보드와 연결된 자바의 표준 입력 스트림
  - 입력되는 키를 바이트(문자아님)로 리턴하는 저수준 스트림
  - System.in을 직접 사용하면 바이트를 문자나 숫자로 변환하는 많은 어려움 있음
* Scanner 클래스
  - 읽은 바이트를 문자, 정수, 실수, 불린, 문자열 등 다양한 타입으로 변환하여 리턴
  - 객체를 생성해서 사용
  - 키보드에 연결된 System.in에게 키를 읽게 하고, 원하는 타입으로 변환하여 리턴
  - 입력되는 키 값을 공백으로 구분되는 토큰 단위로 읽음
  - 공백 문자: '\r', '\n', '\f' (페이지 나누기, 폼 피드, 프린트에서 사용)
* Scanner는 개발자가 원하는 타입 값으로 쉽게 읽을 수 있음

연산자
* 연산: 주어진 식을 계산하여 결과를 알아내는 과정
  - 증감: ++ --
  - 산술: + - * / %
  - 시프트: >> << >>>
  - 비교: > < >= <= == !=
  - 비트: & | ^ ~
  - 논리: && || ! ^
  - 조건: ? :
  - 대입: = *= /= += -= &= ^= |= <<= >>= >>>=

산술 연산자
* 산술연산자: 더하기(+), 빼기(-), 곱하기(*), 나누기(/), 나머지(%)

증감 연산
* 1 증가 혹은 감소 시키는 연산: ++, --
* 변수의 앞에 붙으면 먼저 더해서 넣는 것(전위 연산자)
* 변수의 뒤에 붙으면 넣은 후 더하는 것(후위 연산자)

대입 연산
* 연산의 오른쪽 결과를 왼쪽 변수에 대입

비교 연산, 논리 연산
* 비교연산자: 두 개의 값을 비교하여 true/ false 결과
* 논리연산자: 두 개의 논리 값에 논리 연산, 논리 결과

조건 연산
* 3개의 피연산자로 구성된 삼향(ternary) 연산자
* opr1 ? opr2 : opr3 -> opr1이 결과가 true면 opr2, false면 opr3
* if-else을 조건연산자로 간결하게 표현 가능

조건 연산자 사용하기
* 다음 코드의 실행 결과는?
``` java

public class ex2_9 {
    public static void main(String[] args) {
        int a = 3, b = 5;

        System.out.println("두 수의 차는 " + ((a>b) ? (a-b) : (b-a)));
    }
}

결과: 두 수의 차는 2
```

비트 연산
* 비트 논리 연산: 비트끼리 AND, OR, XOR, NOT 연산
* 비트 시프트 연산: 비트를 오른쪽이나 왼쪽으로 이동

  #연산방법보다 사용되는 사례르 확인하는 것이 도움됨

비트 연산이 사용되는 경우
* 비트 연산은 하드웨어 프로그래밍 뿐만 아니라 일반 소프트웨어 개발에서도 여러가지 용도로 사용됨
* 특히 성능이 주요한 경우나 최적화가 필요한 경우에 많이 활용됨

1. 성능 최적화 및 연산 속도 향상: 곱셈(*)과 나눗셈(/)보다 비트 연산(<<, >>)이 훨씬 빠름

2. 권한 및 플래그 설정(비트 마스크): 여러 개의 상태(flag)를 하나의 int 변수에 저장할 때 사용

3. 데이터 압축 및 최적화
    - 불필요한 공간을 줄이기 위해 여러 개의 작은 값을 하나의 정수에 저장

4. 해싱(Hashing) 및 암호화(Encryption)
    - 비트 연산을 활용하여 해시 함수 및 암호화 알고리즘을 최적화

5. 빠른 연산(짝수/홀수 판별, 절댓갑 계산 등)

  - 비트 연산은 일반 소프트웨어의 최적화, 보안, 데이터 저장등 다양한 용도로 활용됨

  - 특히 성능이 중요한 게임 엔진, 데이터 압축, 네트워크 프로토콜 등에는 필수적인 기법

조건문 - 단순 if 문, if-else 문
* 단순 if 문
  - if의 괄호 안에 조건식(논리형 변수나 논리 연산)
  - 실행문장이 단일 문장인 경우 둘러싸는 {} 생략 가능

* if-else 문
  - 조건식이 참인 경우와 거짓인 경우에 실행할 문장을 각각 지시

다중 if-else 문
* if-else 문이 연속되는 것
* 조건문이 너무 많은 경우, switch 문 사용 권장

switch 문
* switch 문의 식과 case 문의 값과 비교

  -> case의 비교 값과 일치하면 해당 case의 실행문장 수행

  -> break를 만나면 switch 문을 벗어남

  -> case의 비교 값과 일치하는 것이 없으면 default 문 실행

  -> default 문은 생략 가능


---
## 3월 20일(3주차)
#### README.md 파일 편집
*이름 학번 h1 제일 위에 기재

*날짜(주차)

*배운내용&코드

*최근 날짜가 제일 위로 올라오게

---
## 수업 내용

### Java Project 생성
1. Command Pallet 키: ctrl+shift+p
2. JAVA: CREATE Java Project 선택
3. No build tools 선택
4. 프로젝트 이름 설정

워킹 디렉토리와 프로젝트 디렉토리를 구분

### 프로그래밍 언어
[기계어]

0, 1의 이진수로 구성된 언어

컴퓨터의 CPU는 기계어만 이해하고 처리가 가능

[어셈블리어]

기계어 명령을 ADD, SU, MOVE 등과 같은 표현하기 쉬운 상징적인 단어인 니모닉 기호(mnemonic symbol)로 일대일 대응시킨 언어

[고급언어]

사람이 사용하는 언어로 이해하기 쉽고, 쉽게 표현할 수 있도록 고안된 언어

Pascal, Basic, C/C++, Java, c# 

절차 지향 언어와 객체 지향 언어로 나눌 수 있음

### 프로그램 언어의 패러다임 변화
[절차 지향 언어]

프로그램을 절차, 순서에 따라서 실행하는 방식

데이터(입력)와 함수를 분리하여 작성

코드의 유연성이 부족, 재사용 어려움

전역 변수를 많이 사용하기 때문에 코드의 가독성과 유지보수가 어려움

C, Pascal, Fortran 등이 있음

[객체 지향 언어]

현실의 객체를 모델링하여 프로그램을 작성하는 방식

객체는 데이터와 데이터를 처리하는 메소드(함수)를 모두 포함

상속, 캡슐화, 다형성 등의 개념을 활용하여 유연하고 재사용 가능한 코드를 작성할 수 있음

Java, C++, Python

[함수 지향 언어]

함수형 언어는 함수를 일급 객체로 취급, 상태 변경을 피하고 불변성을 지향하는 프로그래밍 패러다임

함수형 언어에서는 함수의 조합으로 복잡한 작업을 수행, 상태 변경 대신 데이터를 변환하는 방식으로 프로그램을 작성

### 프로그래밍 언어의 진화
1950s COBOL, Fortran, Lisp

1960s ALGOL 60, BASIC

1970s SQL, C, Pascal, Smalltalk

1980s Objective-C, C++, Pert

1990s JavaScript, Java, Ruby, Python, PHP

2000s Scala, C#, Go lang

2010s Swift, TypeScript, Dart, Rust

### 프로그래밍과 컴파일
소스: 프로그래밍 언어로 작성된 텍스트 파일

컴파일: 소스 파일을 컴퓨터가 이해할 수 있는 기계어로 만드는 과정

자바: .java -> .class(반 정도 컴파일)
C: .c -> .obj -> .exe
C++: .cpp -> .obj -> .exe

### 자바의 태동
1991년 그린 프로젝트(Green Project)로 시작
* 선마이크로시스템즈의 제임스 고슬링에 의해 시작
* 가전 제품에 들어갈 소프트웨어를 위해 개발
* 1995년에 자바 발표
* 초기 이름은 오크(OAK)였으며 인터넷과 웹의 발전과 함께 성장

[목적]

플랫폼 호환성 문제 해결
* 기존 언어로 다시 작성된 프로그램은 플랫폼 간에 호환성 없음
* 소스를 다시 컴파일 하거나 프로그램을 재작성해야 하는 단점

플랫폼 독립적인 언어 개발
* 모든 플랫폼에서 호환성을 갖는 프로그래밍 언어 필요
* 네트워크, 특히 웹에 최적화된 프로그래밍 언어의 필요성 대두

메모리 사용량이 적고 다양한 플랫폼을 가지는 가전 제품에 적용
* 가전제품: 작은 량의 메모리를 가지는 제어 장치
* 내장형 시스템 요구 충족

### 기존 언어의 플랫폼 종속성
플랫폼 = 하드웨어 플랫폼 + 운영체제 플랫폼

프로그램의 플랫폼 호환성이 없는 이유
* 기계어가 CPU마다 다름
* 운영체제마다 API 다름
* 운영체제마다 실행파일 형식 다름

### 자바의 플랫폼 독립성,WORA
WORA(Write Once Run Anywhere)
* 한번 작성된 코드는 수정없이 실행가능
* 운영체제나 CPU 등 플랫폼에 상관없이 자바 가상 기계(JVM)만 있으면 어떤 컴퓨터에서든 동일하게 실행

### 자바 JVM과 자바 실행 환경
바이트 코드(.class)
* 자바 JVM에서 실행가능한 바이너리 코드
* 바이트 코드는 컴퓨터 CPU에 의해 직접 실행되지 않음
* 자바JVM이 작동 중인 플랫폼에서 실행
* 자바 JVM이 인터프리터 방식으로 바이트 코드 해석

### JVM(Java Virtual Machine)
* 각기 다른 플랫폼에 맞는 JVM을 제공 JVM 자체는 플랫폼에 종속적
* JVM 각기 다른 플랫폼에서도 동일한 자바 실행 환경을 제공
* JVM은 자바 개발사인 오라클 외 IBM, MS 등 다양한 회사에서 제작 공급
* 자바의 실행은 JVM에서 클래스 파일(.class)을 바이트 코드 실행 하는 것

### 자바 응용프로그램 실행 환경
실행환경은 JVM + java API(클래스 라이브러리)로 구성

응용프로그램의 실행
* main()메소드를 가진 클래스의 main()에서 실행
* JVM은 필요할 때 클래스 파일 로딩하기 때문에 적은 메모리로도 실행 가능

### JDK와 JRE
JDK의 bin 디렉토리에 포홤된 주요 개발 도구
* javac: 자바 소스를 바이트 코드로 변환하는 컴파일러 
* java: 자바 응용프로그램 실행기. 자바 JVM를 작동시켜 자바프로그램 실행 
* javadoc: 자바 소스로브터 HTML 형식의 API 도큐먼트 생성
* jar: 자바 클래스들(패키치포함)을 압축한 자바 아카이브 파일(.jar) 생성 관리
* jmod: 자바의 모듈 파일(.jmod)을 만들거나 모듈 파일의 내용 출력
* jlink: 응용프로그램에 맞춘 맞춤형(custom) JRE 제공
* jdb: 자바 응용프로그램의 실행 중 오류를 찾는 데 사용하는 디버거
* javap: 클래스 파일의 바이트 코드를 소스와 함께 보여주는 디어셈블러

JDK > JRE > JVM, Java Class Library
    > Java Dev Tools > javac, java ...

### Java 표준안
* Java SE(Standard Edition)
* Java EE(Enterprise Edition)
* Java ME(Micro Edition)

### Java의 네이밍 방식
초기 버전 표기법은 1.x 방식으로 표기됨

1.2 버전에서 J2SE(Java2 Standard Edition)으로 변경

1.6 버전부터 Java SE 6 형태로 변경

내부 버전 표기는 1.x.x 형태로 유지되고 있음

### Java 9부터 시작된 모듈 프로그래밍
모듈화(modularity):Java 9에서 정의된 새로운 기능,2017년 9월 21일 출시

모듈: 자바 패키지들과 이미지,XML 파일 등의 자원들을 묶은 단위

모듈 프로그래밍: 프로그램을 레고 만들듯이 필요한 모듈을 연결하는 방식으로 작성

### 자바 플랫폼의 모듈화
* 실행 시간에 사용되는 자바API의 모든 클래스들을 모듈로 분할
* 세밀한 모듈화, 자바 응용프로그램이 실행되는데 필요없는 모듈 배재
* 작은 크기의 실행 환경 구성
* 하드웨어가 열악한 소형 IoT 장치 지원

최근 프로그래밍 방식이 모듈화, 컴포넌트화로 생산성을 높이는 방식으로 바뀌고 있음

### 자바에서 제공하는 전체 모듈 리스트(Java SE)
Java 9부터 SE의 모든 클래스들을 모듈로 재구성

JDK의 설치 디렉토리 밑의 jmods 디렉토리에서 확인 가능

### 자바 API
자바 AP(Application Programming Interface)란
* JDK에 포함된 클래스 라이브러리
* 개발자는 API를 이용하여 쉽고 빠르게 자바 프로그램 개발

자바 패키지(package)
* 자바 API(클래스 라이브러리)는 JDK에 패키지 형태로 제공
* 서로 관련된 클래스들을 분류하여 계층 구조로 묶어 놓은 것

### 자바 소스 편집
src에 Hello.java 파일을 생성

``` java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```
작성

터미널에서 경로를 src로 변환(cd src)

리스트 확인(ls)

클래스 생성(javac Hello.java)(src에 Hello.class 생성됨)

실행(java Hello)

결과: Hello

### 자바 응용프로그램의 종류
데스크톱 응용프로그램
* 가장 일반적인 자바 응용프로그램
* JRE이 설치된 어떤 컴퓨터에서도 실행되며 다른 응용프로그램의 도움 없이 단독으로 실행됨

서블릿 응용프로그램
* 웹 서버에서 실행되는 자바 프로그램
* 사용자 인터페이스를 필요로 하지 않으며 웹 서버에 의해 실행이 제어

모바일 응용프로그램
* 현재 가장 많이 응용되는 것이 안드로이드 플랫폼
* 구글의 주도로 여러 모바일 회사가 모여 개발한 무료 모바일 플랫폼이 안드로이드

### 자바의 특성
플랫폼 독립성
* 하드웨어, 운영체제에 종속되지 않는 바이트 코드로 플랫폼 독립성

객체지향
* 캡슐화, 상속, 다형성 지원

클래스로 캡슐화
* 자바의 모든 변수나 함수는 클래스 내에 선언
* 클래스 안에서 클래스, 즉 내부 클래스 작성 가능

소스(.java)와 클래스(.class) 파일
* 하나의 소스 파일에 여러 클래스를 작성가능:public 클래스는 하나만 가능
* 내부 클래스 각각의 클래스파일이 생성됨

실행 코드 배포
* 한 개의 class 파일 또는 다수의 Class 파일로 구성
* 여러 폴더에 걸쳐 다수의 클래스 파일로 구성된 경우: jar 압축 파일로 배포
* 자바 응용프로그램의 실행은 main() 메소드에서 시작
* 하나의 클래스 파일에 두 개 이상의 main()메소드가 있을 수 없음
* 각 클래스 파일이 main()메소드를 포함하는 것은 상관 없음

패키지
* 서로 관련 있는 여러 클래스를 패키지로 묶어 관리
* 패키지는 폴더 개념

예: java.lang.System은 java\lang 디렉토리의 Sysstem.class파일

멀티스레드
* 여러 스레드의 동시 수행 환경 지원
* 자바는 운영체제의 도움 없이 자체적으로 멀티스레드 지원
* C/C++ 프로그램은 멀티스레드를 위해 운영체제 API를 호출

---

## 3월 13일(2주차)
#### github 연동

# h1 tag
## h2
### h3
#### h4
##### h5 
###### h6



---

* 가가가
- 나나나


1. 나나나
2. 다다다
5. 라라라

```java
public class Main {
  public static void main(String[] args) {
    System.out.println("Hello World");
  }
}

```
<<<<<<< HEAD

=======
>>>>>>> 137a4e284297681cf370973170c26c2b8cfe7476
