<h2 id="반복문">반복문</h2>
<h3 id="이중-for문">이중 for문</h3>
<h4 id="예제-구구단">예제) 구구단</h4>
<pre><code class="language-java">import java.util.Scanner

public class 구구단{
    public static void main(String[] args){
        // 구구단 만들기
        for(int i=2;i&lt;=9;i++){
            System.out.println(i + &quot;단&quot;);
            for(int j=1;j&lt;=9;j++){
                System.out.print(i+&quot;*&quot;+j+&quot;=&quot;+(i*j));
            }
        }

        // 사용자가 출력하고 싶은 단을 입력받아 출력하기
        Scanner sc = new Scanner(System.in);
        System.out.print(&quot;단 입력 : &quot;);
        int dan = sc.nextInt();

        for(int i=1;i&lt;=9;i++){
            System.out.println(dan + &quot;*&quot; + i + &quot;=&quot; + (dan*i));
        }
    }
}</code></pre>
<h4 id="예제-별-찍기">예제) 별 찍기</h4>
<pre><code class="language-java">for(int j=0;j&lt;=5;j++){
    for(int i=0;i&lt;=j;i++){
        System.out.print(&quot;*&quot;);
    }
    System.out.println();
}
// 별 몇 줄 찍을지 입력받아서 출력하기
System.out.print(&quot;행 개수 : &quot;);
Scanner sc = new Scanner(System.in);
int h = sc.nextInt();

for(int j=0;j&lt;=h;j++){ // 행의 수 만큼 반복
    for(int i=0;i&lt;=j;i++){ // 별의 개수 만큼 반복 
        System.out.print(&quot;*&quot;);
    }
    System.out.println();
}</code></pre>
<ul>
<li>출력결과
```</li>
<li></li>
<li>*</li>
</ul>
<hr />
<hr />
<hr />
<hr />
<p>행 개수 : 5</p>
<ul>
<li></li>
<li><ul>
<li></li>
</ul>
</li>
</ul>
<hr />
<hr />
<hr />
<hr />
<pre><code>

```java
// 별 반대로 출력하기
for(int j=5;j&gt;=0;j--){
    for(int i=0;i&lt;=j;i++){
        System.out.print(&quot;*&quot;);
    }
    System.out.println();
}

// 입력받은 개수만큼 출력하기
System.out.print(&quot;행 개수 : &quot;);
Scanner sc = new Scanner(System.in);
int h = sc.nextInt();
for(int j=r;j&gt;=0;j--){
    for(int i=j;i&gt;=0;i--){
        System.out.print(&quot;*&quot;);
    }
    System.out.println();
}</code></pre><ul>
<li>출력결과<pre><code></code></pre></li>
</ul>
<hr />
<hr />
<hr />
<hr />
<p>**
*
행 개수 : 5</p>
<hr />
<hr />
<hr />
<hr />
<p>**
*</p>
<pre><code>
```java
// 이중 for문 공포의 별찍기
for(int j=0;j&lt;5;j++){
    for(int i=0;i&lt;4-j;i++){
        System.out.print(&quot; &quot;);
    }
    for(int i=0;i&lt;1+j;i++){
        System.out.print(&quot;*&quot;);
    }
    System.out.println();
}</code></pre><ul>
<li>출력결과<pre><code>  *
 **
***
****</code></pre></li>
</ul>
<hr />
<pre><code>

## Random, equals
### 1) Random
- Radnom한 값을 불러오는 방법
```java
import java.util.Random;//라이브러리 호출
Random rd = new Random();
int num = rd.nextInt(10); // 0~9 총 10개의 정수 랜덤으로 입력
//만약 1~10까지 10개의 정수를 랜덤으로 받고 싶다면
int num = rd.nextInt(10)+1;</code></pre><ul>
<li>라이브러리 호출 단축키 : ctrl + shift + 'o'</li>
</ul>
<h3 id="2-equals">2) equals</h3>
<ul>
<li>equals는 안의 값이 같은지 판단</li>
<li>&quot;문자&quot;.equals(변수) : &quot;문자&quot;와 변수의 값이 같은가</li>
<li>!&quot;문자&quot;.equals(변수) : &quot;문자&quot;와 변수의 값이 다른가</li>
</ul>
<h4 id="radom-equals-예제">Radom, equals 예제</h4>
<ul>
<li>예시) 덧셈 게임<pre><code class="language-java">import java.util.Random;
import java.util.Scanner;
</code></pre>
</li>
</ul>
<p>public class plus게임{
    public static void main(String[] args){
        Random rd = new Random();
        Scanner sc = new Scanner(System.in);</p>
<pre><code>    String play = &quot;&quot;;
    // 두 변수에 1~10사이의 랜덤수 생성하기
    while(!play.equals(&quot;N&quot;) &amp;&amp; !play.equals(&quot;n&quot;){
        int num1 = rd.nextInt(10)+1;
        int num2 = rd.nextInt(10)+1;

        // 만들어진 랜덤수 출력하기
        System.out.print(num1 + &quot;+&quot; + num2 + &quot;=&quot;);

        // 사용자가 정답 입력하기
        int result = sc.nextInt();

        // 출제된 문제와 정답이 맞는 지 판단하기
        // 정답시 Success 출력
        // 오답시 Fail, 게임 지속 여부 묻기
        if(num1+num2 == result){
            System.out.println(&quot;Success&quot;);
        }else{
            System.out.println(&quot;Fail&quot;);
            System.out.print(&quot;계속 하시겠습니까? &gt;&gt; &quot;);
            play = sc.next(); // 문자열을 입력받는다.
        }
    }
}</code></pre><p>}</p>
<pre><code>- 출력결과
3 + 2 = 5
Success
6 + 4 = 10
Success
6 + 1 = 1
Fail
계속 하시겠습니까? &gt;&gt; N</code></pre>