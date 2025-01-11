<p>Docker를 사용하기 위해서는 네트워크를 조금 알아야한다고 한다.
<del>왜이렇게 알아야할게 많을까...?</del>
도커를 동작하는 많은 서버들이 네트워크를 사용하기 때문이라구...</p>
<hr />
<h2 id="도커와-웹서버">도커와 웹서버</h2>
<p>도커에서 웹서버를 사용하면, 웹서버는 container에 설치된다.
이 container가 설치된 운영체제를 <strong>host</strong> 라고 한다.
container와 host는 각각 독립적인 시스템이기 때문에 다른 포트와 
File System을 가지고 있다.</p>
<h3 id="포트포워딩">포트포워딩</h3>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/b680b990-0e6f-4fe3-89f9-efca3c2a23af/image.png" /></p>
<h3 id="실습">실습</h3>
<ul>
<li><p>아파치(Apache) 웹서버를 설치
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/69c4eefb-91ed-4be8-b689-e1e422e34569/image.png" />
cmd화면에서 </p>
<pre><code>docker pull httpd</code></pre><p>를 입력하여 설치할 수 있다.</p>
</li>
<li><p>image를 생성할 때 몇가지 옵션이 있다.</p>
<ul>
<li>image에서 run 버튼을 입력하면 container를 생성할 수 있다.(노란색 동그라미)</li>
<li>container의 포트는 이미지를 만든 제작자가 미리 설정해둔 값이다.(빨간색 동그라미(?))
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/fde65de5-df2b-47fb-9dd5-267b95b9a6d9/image.png" />
　</li>
</ul>
</li>
<li><p>cmd를 사용하여 설치하는 방법</p>
<pre><code>docker ps</code></pre><p>를 사용하여 현재 돌아가고 있는 image들을 확인한다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/367770bd-f7c0-4b3d-a90a-8840ddfde390/image.png" /></p>
</li>
</ul>
<pre><code>docker run --name ws4 -p 8082:80 httpd</code></pre><p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/c17f9100-37f0-41fb-a686-deae84649a87/image.png" /></p>
<pre><code>docker ps</code></pre><p>를 쳐서 다시 확인해보면
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/d171f728-ef33-4be0-911a-93ba9a2691c9/image.png" />
잘 만들어 진 것을 확인할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/8108ef37-0498-42de-a432-ab2f142ace5a/image.png" />
GPU환경에서도 만들어진 것을 확인할 수 있다.</p>
<ul>
<li>만든 web 서버 사용하기
잘 접속이 되었는지 확인
web브라우저에서 검색
&quot;<a href="http://localhost:8081/index.html&quot;">http://localhost:8081/index.html&quot;</a></li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/4ff89ab0-a38c-4061-90c2-0e8855e94792/image.png" /></p>
<p>httpd를 사용할 수 있는 환경이 만들어진 것을 확인할 수 있다.</p>
<hr />
<h2 id="출처">출처</h2>
<ul>
<li><a href="https://youtu.be/SJFO2w5Q2HI?si=FD4EIXUPDcjJ9RE2">생활코딩 Docker 입문수업</a></li>
</ul>