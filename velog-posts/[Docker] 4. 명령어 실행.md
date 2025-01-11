<p>서버를 이용하기 위해서 컨테이너를 수정하기!</p>
<hr />
<h2 id="간단한-명령어-수행">간단한 명령어 수행</h2>
<h3 id="docker-desktop">Docker desktop</h3>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/afb50912-2b49-4a4d-8735-d12fc7e28d3c/image.png" />
ws2를 실행한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/1be2ebe1-502e-453e-961a-6997f8fa3fd7/image.png" />
terminal을 실행시킨다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/85836709-6130-475f-9a6c-876e8b429dae/image.png" />
terminal에 </p>
<pre><code>pwd</code></pre><p>를 입력하여서 경로를 확인한다.
이 경로는 host가 아닌 container안에서 실행시킨 것이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/0fc770c2-d2b9-4b50-aba0-74b6aa90b2a0/image.png" /></p>
<pre><code>ls -al</code></pre><p>을 실행시키면 현재 container가 가지고 있는 폴더들을 확인할 수 있다.</p>
<h3 id="cmd">CMD</h3>
<ul>
<li>기존에 있는 container(ws3) 실행
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/c4ce41d6-fa02-43ba-ace4-f4f8cceb6cc7/image.png" />
cmd창을 실행시키고<pre><code>docker start ws3</code></pre>실행시키고 싶은 container(기존에 있을 때)를 실행시기고<pre><code>docker ps</code></pre>를 입력하여 현재 실행되고 있는 container목록을 확인한다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/62743a54-9bb3-4223-b139-f35b605e19c3/image.png" /></p>
<pre><code>docker exec ws3 pwd</code></pre><p>현재 container에서 실행시키고 싶은 명령어를 뒤에 붙여서 실행한다.</p>
<p><img alt="sh로 실행했을 때" src="https://velog.velcdn.com/images/ju_hyanghyang/post/634eba3b-30c3-475a-b775-497ae5c78912/image.png" /></p>
<ul>
<li>sh로 실행했을 때
<img alt="bash로 실행했을 때" src="https://velog.velcdn.com/images/ju_hyanghyang/post/3be62a5e-6fe1-405f-aa74-a4eccb548352/image.png" /></li>
<li>bash로 실행했을 때</li>
</ul>
<p>만약 container와 지속적으로 연결하면서 명령어를 전달하고 싶을 때는 </p>
<pre><code>docker exec -it ws3 /bin/sh
또는
docker exec -it ws3 /bin/bash

- it
i : interactive / t : tty</code></pre><p>를 입력한다.
그럼 #이 뜨게 되는데, 이는 ws3 container를 대상으로 해서 내려지는 명령이라는 뜻이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/37af7ce6-caee-4bae-ab5b-c5e94082cfbf/image.png" />
실행하면 docker desktop에서 ws3의 terminal창에서 실행했던 결과와 같은 결과가 나오는 것을 확인할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/2f9adebe-c02e-47a7-87bb-340374fa59cf/image.png" />
컨테이너를 나오고 싶다면</p>
<pre><code>exit</code></pre><p>를 작성해주면 된다.</p>
<hr />
<h2 id="웹서버의-container수정해보기">웹서버의 container수정해보기</h2>
<p>현재 웹서버 경로 &quot;<a href="http://localhost:8000/index.html&quot;">http://localhost:8000/index.html&quot;</a></p>
<h3 id="indexhtml-수정해보기">index.html 수정해보기</h3>
<p>현재 사용하는 image인 <a href="https://hub.docker.com/_/httpd">Apache 웹서버</a>에서 index.html 파일이 어디에 있는지 알 수있다.</p>
<pre><code>/usr/local/apache2/htdocs/</code></pre><p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/81d486fb-a3f2-4343-bf75-f6c5777a807f/image.png" /></p>
<pre><code>cd /usr/local/apache2/htdocs/
ls -al</code></pre><p>cd(change directory)를 사용하여서 해당 경로로 들어간 뒤 파일 목록을 살펴본다.
index.html이 존재하는 것을 확인할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/99f1279b-232f-4b09-a433-acb179e914be/image.png" />
container는 가벼운 것이 덕목이기 때문에 nano(쉘 기반의 텍스트 편집기) 명령어가 존재하지 않는다.</p>
<p>nano 설치하기</p>
<pre><code>apt update
apt install nano</code></pre><p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/a9dbf461-480c-485e-a23b-3febd754dbcc/image.png" />
nano를 설치 후 다시</p>
<pre><code>nano index.html</code></pre><p>을 실행하면 위와 같은 화면이 나오게 된다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/c30dcb22-3fbd-45a8-90f2-a29db8648aa0/image.png" />
내용을 수정하고 ctrl+x, ctrl+y를 차례로 눌러준다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/046c2e82-21f4-44c1-9c15-08bc2c7a3824/image.png" />
새로고침을 눌러주면 화면이 바뀐 것을 확인할 수 있다!</p>
<p>하지만 이렇게 변경하는 방법은 굉장히 위험하다! -&gt; 컨테이너가 사라지면 우리가 편집했던 모든 것들이 날아가기 때문!
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/3a657754-a386-4c26-aa0b-abc94207c373/image.png" />
때문에 위와 같이 실행환경은 container에게 맡기고, 파일을 수정하는 작업하는 것은 host에게 맡기는 방법을 알아보도록 하자!</p>
<hr />
<h2 id="host에서-수정하기">Host에서 수정하기</h2>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/682c204b-ee5b-424b-a5de-b9c7afbe8309/image.png" />
vscode에 있는 docker를 다운 받고, vscode에서 진행해보도록 하겠다.(필수 아님!)</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/ae3ca907-f6cf-429c-af27-aa4ac46a5c00/image.png" />
기존에 만들어 놓은 html파일을 가지고 실습을 진행해보도록 하겠다.</p>
<p>아래의 명령어를 terminal창에서 실행시킵니다.</p>
<pre><code>docker run -p 8000:80 -v (html파일 경로):/usr/local/apache2/htdocs/ httpd 

-p : port
-v : volume</code></pre><p>'/usr/local/apache2/htdocs/'는 index.html를 찾기 때문에 파일 이름을 index.html로 바꿨습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/30edb18a-0db0-47f8-88b7-02238fe7c6be/image.png" />
실행결과 이렇게 나오는 것을 볼 수 있습니다.</p>
<p>만약 해당 포트번호에 해당하는 컨테이너가 미리 실행중이라면 오류가 발생할 수 있으니 포트번호를 잘 확인하시고 실행하시면 됩니다.!</p>
<hr />
<h2 id="출처">출처</h2>
<ul>
<li><a href="https://youtu.be/P0ZFyB4iQd0?si=Q_Nu-wrdsgrzHL13">생활코딩 Docker 입구 수업</a></li>
</ul>