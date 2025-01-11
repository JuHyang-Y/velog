<p>Docker에 대해서 간단히 정리를 해야겠다고 느꼈다.
물론 앞으로 공식홈페이지에 올라와있는 아이들을 보면서 공부를 할테지만, 개념이 아예 없는 나를 위해 아주아주아주 간단하고 단순하게 적어보려한다.</p>
<p>주변인들에게 Docker에 대해 물어본 결과 &quot;아주 화나는 것들&quot;이라는 답변을 받았다... 네?</p>
<hr />
<h2 id="docker-정의">Docker 정의</h2>
<p>간단히 말하자면, Docker는 <strong>가상환경 셋팅 툴(프레임워크)</strong>이다.</p>
<ul>
<li>Docker를 사용하면 버전차이로 인한 오류를 가상의 컴퓨터 환경 세팅을 구축하여 해결할 수 있다.(그렇기에, 환경에 구애 받지 않고 언제든 서버를 항상 똑같은 상태로 만들 수 있다는 장점을 가지고 있다.)</li>
<li>또한, 완전히 독립된 환경으로 실행되기 때문에 여러 컨테이너에서 같은 프로그램을 실행할 수 있다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/0ab9df96-2be9-41f1-a664-436743fe0b6e/image.png" />
원래는 왼쪽과 같이 가상환경을 만들 때 하나의 os를 쪼개서 사용했다면, 
docker를 사용하게 되면 docker엔진에 있는 container를 사용하기 때문에 메모리자원을 아끼고 실행속도도 빠르게 돌릴 수 있다.</li>
<li>Docker는 하나의 시스템을 위한 여러가지 프로그램을 한꺼번에 실행시킬 때도 사용이 가능하다.</li>
<li>Docker는 리눅스 환경을 사용하는데, 실제로 컴퓨터가 윈도우여도 윈도우가 리눅스처럼 돌아갈 수 있도록 Docker가 만들어준다.</li>
<li>Docker에서는 image와 container라는 아이가 있다. 
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/ca663d05-39b7-421f-b8b5-1505af46eb5a/image.png" />
앱스토어로 비유하자면, 
docker hub라는 친구가 앱스토어이고, image라는 친구는 app이라고 생각하면 된다. 
그리고 image를 실행하는 것이 container라고 생각하면 된다.<del>(엇 여기는 비유가 아니네?)</del></li>
</ul>
<hr />
<p>아주아주 간단하고 제멋대로 Docker를 정의해보았는데, 아직은 그냥 이런 느낌으로 쓰는 건가 보다라고 생각하고 있는 중이라서 더 사용해보면서 감을 잡아야할 것 같다!</p>
<hr />
<h2 id="출처">출처</h2>
<ul>
<li><a href="https://youtu.be/EbTJtanJUfE?si=N4UHucF1ahNDX8u7">생활코딩 Docker 입구 수업</a></li>
<li><a href="https://www.yalco.kr/08_docker/">Docker가 뭐고 왜 쓰는건가요?</a></li>
</ul>