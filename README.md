# 주우성 202230236
## 6월 5일(14주차)
### 자바의 이벤트 처리
독립 클래스로 Action 이벤트 리스너 만들기
``` java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class ex9_1 extends JFrame{
    public ex9_1() {
        setTitle("Action 이벤트 리스너 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        Container c = getContentPane();
        c.setLayout(new FlowLayout());
        JButton btn = new JButton("Action");
        btn.addActionListener(new MyActionListener()); //Action 이벤트 리스너 달기
        c.add(btn);

        setSize(250,120);
        setVisible(true);
    }
    public static void main(String [] args){
        new ex9_1();
    }
}

//독립된 클래스로 이벤트 리스너를 작성한다
class MyActionListener implements ActionListener{
    public void actionPerformed(ActionEvent e){
        JButton b = (JButton)e.getSource(); // 이벤트 소스 버튼 알아내기
        if(b.getText().equals("Action")) // 버튼의 문자일여 "Action"인지 비교
            b.setText("액션"); // 버튼의 문자열을 "액션"으로 변경
        else
            b.setText("Action"); // 버튼의 문자열을 "Action"으로 변경
    }
}
```

내부 클래스로 Action 이벤트 리스너 만들기
``` java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class ex9_2 extends JFrame{
    public ex9_2() {
        setTitle("Action 이벤트 리스너 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        Container c = getContentPane();
        c.setLayout(new FlowLayout());
        JButton btn = new JButton("Action");
        btn.addActionListener(new MyActionListener());
        c.add(btn);

        setSize(200,120);
        setVisible(true);
    }

    //내부 클래스로 Action 리스너를 작성한다.
    private class MyActionListener implements ActionListener {
        public void actionPerformed(ActionEvent e) {
            JButton b = (JButton)e.getSource();
            if(b.getText().equals("Action"))
                b.setText("액션");
            else
                b.setText("Action");

            ex9_2.this.setTitle(b.getText());
        }
    }
    public static void main(String [] args) {
        new ex9_2();
    }
}
```

익명 클래스로 이벤트 리스너 작성
* 익명 클래스(anonymous class) : 이름 없는 클래스
  - (클래스 선언 + 인스턴스 생성)을 한번에 달성
  - 간단한 리스너의 경우 익명 클래스 사용 추천
  - 메소드의 개수가 1, 2개인 리스너(ActionListener, ItemListener) 에 대해 주로 사용

마우스 이벤트 리스너 작성 연습 - 마우스로 문자열 이동시키기
``` java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class ex9_4 extends JFrame{
    private JLabel la = new JLabel("Hello"); // "Hello" 문자열을 출력하기 위한 레이블

    public ex9_4() {
        setTitle("Mouse 이벤트 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container c = getContentPane();
        c.addMouseListener(new MyMouseListener()); // 컨텐트팸에 이벤트 리스너 달기

        c.setLayout(null); // 컨텐트팬의 배치관리자 삭제
        la.setSize(50,20); // 레이블의 크기 50x20 설정
        la.setLocation(30, 30); // 레이블의 위치 (30, 30)으로 설정
        c.add(la); // 레이블 삽입
        
        setSize(200, 200);
        setVisible(true);
    }

    class MyMouseListener implements MouseListener {
        public void mousePressed(MouseEvent e) {
            int x = e.getX();
            int y = e.getY();
            la.setLocation(x, y);
        }
        public void mouseReleased(MouseEvent e) {}
        public void mouseClicked(MouseEvent e) {}
        public void mouseEntered(MouseEvent e) {}
        public void mouseExited(MouseEvent e) {}
    }

    public static void main(String [] args) {
        new ex9_4();
    }
}
```

어댑터 클래스
* 이벤트 리스너 구현에 따른 부담
  - 리스너의 추상 메소드를 모두 구현해야 하는 부담
  - 예) 마우스 리스너에서 마우스가 눌러지는 경우(mousePressed())만 처리하고자 하는 경우에도 나머지 4 개의 메소드를 모두 구현해야 하는 부담
* 어댑터 클래스(Adapter)
  - 리스너의 모든 메소드를 단순 리턴하도록 만든 클래스(JDK에서 제공)
* 추상 메소드가 하나뿐인 리스너는 어댑터 없음
  - ActionAdapter, ItemAdapter 클래스는 존재하지 않음

Key 이벤트와 포커스
* 키 입력 시, 다음 세 경우 각각 Key 이벤트 발생
  - 키를 누르는 순간
  - 누른 키를 떼는 순간
  - 누른 키를 떼는 순간(Unicode키의 경우에만)

* 키 이벤트를 받을 수 있는 조건
  - 모든 컴포넌트
  - 현재 포커스(focus)를 가진 컴포넌트가 키 이벤트 독점

* 포커스(focus)
  - 컴포넌트나 응용프로그램이 키 이벤트를 독점하는 권한
  - 컴포넌트에 포커스 설정 방법: 다음 2 라인 코드 필요
  ``` java
  component.setFocusable(true); //component가 포커스를 받을 수 있도록 설정
  component.requestFocus(); // component에 포커스 강제 지정
  ```

* 자바 플랫폼마다 실행 환경의 초기화가 서로 다를 수 있기 때문에 다음 코드가 필요함 <br>
component.setFocusable(true);

KeyListener
* 응용프로그램에서 KeyListener를 상속받아 키 리스너 구현

유니코드(Unicode) 키
* 유니코드 키의 특징
  - 국제 산업 표준
  - 전 세계의 문자를 컴퓨터에서 일관되게 표현하기 위한 코드 체계
  - 문자들에 대해서만 키 코드 값 정의: A~Z, a~z, 0~9, !, @, & 등

* 문자가 아닌 키 경우에는 표준화된 키 코드 값 없음
  - Function 키, Home 키, UP 키, Delete 키, Control 키, Shift 키, Alt 키 등은 플랫폼에 따라 키 코드 값이 다를 수 있음
 * 유니코드 키가 입력되는 경우
  - keyPressed(), keyTyped(), keyReleased() 가 순서대로 호출
* 유니코드 키가 아닌 경우
  - keyPressed(), keyReleased() 만 호출됨

가상 키와 입력된 키 판별
* KeyEvent 객체
  - 입력된 키 정보를 가진 이벤트 객체
  - KeyEvent 객체의 메소드로 입력된 키 판별
* KeyEvent 객체의 메소드로 입력된 키 판별
  - char KeyEvent.getKeyChar()
  - 키의 유니코드 문자 값 리턴
  - Unicode 문자 키인 경우에만 의미 있음
  - 입력된 키를 판별하기 위해 문자 값과 비교하면 됨
  ``` java
  public void keyPressed(KeyEvent e){
    if(e.getKeyChar() == 'q')
      System.exit(0);
  // q키를 누르면 프로그램 종료
  }
  ```

* int KeyEvent.getKeyCode()
  - 유니코드 키 포함
  - 모든 키에 대한 정수형 키 코드 리턴
  - 입력된 키를 판별하기 위해 가상키(Virtual Key) 값과 비교하여야 함
  - 가상 키 값은 KeyEvent 클래스에 상수로 선언
   ``` java
  public void keyPressed(KeyEvent e){
    if(e.getKeyCode() == KeyEvent.VK_F5)
      System.exit(0);
  // F5키를 누르면 프로그램 종료
  }
  ```

가상 키(Virtual Key)
* 가상 키는 KeyEvent 클래스에 상수로 선언

Mouse 이벤트와 MouseListener, MouseMotionListener
* Mouse 이벤트: 사용자의 마우스 조작에 따라 발생하는 이벤트
  - mouseClicked(): 마우스가 눌러진 위치에서 그대로 떼어질 때 호출
  - mouseReleased(): 마우스가 눌러진 위치에서 그대로 떼어지든 아니든 항상 호출
  - mouseDragged(): 마우스가 드래그되는 동안 계속 여러번 호출
* 마우스가 눌러진 위치에서 떼어지는 경우 메소드 호출 순서
> mousePressed(),mouseReleased(),mouseClicked()

* 마우스가 드래그될 때 호출되는 메소드 호출 순서
> mousePressed(), mouseDragged(), mouseDragged()....mouseDragged(), mouseReleased()

마우스 리스너 달기와 MouseEvent 객체 활용
* 마우스 리스너 달기
  - 마우스 리스너는 컴포는트에 다음과 같이 등록
  ``` java
  component.addMouseListener(myMouseListener);
  ```
  - 컴포넌트가 마우스 무브(mouseMoved())나 마우스 드래깅(mouseDragged())을 함께 처리하고자 하면, MouseMotion 리스너 따로 등록
  ``` java
  component.addMouseMotionListener(myMouseMotionListener);
  ```

* MouseEvent 객체 활용
  - 마우스 포인터의 위치, 컴포넌트 내 상대 위치: int getX(), int getY()
  ``` java
  public void mousePressed(MouseEvent e) {
    int x = e.getX(); // 마우스가 눌러진 x좌표
    int y = e.getY(); // 마우스가 눌러진 y좌표
  }
  ```
* 마우스 클릭 횟수: int getClickCount()
``` java
public voidClicked(MouseEvent e) {
  if(e.getClickCount() == 2) {
    ..... // 더블클릭 처리 루틴
  }
}
```

### 스윙 컴포넌트 활용
자바의 GUI 프로그래밍 방법
* 컴포넌트 기반 GUI 프로그래밍
  - 스윙 컴포넌트를 이용하여 쉽게 GUI를 구축
  - 자바에서 제공하는 컴포넌트의 한계를 벗어나지 못함

* 그래픽을 이용하여 GUI 구축
  - 그래픽 기반 GUI 프로그래밍
  - 개발자가 직접 그래픽으로 화면을 구성하는 부담
  - 독특한 GUI를 구성할 수 있는 장접
  - GUI 처리의 실행 속도가 빨라, 게임 등에 주로 이용

스윙 컴포넌트의 공통 메소드, JComponent의 메소드
* JComponent
  - 스윙 컴포넌트의 멤버를 모두 상속받는 슈퍼 클래스, 추상 클래스
  - 스윙 컴포넌트들이 상속받는 공통 메소드와 상수 구현

나머지 챕터의 내용 정리
* 11장 그래픽: paintComponent()활용하여 app에 직접 그림을 그리는 방법
* 12장 자바 스레드 기초: 멀티 태스킹과 스레드의 개념
* 13장 입출력 스트림과 파일 입출력: 자바의 입출력 스트림. 텍스트와 바이너리 File 입출력.
* 14장 자바 소캣 프로그래밍: 소캣 통신에 대한 이해. 인터넷 통신.

* 4장 ,5장, 8장, 9장 복습
  




---
## 5월 29일(13주차)
### 자바 GUI 스윙 기초

컨테이너와 컴포넌트
* 컨테이너
  - 다른 컴포넌트를 포함할 수 있는 GUI 컴포넌트 : java.awt.Container를 상속받음
  - 다른 컨테이너에 포함될 수 있음
  - AWT 컨테이너 : Panel, Frame, Applet, Dialog, Window
  - Swing 컨테이너 : JPanel, JFrame, JApplet, JDialog, JWindow

* 컴포넌트
  - 컨테이너에 포함되어야 화면에 출력될 수 있는 GUI 객체
  - 다른 컴포넌트를 포함할 수 없는 순수 컴포넌트
  - 모든 GUI 컴포넌트가 상속받는 클래스 : java.awt.Component
  - 스윙 컴포넌트가 상속받는 클래스 : Javax.swing.Jconponent

* 최상위 컨테이너
  - 다른 컨테이너에 포함되지 않고도 화면에 출력되며, 독립적으로 존재 가능한 컨테이너
  - 스스로 화면에 자신을 출력하는 컨테이너 : JFrame, JDialog, JApplet

컨테이너와 컴포넌트의 포함관계
* 최상위 컨테이너를 바닥에 깔고,
* 그 위에 컨테이너를 놓고,
* 다시 컴포넌트를 쌓아가는 방식,
* 즉 레고 블록을 쌓는 듯이 GUI 프로그램을 작성

Swing GUI 프로그램 만들기
* 스윙 GUI 프로그램을 만드는 과정
  1. 스윙 프레임 만들기
  2. main() 메소드 작성
  3. 스윙 프레임에 스윙 컴포넌트 붙이기
