<h2 id="반복문">반복문</h2>
<h3 id="while문">while문</h3>
<ul>
<li>while(){}
()안에 조건이 True일 때, 반복을 진행한다.
반복 횟수가 정해지지 않았을 때 사용</li>
<li>예제) 입력받은 수가 10보다 작은지 큰지 판단하여 작다면 반복 종료<pre><code class="language-java">Scanner sc = new Scanner(System.in);
</code></pre>
</li>
</ul>
<p>// 첫번째 방법
while(true){
    System.out.println(&quot;정수 입력 : &quot;);
    int num = sc.nextInt();</p>
<pre><code>if(num &gt; 10){
    System.out.println(&quot;종료되었습니다.&quot;);
    break; // break를 만나면 바로 멈춘다.
}</code></pre><p>}</p>
<p>// 두번째 방법
int num = 0;
while(num&lt;10){
    System.out.print(&quot;정수 입력 : &quot;);
    int num = sc.nextInt();
}
System.out.println(&quot;종료되었습니다.&quot;);</p>
<pre><code>
- while문을 멈추는 방법
```java
// while문의 조건을 담을 수 있는 변수 선언
boolean result = true;

while(result){
    System.out.println(&quot;반복문 1번만 실행&quot;);
    // 1번째 방법 
    // 속해있는 영역을 벗어난다.
    break;
    // 2번째 방법
    result = false;
}</code></pre><h3 id="do-while문">do-while문</h3>
<ul>
<li>do{실행문}while(조건식);
무조건 do안의 실행문을 한번 실행하고 조건에 따라 반복을 결정</li>
<li>예제) 목표 몸무게까지 감량하면 반복을 멈추는 반복문<pre><code class="language-java">Scanner sc = new Scanner(System.in);
// 현재/목표 몸무게 입력받기
System.out.print(&quot;현재 몸무게 : &quot;);
int now = sc.nextInt();
System.out.print(&quot;목표 몸무게 : &quot;);
int goal = sc.nextInt();
</code></pre>
</li>
</ul>
<p>// 몇 주차를 표현할 수 있는 변수 선언
int w = 1;</p>
<p>do{
    // 반복될 내용
    // 주차별 감량 몸무게 입력 받기
    System.out.print(w + &quot;주차 감량 몸무게 입력 : &quot;);
    int lose = sc.nextInt();</p>
<pre><code>// 원래 몸무게 - 감량 몸무게
now -= lose;
w++;</code></pre><p>}while(now &gt;= goal); // 다이어트의 성공 여부 판단</p>
<p>System.out.println(now + &quot;kg 달성! 축하합니다!&quot;);</p>
<pre><code>- 출력결과
현재 몸무게 : 70
목표 몸무게 : 60
1주차 감량 몸무게 입력 : 5
2주차 감량 몸무게 입력 : 4
3주차 감량 몸무게 입력 : 3
58kg 달성! 축하합니다!


### for문
- for(변수선언;변수조건;변수증감){반복실행문;}
반복해야될 횟수를 알고 있을 때 사용
- 예시) 1부터 3까지 반복하며 출력할 때
```java
// 그냥 3번 출력
System.out.println(&quot;1&quot;);
System.out.println(&quot;2&quot;);
System.out.println(&quot;3&quot;);

//while문
int num = 1;
while(True){ // 또는 while(num&lt;
    System.out.println(num);
    num ++
    if(num&gt;3){
        break;
    }
}

// for문
for(int i = 1; i &lt; 4; i++){
    System.out.println(i);
}
</code></pre><ul>
<li><p>출력결과(모두 동일)
1
2
3</p>
</li>
<li><p>예시) 약수구하기</p>
<pre><code class="language-java">// 숫자 입력받기
Scanner sc = new Scanner(System.in);
System.out.print(&quot;정수 입력 : &quot;);
int num =sc.nextInt();
</code></pre>
</li>
</ul>
<p>// 입력받은 숫자 num을 임의의 숫자(1~num)로 나누었을 때 나머지가 0인 약수 출력
for(int i = 1; i&lt;=num;i++){
    if(num%i==0){
        System.out.prtint(i + &quot; &quot;);
    }
}</p>
<pre><code>- 출력결과
정수 입력 : 9
1 3 9 

- 예시) 
![](https://velog.velcdn.com/images/ju_hyanghyang/post/eb7690ee-b589-47f1-93b3-7c401873d603/image.png)
```java
int total = 0;
for(int i=77;i&gt;=1;i--){
    total += (i*(78-i));
}
System.out.println(total);</code></pre><ul>
<li>출력결과
79079</li>
</ul>
<pre><code class="language-java">// 또 다른 풀이, for문 안에 변수 두개를 선언하여 사용
int total = 0;
for(int i=77, j=1; i&gt;=1;i--, j++){
    // i가 끝나면 반복문이 끝나기 때문에, j의 조건 값은 지정하지 않아도 된다.
    total += (i*j);
}
System.out.println(total);</code></pre>
<ul>
<li>출력결과
79079</li>
</ul>