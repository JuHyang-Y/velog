<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/abef75b9-bb7d-4d1b-9b80-a7f1925e23ff/image.png" /></p>
<p>Docker의 이미지와 컨테이너를 생성하고 작동시키는 방법에 대해서 작성하겠습니다.</p>
<hr />
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/ccee109a-f8bb-496c-9f3e-6f1ac4597e60/image.png" /></p>
<p>docker에서 Image를 가져오는 것을 pull이라고 하고, image에서 container를 생성하는 것을 run이라고 한다.</p>
<hr />
<h2 id="이미지-pull">이미지 pull</h2>
<h3 id="httpd-이미지-설치">httpd 이미지 설치</h3>
<ol>
<li><p>docker hub에 들어가서 검색창에 'httpd'를 검색한다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/48f2650c-316e-4122-b35b-ce9aa8f15eb5/image.png" /></p>
</li>
<li><p>httpd 이미지가 있는 것을 확인할 수 있다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/9ff8f9ce-06c9-47e6-b24d-f4dc18fc9f3c/image.png" /></p>
</li>
<li><p>클릭해서 들어가면 httpd에 대한 다양한 설명을 볼 수 있고 다운 받을 수 있는 코드도 함께 나와있다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/41444032-87ca-4ae1-be89-581161c915a6/image.png" /></p>
</li>
<li><p>cmd창에서 copy한 코드 또는</p>
<pre><code>docker pull httpd</code></pre><p>입력하여 실행시킨다.</p>
</li>
<li><p>이미지가 잘 다운 받아졌는지 확인하기 위해서 cmd창에서</p>
<pre><code>docker images</code></pre><p>입력하여 확인한다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/4529da5c-6ca3-49d0-b6ee-2a089fea5596/image.png" /></p>
</li>
</ol>
<p>5-1. docker desktop(GUI 화면)에서도 이미지가 잘 설치된 것을 확인할 수 있다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/9bf07e50-7a2e-4444-b09b-2b8b4be12ba3/image.png" /></p>
<ol start="6">
<li>만약 삭제하고 싶다면</li>
</ol>
<ul>
<li><p>gui환경
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/d5b74a91-2204-44db-b477-a5c6b51f474b/image.png" />
romove를 눌러서 삭제할 수 있다.</p>
</li>
<li><p>cmd</p>
<pre><code>docker rmi httpd</code></pre><p>를 입력하여 지울 수 있다.</p>
</li>
</ul>
<h2 id="컨테이너-run">컨테이너 run</h2>
<h3 id="gui">GUI</h3>
<ol>
<li><p>docker의 image에서 run버튼을 클릭하면 컨테이너를 만들 수 있다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/fce53ff7-9aa6-43d1-9df8-098301f675f5/image.png" /></p>
</li>
<li><p>관리를 편리하게 하기 위해서 Container name을 잘 지정해주면 좋다.(지정하지 않고 run버튼을 입력해도 container가 생성된다.) 
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/52a626ca-d0bf-498b-968d-227d8c01792b/image.png" /></p>
</li>
</ol>
<p>-&gt; ws1으로 지정하고 run
container가 실행되고 있는 모습, 자세한 정보를 볼 수 있다.</p>
<ol start="3">
<li>start를 누르면 container를 실행시킬 수 있고, stop을 누르면 정지시킬 수 있다.
delete버튼을 누르면 삭제가 가능하다.</li>
</ol>
<h3 id="cmd">cmd</h3>
<ol>
<li><p>cmd를 실행시키고 실행시키고 싶은 image의 이름을 적고 run을 적는다.</p>
<pre><code>docker run container_name</code></pre></li>
<li><p>만든 container를 확인하고 싶을 때는</p>
<pre><code>docker ps</code></pre><p>를 입력해서 확인할 수 있다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/a199db32-4f57-4ec1-b8d2-61e81bd42af7/image.png" /></p>
</li>
<li><p>image에서 container를 생성할 때 이름을 추가하는 방법이 있다.
image 이름 앞에 --name 이라는 옵션을 작성해준다.</p>
<pre><code>docker run --name ws2 httpd</code></pre></li>
<li><p>실행중인 container를 중지시키고 싶을 때는 stop을 사용한다.</p>
<pre><code>docker stop ws2</code></pre><p>지금은 ws2라는 container의 이름을 적었는데 ID값을 적어도 된다.</p>
</li>
<li><p>잘 정지 되었는지 확인하기 위해서</p>
<pre><code>docker ps</code></pre><p>를 입력하여 확인할 수 있다.</p>
</li>
</ol>
<p>정지는 삭제된 것이 아니기 때문에</p>
<pre><code>docker ps -a</code></pre><p>를 입력하면 container의 전체 목록을 확인할 수 있다.</p>
<ol start="6">
<li><p>다시 키고 싶다면</p>
<pre><code>docker start ws2</code></pre><p>를 입력하면 중지시켰던 container가 다시 실행된다.</p>
</li>
<li><p>log를 보는 방법은 </p>
<pre><code>docker logs ws2</code></pre><p>를 입력하면 볼 수 있다. </p>
<pre><code>docker logs -f ws2</code></pre><p>container 이름 앞에 -f를 붙이면 실시간으로 로그를 확인할 수 있다.</p>
</li>
</ol>
<ol start="8">
<li>container를 삭제할 때는<pre><code>docker rm ws2</code></pre>를 사용하면 된다.</li>
</ol>
<p>실행된 친구는 rm으로 삭제되지 않기 때문에 stop을 먼저 실행해주거나</p>
<pre><code>docker rm --force ws2</code></pre><p>를 입력하여서 강제로 삭제해준다.</p>
<hr />
<h2 id="출처">출처</h2>
<ul>
<li><a href="https://youtube.com/playlist?list=PLuHgQVnccGMDeMJsGq2O-55Ymtx0IdKWf&amp;feature=shared">생활코딩 Docker 입문수업</a></li>
</ul>