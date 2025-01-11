<p>spring을 쓰기 위해서 다시 java공부에 뛰어들기로 했습니다...
<del>겸사겸사 정처기까지 준비되고 좋지..ㅎ</del>
전처럼 엄청난 업로드는 못하겠지만 천천히 굴려보도록 하겠습니다.
제가 과연 Backend를 소화할 수 있을까요?</p>
<p>현재 저의 계획은 딥러닝모델은 FastAPI로, DB와 다른 것들은 Spring으로 처리하고 둘을 연결하려고 합니다. 이때 Docker까지 얹어서 사용해보려고 하는데...
제가 할 수 있기를 기도해봅니다..🙏</p>
<hr />
<h2 id="메소드-정의">메소드 정의</h2>
<h3 id="메소드란">메소드란?</h3>
<p>: 어떤 작업을 수행하기 위한 명령문의 집합 
-&gt; 기능을 미리 만들어서 필요할 때마다 불러 사용한다.
-&gt; 여러 줄의 코드를 하나로 묶어서 표현한 형태이다.
-&gt; 편의성과 유지보수성이 뛰어나다.</p>
<h3 id="메소드-형태">메소드 형태</h3>
<p>접근제한자 리턴타입 메소드이름(매개변수){}</p>
<pre><code class="language-java">// 예시
public static int addNum(int num1, int num2){}</code></pre>
<ul>
<li>접근제한자 : public, private</li>
<li>static : 공유하다 -&gt; 위치에 상관없이 static이라는 키워드를 사용하면 main 메소드와 공유된다.</li>
<li>리턴타입(반환타입) : int, double, void...
void -&gt; 리턴타입이 없음을 의미</li>
<li>매개변수 : 값을 받아오겠다, 값이 자동으로 매개변수에 할당
만약 매개변수가 없는 경우라면 소괄호(매개변수 자리)를 비워도 된다.</li>
</ul>
<h3 id="메소드-생성과-반환">메소드 생성과 반환</h3>
<ul>
<li>메소드는 main 영역을 벗어나 생성한다.</li>
<li>메소드는 main 영역에서 실행시킨다.</li>
<li>메소드는 리턴타입이 void가 아닌 이상 무조건 return에 어떤 값을 갖고 있게 할 지 정해줘야한다.</li>
<li>메소드는 return 키워드를 만나면 데이터를 반환하고 끝내기 때문에 return 키워드 위쪽에만 코드를 작성해야한다.</li>
</ul>
<h2 id="예시">예시</h2>
<ul>
<li><p>계산기 만들기
1) 정수형 num1과 num2를 입력받고, 문자형 op를 선언해 원하는 연산자를 넣는다.
2) num1과 num2를 op에 맞게 연산하여 최종 값을 반환해주는 cal메소드를 만든다.
단, 빼기를 수행할 때는 더 큰 수에서 작은 수를 빼세요!</p>
<pre><code class="language-java">import java.util.Scanner;
public class 계산기{
  public static void main(String[] args){
      // 메소드 실행공간
      Scanner sc = new Scanner(System.in);
      System.out.print(&quot;정수1 입력 : &quot;);
      int num1 = sc.nextInt();
      System.out.print(&quot;정수2 입력 : &quot;);
      int num2 = sc.nextInt();

      char op = '-' // +,-,*,/
      System.out.println(cal(num1, num2, op));
  }

  // 메소드 생성공간
  private static int cal(int num1, int num2, char op){
      int result = 0;
      // op가 어떤 모양인지에 따라 결과가 달라짐
      //switch or if 문 사용
      switch(op){
      case '+' : 
          result = num1 + num2;
          break;
      case '-' : 
          result = num1&gt;num2?num1-num2:num2-num1;
          break;
      case '*' : 
          result = num1*num2;
          break;
      case '/' : 
          result = num1/num2;
          break;
      }
      return result;
  }
</code></pre>
</li>
</ul>
<p>}</p>
<pre><code>- 출력결과
정수1 입력 : 50
정수2 입력 : 15
35

</code></pre>