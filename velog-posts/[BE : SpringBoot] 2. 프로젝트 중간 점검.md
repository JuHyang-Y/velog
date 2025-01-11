<p>프로젝트 하는 동안 알아낸 것들 정리하기!</p>
<h2 id="swagger-ui">Swagger UI</h2>
<p>인터페이스 명세서를 작성해보라고 말씀하셨는데, 모두 파악하고 쓰고 하려면 너무 오래 걸릴 것 같아서 꼼수를 생각해내다가
Spring boot에서도 FastAPI의 <code>/docs</code> 처럼 볼 수 있는 기능을 알아냈다. </p>
<p>바로 Swagger</p>
<p>spring boot에서 간단히 설정해줄 수 있다.
&lt;maven기준&gt;</p>
<ol>
<li>pom.xml파일에<pre><code>&lt;dependency&gt;
      &lt;groupId&gt;org.springdoc&lt;/groupId&gt;
      &lt;artifactId&gt;springdoc-openapi-starter-webmvc-ui&lt;/artifactId&gt;
      &lt;version&gt;2.1.0&lt;/version&gt;
&lt;/dependency&gt;</code></pre>추가해주고,</li>
</ol>
<p>application.properties에</p>
<pre><code>springdoc.swagger-ui.path=/api-docs</code></pre><p>를 넣고
<a href="http://localhost:%ED%8F%AC%ED%8A%B8%EB%B2%88%ED%98%B8/swagger-ui/index.html#/">http://localhost:포트번호/swagger-ui/index.html#/</a> 를 실행하면 화면이 나온다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/fc0db61e-ff75-4d2d-bcd2-2a520d2b642d/image.png" /></p>
<h2 id="실행중인-포트-죽이는-배치파일">실행중인 포트 죽이는 배치파일</h2>
<p>실행 중인 프로젝트를 중지하지 않고 다시 실행하면 지금 포트가 사용중이라 실행할 수 없다는 오류가 발생하는데 그때마다
<code>netstat -aon | findstr :포트번호</code>
<code>taskkill /F /PID 포트사용중인 아이 번호</code>
두개를 cmd(관리자권한)으로 실행시켜주었는데, 
.bat로 만들 수 있다고 알려주셔서 만드는 방법을 공유해볼까 한다.
방법은 매우 easy peasy lemon squeezy 하다.</p>
<ol>
<li>화면에서 .txt파일을 만들어주고, <pre><code>@echo off
:: 관리자 권한으로 실행되지 않은 경우 관리자 권한으로 재실행
NET SESSION &gt;nul 2&gt;&amp;1
IF %ERRORLEVEL% NEQ 0 (
 echo 관리자 권한으로 다시 실행 중...
 powershell -Command &quot;Start-Process '%~f0' -Verb RunAs&quot;
 exit
)
</code></pre></li>
</ol>
<p>echo Checking for processes using port 8443...
for /f &quot;tokens=5&quot; %%a in ('netstat -ano ^| findstr :8443') do (
    echo Process ID using port 포트번호: %%a
    taskkill /PID %%a /F
)
echo Port 포트번호 process terminated.
pause</p>
<pre><code>복붙해준다.(포트 번호 바꾸기!)
2. .txt확장자를 .bat으로 바꿔준다.
![](https://velog.velcdn.com/images/ju_hyanghyang/post/297d6410-78a7-4d2b-b5c2-e3df68664445/image.png)
이렇게 만들어지는 것을 확인할 수 있다!



## Spring Security
Security가 정말 애를 많이 먹었다.
![](https://velog.velcdn.com/images/ju_hyanghyang/post/9663eea6-56de-4d0c-9cd7-bcc741650bf9/image.png)

로그인 기능을 넣었지만 로그인을 하지 않아도 모든 페이지에 접근이 가능했는데, 이러면 안되잖아..?
그래서 방법을 찾아보다 전에 만들어놓은 Spring Security가 생각나서 Security의 filter를 사용해서 구현해보기로 했다.


![](https://velog.velcdn.com/images/ju_hyanghyang/post/faf7af63-a242-448f-ba08-c8fc7bf296fe/image.png)

파일은 이런식으로 넣어두었다.

---

가장 많이 애를 먹었던 부분은
시큐리티 연동을 해서 login 부분에서 정보를 입력하면 비교하기 위해 mapper에서 값을 받아오는데, 매칭이 되지않는다는 점이었다.
와이라노 와이라노...

```an internal error occurred while trying to authenticate the user.```

이런 에러였는데, 찾아봐도 gpt한테 물어봐도 안되는 것이다..
대답해줘 gpt...

아니.. 시큐리티하기 전에는 잘만 받아왔는데, 왜 그러는 걸까요...
근데 선생님이 보시더니... entity문제인 것 같다고 하셔서
원래 카멜케이스로 정의내렸던 것을 바꾸었더니 거짓말처럼 되는 것이다...
진짜... 거짓말하지 말아라...

그래도 결국에는 security를 구현했다는 것!
로그인을 하기 전에는 권한을 허락해준 것들만 접근이 가능하게 되고,
로그인 후에는 다 접근이 가능하도록 수정하였다!!

이제 페이지끼리와 값 불러오는 건 다 해결했고, 
모델연결하고 모델에서 받은 값 db로 저장하도록 연결하고,
Cam버튼 눌렀을 때 gradcam으로 그린 heatmap이 나오도록 지정하게 하면 끝이다!!!!!! 야호!!!!

</code></pre>