* 스윙 프로그램 작성에 필요한 import문
``` java
import java.awt.*; // 그래픽 처리를 위한 클래스들의 경로명
import java.awt.event.*; // AWT 이벤트 사용을 위한 경로명
import java.swing.*; // 스윙 컴포넌트 클래스들의 경로명
import java.swing.event.*; // 스윙 이벤트를 위한 경로명
```

Swing 프레임
* 스윙 프레임: 모든 스윙 컴포넌트를 담는 최상위 컨테이너
  - JFrame을 상속받아 구현
  - 컴포넌트들은 화면에 보이려면 스윙 프레임에 부착되어야 함
  - 프레임을 닫으면 프레임에 부착된 모든 컴포넌트가 보이지 않게 됨
* 스윙 프레임(JFrame)기본 구성
  - 프레임: 스윙 프로그램의 기본 틀
  - 메뉴바: 메뉴들이 부착되는 공간
  - 컨텐트팬: GUI 컴포넌트들이 부착되는 공간

프레임 만들기, JFrame 클래스 상속
* 스윙프레임
  - JFrame 클래스를 상속받은 클래스 작성
  - 프레임의 크기를 반드시 지정: setSize() 호출
  - 프레임을 화면에 출력하는 코드 반드시 필요: setVisible(true) 호출
* 300x300 크기의 스윙 프레임 만들기
``` java
import javax.swing.*;

public class ex8_1 extends JFrame {
    public ex8_1() {
        setTitle("300x300 스윙 프레임 만들기");
        setSize(300, 300); // 프레임 크기 300x300
        setVisible(true); // 프레임 출력
    }

    public static void main(String[] args) {
        ex8_1 frame = new ex8_1();
    }
}
```

Swing 응용프로그램에서 main()의 기능과 위치
* 스윙 응용프로그램에서 main()의 기능 최소화 바람직
  - 스윙 응용프로그램이 실행되는 시작점으로서의 기능만
  - 스윙 프레임을 생성하는 정도의 코드로 최소화
``` java
public static void main(String [] args) {
  MyFrame frame = new MyFrame(); // 스윙 프레임 생성
}
```
* frame 객체를 생성하고 사용하지 않기 때문에 worrying이 발생
* 실무에서는 다음과 같이 코딩하는 것이 일반적
``` java
public static void main(String [] args){
  //ex8_1 frame = new ex8_1();
  javax.swing.SwingUtilities.invokeLater(() -> {});
}
```

프레임에 컴포넌트 붙이기
* 타이틀 달기
  - super()나 setTitle() 이용
    ``` java
  MyFrame(){ //생성자
    super("타이틀 문자열"); //JFrame("타이틀문자열") 생성자 호출
  }
  ```
  ``` java
  MyFrame(){ //생성자
    setTitle("타이틀문자열"); //타이틀 달기
  }
  ```
* 컨텐트팬에 컴포넌트 달기
  - 컨텐트팬이란? 스윙 컴포넌트들이 부작되는 공간
  - 컨텐트팬 알아내기: 스윙 프레임에 붙은 디폴트 컨텐트팬 알아내기
  - 컨텐트팬에 컴포넌트 붙이기
  - 컨텐트팬 변경

컨텐트팬에 대한 JDK 1.5 이후의 추가 사항
* jDK 1.5 이전
  - 프레임의 컨텐트팬을 알아내어, 반드시 컨텐트팬에 컴포넌트 부착
* JDK 1.5 이후 추가된 사항
  - 프레임에 컴포넌트를 부착하면 프레임이 대신 컨텐트팬에 부착

3개의 버튼 컴포넌트를 가진 스윙 프레임 만들기 (JDK1.5이전)
``` java
import javax.swing.*;
import java.awt.*;

public class ex8_2 extends JFrame{
    public ex8_2() {
        setTitle("ContentPane과 JFrame 예제"); //프레임의 타이틀 달기
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); // 프레임 윈도우를 닫으면 프로그램 종료

        Container contentPane = getContentPane(); // 컨텐트팬을 알아낸다
        contentPane.setBackground(Color.ORANGE); // 오렌지색 배경 설정
        contentPane.setLayout(new FlowLayout()); // 컨텐트팬에 FlowLayout 배치관리자 달기

        contentPane.add(new JButton("OK")); // OK 버튼 달기
        contentPane.add(new JButton("Cancel")); // Cancel 버튼 달기
        contentPane.add(new JButton("Ignore")); // Ignore 버튼 달기

        setSize(300,150); // 프레임 크기 300x150 설정
        setVisible(true); // 화면에 프레임 출력
    }

    public static void main(String[] args) {
        new ex8_2();
    }
}
```
3개의 버튼 컴포넌트를 가진 스윙 프레임 만들기 (JDK1.5이후)
``` java
import javax.swing.*;
import java.awt.*;

public class ex8_2 extends JFrame{
    public ex8_2() {
        setTitle("ContentPane과 JFrame 예제"); //프레임의 타이틀 달기
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); // 프레임 윈도우를 닫으면 프로그램 종료


        getContentPane().setBackground(Color.ORANGE); // 오렌지색 배경 설정
        getContentPane().setLayout(new FlowLayout()); // 컨텐트팬에 FlowLayout 배치관리자 달기

        add(new JButton("OK")); // OK 버튼 달기
        add(new JButton("Cancel")); // Cancel 버튼 달기
        add(new JButton("Ignore")); // Ignore 버튼 달기

        setSize(300,150); // 프레임 크기 300x150 설정
        setVisible(true); // 화면에 프레임 출력
    }

    public static void main(String[] args) {
        new ex8_2();
    }
}
```

Swing 응용프로그램의 종료
* 응용프로그램 내에서 스스로 종료하는 방법
  - 언제 어디서나 무조건 종료
  ``` java
  System exit(0);
  ```
* 프레임의 오른쪽 상단의 종료버튼(x)이 클랙되면 어떤 일이 일어나는가?
  - 프레임 종료, 프레임 윈도우를 닫음: 프레임이 화면에서 보이지 않게 됨
* 프레임이 보이지 않게 되지만 응용프로그램이 종료한 것 아님
  - 키보드나 마우스 입력을 받지 못함
  - 다시 setVisible(true)를 호출하면, 보이게 되고 이전 처럼 작동함
* 프레임 종료버튼이 클랙될 때, 프레임과 함께 프로그램을 종료시키는 방법
``` java
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
```

컨테이너 배치, 배치관리자 개념
* 컨테이너의 배치관리자
  - 컨테이너마다 하나의 배치관리자 존재
  - 컨테이너에 부착되는 컴포넌트의 위치와 크기 결정
  - 컨테이너의 크기가 변경되면, 컴포넌트의 위치와 크기 재결정

배치 관리자 대표 유형 4가지
* FlowLayout 배치 관리자
  - 컴포넌트가 삽입되는 순서대로 왼쪽에서 오른쪽으로 배치
  - 배치할 공간이 없으면 아래로 내려와서 반복
* BorderLayout 배치관리자
  - 컨테이너의 공간을 동, 서 ,남, 북, 중앙의 5개 영역으로 나눔
  - 5개 영역 중 응용프로그램에서 지정한 영역에 컴포넌트 배치
* GridLayout 배치 관리자
  - 컨테이너를 프로그램에서 설정한 동일한 크기의 2차원 격자로 나눔
  - 컴포넌트는 삽입 순서대로 좌에서 우로, 다시 위에서 아래로 배치
* CardLayout
  - 컨테이너의 공간에 카드를 쌓아놓은 듯이 컴포넌트를 포개서 배치

컨테이너와 디폴트 배치관리자
* 컨테이너의 디폴트 배치관리자: 컨테이너 생성시 자동으로 생성되는 배치관리자

| AWT와 스윙 컨테이너 | 디폴트 배치관리자 |
|---|---|
|Window, JWindow | BorderLayout
|Frame, JFrame | borderLayout
|Dialog, JDialog | BorderLayout
|Panel, JPanel | FlowLayout
|Applet, JApplet | FlowLayout

컨테이너에 새로운 배치관리자 설정
* 컨테이너에 새로운 배치관리자 설정
  - setLayout(LayoutManager lm)메소드 호출: lm을 새로운 배치관리자로 설정
* [사례]
  - JPanel 컨테이너에 BorderLayout 배치관리자를 설정하는 예
  ``` java
  JPanel p = new JPanel();
  p.setLayout(new BorderLayout()); //패널에 BorderLayout 배치관리자 설정
  ```
  - 컨텐트팬의 배치관리자를 FlowLayout 배치관리자로 설정
  ``` java
  Container c = frame.getContentPane(); //프레임의 컨텐트팬 알아내기
  c.setLayout(new FlowLayout()); //컨텐트팬에 FlowLayout 설정
  ```
  - 오류
  ``` java
  c.setLayout(FlowLayout); // 오류
  ```

FlowLayout 배치관리자
* 배치 방법:
  - 컴포넌트를 컨테이너 내에 왼쪽에서 오른쪽으로 배치
  - 다시 위에서 아래로 순서대로 배치
``` java
container.setLayout(new FlowLayout());
container.add(new JButton("add"));
container.add(new JButton("sub"));
container.add(new JButton("mul"));
container.add(new JButton("div"));
container.add(new JButton("Calculate"));
```

FlowLayout의 생성자
* 생성자: 
  - FlowLayout()
  - FlowLayout(int align, int hGap, int vGap)
* align: 컴포넌트를 정렬하는 방법 지정. 왼쪽 정렬(FlowLayout.LEFT), 오른쪽 정렬(FlowLayout.RIGHT), 중앙 정렬(FlowLayout.CENTER(디폴트))
* hGap: 좌우 두 컴포넌트 사이의 수평 간격, 픽셀 단위. 디폴트는 5
* vGap: 상하 두 컴포넌트 사이의 수직 간격, 픽셀 단위. 디폴트는 5

FlowLayout 배치관리자 활용
``` java
import javax.swing.*;
import java.awt.*;

public class ex8_3 extends JFrame{
    public ex8_3() {
        setTitle("FlowLayout 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container contentPane = getContentPane(); // 컨텐트팬 알아내기

        //왼쪽 정렬로, 수평 간격을 30, 수직 간격을 40 픽셀로 배치하는 FlowLayout 생성
        contentPane.setLayout(new FlowLayout());

        contentPane.add(new JButton("add"));
        contentPane.add(new JButton("sub"));
        contentPane.add(new JButton("mul"));
        contentPane.add(new JButton("div"));
        contentPane.add(new JButton("Calculate"));

        setSize(300, 200);
        setVisible(true);
    }
    public static void main(String[] args) {
        new ex8_3();
    }
}
```

BorderLayout 배치관리자
* 배치방법
  - 컨테이너 공간을 5 구역으로 분할, 배치: 동, 서, 남, 북, 중앙

BorderLayout 생성자와 add() 메소드
* 생성자
  - BorderLayout()
  - BorderLayout(int hGap, int vGap)

GridLayout 배치관리자
* 배치 방법
  - 컨테이너 공간을 동일한 사각형 격자(그리드)로 분할하고 각 셀에 컴포넌트 하나씩 배치
    - 생성자에 행수와 열수 지정
    - 셀에 왼쪽에서 오른쪽으로, 다시 위에서 아래로 순서대로 배치

GridLayout 생성자
* GridLayout(int rows, int cols, int hGap, int vGap)
  - rows: 격자의 행수(디폴트: 1)
  - cols: 격자의 열수(디폴트: 1)

배치관리자 없는 컨테이너
* 배치관라자가 없는 컨테이너가 필요한 경우
  - 응용프로그램에서 직접 컴포넌트의 크기와 위치를 결정하고자 하는 경우
    1. 컴포넌트의 크기나 위치를 개발자 임의로 결정하고자 하는 경우
    2. 게임 프로그램과 같이 시간이나 마우스/키보드의 입력에 따라 컴포넌트들의 위치와 크기가 수시로 변하는 경우
    3. 여러 컴포넌트들이 서로 겹쳐 출력하고자 하는 경우
* 컨테이너의 배치 관리자 제거 방법
  - container.setLayout(null);
  - 컨테이너의 배치관리자가 없어지면, 컴포넌트에 대한 어떤 배치도 없음
    - 추가된 컴포넌트의 크기가 0으로 설정, 위치는 예측할 수 없게 됨
    ``` java
    //패널 p에는 배치관라자가 없으면 아래 두 버튼은 배치되지 않는다
    p.add(new.JButton("click")); //폭과 높이가 0인 상태로 화면에 보이지 않는다
    p.add(new.JButton("me!"));//폭과 높이가 0인 상태로 화면에 보이지 않는다
    ```

