<p>이제 마지막날까지 24일 남았다....
쥐인장~~!
바쁘다고 생각되니깐 블로그에 손이 가지 않아서 참으로 곤란하다...</p>
<hr />
<h2 id="기록">기록</h2>
<p>하도 기록을 안해서 내가 어떻게 하고 있는지 잊어버리는 것 같아서 시작과 얼마나 달라졌는지 기록하기 위해 블로그를 작성한다.</p>
<h3 id="환경세팅">환경세팅</h3>
<p>일단, 환경세팅에서 변화가 생겼는데
큰 변화라고 한다면 springboot를 gradle에서 maven으로 바꾸었다.
그래서 현재 springboot 환경은
Project : Maven
Language : Java
Spring Boot : 3.3.4
Project Metadata
Project Metadata - Packaging : Jar
Project Metadata - Java : 17</p>
<p>FastAPI는 
python : 3.10.13 → torch 2.4.1+cpu / ultralytics 8.3.9
FastAPI version : 0.115.0
FastAPI CLI version : 0.0.5</p>
<p>DB는 MariaDB 10.5를 사용하고 있다.</p>
<h3 id="chatgpt-유료">chatGPT 유료</h3>
<p>그리고 결국 chatGPT유료버전을 구매하였다...
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/34c82fec-b458-459b-9d44-aaa117e88a6d/image.png" />
유료구매를 하니... 너무 편했다... 
당연한 말이긴 하지만, 코드도 훨씬 잘짜줘서 약간 배신감 느낌...
현질이 답이었군...</p>
<h3 id="굴곡들">굴곡들</h3>
<ol>
<li>DB와 springboot를 연결시켰는데, 너무 힘들었다.. properties에서 막 이거저거 바꾸면서 왜 안되냐고 2~3일을 막 머리를 쥐뜯었는데, 옆에서 보시다가 1시간만에 연결시킨 행님께.. 큰 감사를 전합니다.</li>
<li>그리고 DB를 연동했는데, entity에서 선언하고 lombok을 불러도 전혀 연결이 되지 않아서 또 난항을 겪고 있었다.
jackson 직렬화 설정하고 myBatis도 다시 깔아보았다...</li>
</ol>
<p>너무 예전 일이라 까마득하지만 springboot 의존성을 설치할 때 lombok을 넣어도, 아주 기본틀만 가지고 있고 추가로 더 설치를 해주어야 한다는 결말을 얻었다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/c89c0cd1-818e-486b-8016-dd1d52b7658b/image.png" /></p>
<p>help - install new software 을 클릭해주시고
그곳에 
<a href="https://projectlombok.org/p2">https://projectlombok.org/p2</a>
링크를 넣고 설치를 진행하였다.(자세한 과정은 밑에 출처 넣어두었다.)</p>
<p>거짓말같이 너무 잘되어서 또 참으로 괴롭던 시절이었다...</p>
<ol start="2">
<li><p>화면은 제대로 보고 살자..
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/a13d4baf-b06d-4abe-b975-c3e3552796ce/image.png" />
이클립스 화면 불편하게 보고 있었는데, 저 화면으로 보면 훨씬 낫다는 것을... 알게되었다.(버튼 오른쪽 상단에 있음)</p>
</li>
<li><p>연결...
BE를 왜 한다고 했을까... 진짜 나는 아무것도 모르는 나부랭이었고..
뭣도 모를때 가장 용감하다는 것을 알았다.
나는 spring을 배웠지만 Controller와 RestController의 차이를 모르고 있었다....
저어런.....OTL
아주 큰 차이로는 결과를 return 할 때 Controller는 html을 반환을 하고,
RestController는 json과 같은 결과값을 반환한다는 점이다.</p>
</li>
</ol>
<p>그걸 알고나서 지금 컨트롤러가 겁나많이 생기고 있다... 두둥...!!</p>
<ol start="4">
<li>FastAPI와의 통신
지금 모델은 만들어지고 있는 중이고, 전처리 코드가 먼저 완성이 되어서 fastapi에 전처리 코드를 올리고 자바환경과 통신하게 만드는 환경을 구축하고 있다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/01a08b05-6503-4521-b30b-ad40068e4bf7/image.png" /></li>
</ol>
<p>나름 이렇게 구현하기 위해서 구현을 하고 있었는데, 강의와 다르게 자꾸 값을 못보내고 못받아오는 것이다.
CORS에러가 발생했다고 했는데, 어떻게 하는 건지.. 전혀모르겠는 것이다.
그래서 http에서 https로 바꿔보기도 했는데, 계속 CORS에러가 발생하고 인증서 다운받고... 눙물을 머금고...
ChatGPT와 잘하는 행님과 2일을 고생했다..(<del>사실 행님만.. 나는 가만히 지켜보기 역할...ㅋㅋㅋㅋㅋ</del>)</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/f1c71ccf-6ce0-4cd5-bfed-22a05c44c071/image.png" />
알고봤더니 cors 다 설정해놓고 밑에 FastAPI를 다시 app에 불러와서 안되는 거였다...ㅎㅎㅎㅎ</p>
<p>이제 CAM이랑 모델 올리는 일이 남았는데...
잘 극복할 수 있을까 걱정이 된다...</p>
<hr />
<h2 id="출처">출처</h2>
<ul>
<li><a href="https://bmangrok.tistory.com/entry/Spring-%EC%9D%B4%ED%81%B4%EB%A6%BD%EC%8A%A4%EC%97%90-Lombok-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0-%EC%9D%B4%ED%81%B4%EB%A6%BD%EC%8A%A4-%EB%A9%94%EB%89%B4-%EB%B0%8F-Maven%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%B4-%EA%B0%84%ED%8E%B8%ED%95%98%EA%B2%8C">이클립스에 Lombok 설치하기 - 이클립스 메뉴 및 Maven을 이용해 간편하게</a></li>
</ul>