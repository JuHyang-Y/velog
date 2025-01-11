<p>안녕하세요? 오랜만의 게시글 입니다...
제가 3주간 열심히 java수업을 들었었는데요? 학원에서 3일만에... 더 정확히는 9시간만에... 제 3주가 따라 잡히는 바람에... 
너무 현타가 쎄게 왔구... 그래서 잠시 손을 놓고 있다가!
그래도 시작한 거 끝을 보자라는 마음으로 다시 시작하였습니다!</p>
<p>그리고 수업으로 추가된 내용은 전에 올렸던 게시글의 수정의 수정을 통해 업로드 하도록 하겠습니다!</p>
<hr />
<h2 id="배열">배열</h2>
<h3 id="정의">정의</h3>
<ul>
<li>같은 타입의 여러 변수를 하나의 묶음으로 다루는 자료구조</li>
<li>인덱스와 인덱스에 대응하는 데이터들로 이루어진 자료구조<ul>
<li>인덱스란? 
  -&gt; 배열의 시작 위치에서부터 데이터가 있는 상대적인 위치
  -&gt; 순차적으로 데이터를 다룬다
  -&gt; 0부터 시작</li>
</ul>
</li>
<li>같은 종류의 데이터들이 순차적으로 저장되는 공간</li>
</ul>
<h3 id="특징">특징</h3>
<ul>
<li>같은 자료형 하나로 묶을 수 있다.</li>
<li>인덱스 번호를 가지고 있다. -&gt; 0부터 시작해서 1씩 증가하는 형태</li>
<li>크기가 고정적이다.<h4 id="파이썬과-자바-배열의-차이점">파이썬과 자바 배열의 차이점</h4>
</li>
<li>자바에서의 배열은 한가지 타입의 데이터만 다룰 수 있다.
  -&gt; Object는 최상위 클래스이기 때문에, Object 배열로 선언하면 많은 배열의 데이터 타입을 다룰 수 있다.(사용법이 다름)</li>