컴포넌트의 절대 위치와 크기 설정
* 배치관리자가 없는 컨테이너에 컴포넌트를 삽입할 때
  - 프로그램에서 컴포넌트의 절대 크기와 위치 설정
  - 컴포넌트들이 서로 겹치게 할 수 있음
* 컴포넌트의 크기와 위치 설정 메소드
``` java
void setSize(int width, int height); // 컴포넌트 크기 설정
void setLocation(int x, int y); // 컴포넌트 위치 설정
void setBounds(int x, int y, int width, int height); // 위치와 크기 동시 설정
```

### 자바의 이벤트 처리
이벤트 기반 GUI 프로그래밍
* 이벤트 기반 프로그래밍(Event Driven Programming)
  - 이벤트의 발생에 의해 프로그램 흐름이 결정되는 방식
    - 이벤트가 발생하면 이벤트를 처리하는 루틴(이벤트 리스너) 실행
    - 실행될 코드는 이벤트의 발생에 의해 전적으로 결정
  - 반대되는 개념: 배치 실행(batch programming)
    - 프로그램의 개발자가 프로그램의 흐름을 결정하는 방식
  - 이벤트 종류
    - 사용자의 입력: 마우스 드래그, 마우스 클릭, 키보드 누름 등
    - 센서로부터의 입력, 네트워크로부터 데이터 송수신
    - 다른 응용프로그램이나 다른 스레드로부터의 메세지
* 이벤트 기반 응용 프로그램의 구조
  - 각 이벤트마다 처리하는 리스너 코드 보유
* GUI 응용프로그램은 이벤트 기반 프로그래밍으로 작성됨
  - GUI 라이브러리 종류: C++의 MFC, C# GUI, Visual Basic, X Window, Android 등
  - 자바의 AWT와 Swing

자바 스윙 프로그램에서 이벤트 처리 과정
1. 이벤트 발생
  - 예: 마우스와 움직임 혹은 키보드 입력
2. 이벤트 객체 생성
  - 현재 발생한 이벤트에 대한 정보를 가진 객체
3. 응용프로그램에 작성된 이벤트 리스너 찾기

이벤트 객체
* 이벤트 객체
  - 발생한 이벤트에 관한 정보를 가진 객체
  - 이벤트 리스너에 전달됨: 이벤트 리스너 코드가 발생한 이벤트에 대한 상황을 파악할 수 있게 함
* 이벤트 객체가 포함하는 정보
  - 이벤트 종류와 이벤트 소스
  - 이벤트가 발생한 화면 좌표 및 컴포넌트 내 좌표
  - 이벤트가 발생한 버튼이나 메뉴 아이템의 문자열
  - 클릭된 마우스 버튼 번호 및 마우스의 클릭 횟수
  - 키의 코드 값과 문자 값
  - 체크박스, 라디오버튼 등과 같은 컴포넌트에 이벤트가 발생하였다면 체크 상태
* 이벤트 소스를 알아내는 메소드 : Object getSource()
  - 발생한 이벤트의 소스 컴포넌트 리턴
  - Object 타입으로 리턴하므로 캐스팅하여 사용
  - 모든 이벤트 객체에 대해 적용

리스너 인터페이스
* 이벤트 리스너: 이벤트를 처리하는 자바 프로그램 코드, 클래스로 작성
* 자바는 다양한 리스너 인터페이스 제공
  - 예) ActionListener 인터페이스 - 버튼 클릭 이벤트를 처리하기 위한 인터페이스
  - 예) MouseListener 인터페이스 - 마우스 조작에 따른 이벤트를 처리하기 위한 인터페이스
* 사용자의 이벤트 리스너 작성
  - 자바의 리스너 인터페이스를 상속받아 구현
  - 리스너 인터페이스의 모든 추상 메소드 구현

이벤트 리스너 작성 과정 사례
1. 이벤트와 이벤트 리스너 선택
  - 버튼 클릭을 처리하고자 하는 경우
    - 이벤트: Action 이벤트, 이벤트 리스너: ActionListener
2. 이벤트 리스너 클래스 작성: ActionListener 인터페이스 구현
3. 이벤트 리스너 등록
  - 이벤트를 받아 처리하고자 하는 컴포넌트에 이벤트 리스너 등록
  - component.addXXXListener(listener)
    - xxx: 이벤트 명, listener: 이벤트 리스너 객체

이벤트 리스너 작성 방법
* 독립 클래스로 작성
  - 이벤트 리스너를 완전한 클래스로 작성
  - 이벤트 리스너를 여러 곳에서 사용할 때 적합
* 내부 클래스로 작성
  - 클래스 안에 멤버처럼 클래스 작성
  - 이벤트 리스너를 특정 클래스에서만 사용할 때 적합
* 익명 클래스로 작성
  - 클래스의 이름 없이 간단히 리스너 작성
  - 클래스 조차 만들 필요 없이 리스너 코드가 간단한 경우에 적합

---
## 5월 22일(12주차)
### 모듈과 패키지 개념, 자바 패키지 활용
StringBuffer 클래스
* 가변 스트링을 다루는 클래스
* StringBuffer 객체 생성
``` java
StringBuffer sb = new StringBuffer("java"); //Java를 가진 StringButter 객체
```
* String 클래스와 달리 문자열 변경 가능
  - 가변 크기의 버퍼를 가지고 있어 문자열 수정 가능
  - 문자열의 수정이 많은 작업에 적합
* 스트링 조작 사례
``` java
StringBuffer sb = new StringBuffer("This");

sb.append(" is pencil"); // sb = "This is pencil"
sb.insert(7, " my"); // sb = "this is my pencil"
sb.replace(8, 10, "your"); // sb = "This is your pencil"
System.out.println(sb); //"This is your pencil" 출력
```

StringTokenizer 클래스
* 구분 문자를 기준으로 문자열을 분리하는 클래스
  - 구분 문자(delimiter): 문자열을 구분할 때 사용되는 문자
  - 토큰(token): 구분 문자로 분리된 문자열
``` java
int count = st.countTokens(); // 토큰 개수 알아내기.
String token  = st.nextToken(); // 토큰을 하나씩 얻어내기
```

StringTokenizer를 이용한 문자열 분리
``` java
import java.util.StringTokenizer;
public class ex6_7 {
    public static void main(String[] args) {
        String query = "name=kitae&addr=seoul&age=21";
        StringTokenizer st = new StringTokenizer(query, "&");

        int n =st.countTokens(); // 분리된 토큰 개수
        System.out.println("토큰 개수 = " + n);
        while(st.hasMoreTokens()) { // for(int i=0; i<n; i++)와 동일
            String token = st.nextToken(); // 토큰 얻기
            System.out.println(token); // 토큰 출력
        }
    }
}
결과: 토큰 개수 = 3
name=kitae
addr=seoul
age=21 
```

Math 클래스
* 기본 산술 연산 메소드를 제공하는 클래스
* 모든 메소드는 static으로 선언
  - 클래스 이름으로 호출 가능
* Math.randon() 메소드로 난수 발생
  - random()은 0보다 크거나 같고 1.0보다 작은 실수 난수 발생
  - 1에서 100까지의 랜덤 정수 10개를 발생시키는 코드 사례
``` java
for(int x=0; x<10; x++){
  int n = (int)(Math.random()*100 + 1); // 1~100까지의 랜덤 정수 발생
  System.out.println(n);
}
```

* java.util.Random 클래스를 이용하여 난수 발생 가능
``` java
Random r = new Random();
int n = r.nextInt(); // 음수, 양수, 0 포함, 자바의 정수 범위 난수 발생
int m = r.nextInt(100); // 0에서 99 사이(0과 99포함)의 정수 난수 발생
```

Math 클래스 활용
``` java
public class ex6_8 {
    public static void main(String[] args) {
        System.out.println(Math.abs(-3.14)); // 절댓값 구하기
        System.out.println(Math.sqrt(9.0)); // 제곱근
        System.out.println(Math.exp(2)); // e의 2승
        System.out.println(Math.round(3.14)); // 반올림

        // [1, 25] 사이의 정수형 난수 5개 발생
        System.out.print("이번주 행운의 번호는 ");
        for(int i=0; i<5; i++)
            System.out.print((int)(Math.random()*45 + 1) + " "); // 난수 발생
    }
}
결과: 3.14
3.0
7.38905609893065
3
이번주 행운의 번호는 27 21 17 37 41 
```


### 컬렉션과 제네릭
컬렉션(collection)의 개념
* 요소(element)라고 불리는 가변 개수의 객체들의 저장소
  - 객체들의 컨테이너라고도 불림
  - 요소의 개수에 따라 크기 자동 조절
  - 요소의 삽입, 삭제에 따른 요소의 위치 자동 이동
* 고정 크기의 배열을 다루는 어려움 해소
* 다양한 객체들의 삽입, 삭제, 검색 등의 관리 용이

컬렉션 자바 인터페이스와 클래스

컬렉션의 특징
1. 컬렉션은 제네릭(generics) 기법으로 구현
* 제네릭
  - 특정 타입만 다루지 않고, 여러 종류의 타입으로 변신할 수 있도록 클래스나 메소드를 일반화 시키는 기법
  - 클래스나 인터페이스 이름에 <E>, <K>, <V> 등 타입 매개변수 포함
* 제네릭 컬렉션 사례 : 벡터 Vector<E>
   -<E>에서 E에 구체적인 타입을 주어 구체적인 타입만 다루는 벡터로 활용
   - 정수만 다루는 컬렉션 벡터 Vector<Integer>
   - 문자열만 다루는 컬렉션 벡터 Vector<String>

2. 컬렉션의 요소는 객체만 가능
* int, char, double 등의 기본 타입으로 구체화 불가
* 컬렉션 사례
``` java
Vector<int> v = new Vector<int>(); // 컴파일 오류, int는 사용 불가
Vector<Integer> v = new Vector<Integer>() // 정상 코드
```

제네릭은 형판과 같은 개념
* 제네릭은 클래스나 메소드를 형판에서 찍어내듯이 생산할 수 있도록 일반화된 형판을 만드는 기법

제네릭의 기본 개념
* 제네릭
  - JDK 1.5부터 도입(2004년 기점)
  - 모든 종류의 데이터 타입을 다룰 수 있도록 일반화된 타입 매개 변수로 클래스(인터페이스)나 메소드를 작성하는 기법
  - C++의 템플릿(template)과 동일

Vector<E>의 특징
* <E>에 사용할 요소의 특정한 타입으로 구체화
* 배열을 가변 크기로 다룰 수 있게 하는 컨테이너
  - 배열의 길이 제한 극복
  - 요소의 개수가 넘치면 자동으로 길이 조절
* 요소 객체들을 삽입, 삭제, 검색하는 컨테이너
  - 삽입, 삭제에 따라 자동으로 요소의 위치 조정
* Vector에 삽입 가능한 것
  - 객체, null
  - 기본 타입의 값은 Wrapper 객체로 만들어 저장
* Vector에 객체 삽입
  - 벡터의 맨 뒤, 중간에 객체 삽입 가능
* Vector에서 객체 삭제
  - 임의의 위치에 있는 객체 삭제 가능
``` java
Vector<Integer> v = new Vector<Integer>(); //정수만 사용 가능한 벡터
Vector<int> v = new Vector<int>(); // 오류. int는 사용 불가
Vector<Integer> v = new Vector<Integer>(); // 초기 용량이 7인 벡터 생성
```

타입 매개 변수 사용하지 않는 경우 경고 발생
* Vector<Integer>나 Vector<String> 등 타입 매개 변수를 사용해야 함

Vector<E> 클래스의 주요 메소드
* boolean add(E element): 벡터의 맨 뒤에 element 추가
* void add(int index, e element): 인덱스 index에 element를 삽입
* int capacity(): 벡터의 현재 용량 리턴
boolean addAll(Collction?extends e> c): 컬렉션 c의 모든 요소를 벡터의 맨 뒤에 추가
* void clear(): 벡터의 모든 요소 삭제
* boolean contains(Object o): 벡터가 지정된 객체 o를 포함하고 있으면 true 리턴
* E elementAt(int inedx): 인덱스 index의 요소 리턴
* E get(int index): 인덱스 index의 요소 리턴
...

