<p>다들 추석 잘 보내셨나요...?</p>
<hr />
<ul>
<li>public class나 main은 생략하고 작성했습니다.</li>
</ul>
<hr />
<h2 id="이차원-배열">이차원 배열</h2>
<h3 id="정의">정의</h3>
<ul>
<li>1차원 배열 안에 또 다른 배열이 있는 형태</li>
</ul>
<h3 id="선언방법">선언방법</h3>
<pre><code class="language-java">보관하고자 하는 자료형(배열타입)[][](이차원 배열 선언)배열명(배열에 대한 래퍼런스 변수) = new(배열생성)자료형(선언한 배열 타입과 동일)[][](배열크기, 행, 열)
// 예시
// 3X3형태의 2차원 array라는 이름의 배열 
int[][] array = new int[3][3];</code></pre>
<h3 id="배열-삽입과-출력">배열 삽입과 출력</h3>
<pre><code class="language-java">// 삽입
// 0 -&gt; 0, 1, 2
// 1 -&gt; 0, 1, 2
array[0][0] = 1;
array[0][1] = 2;
array[0][2] = 3;

array[1][0] = 4;
array[1][1] = 5;
array[1][2] = 6;

// 출력
System.out.println(array[0][0]); 
System.out.println(array[1][1]); </code></pre>
<ul>
<li>출력 결과
1
5</li>
</ul>
<pre><code class="language-java">// FOR문을 이용한 삽입과 출력
// 삽입이 잘되었는 지 확인하기 위해 출력도 같이 실행
// 1. 배열선언
int[][] array = new int[3][3];

// 2. 2차원 삽입
int num = 1;
for(int i=0;i&lt;array.length;i++) {
    for(int j=0;j&lt;array[i].length;j++) {
        array[i][j] = num++;
        System.out.print(array[i][j] + &quot;\t&quot;); 
        // &quot;\t&quot;를 사용하면 일정한 간격으로 출력
    }
    System.out.println();
}</code></pre>
<ul>
<li>출력결과
1 2 3
4 5 6
7 8 9</li>
</ul>
<pre><code class="language-java">// Arrays.toString 사용하여 출력
import java.util.Arrays;

System.out.println(Arrays.toString(array[0]));
System.out.println(Arrays.toString(array[1]));</code></pre>
<ul>
<li>출력결과
[1, 2, 3] // 대괄호를 쓰면 개행이 안되어서 넣었습니다.
[4, 5, 6] //</li>
</ul>
<h3 id="응용문제">응용문제</h3>
<h4 id="스네이크-1">스네이크 1</h4>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/4a57e6fb-abb2-451b-8e98-478d7eb21e48/image.png" /></p>
<pre><code class="language-java">// 필요한 라이브러리
import java.util.Iterator;

// 데이터 선언
int[][] array = new int[5][5];

//배열에 데이터 추가
int num = 21;
for(int i=0;i&lt;array.length;i++){
    for(int j=0;j&lt;array[i].length;j++){
        array[i][j] = num++;
    }
}

// 배열 출력
for(int i=0;i&lt;array.length;i++){
    for(int j=0;j&lt;array[i].length;j++){
        System.out.print(array[j][i]+&quot;\t&quot;);
    }
    System.out.println();
}</code></pre>
<ul>
<li>출력결과
21    26    31    36    41<br />22    27    32    37    42<br />23    28    33    38    43<br />24    29    34    39    44<br />25    30    35    40    45</li>
</ul>
<h4 id="스네이크-2">스네이크 2</h4>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/4e84967a-1c6c-4098-92e4-addc39eaee89/image.png" /></p>
<ul>
<li>입력으로 구현하는 방법<pre><code class="language-java">//입력
int[][] arr = new int[5][5];
// 0,2,4 -&gt; 왼쪽에서 오른쪽으로 데이터 추가
// 1,3 -&gt; 오른쪽에서 왼쪽으로 데이터 추가
int num = 21;
for(int i=0;i&lt;arr.length;i++){
  if(i%2==0){
      for(int j=0;j&lt;arr.length;j++){
          arr[i][j] = num++;
      }
  }else{
      for(int j=arr.length-1;j&gt;=0;j--){
          arr[i][j] = num++;
      }
  }
}
</code></pre>
</li>
</ul>
<p>// 출력
for(int i=0;i&lt;arr.length;i++){
    for(int j=0;j&lt;arr[i].length;j++){
        System.out.print(arr[i][j].length;j++);
    }
    System.out.println();
}</p>
<pre><code>
- 출력으로 구현하는 방법
```java
int[][] arr = new int[5][5];
int num = 21;

// 입력
for(int i=0;i&lt;arr.length;i++){
    for(int j=0;j&lt;arr[i].length;j++){
        arr[i][j] = num++;
    }
}

// 출력
for(int i=0;i&lt;arr.length;i++){
    for(int j=0;j&lt;array[i].length;j++){
        if(j%2==1){
            System.out.print(array[i][4-j] + &quot;\t&quot;);
        }else{
            System.out.print(array[i][j] + &quot;\t&quot;);
        }
    }
    System.out.println();
}</code></pre><hr />
<p>이차원 배열은 아직 너무 어렵다... 다행히도 그렇게 많이 쓰이는 개념은 아니라고 한다...!!</p>