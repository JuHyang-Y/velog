<p>저번에 docker desktop에 올린 Spring Boot image를 cmd창에서 확인하고 image를 실행시키는 걸 해보도록 하겠습니다!</p>
<hr />
<h2 id="이미지-확인">이미지 확인</h2>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/f1ec7b94-83c3-43ff-8a75-b1f2a89c98d5/image.png" />
cmd 창을 실행시킨 뒤</p>
<pre><code>docker images</code></pre><p>를 통해 현재 가지고 있는 docker의 image들을 확인합니다.</p>
<h2 id="이미지-컨테이너화">이미지 컨테이너화</h2>
<ul>
<li>docker desktop에서 만들기
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/81ea9eee-f46c-4433-86ff-17326ad91f2c/image.png" />
이미지에 있는 run 버튼을 클릭한다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/76fefea5-4c19-4417-905a-d0fe2d2e3ddf/image.png" />
optional setting에서 container name을 입력한뒤 Run을 눌러준다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/3f2bb0ff-2f95-4cee-ac7e-e4d30655d7dd/image.png" />
실행이 됐다...(오잉?)
이렇게 실행이되도 맞는건가...?</p>
<ul>
<li>CMD에서 실행하기
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/5ef345fc-21cb-45f0-b41e-f712525254b1/image.png" /><pre><code>docker run -d -p 9000:9000 이미지REPOSITORY명 --server.port=9000</code></pre>컨테이너를 생성할 때 detached모드로 실행하고 포트는 9000번으로 설정한다.</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/f3f5a92d-690e-4ce7-acdb-81f3e2482db6/image.png" /></p>
<pre><code>docker ps</code></pre><p>를 입력하여 현재 실행되고 있는 container를 확인한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/54d7212a-4ec9-48a8-89a3-44c76f794aa7/image.png" /></p>
<pre><code>docker logs 컨테이너의NAMES</code></pre><p>를 입력하면 container가 실행되고 있는 것을 볼 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/6dd5ff1e-63d2-4e49-b2a9-e93b5476c61c/image.png" /></p>
<pre><code>http://localhost:9000/</code></pre><p>포트번호를 띄워놓고 잘 동작하는지 확인합니다.</p>
<hr />
<h2 id="출처">출처</h2>
<ul>
<li><a href="https://angrypig123.github.io/posts/docker(6)/">Spring Boot, Dockerfile</a></li>
</ul>