컬렉션과 자동 박싱/언박싱
* JDK 1.5 이전
  - 기본 타입 데이터를 Wrapper 객채로 만들어 삽입
  ``` java
  Vector<Integer> v = new Vector<Integer>();
  v.add(Integer.valueOf(4));
  ```
  - 컬렉션으로부터 요소를 얻어올 때, Wraper 클래스로 캐스팅 필요
  ``` java
  Integer n = (integer)v.get(0);
  int k = n.intValue(); // k = 4
  ```

* JDK 1.5 부터
  - 자동 박싱/언박싱이 작동하여 기본 타입 값 삽입 가능
  ``` java
  Vector<Integer> v = new Vector<Integer>();
  v.add(4); // 정수 4가 Integer(4)로 자동 박싱됨
  ```
  - 그러나, 타입 매개 변수를 기본 타입으로 구체화할 수는 없음
  ``` java
  int k = v.get(0); // k = 4
  ```

컬렉션 생성문의 진화: Java 7, Java 10
* Java 7 이전
``` java
Vector<Integer> v = new Vector<Integer>();
```
* Java 7 이후
  - 컴파일러의 타입 추론 기능 추가
  - <>(다이어몬드 연산자)에 타입 매개변수 생략
``` java
Vector<Integer> v = new Vector<>(); //Java 7부터 추가, 가능
```
* Java 10 이후
  - var 키워드 도입, 컴파일러의 지역 변수 타입 추론 가능
``` java
var v = new Vector<Integer>(); // Java 10부터 추가, 가능
```

ArrayList<E>
* 가변 크기 배열을 구현한 클래스
  - <E>에 요소로 사용할 특정 타입으로 구체화
* 벡터와 거의 동일
  - 요소 삽입, 삭제, 검색 등 벡터 기능과 거의 동일
  - 벡터와 달리 스레드 동기화 기능 없음
  - 다수 스레드가 동시에 ArrayList에 접근할 때 동기화되지 않음
  - 개발자가 스레드 동기화 코드 작성

ArrayList와 Vector의 차이
* ArrayList와 Vector는 모두 동적으로 크기가 늘어나는 배열 기반으 리스트 클래스
* 비교 요약 <br>

| 항목 | ArrayList | Vector |
|---|---|---|
|초기화 여부|비동기화(스레드안전X)|동기화(스레드안전O)
|성능|빠름(싱글 스레드에 적합)|느림(동기화로 인한 오버헤드 발생)
|기본 크기 증가|1.5배씩 증가|2배씩 증가
|도입 시기|Java 1.2(Collecton Framework)|Java1.0(초기부터 존재)
|사용 권장 여부|현대 개발에서 추천|특별한 이유가 없다면 지양

* 요즘은 ArrayList가 기본 선택지
* Vector는 이제 거의 사용하지 않고, 멀티스레드가 필요하면 다른 방법(synchronizedList, CopyOnWriteArrayList)을 사용

컬렉션의 순차 검색을 위한 Iterator
* Iterator<E> 인터페이스
  - 리스트 구조의 컬렉션에서 요소의 순차 검색을 위한 인터페이스
  - Vector<E>, ArrayList<E>, LinkedList<E>가 상속받는 인터페이스
* Iterator 객체 얻어내기
  - 컬렉션의 iterator() 메소드 호출: 해당 컬렉션을 순차 검색할 수 있는 Iterator 객체 리턴
  ``` java
  Vector<Integer> v = new Vector<Integer>();
  Iterator<Integer> it = v.iterator();
  ```
* 컬렉션 검색 코드
``` java
while(int.hasNext()){ // 모든 요소 방문
  int n = it.next(); // 다음 요소 리턴
  ...
}
```

HashMap<K, V>
* 키(key)와 값(value)의 쌍으로 구성되는 요소를 다루는 컬렉션
  - K: 키로 사용할 요소의 타입
  - V: 값으로 사용할 요소의 타입
  - 키와 값이 한 쌍으로 삽입
  - '값'을 검색하기 위해서는 반드시 '키' 이용
* 삽입 및 검색이 빠른 특징
  - 요소 삽입: put() 메소드
  - 요소 검색: get() 메소드
* 예) HashMap<String, String> 생성, 요소 삽입, 요소 검색
``` java
HashMap<String, String> h = new HashMap<String, String>(); // 해시맵 객체 생성

h.put("apple", "사과"); // apple" 키와 "사과" 값의 쌍을 해시맵에 삽입
String kor = h.get("apple"); // "apple" 키로 값 검색. kor는 "사과"
```

제네릭 만들기
* 제네릭 클래스 작성: 클래스 이름 옆에 일반화된 타입 매개 변수 추가
``` java
public class Myclass<T>{ //제네릭 클래스 MyClass 선언, 타입 매개 변수 T
  T val;
  void set(T a){
    val = a; // T 타입의 값 a를 val에 지정
  }
  T get(){
    return val; // T 타입의 값 val 리턴
  }
}
```
* 제네릭 객체 생성 및 활용
  - 제네릭 타입에 구체적인 타입을 지정하여 객체를 생성하는 것을 구체화라고 함
``` java
MyClass<String> s = new MyClass<String>(); // T를 String으로 구체화
s.set("Hello");
System.out.println(s.get()); // "Hello" 출력

MyClass<Integer> n = new MyClass<Integer>(); // T를 Integer로 구체화
n.set(5);
System.out.println(n.get()); // 숫자 5 출력
```

### 자바 GUI 스윙 기초
자바의 GUI
* GUI: 사용자가 편리하게 입출력 할 수 있도록 그래픽으로 화면을 구성하고, 마우스나 키보드로 입력 받을 수 있도록 지원하는 사용자 인터페이스
* 자바 언어에서 GUI 응용프로그램 작성: AWT와 Swing 패키지에 강력한 GUI 컴포넌트 제공

* AWT(Abstract Windowing Toolkit) 패키지
  - 자바가 처음 나왔을 때 부터 배포된 GUI 패키지, 최근에는 거의 사용하지 않음
  - AWT 컴포넌트는 중량 컴포넌트(heavy weight component)
  - AWT 컴포넌트의 그리기는 운영체제에 의해 이루어지며, 운영체제의 자원을 많이 소모하고 부담을 줌
  - 운영체제가 직접 그리기 때문에 속도는 빠름

* Swing 패키지
  - AWT 기술을 기반으로 작성된 자바 라이브럴
  - 모든 AWT 기능 + 추가된 풍부하고 화려한 고급 컴포넌트
  - AWT 컴포넌트를 모두 스윙으로 재작성
  - AWT 컴포넌트 이름 앞에 J자를 덧붙임
  - 순수 자바 언어로 구현
  - 스윙 컴포넌트는 경량 컴포넌트(light weight component)
  - 스윙 컴포넌트는 운영체제의 도움을 받지 않고, 직접 그리기 때문에 운영체제에 부담주지 않음
  - 현재 자바의 GUI 표준으로 사용됨

GUI 패키지 계층 구조
* 모든 GUI 컴포넌트들은 Component 클래스를 반드시 상속받음
* 그 중 스윙 컴포넌트의 클래스 명은 모두 J로 시작

---
## 5월 15일(11주차)
### 모듈과 패키지 개념, 자바 패키지 활용
모듈 개념
* Java 9에서 도입된 개념
* 패키지와 이미지 등의 리소스를 담은 컨테이너
* 모듈 파일(.mod)로 저장

자바 플랫폼의 모듈화
* 자바 플랫폼
  - 자바의 개발 환경(JDK)와 자바의 실행 환경(JRE)를 지칭. Java SE(자바 API) 포함
  - 자바 API의 모든 클래스가 여러 개의 모듈로 재구성됨
  - 모듈 파일은 JDK와 jmods 디렉터리에 저장하여 배포
* 모듈 파일로부터 모듈을 푸는 명령
  - jmod extract "C:\Program Files\Java\jdk-1.0.3+7\jmods\java.base.jmod"
  - 현재 디렉터리에 java.base 모듈이 패키지와 클래스들로 풀림
* 테스트를 할 때는 temp 디렉토리를 만들어서 하는 것이 좋음

자바 모듈화의 목적
* 자바 컴포넌트들을 필오에 따라 조립하여 사용하기 위함
* 컴퓨터 시스템의 불필요한 부담 감소
  - 세밀한 모듈화를 통해 필요 없는 모듈이 로드되지 않게 함
  - 소형 IoT 장치에도 자바 응용프로그램이 실행되고 성능을 유지하게 함

JDK의 주요 패키지
* java.lang
  - 스트링, 수학 함수, 입출력 등 자바 프로그래밍에 필요한 기본적인 클래스와 인터페이스
  - 자동으로 import 됨- import 문 필요 없음
* java.util
  - 날짜, 시간, 벡터, 해시맵 등의 유틸리티 클래스와 인터페이스
* java.io
  - 키보드, 모니터, 프린터 등의 입출력 클래스와 인터페이스
* java.awt
   - GUI 프로그래밍에 필요한 AWT 클래스와 인터페이스
* javax.swing
  - 스윙 GUI 프로그래밍에 필요한 클래스와 인터페이스

Object 클래스
* 모든 자바 클래스는 반드시 Object를 상속받도록 자동 컴파일
* 모든 클래스의 수퍼 클래스
* 모든 클래스가 상속받는 공통 메소드 포함
* 주요 메소드
  - boolean equals(Object obj)
  - Class getClass()
  - int hashCode
  - String toString()
  - void notify()
  - void notifyAll()
  - void wait()

객체 속성
* Object 클래스는 객체의 속성을 나타내는 메소드 제공
* hashCode() 메소드
  - 객체의 해시코드 값을 리턴하며, 객체마다 다름
* getClass() 메소드
  - 객체의 클래스 정보를 담은 Class 객체 리턴
  - Class 객체의 getName() 메소드는 객체의 클래스 이름 리턴
* toString() 메소드
  - 객체를 문자열로 리턴

Object 클래스로 겍체의 속성 알아내기
``` java
class Point {
    private int x, y;
    public Point(int x, int y){
        this.x = x; this.y = y;
    }
}

public class ex6_1 {
    public static void main(String[] args) {
        Point p = new Point(2,3);
        System.out.println(p.getClass().getName());
        System.out.println(p.hashCode());
        System.out.println(p.toString());
    }
}
결과: Point
804564176
Point@2ff4acd0
```

toString() 메소드, 객체를 문자열로 변환
* 각 클래스는 toString()을 오버라이딩하여 자신만의 문자열 리턴 가능
  - 객체를 문자열로 반환
  - 원형: public String toString();
``` java
public String toString(); //public으로 선언해야 함에 특히 주의
```
* 컴파일러에 의한 toString() 자동 변환
  - '객체' + '문자열' -> '객체.toString() + 문자열'로 자동 변환
  - 객체를 단독으로 사용하는 경우 -> 객체.toString()으로 자동 변환
``` java
Point a = new Point(2, 3);
String s = a + "점"; // a.toString() + "점"으로 자동 변환됨
System.out.println(a); // System.out.println(a.toString());으로 자동 변환됨
```

Point 클래스에 toString() 작성
``` java
class Point {
    private int x, y;
    public Point(int x, int y){
        this.x = x; this.y = y;
    }
    public String toString() {
        return "Point(" + x + "," + y + ")";
    }
}

public class ex6_2 {
    public static void main(String[] args) {
        Point a = new Point(2,3);
        System.out.println(a.toString());
        System.out.println(a); // a는 a.toString()으로 자동 변환됨
    }
}
결과: Point(2, 3)
Point(2, 3)
```

객체 비교(==)와 equals() 메소드
* == 연산자: 객체 레퍼런스 비교
``` java
Point a = new Point(2,3);
Point b = new Point(2,3);
Point c = a;

if (a==b) // false
  System.out.println("a==b");
if (a==c) // true
  System.out.println("a==c");
결과: a==c
```

* boolean equals(Object obj)
  - 두 객체의 내용물 비교
  - 객체의 내용물을 비교하기 위해 클래스의 멤버로 작성