<li>자바에서 배열은 크기가 고정적이다.</li>
</ul>
<h3 id="선언-방법">선언 방법</h3>
<pre><code class="language-java">보관하고자 하는 자료형(배열타입)[](배열선언) 배열명(변수명) = new(레퍼런스 생성 키워드, 배열 생성)자료형[배열 크기]
// 예시
// 정수형 데이터 5개를 보관할 수 있는 array라는 이름의 배열
int[] array = new int[5];</code></pre>
<h3 id="배열-출력">배열 출력</h3>
<pre><code class="language-java">// 배열을 그냥 출력하면 주소값이 나온다.
System.out.println(&quot;array 출력 :&quot; + array);
// 출력결과 : [I@7382f612 
// 배열처럼 여러개의 데이터를 가지고 있는 구조는 래퍼런스 변수(메모리를 찾아갈 수 있는 주소값)-&gt;참조변수
// 배열의 변수명과 [] 사이의 인덱스 번호를 사용하여 접근
System.out.println(array[0]); // 결과 0</code></pre>
<h3 id="배열-삽입">배열 삽입</h3>
<ul>
<li><p>이미 생성된 배열에 값을 집어넣는 방법</p>
<pre><code class="language-java">// 배열 array 0번째 인덱스에 3을 넣는다.
array[0] = 3;
// 값이 잘 들어갔는지 확인
System.out.println(array[0]); // 결과 3</code></pre>
</li>
<li><p>배열을 생성함과 동시에 데이터를 넣는 방법</p>
<pre><code class="language-java">// 이름을 보관할 수 있는 names라는 배열을 생성과 동시에 데이터를 넣기
String[] names = {&quot;김철수&quot;, &quot;홍길동&quot;, &quot;김영희&quot;};
// 잘 생성되었는지 확인
for(int i=0;i&lt;names.length;i++){
  System.out.println(names[i]);
}</code></pre>
</li>
<li><p>출력결과 
김철수
홍길동
김영희</p>
</li>
<li><p>배열의 타입에 맞지않는 데이터는 입력할 수 없다.</p>
<pre><code class="language-java">// 예시
// 정수형으로 배열을 선언
int array[] = new int[4]; 
array[0] = &quot;안녕&quot;; //안녕은 문자열이기 때문에 배열에 삽입할 수 없다.</code></pre>
</li>
<li><p>배열의 크기를 넘어서는 데이터를 입력할 수 없다.</p>
<pre><code class="language-java">// 예시
int array[] = new int[4]; // 배열은 4개의 공간(0,1,2,3)을 가지고 있다.
array[4] = 50; // 오류 발생 ArrayIndexOutOfBoundsException : 배열의 크기를 넘어간다.</code></pre>
</li>
</ul>
<h3 id="배열-예제">배열 예제</h3>
<h4 id="배열예제1">배열예제1</h4>
<ul>
<li>5개 과목의 점수를 입력하고, 최대, 최저, 총합과 평균 점수를 출력하시오.<pre><code class="language-java">import java.util.Arrays;
import java.util.Scanner;
</code></pre>
</li>
</ul>
<p>public class 점수 {
    public static void main(String[] args){
    Scanner sc = new Scanner(System.in);</p>
<pre><code>// 1. 정수형 데이터 5개를 저장할 수 있는 배열 array를 선언하세요
int[] array = new int[5];
// 2. 배열 안의 데이터를 모두 입력 받으세요
for(int i=0;i&lt;array.length;i++){
    System.out.print((i+1) + &quot;번째 입력 &gt;&gt; &quot;);
    array[i] = sc.nextInt();
}
int max = array[0];
int min = array[0];
int sum = 0;

for(int i=0;i&lt;array.length;i++){
    // 최고 점수 구하기
    if(max&lt;array[i]){
        max = array[i];
    }
    // 최저 점수 구하기
    if(min&gt;array[i]){
        min = array[i];
    }
    // 총합 구하기(누적)
    sum += array[i];
}

// 3. 입력한 점수를 출력하세요
System.out.println(&quot;입력된 점수 : &quot; + Arrays.toString(array));

// 4. 최고 점수와 최저 점수를 출력하세요.
System.out.println(&quot;최고 점수  : &quot; + max);
System.out.println(&quot;최저 점수  : &quot; + min);

// 5. 점수 총합과 평균을 출력하세요.
System.out.println(&quot;총합 : &quot; + sum);
System.out.println(&quot;평균 : &quot; + (float)sum/array.length);
}</code></pre><p>} </p>
<pre><code>- 출력결과
1번째 입력 &gt;&gt; 50
2번째 입력 &gt;&gt; 60
3번째 입력 &gt;&gt; 70
4번째 입력 &gt;&gt; 80
5번째 입력 &gt;&gt; 90
입력된 점수 : [50, 60, 70, 80, 90]
최고 점수 : 90
최저 점수 : 50
총합 : 350
평균 : 70.0

#### 배열예제2
- 로또 뽑기 : 5개의 숫자(1~10)를 중복없이 뽑아서 출력하기
```java
import java.util.Arrays
import java.util.Random;

public class 로또뽑기{
    public static void main(String[] args){
        // 1. 정수형 데이터 5개를 저장할 수 있는 array 배열 선언
        int[] array = new int[5];

        // 2. 배열 안의 데이터를 모두 임의의 값으로 초기화(1~10)
        Random rd = new Random();

        for(int i=0;i&lt;array.length;i++){
            array[i] = rd.nextInt(10)+1; // 배열에 랜덤한 값을 넣는다.
            for(int j=0;j&lt;i;j++){ // 3. 배열에서 중복된 값을 제거
                if(array[i] == array[j]){
                    // array[i] = rd.nextInt(10)+1; 
                    // i--를 하면 다시 위로 돌아가서 랜덤한 숫자를 넣어주기때문에 생략
                    i--;
                }
            }
        }

        4. 배열 안의 데이터를 모두 출력
        System.out.println(&quot;=====로또타임=====&quot;);
        System.out.println(&quot;이번주 출력번호는요..!!! 두구두구두구!!!&quot;);
        System.out.println(Array.toString(array));
    }
}</code></pre>