Point 클래스의 equals() 작성
``` java
class Point2{
    private int x, y;
    public Point2(int x, int y){ this.x = x; this.y = y;}
    public  boolean equals(Object obj){
        Point2 p = (Point2)obj; // obj를 Point 타입으로 다운 캐스팅
        if(x == p.x && y == p.y) return true;
        else return false;
    }
}

public class ex6_3 {
    public static void main(String[] args) {
        Point2 a = new Point2(2,3);
        Point2 b = new Point2 (2,3);
        Point2 c = new Point2(3,4);
        if(a == b) System.out.println("a==b");
        if(a.equals(b)) System.out.println("a is equal to b");
        if(a.equals(c)) System.out.println("a is equal to c");
    }
}
결과: a is equla to b
```

Rect 클래스와 equals() 메소드 만들기 연습
``` java
class Rect1 {
    private int width, height;
    public Rect1(int width, int height){
        this.width = width; this.height = height;
    }
    public boolean equals(Object obj){ // 사각형 면적 비교
        Rect1 p = (Rect1)obj; // obj를 Rect로 다운 캐스팅
        if (width*height == p.width*p.height) return true;
        else return false;
    }
}

public class ex6_4 {
    public static void main(String[] args) {
        Rect1 a = new Rect1(2,3); // 면적 6
        Rect1 b = new Rect1(3,2); // 면적 6
        Rect1 c = new Rect1(3,4); // 면적 12
        if(a.equals(b)) System.out.println("a is equal to b");
        if(a.equals(c)) System.out.println("a is equal to c");
        if(b.equals(c)) System.out.println("b is equal to c");
    }
}
결과: a is equal to b
```

Wrapper 클래스
* Wrapper 클래스: 자바의 기본 타입을 클래스화 한 8개 클래스를 통칭
* 용도: 객체만 사용할 수 있는 컬렉션 등에 기본 타입의 값을 사용하기 위해 Wrapper 객체로 만들어 사용

Wrapper 객체 생성
* 기본 타입의 값으로 Wrapper 객체 생성
``` java
Integer i = Integer.valueOf(10);
Character c = Character.valueOf('c');
Double f = Double.valueOf(3.14);
Boolean b = Boolean.valueOf(true);
```
* 문자열로 Wrapper 객체 생성
``` java
Integer i = Integer.valueOf("10");
Boolean b = Boolea.valueOf("false");
```

주요 메소드
* 가장 많이 사용하는 Integer 클래스의 주요 메소드 <br>
: 다른 Wrapper 클래스의 메소드는 이와 유사

* Wrapper 객체로부터 기본 타입 값 알아내기
``` java
Integer i = Integer.valueOf(10);
int ii = i.IntValue(); // ii = 10
Character c = Character.valueOf('c');
char cc = c.charValue(); // cc = 'c'
Boolean b = Boolean.valueOf(true);
boolean bb = b.booleanValue(); // bb = true
```
* 문자열을 기본 데이터 타입으로 변환
``` java
int i =  Integer.parseInt("123") // i = 123
double d = Double.parseDouble("3.142592"); // d = 3.141592
```
* 기본 타입을 문자열로 변환
``` java
String s1 = Integer.toString(123); // 정수 123을 문자열 "123"으로 변환
String s2 = Integer.toHexString(123); // 정수 123을 16진수의 문자열 "7b"로 변환
String s3 = Double.toString(3.14); // 실수 3.14를 문자열 "3.14"로 변환
String s4 = Character.toString('a'); // 문자 'a'를 문자열 "a"로 변환
String s5 = Boolean.toString(true); // 불린 값 true를 문자열 "true"로 변환
```

박싱과 언박싱
* 박싱(boxing): 기본 타입의 값을 Wrapper 객체로 변환하는 것
* 언박싱(unboxing): Wrapper 객체에 들어 있는 기본 타입의 값을 빼내는 것. 박싱의 반대
* 자동 박싱과 자동 언박싱: JDK 1.5부터 박싱과 언박싱은 자동으로 이루어지도록 컴파일 됨
``` java
Integer ten = 10; // 자동 박싱. Integer ten = Integer.valueOf(10);로 자동 처리
Int n = ten; // 자동 언박싱. int n = ten.intValue();로 자동 처리
```

String의 생성과 특징
* String 클래스는 문자열을 나타냄
* 스트링 리터럴(문자열 리터럴)은 String 객체로 처리됨
* 스트링 객체의 생성 사례
``` java
String str1 = "abcd"; // 스트링 리터럴로 스트링 객체 생성

char data[] = {'a', 'b', 'c', 'd'};
String str2 = new String(data);
String str3 = new String("abcd"); // str2와 str3은 모두 "abcd" 문자열
```

스트링 리터럴과 new String()
* 스트링 리터럴
  - 자바 가상 기계 내부에서 리터럴 테이블에 저장되고 관리됨
  - 응용프로그램에서 공유됨
  - 스트링 리터럴 사례: String s = "Hello";
* new String()으로 생성된 스트링
  - 스트링 객체는 힙에 생성
  - 스트링은 공유되지 않음

스트링 객체의 주요 특징
* 스트링 객체는 수정 불가능
  - 리터럴 스트링이든 new String()을 생성했든 객체의 문자열 수정 불가능 <

String 활용
* 스트링 비교, equals()와 compareTo() <br>
-> 스트링 비교에 == 연산자 절대 사용 금지
  - equals(): 스트링이 같으면 true, 아니면 false 리턴
``` java
String java="Java";
if(java.equals("Java")) //true
```

* int compareTo(String anotherString)
  - 문자열이 같으면 0 리턴
  - 이 문자일여 anotherString 보다 먼저 나오면 음수 리턴
  - 이 문자열이 anotherString 보다 나중에 나오면 양수 리턴
``` java
String java = "Java";
String cpp = "C++";
int res = java.compareTo(cpp);
if(res == 0) System.out.println("the same");
else if(res < 0) System.out.println(java + "<" + cpp);
else System.out.println(java + ">" + cpp);
결과: Java > C++
```

String 활용
* 공백 제거, String trim()
* 키보드나 파일로부터 스트링을 입력 시, 스트링 앞 뒤 공백이 끼는 경우가 많다
trim()은 스트링 앞 뒤에 있는 공백 문자를 제거한 스트링을 리턴
``` java
String a = "  xyz\t";
String b = a.trim(); // b = "xyz". 스페이스와 '\t'는 제거됨
```

---
## 5월 8일(10주차)
### 상속
추상 클래스
* 추상 메소드(abstract method): abstract로 선언된 메소드, 메소드의 코드는 없고 원형만 선언
``` java
abstract public String getNane(); //추상 메소드
abstract public String fail() { retrun "Good Bye";} // 추상 메소드 아님. 컴파일 오류
```

추상 클래스(abstract class)
* 추상 메소드를 가지며, abstract로 선언된 클래스
* 추상 메소드 없이, abstract로 선언한 클래스
``` java
// 추상 메소드를 가진 추상 클래스
abstract class shape {
  public Shape() {...}
  public void edit() {...}

  abstract public void draw(); //추상 메소드
}

// 추상 메소드 없는 추상 클래스
abstract class JComponent{
  String name;
  public void load(String name){
    this.name = name;
  }
}
```

추상 클래스의 인스턴스 생성 불가
* 추상 클래스는 온전한 클래스가 아니기 때문에 인스턴스를 생성할 수 없음
``` java
JComponent p; // 오류 없음. 추상 클래스의 레퍼런스 선언
p = new JComponent(); // 컴파일 오류. 추상 클래스의 인스턴스 생성 불가
Shape obj = new Shape(); //컴파일 오류. 추상 클래스의 인스턴스 생성 불가
```

추상 클래스의 상속과 구현
* 추상 클래스 상속
  - 추상 클래스를 상속받으면 추상 클래스가 됨
  - 서브 클래스도 abstract로 선언 해야 함
``` java
abstract class A { // 추상 클래스
  abstract public int add(int x, int y); //추상 메소드
}
abstract class B extends A {  // 추상 클래스
  public void show() {System.out.println("B");}
}

A a = new A(); // 컴파일 오류. 추상 클래스의 인스턴스 생성 불가
B b = new B(); // 컴파일 오류. 추상 클래스의 인스턴스 생성 불가
```

* 추상 클래스 구현
  - 서브 클래스에서 슈퍼 클래스의 추상 메소드 구현(오버라이딩)
  - 추상 클래스를 구현한 서브 클래스는 추상 클래스 아님
``` java
class C extends A { // 추상 클래스 구현. C는 정상 클래스
  public int add (int x, int y) {return x+y; } //추상 메소드 구현. 오버라이딩
  public void show() {System.out.println("C"); }
}

C c = new C(); // 정상
```

추상 클래스의 목적
* 추상 클래스의 목적
  - 상속을 위한 슈퍼 클래스로 활용하는 것
  - 서브 클래스에서 추상 메소드 구현
  - 다형성 실현

추상 클래스의 구현
``` java
abstract class Calculator {
    public abstract int add(int a, int b); // 두 정수위 합을 구하여 리턴
    public abstract int substract(int a, int b); // 두 정수의 차를 구하여 리턴
    public abstract double average(int[] a); // 정수 배열의 평균 리턴
}
```
``` java
public class ex5_5 extends Calculator {
    @Override
    public int add(int a, int b) { // 추상 메소드 구현
        return a + b;
    }
    @Override
    public int substract(int a, int b){ // 추상 메소드 구현
        return a - b;
    }
    @Override
    public double average(int[] a) { // 추상 메소드 구현
        double sum = 0;
        for(int i=0; i<a.length; i++)
            sum += a[i];
        return sum/a.length;
    }
    public static void main(String [] args) {
        ex5_5 c = new ex5_5();
        System.out.println(c.add(2,3));
        System.out.println(c.substract(2,3));
        System.out.println(c.average(new int [] {2,3,4}));
    }
}
결과: 5
-1 
3.0
```

자바의 인터페이스
* 소프트웨어를 규격화된 모듈로 만들고, 인터페이스 맞는 모듈을 조립하듯이 응용프로그램을 작성 하기 위해서 사용

* 자바의 인터페이스
  - 클래스가 구현해야 할 메소드들이 선언되는 추상형
  - 인터페이스 선언: Interface 키워드로 선언.

``` java
interface PhoneInterface { // 인터페이스 선언
  public static final int TIMEOUT = 10000; // 상수 필드. public static final 생략 가능
  public abstract void sendCall(); // 추상 메소드. public abstract 생략 가능
  public abstract void receiveCall(); // 추상 메소드. public abstract 생략 가능
  public default void printLogo() { // 디폴트 메소드는 public 생략 가능
    System.out.println("** Phone **");
  } //디폴트 메소드
}
```

인터페이스 구성 요소들의 특징
* 상수: public만 허용, public static final 생략
* 추상 메소드: public abstract 생략 가능
* default 메소드:
  - 인터페이스에 코드가 작성된 메소드
  - 인터페이스를 구현하는 클래스에 자동 상속
  - public 접근 지정만 허용. 생략 가능
* private 메소드:
  - 인터페이스 내에 메소드 코드가 작성되어야 함
  - 인터페이스 내에 있는 다른 메소드에 의해서만 호출 가능
* static 메소드: public, private 모두 지정 가능. 생략하면 public

자바 인터페이스 특징
* 인터페이스의 객체 생성 불가
``` java
new PhoneInterface(); // 오류. 인터페이스 PhoneInterface 객체 생성 불가
```
* 인터페이스 타입의 레퍼런스 변수 선언 가능
``` java
PhoneInterface galaxy; //galaxy는 인터페이스에 대한 레퍼런스 변수
```

인터페이스 상속
* 인터페이스 간에 상속 가능:
  - 인터페이스를 상속하여 확장된 인터페이스 작성 가능
  - extends 키워드로 상속 선언
* 예)
``` java
interface MobilePhoneInterface extends PhoneInterface {
  void sendSMS(); // 추상 메소드 추가
  void receiveSMS(); // 추상 메소드 추가
}
```
* 인터페이스 다중 상속 허용( * 일반 상속에서는 허용되지 않음)
* 예)
``` java
interface MusicPhoneInterface extends PhoneInterface, MP3Interface
(
  ......
)
```

인터페이스 구현
* 인터페이스의 추상 메소드를 모두 구현한 클래스 작성
  - implements 키워드 사용
  - 여러 개의 인터페이스 동시 구현 가능
* 인터페이스 구현 사례
  - PhoneInterface 인터페이스를 구현한 SamsungPhone 클래스
``` java
class SamsungPhone inplemets PhoneInterface { // 인터페이스 구현
  // PhoneInterface의 모든 메소드 구현
  public void sendCall() {System.out.println("띠리리리링");}
  public void receiveCall() {System.out.println("전화가 왔습니다.");}

  // 메소드 추가 작성
  public void flash() {System.out.println("전화기에 불이 켜젔습니다.");}
}
```
* SamsungPhone 클래스는 PhoneInterface의 default 메소드 상속

### 모듈과 패키지 개념, 자바 패키지 활용
패키지 개념과 필요성
* 3명이 분담하여 자바 응용프로그램을 개발하는 경우, 동일한 이름의 클래스가 존재할 가능성 있음 <br> 
-> 합칠 때 오류 발생 가능성 <br> 
-> 개발자가 서로 다른 디랙터리로 코드 관리하여 해결

자바의 패키지와 모듈이란?
* 패키지(package)
  - 서로 관련된 클래스와 인터페이스를 컴파일한 클래스 파일들을 묶어 놓은 디렉터리
  - 하나의 응용프로그램은 한 개 이상의 패키지로 작성
  - 패키지는 jar 파일로 압축할 수 있음

* 모듈(module)
  - 여러 패키지와 이미지 등의 자원을 모아 놓은 컨테이너
  - 하나의 모듈을 하나의 .jmod 파일에 저장

* Java 9부터 모듈화 도입
  - 플랫폼의 모듈화: Java 9부터 자바 API의 모든 클래스들(자바 실행 환경)을 패키지 기반에서 모듈들로 완전히 재구성
  - 응용프로그램의 모듈화: 클래스들은 패키지로 만들고, 다시 패키지를 모듈로 만듦. 모듈 프로그래밍은 복잡

자바 모듈화의 목적
* 모듈화의 목적
  - Java 9부터 자바 API를 여러 모듈로 분할: Java 8까지는 rt.jar의 한 파일에 모든 API 저장 # 현재 70개로 정리됨
  - 응용프로그램이 실행할 때 꼭 필요한 모듈들로만 실행 환경 구축: 메모리 자원이 열악한 작은 소형 기기에 꼭 필요한 모듈로 구성된 작은 크기의 실행 이미지를 만들기 위함

* 모듈의 현실
* Java 9부터 전면적으로 도입
* 복잡한 개념
* 큰 자바 응용프로그램에는 개발, 유지보수 등에 적합
* 현실적으로 모듈로 나누어 자바 프로그램을 작성할 필요 없음
* 모듈화 작업은 매우 중요한 개념이며, 소규모 프로젝트부터 적용해야 대형 프로젝트 쉽게 도입, 활용 가능

자바 API의 모듈 파일들
* 자바 JDK에 제공되는 모듈 파일들
  - 자바가 설치된 jmods 디렉터리에 모듈 파일 존재: .jmod 확장자를 가진 파일. 모듈은 수 십개. 모듈 파일은 ZIP 포맷으로 압축된 파일 -> 포맷이 zip이며 확장자는 .jmod
* 모듈 파일에는 자바 API의 패키지와 클래스들이 들어 있음

java.base.jmod 파일을 풀어 놓은 사례
* java.base.jmod 파일을 풀면, 모듈에 있는 패키지와 클래스를 볼 수 있다

패키지 사용하기, import문
* 다른 패키지에 작성된 클래스 사용
  - import를 이용하지 않는 겅우 -> 소스에 클래스 이름의 완전 경로명 사옹
``` java
public class ImportExample{
  public static void main(String[] args){
    java.util.Scanner scanner = 
      new java.util.Scanner(System.in);
  }
}
```

* 필요한 클래스만 import
  - 소스 시작 부분에 클래스의 경로명 import
  - import 패키지.클래스
  - 소스에는 클래스 명만 명시하면 됨
``` java
import java.util.Scanner;
public class ImportExample{
  public static void main(String [] args){
    Scanner scanner = new Scanner(System.in);
    System.out,println(scanner.next());
  }
}
```

* 패키지 전체를 import
  - 소스 시작 부분에 패키지의 경로명.* import
  - import 패키지.*
  - import java.util.*; -> java.util 패키지 내의 모든 클래스만을 지정, 하위 패키지의 클래스는 포함하지 않음
``` java
import java.util.*;
public class ImportExample{
  public static void main(String[] args){
    Scanner scanner = new Scanner(System.in);
    System.out.println(scanner.next());
  }
}
```


패키지 만들기
* 클래스 파일(.class)이 저장되는 위치는?
  - 클래스나 인터페이스가 컴파일 되면 클래스 파일(.class) 생성
  - 클래스 파일은 패키지로 선언된 디렉터리에 저장
* 패키지 선언
  - 소스 파일의 맨 앞에 컴파일 후 저장될 패키지 지정 => package 패키지명;
``` java
package UI; // 아래 Tools를 컴파일하여 UI 패키지(UI 디렉터리)에 저장할 것 지시
public class Tools{
  ......
}
```
``` java
package Graphic; // 아래 Line 클래스를 Graphic 패키지에 저장
import UI.Tools;
public class Line extends Shape{
  public void draw() {
    Tools t = new Tools();
  }
}
```

디폴트 패키지
* package 선언문이 없는 자바 소스 파일의 경우
  - 컴파일러는 클래스나 인터페이스를 디폴트 패키지에 소속시킴
  - 디폴트 패키지 -> 현재 디렉터리

VS Code에서 Java Package 생성하기 1
* Eclipse 보다도 간단히 만들 수 있음
* 일반적으로 package는 com.foo.test와 같이 도메인의 역순으로 만드는 것이 일반적

1. 먼저 다음과 같은 디렉터리 구조 생성. 한 번에 com/foo/test로 입력해도 좋음

2. 클래스 파일에 package com.foo.test

VS Code에서 Java Package 생성하기 2
* Explorer 아래쪽의 "JAVA PROECTS"를 클릭하면 package의 계층 구조를 볼 수 있음
* 사용자 정의 package를 만든 후 사용하려면 import 키워드 사용 <br>
// 파일: src/com/example/utils/HelloUtill.java <br>
// 파일: src/com/example/Main.java
* 어떤 클래스 파일에서 package선언을 생략하면 default package에 속함
* 같은 기본 패키지에 있는 다른 클래스에서는 import 없이 사용 가능 -> 5장까지 했던 방식
* default package에 속해 있으면 다른 package를 사용할 수 없음
* 실제 프로젝트에서는 거의 모든 클래스가 명시적으로 package를 선언

package의 운영 방법
* 패키지 이름은 도메인 기반으로 시작(일반 관례)형식: com.회사이름.프로젝트명.기능명 -> 충돌 방지(전 세계 어디서든 유일한 패키지명 확보 가능) / 모듈별 분리 가능
* 기능/역할별로 하위 패키지를 구분: utils, controllerm service 등
* 디렉토리 구조와 package 선언을 정확히 일치해야 함
* import는 필요한 만큼만 * 전체 import는 피하는 것이 좋음

---
## 4월 18일(9주차)
### 클래스와 객체
static 메소드의 제약 조건 2
* static 메소드에서는 this 사용 불가
* static 메소드는 객체 없이도 사용 가능하므로, this 레퍼런스 사용할 수 없음

final 클래스와 메소드
* final 클래스 - 더 이상 클래스 상속 불가능
``` java
final class FinalClass{
  ....
}
class SubClass extends FinalClass{ // 컴파일 오류 발생
  .....
}
```
* final 메소드 - 더 이상 오버라이딩 불가능
```java
public class SuperClass{
  protected final int finalMethod(){...}
}
class SubClass extends Superclass{ // SubClass가 SuperClass를 상속받음
  protected in finalMethod(){...} // 컴파일 오류. finalMethod() 오버라이딩 할 수 없음
}
```

final 필드
* final 필드: 상수를 선언할 때 사용
* 상수 필드는 선언 시에 초기 값을 지정하여야 한다
* 상수 필드는 실행중에 값을 변경할 수 없다

### 상속(inheritance)
상속(inheritance)의 필요성
* 클래스 사이의 멤버 중복 선언 불필요 - 클래스의 간결화
* 클래스들의 계층적 분류로 클래스 관리 용이
* 클래스 재사용과 확장을 통한 소프트웨어의 생산성 향상

클래스 상속과 객체
* 상속 선언: extends 키워드 사용
* 부모 클래스를 돌려받아 자식 클래스를 확장한다는 의미
* 부모 클래스 -> 슈퍼 클래스(super class)
* 자식 클래스 -> 서브 클래스(sub class)
``` java
class Point{
  int x, y;
}
class ColorPoint extends Point{ //Point를 상속받는 ColorPoint 클래스 선언

}
```
* ColorPoint는 Point를 물려 받으므로, Point에 선언된 필드나 메소드를 재 선언할 필요가 없음

클래스 상속 - Point와 ColorPoint 클래스
* (x,y)의 한 점을 표현하는 Point 클래스와 이를 상속받아 점에 색을 추가한 ColorPoint 클래스
``` java
class Point {
    private int x, y; // 한 점을 구성하는 x, y 좌표
    public void set(int x, int y){
        this.x = x; this.y = y;
    }
    public void showPoint(){ // 점의 좌표 출력
        System.out.println("(" + x + "," + y + ")");
    }
}

class ColorPoint extends Point{ //Point를 상속받은 ColorPoint 선언
    private String color; // 점의 색
    public void setColor(String color){
        this.color = color;
    }
    public void showColorPoint(){ // 컬러 점의 좌표 출력
        System.out.print(color);
        showPoint(); // Point 클래스의 set() 호출
    }
}

public class ex5_1{
    public static void main(String[] args) {
        Point p = new Point(); // Point 객체  생성
        p.set(1,2); // Point 클래스의 set() 호출
        p.showPoint();

        ColorPoint cp = new ColorPoint(); // ColorPoint 객체 생성
        cp.set(3,4); // Point 클래스의 set() 호출
        cp.setColor("red"); // ColorPoint 클래스의 setColor() 호출
        cp.showColorPoint(); // 컬러와 좌표 출력
    }
}
결과: (1,2)
red(3,4)
```

서브 클래스 객체의 모양
* 슈퍼 클래스 객체와 서브 클래스의 객체는 별개
* 서브 클래스 객체는 슈퍼 클래스 멤버 포함

자바 상속의 특징
* 클래스 다중 상속(multiple inheritance) 불허
  > 하나의 클래스가 둘 이상의 부모 클래스를 동시에 상속받는 것을 말한다
  - C++는 다중 상속 가능
  - C++는 다중 상속으로 멤버가 중복 생성되는 문제 있음(다이아몬드 상속)
    > 부모 클래스 간에 계층적 관계가 있을 경우, 중복된 멤버가 생성될 수 있음
    > 모호성(Ambiguity)문제: 두 부모 클래스에 동일한 이름의 멤버(변수나 함수)가 존재할 경우, 어떤 부모의 멤버를 호출해야 할 지 모호해짐
* 자바는 인터페이스(interface)의 다중 상속 허용
  > 다중 상속과 유사한 기능을 제공
* 모든 자바 클래스는 묵시적으로 Object클래스 상속받음
  - java.lang.Object는 클래스는 모든 클래스의 슈퍼 클래스

슈퍼 클래스의 멤버에 대한 서브 클래스의 접근
* 슈퍼 클래스의 private 멤버: 서브 클래스에서 접근 할 수 없음
* 슈퍼 클래스의 디폴트 멤버: 서브 클래스가 동일한 패키지에 있을 때, 접근 가능
* 슈퍼 클래스의 public 멤버: 서브 클래스는 항상 접근 가능
* 슈퍼 클래스의 protected 멤버:
  - 같은 패키지 내의 모든 클래스 접근 허용
  - 패키지 여부와 상관없이 서브 클래스는 접근 가능

protected 멤버
* 슈퍼 클래스의 protected 멤버에 대한 접근: 같은 패키지의 모든 클래스에게 허용
* 상속되는 서브 클래스가 같은 패키지든 다른 패키지든 상관 없이 허용

서브 클래스/슈퍼 클래스의 생성자 호출과 실행
* 서브 클래스의 객체가 생성될 때: 슈퍼클래스 생성자와 서브 클래스 생성자 모두 실행
* 호출 순서: 서브 클래스의 생성자 먼저 호출 -> 슈퍼 클래스 생성자 호출
* 실행 순서: 슈퍼 클래스의 생성자가 먼저 실행 -> 서브 클래스의 생성자 실행

서브 클래스에서 슈퍼 클래스 생성자 선택
* 슈퍼 클래스와 서브 클래스: 각각 여러 개의 생성자 작성 가능
* 서브 클래스의 객체가 생성될 때: 슈퍼 클래스 생성자 1개와 서브 클래스 생성자 1개가 실행
* 서브 클래스의 생성자와 슈퍼 클래스의 생성자가 결정되는 방식
1. 개발자의 병시적 선택
  - 서브 클래스 개발자가 슈퍼 클래스의 생성자 명시적 선택
  - super() 키워드를 이용하여 선택
2. 컴파일러가 기본 생성자 선택
  - 서브 클래스 개발자가 슈퍼 클래스의 생성자를 선택하지 않는 경우
  - 컴파일러가 자동으로 슈퍼 클래스의 개본 생성자 선택

컴파일러에 의해 슈퍼 클래스의 기본 생성자가 묵시적 선택
* 개발자가 서브 클래스의 생성자에 대해 슈퍼 클래스의 생성자를 명시적으로 선택하지 않은 경우

서브 클래스의 매개 변수를 가진 생성자에 대해서도 슈퍼 클래스의 기본 생성자가 자동 선택
* 개발자가 서브 클래스의 생성자에 대해 슈퍼 클래스의 생성자를 명시적으로 선택하지 않은 경우

super()로 슈퍼 클래스의 생성자 명시적 선택
* super(): 서브 클래스에서 명시적으로 슈퍼 클래스의 생성자 선택 호출
* 사용방식
  - super(parameter);
  - 인자를 이용하여 슈퍼 클래스의 적당한 생성자 호출
  - 반드시 서브 클래스 생성자 코드의 제일 첫 라인에 와야 함

super()를 활용한 ColorPoint 작성
``` java
class Point{
    private int x, y; //한 점을 구성하는 x, y 좌표
    public Point(){
        this.x = this.y = 0;
    }
    public Point(int x, int y){
        this.x = x; this.y = y;
    }
    public void showPoint() {// 점의 좌표 출력
        System.out.println("(" + x + "," + y + ")");
    }
}

class ColorPoint extends Point{ // Point를 상속받은 ColorPoint 선언
    private String color; // 점의 색
    public ColorPoint(int x, int y, String color){
        super(x, y); // Point의 생성자 Point(x, y) 호출
        this.color = color;
    }
    public void showColorPoint() { // 컬러 점의 좌표 출력
        System.out.print(color);
        showPoint(); // Point 클래스의 showPoint() 호출
    }
}

public class ex5_2 {
    public static void main(String[] args) {
        ColorPoint cp = new ColorPoint(5, 6, "blue");
        cp.showColorPoint();
    }
}
결과: blue(5,6)
```

업캐스팅(upcasting) 개념
* 하위 클래스의 레퍼런스는 상위 클래스를 가리킬 수 없지만, 상위 클래스의 레퍼런스는 하위 클래스를 가리킬수 있다
* 생물이 들어가는 밖스에 사람이나 코끼리를 넣어도 무방
* 사람이나 코끼리 모두 생물을 상속받았기 때문
* 업캐스팅(upcasting)이란?
  - 서브 클래스의 레퍼런스를 슈퍼 클래스 레퍼런스에 대입
  - 슈퍼 클래스 레퍼런스로 서브 클래스 객체를 가리키게 되는 현상

업캐스팅 사례
``` java
class Person{
  String name;
  String id

  public Person(String name){
    this.name = name;
  }
}
class Student extends Person{
  String grade;
  String department;

  public Student(String name){
    super(name);
  }
}
public claass UpcastingEx{
  public static void main(String[] args){
    Person p;
    Student s = new Student("이재문");
    p = s; //업캐스팅

    system.out.println(p.name); // 오류 없음

    p.grade = "A"; // 컴파일 오류
    p.department = "Com"; // 컴파일 오류
  }
}
```
그렇다면 왜 p = s 로 업캐스팅을 한 걸까?
* 이 사례는 업캐스팅의 제한 사항을 설명하기 위한 코드
* 실제로는 이런 식으로 업새크싱을 사용하지 않음
* 실제로는 여러 자식 클래스를 하나의 부모 타입으로 다루기 위해 사용
``` java
Person[] people = new Person[3];
people[0] = new Student("홍길동");
people[1] = new Student("김영희");
people[2] = new Person("이순신");
```
* 이렇게 하면 공통된 타입(Person) 으로 여러 자식 클래스를 한 배열에 담을 수 있음
* 대신 접근은 Person 수준에서만 가능

다운캐스팅(downcasting)
* 슈퍼 클래스 레퍼런스를 서브 클래스 레퍼런스에 대입
* 업캐스팅 된 것을 다시 원래대로 되돌리는 것
* 반드시 명시적 타입 변환 지점
* 다운 캐스팅 사례
``` java
public class DowncastingEX{
  public static void main(String[] args){
    Person p = new Student("이재문"); //업캐스팅 발생
    Student s;

    s = (Student)p; // 다운캐스팅

    System.out.println(s.name); //오류 없음
    s.grade = "A"; // 오류 없음
  }
}
```

업캐스팅 레퍼런스로 객체 구별?
* 업캐스팅된 레퍼런스로는 객체의 실제 타입을 구분하기 어려움
* 슈퍼 클래스는 여러 서브 클래스에 상속되기 때문
* 예를 들어 아래의 클래스 계층 구조에서 p가 가리키는 객체가 Person 객체인지, Student 객체인지, Professor 객체인지 구분하기 어려움
``` java
Person p = new Person();
Person p = new Student(); // 업캐스팅
Person p = new Professor(); // 업캐스팅
```

instanceof 연산자 사용
* 레퍼런스가 가리키는 객체의 타입 식별: 연산의 결과는 true/false의 불린 값으로 변환
* instanceof 연산자 사용 사례
``` java
Person p = new Professor();

if(p instanceof Person) //true
if(p instanceof Student) //false, Student를 상속받지 않기 때문
if(p instanceof Researcher) //true
if(p instanceof Professor) //true

if("java" instanceof String) //true

if(3 instanceof int) // 문법 오류, instanceof는 객ㅊ에 대한 레퍼런스만 사용
```

메소드 오버라이딩(Method Overriding)의 개념
* 서브 클래스에서 슈퍼 클래스의 메소드 중복 작성
* 슈퍼 클래스의 메소드 무력화, 항상 서브 클래스에 오버라이딩한 메소드가 실행되도록 보장됨
* "메소드 무시하기"로 번역되기도 함
* 오버라이딩 조건
  > 슈퍼 클래스 메소드의 원형(메소드 이룸, 인자 타입 및 개수, 리턴타입) 동일하게 작성

서브 클래스 객체와 오버라이딩 된 메소드 호출
* 오버라이딩 한 메소드가 실행됨을 보장
``` java
class A{
  void f() {
    System.out.println("A의 f() 호출");
  }
}
class B extends A{
  void f() { //A의 f()를 오버라이딩
    System.out.println("B의 f() 호출");
  }
}
```

오버라이딩의 목적, 다형성 실현
* 오버라이딩으로 다형성 실현
* 하나의 일터페이스(같은 이름)에 서로 다른 구현
* 슈퍼 클래스의 메소드를 서브 클래스에서 각각 목적에 맞게 다르게 구현
* 사례 Shape의 draw() 메소드를 Line, Rect, Circle에서 오버라이딩하여 다르게 구현

메소드 오버라이딩으로 다형성 실현
* Shape의 draw() 메소드를 Line, Circle, Rect 클래스에서 목적에 맞게 오버라이딩 하는 다형성의 사례
``` java
class Shape { // 도형의 슈퍼 클래스
    public void draw(){
        System.out.println("shape");
    }
}
class Line extends Shape {
    public void draw(){ // 메소드 오버라이딩
        System.out.println("Line");
    }
}
class Rect extends Shape {
    public void draw(){ // 메소드 오버라이딩
        System.out.println("Rect");
    }
}
class Circle extends Shape {
    public void draw(){ // 메소드 오버라이딩
        System.out.println("Circle");
    }
}

public class ex5_4 {
    static void paint(Shape p) { // Shape을 상속받은 모든 객체들이 매개 변수로 넘어올 수 있음
        p.draw(); // p가 가리키는 객체에 오버라이딩한 draw() 호출. 동적 바인딩
    }
    public static void main(String[] args) {
        Line line = new Line();
        paint(line); // Line의 draw() 실행. "Line" 출력

        //다음 호출들은 모두 paint() 메소드 내엣 Shape에 대한 레퍼런스 pfh 업캐스팅됨
        paint(new Shape()); // shape의 draw() 실행. "Shape" 출력
        paint(new Line()); // 오버라이딩된 메소드 Line의 draw() 실행. "Line" 출력
        paint(new Rect()); // 오버라이딩된 메소드 Rect의 draw() 실행. "Rect" 출력
        paint(new Circle());// 오버라이딩된 메소드 Circle의 draw() 실행. "Circle" 출력
    }
}
결과: Line
Shape
Line
Rect
Circle
```

super 키워드로 슈퍼 클래스의 멤버 접근
* 슈퍼 클래스의 멤버를 접근할 때 사용되는 레퍼런스 super.슈퍼클래스의 멤버
* 서브 클래스에서만 사용
* 슈퍼 클래스의 필드 접근
* 슈퍼 클래스의 메소드 호출 시 super로 이루어지는 메소드 호출: 정적 바인딩

오버로딩과 오버라이딩
* 교재 217p의 <표5-2> 참조

---
## 4월 17일(7주차)
### 클래스와 객체
생성자의 종류
* 기본 생성자(default constructor): 매개 변수 없고, 아무 작업 없이 단순 리턴하는 생성자
``` java
clas Circle {
    public Circle() {} // 기본 생성자, 매개 변수 없고, 아무 일 없이 단순 리턴
}
```
* 기본 생성자가 자동 생성되는 경우
  - 클래스에 생성자가 하나도 선언되어 있지 않을 때
  - 컴파일러에 의해 기본 생성자 자동 생성
* 기본 생성자가 자동 생성되지 않는 경우
  - 클래스에 생성자가 선언되어 있는 경우
  - 컴파일러는 기본 생성자를 자동 생성해 주지 않는다

this 레퍼런스
* 객체 자신에 대한 레퍼런스
* 컴파일러에 의해 자동 관리, 개발자는 사용하기만 하면 됨
* this.멤버 형태로 멤버를 접근할 때 사용

this()로 다른 생성자 호출
* 같은 클래스의 다른 생성자 호출
* 생성자 내에서만 사용 가능
* 생성자 코드의 제일 앞에 있어야 함
* this() 사용 실패 사례
``` java
public Book() {
    System.out.println("생성자 호출됨");
    this("",""); //컴파일 오류. 이 문장이 생성자의 첫 번째 문장이 아니기 때문
}
```

객체 배열
* 객체에 대한 레퍼런스 배열
* 자바의 객체 배열 만들기 3단계
  1. 배열 레퍼런스 변수 선언
  2. 레퍼런스 배열 생성
  3. 배열의 각 원소 객체 생성

``` java
Circle [] c; //Circle 배열에 대한 레퍼런스 변수 c 선언
c = new Circle[5]; // 레퍼런스 배열 생성

for(int i=0; i <c.length; i++) // c.length는 배열 c의 크기로서 5
  c[i] = new Circle(i); //각 원소 객체 생성

for(int i=0; i<c.length; i++) // 모든 객체의 면적 출력
  System.out.print((int)(c[i].getArea()) + " "); // 배열의 원소 객체 사용
```

Circle 배열 만들기
* 반지름이 0~4인 Circle 객체 5개를 가지느 배열을 생성, 배열에 있는 모든 Circle 객체의 면적을 출력
``` java
class Circle{
    int radius;
    public Circle(int radius){
        this.radius = radius;
    }
    public double getArea(){
        return 3.14 * radius * radius;
    }
}

public class ex4_6 {
    public static void main(String[] args) {
        Circle [] c; // Circle 배열에 대한 레퍼런스 c 선언
        c = new Circle[5]; // 5개의 레퍼런스 배열 생성

        for(int i=0; i<c.length; i++) //배열의 개수 만큼
            c[i] = new Circle(i); // i 번째 원소 객체 생성
        
        for(int i=0; i<c.length; i++) // 배열의 모든 Circle 객체의 면적 출력
            System.out.print((int)(c[i].getArea()) + " ");
    }    
}
결과: 0 3 12 28 50 
```

객체 배열 만들기 연습
* 예제 4-4를 활용하여 2개짜리 book(ex4_4) 객체 배열을 만들고, 사용자로부터 책의 제목과 저자를 입력받아 배열을 완성하라
``` java
import java.util.Scanner;

class ex4_4{
    String title, author;
    public ex4_4(String title, String author){ // 생성자
        this.title = title;
        this.author = author;
    }
}

public class ex4_7 {
    public static void main(String[] args) {
        ex4_4 [] ex4_4 = new ex4_4[2];

        Scanner scanner = new Scanner(System.in);
        for(int i=0; i<ex4_4.length; i++){ // ex4_4.length = 2
            System.out.print("제목>>");
            String title = scanner.nextLine();
            System.out.print("저자>>");
            String author = scanner.nextLine();
            ex4_4[i] = new ex4_4(title, author); //배열 원소 객체 생성
        }

        for(int i=0; i<ex4_4.length; i++)
            System.out.print("(" + ex4_4[i].title + ", " + ex4_4[i].author + ")");

        scanner.close();

    }
}
결과: 제목>>사랑의 기술
저자>>에리히 프롬
제목>>시간의 역사
저자>>스티븐 호킹
(사랑의 기술, 에리히 프롬)(시간의 역사, 스티븐 호킹)
```

메소드 
* 메소드는 C/C++의 함수와 동일
* 자바의 모든 메소드는 반드시 클래스 안에 있어야 함(캡슐화 원칙)
* 메소드 형식
``` java
public int getSum(int i, int j){
  int sum;
  sum = i + j;
  return sum;
}

에서 
public = 접근 지정자
int = 리턴 타입
getSum = 메소드 이름
(int i, int j) = 메소드 인자들
int sum;
  sum = i + j; = 메소드 코드
  return sum;

```
* 접근 지정자: 다른 클래스에서 메소드를 접근할 수 있는지 여부 선언
  - public, private, protected, 디폴트(접근 지정자 생략)
* 리턴 타입: 메소드가 리턴하는 값의 데이터 타입

인자 전달 - 기본 타입의 값이 전달되는 경우
* 매개 변수가 byte, int, double 등 기본 타입으로 선언되었을 때
  - 호출자가 건네는 값이 매개 변수에 복사되어 전달, 실 인자 값은 변경되지 않음

인자 전달 - 객체가 전달되는 경우
* 객체의 레퍼런스만 전달: 매개 변수가 실 인자 객체 공유

인지 전달 - 배열이 전달되는 경우
* 배열 레퍼런스만 매개 변수에 전달: 배열 통채로 전달되지 않음
* 객체가 전달되는 경우와 동일: 매개 변수가 실 인자의 배열 공유

인자로 배열이 전달되는 예
* char[] 배열을 전달받아 배열 속의 공백(' ')문자를 ','로 대치하는 메소드를 작성
``` java
public class ex4_8 {
    static void replaceSpace(char a[]){ //배열 a의 공백문자를 ','로 변경
        for(int i=0; i<a.length; i++)
            if(a[i] == ' ') // 공백 문자를 ','로 변경
                a[i] = ',';
    }

    static void printCharArray(char a[]){ //배열 a의 문자들을 화면에 출력
        for(int i=0; i<a.length; i++)
            System.out.print(a[i]); //배열 원소 문자 출력
        System.out.println(); // 배열 워소 모두 출력 후 바꿈
    }

    public static void main(String[] args) {
        char c[] = {'T','h','i','s',' ','i','s',' ','a',' ','p','e','n','c','i','l','.'};
        printCharArray(c); // 원래 배열 원소 출력
        replaceSpace(c); // 공백 문자 바꾸기
        printCharArray(c); // 수정된 배열 원소 출력
    }

}
결과:This is a pencil.
This,is,a,pencil.
```

메소드 오버로딩(Overloading)
* 한 클래스 내에서 두 개 이상의 이름이 같은 메소드 작성
  - 메소드 이름이 동일해야 함
  - 매개 변수의 개수 혹은 타입이 달라야 함
  - 리턴 타입은 오버로딩과 관련 없음

객체 치환 시 주의할 점
* 객체 치환은 객체 복사가 아니며, 레퍼런스의 복사이다

객체 소멸
* new로 할당 받은 객체와 메모리를 JVM으로 되돌려 주는 행위
* 자바는 객체 소멸 연산자 없음
* 객체 소멸은 JVM의 고유한 역할
* C/C++에서는 할당 받은 객체를 개발자가 프로그램 내에서 삭제해야 함
* C/C++의 프로그램 작성을 어렵게 만드는 요인
* 자바에서는 사용하지 않는 객체나 배열을 돌려주는 코딩 책임으로부터 개발자 해방

가비지
* 가비지는 레퍼런스가 하나도 없는 객체
* 더이상 접근할 수 없어 사용할 수 없게 된 메모리
* 가비지 컬렉션: JVM의 가비지 컬렉터가 자동으로 가비지 수집, 반환

가비지 컬렉션(garbage collection)
* JVM이 가비지 자동 회수
  - 가용 메모리 공간이 일정 이하로 부족해질 때
  - 가비지를 수거하여 가용 메모리 공간으로 확보
* 가비지 컬렉터(garbage collector)에 의해 자동 수행
* 강제 가비지 컬렉션 강제 수행: System 또는 Runtime 객체의 gc() 메소드 호출
``` java
System.gc(); // 가비지 컬렉션 작동 요청
```
* 이 코드는 JVM에 강력한 가비지 컬렉션 요청
* 그러나 JVM이 가비지 컬렉션 시점을 전적으로 판단

자바의 패키지 개념
* 패키지
* 상호 관련 있는 클래스 파일(컴파일된 .class)을 저장하여 관리하는 디렉터리
* 자바 응용프로그램은 하나 이상의 패키지로 구성

접근 지정자
* 자바의 접근 지정자 4가지: private, protected, public, 디폴트(접근 지정자 생략)
* 접근 지정자의 목적
  - 클래스나 일부 멤버를  공개하여 다른 클래스에서 접근하도록 허용
  - 객체 지향 언어의 캡슐화 정책은 멤버를 보호하는 것
    
    -> 접근 지정은 캡슐화에 묶인 보호를 일부 해제할 목적으로 사용
* 접근 지정자에 따른 클래스나 멤버의 공개 범위
  - private: 외부로부터 완벽 차단
  - 디폴트: 동일 패키지에 허용
  - protected: 동일 패키지와 자식 클래스에 허용
  - public: 모든 클래스에 허용

클래스 접근 지정
* 다른 클래스에서 사용하도록 허용할 지 지정
* public 클래스: 다른 모든 클래스에게 접근 허용
* 디폴트 클래스(접근 지정자 생략): 같은 패키지의 클래스에만 접근 허용
``` java
public class World{ // public 클래스

}
class Local{ // 디폴트 클래스

}
```

멤버 접근 지정
* public 멤버: 패키지에 관계없이 모든 클래스에게 접근 허용
* private 멤버: 동일 클래스 내에만 접근 허용. 상속 받은 서브 클래스에서 접근 불가
* protected 멤버:
  - 같은 패키지 내의 다른 모든 클래스에게 접근 허용
  - 상속받은 서브 클래스는 다른 패키지에 있어도 접근 가능
* 디폴트(default) 멤버: 같은 패키지 내의 다른 클래스에게 접근 허용

static 멤버
* static 멤버 선언
```java
class StaticSample{
    int n;; // non-static 필드
    void g() {...} // non-static 메소드
    static int m; // static 필드
    static void f() {...} // static 메소드
}
```
* 객체 생성과 non-static 멤버의 생성
  - : non-static 멤버는 객체가 생성될 때, 객체마다 생긴다
* 객체마다 n, g()의 non-static 멤버들이 생긴다
* non-static 모든 객체에 멤버 생성, static은 멤버 공유

static 멤버의 생성
* static 멤버는 클래스당 하나만 생성
* 객체들에 의해 공유됨

static 멤버 사용
* 클래스 이름으로 접근 가능
``` java
StaticSample.m = 3; // 클래스 이름으로 static 필드 접근
StaticSample.f();   // 클래스 이름으로 static 메소드 호출
```
* 객체의 멤버로 접근 가능
``` java
StaticSample b1 = new StaticSample();

b1.m = 3; // 객체 이름으로 static 필드 접근
b1.f();   // 객체 이름으로 static 메소드 호출
```
* non-static 멤버는 클래스 이름으로 접근 안 됨
``` java
StaticSample.n=5; // n은 non-static이므로 컴파일 오류
StaticSample.g(); // g()는 non-static이므로 컴파일 오류
```
* non-static은 모든 객체에 멤버 생성, static은 멤버 공유

static의 활용
* 전역 변수와 전역 함수를 만들 때 활용
* 공유 멤버를 만들 떄: static으로 선언한 멤버는 클래스의 객체들 사이에 공유

static 메소드의 제약 조건 1
* static 메소드는 오직 static 멤버만 접근 가능
  - 객체가 생성되지 않은 상황에서도 static 메소드는 실행될 수 있기 때문에, non-static 멤버 활용 불가
  - non-static 메소드는 static 멤버 사용 가능


---
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
1. 레퍼런스 변수 선언 
2. 객체 생성, new 연산자 이용 
3. 객체 멤버 접근, 점(.) 연산자 이용 

``` java
import java.util.Scanner;

class Rectangle {
    int width;
    int height;
    public int getArea() {
        return width*height;
    }
}

public class ex4_2 {
    public static void main(String[] args) {
        Rectangle rect = new Rectangle();
        Scanner scanner = new Scanner(System.in);
        System.out.print(">> ");
        rect.width = scanner.nextInt();
        rect.height = scanner.nextInt();
        System.out.println("사각형의 면적은 " + rect.getArea());
        scanner.close();
    }
}
결과: >> 4 5
사각형의 면적은 20
```

생성자 개념과 목적
* 생성자
  - 객체가 생성될 때 초기화 목적으로 실행되는 메소드
  - 객체가 생성되는 순간에 자동 호출
``` java
public class ex4_3 {
    int radius;
    String name;

    public ex4_3(){ //매개 변수 없는 생성자
        radius = 1; name = ""; // radius의 초기값은 1
    }

    public ex4_3(int r, String n) {
        radius = r; name = n;
    }

    public double getArea() {
        return 3.14*radius*radius;
    }

    public static void main(String[] args) {
        ex4_3 pizza = new ex4_3(10, "자바피자"); // ex4_3 객체 생성, 반지름 10
        double area = pizza.getArea();
        System.out.println(pizza.name + "의 면적은 " + area);

        ex4_3 donut = new ex4_3(); // ex4_3 객체 생성, 반지름 1
        donut.name = "도넛피자";
        area = donut.getArea();
        System.out.println(donut.name + "의 면적은 " + area);
    }
}
결과: 자바피자의 면적은 314.0
도넛피자의 면적은 3.14
```
생성자의 특징
* 생성자 이름은 클래스 이름과 동일
* 생성자는 여러 개 작성 가능(생성자 중복)
* 생성자는 객체 생성시 한 번만 호출
  - 자바에서 객체 생성은 반드시 new 연산자로 함
* 생성자의 목적은 객체 생성 시 초기화
* 생성자는 리턴 타입을 지정할 수 없음

``` java
public class ex4_4 {
    String title;
    String author;
    public ex4_4(String t) { // 생성자
        title = t;
        author = "작자미상";
    }
    public ex4_4(String t, String a) { // 생성자
        title = t;
        author = a;
    }

    public static void main(String[] args) {
        ex4_4 littlePrince = new ex4_4("어린왕자", "생텍쥐페리"); // 생성자 ex4_4(String t, String a) 호출
        ex4_4 loveStory = new ex4_4("춘향전"); // 생성자 ex4_4(String t) 호출
        System.out.println(littlePrince.title + " " + littlePrince.author);
        System.out.println(loveStory.title + " " + loveStory.author);
    }
}
결과: 어린왕자 생텍쥐페리
춘향전 작자미상
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
