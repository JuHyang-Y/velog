<p>Docker에 올리기 위한 SpringBoot만들기를 시작해볼까한다.</p>
<p>요즘에는 <a href="https://start.spring.io/">spring initalizr</a>에서 다운받아서 쓴다고 합니다...
(이 방법을 알려준 제 킹갓제너럴친구에게 깊은 감사를 드립니다.)</p>
<h2 id="환경설정">환경설정</h2>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/762cbc23-9f6d-42bb-9612-7b11c0936746/image.png" />
(2024년 10월 기준)
<strong>Project :</strong> Gradle-Groovy
<strong>Language :</strong> Java
<strong>SpringBoot :</strong> 3.3.4(SNAPSHOT이 아닌 것들 중 가장 최신 버전을 깔면 된다고 합니다.)
<strong>Project Metadata</strong> 나머지는 다 기본값으로 뒀습니다.
<strong>Project Metadata - Packaging :</strong> Jar
<strong>Project Metadata - Java :</strong> 17 (제 JDK버전에 맞춰서 설치했습니다.)
<strong>Dependencies :</strong> Spring Web, Lombok (아마 Thymeleaf도 했을 거 같은데 기억이 잘...)</p>
<ul>
<li>Java 버전 확인한는 방법
1) cmd창을 실행시킨다.
2) 명령어를 입력한다.<pre><code>java - version</code></pre><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/48a889e3-8fb7-4bbc-9000-9e7e5cf602b5/image.png" /></li>
</ul>
<ul>
<li><p>Maven과 Gradle
Dependencies에서 추가하지 못했더라도 
Maven은 경우에는 pom.xml
Gradle은 build.gradle 파일에서 추가하면 된다고 합니다!
<del>저는 Maven과 Gradle차이를 몰라서 Gradle깔아놓고 xml파일 찾고 있었다는 이야기...</del></p>
</li>
<li><p>JDK같은 경우 Spring 3버전 이상은 17 이상으로 다운 받으면 된다고 합니다.</p>
</li>
</ul>
<h2 id="import하기">Import하기</h2>
<p>저는 IDE를 Eclipse 에서 진행해보려 합니다!</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/4aca8607-8d5b-4bf0-9747-7f488a3b636d/image.png" />
만들어 놓은 프로젝트를 가져온 뒤 </p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/04c8c183-f4e5-4736-b9b1-79fb19957328/image.png" />
Gradel -&gt; Existing Gradle Project를 선택해줬습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/3229d0f2-f03d-4d32-8bbf-dd59a62b602e/image.png" />
그리고 다시 제 폴더가 있는 곳 경로를 선택해주고
Next를 눌러줬습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/7f6f5196-237d-4eb1-9a8c-826bbef9ccf1/image.png" />
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/1f8e18e7-d054-4c72-8c6a-17186f9b5ae9/image.png" />
로딩 화면 끝에 Finish를 눌러주면</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/eacdc3d7-0c2d-462f-8662-975d54556879/image.png" />
import가 완료 되었습니다!</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/e8b56c1f-64f2-45af-a748-76d0b82c5fb5/image.png" />
근데 프로젝트 우클릭 -&gt; Run As -&gt; Spring Boot App을 선택하라는데, Spring Boot App 이 안보인다. 단축키 Alt+Shift+X, B 도 안먹힌다 <del>씨앙....</del></p>
<h2 id="이클립스에-spring-tool-다운">이클립스에 Spring Tool 다운</h2>
<p>찾아보았더니 이클립스에서 Spring Boot를 사용하기 위해서는 별도의 작업이 필요하다고 한다.
보통 초기에 셋팅하던데 그냥 막 설치해본다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/7eb5f384-f67f-4af9-b37a-c50c8e205517/image.png" />
상단에 보면 Help 에 Eclipse Marketplace가 뜬다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/815262ce-aa27-4a64-8076-33d799dff15c/image.png" />
우선 BuildShip을 설치하라고 했는데 이미 설치가 되어있었다.(롸?)</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/f7b63306-a36f-4813-8ae9-c1e08eb39ac5/image.png" />
그 다음은 Spring Tools를 설치한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/768496dc-81db-4fc4-9b45-c497add5f668/image.png" />
뭘 설치해야될지 모르겠어서 일단 기본 설정만 눌러서 다운받았다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/5878992f-5912-416f-be4f-1f7f91c6c637/image.png" />
영어 울렁증이 도졌다. 모르겠고 일단 I accept 뭐시기를 눌렀다.</p>
<p>갑자기 꺼져서 다시 install을 눌렀는데 이번엔 다른 창이 나왔다
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/05c0631c-eaf2-454b-978f-97b5eb1d9baa/image.png" />
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/43812baf-8453-436b-8742-06bf51145540/image.png" />
일단 체크박스 다 누르고 본다(망해가는 과정 시발점을 보고 계십니다)</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/1ae50405-42b6-4e8f-aba3-d23edf0bab68/image.png" />
재시작을 물어본다. 난 직진이다. Restart Now..!!!</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/5a13ce4d-1842-4aea-ada2-4d9da1005ab4/image.png" />
이런 걸 물어봐? 일단 Yes... 나는야.. yes person...</p>
<p>Yes를 눌러서인가 재시작을 안하길래 내가 껐다 켰다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/f48216e7-feb9-4811-9806-8f6d2be9a7a8/image.png" />
다시 확인한 순간 Spring Boot App이 생겼다!!! 됐ㄸ아!!!
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/ffc718b3-e419-4aa5-a46a-67fefcf7ba87/image.png" />
아주 잘 동작..
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/55c1e03b-a7d9-43e2-9237-fe4ac77dc00c/image.png" />
네? 누구세요 진짜...  저 포트에서 방 좀 빼주세요.. </p>
<h2 id="포트-끄기">포트 끄기</h2>
<p>친구에게 SOS를 청했다(매우 든든한 내 친구!)</p>
<p>일단 돌아가고 있는 아이를 확인한다.
cmd창을 열고</p>
<pre><code>netstat -aon | findstr :8080</code></pre><p>를 입력하여 확인한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/9e1ef3a4-de79-47e2-bf4a-345f0aac8281/image.png" />
하 누구세요 진짜 방 빼요...</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/8e8a3d86-ce63-4582-bb78-dd87f0a18361/image.png" />
친구가 명령어를 알려줬는데, 액세스가 거부됐단다.. 이보쇼!!</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/3cd28484-82d7-490c-8189-a692fc64bbe4/image.png" />
친구 Say 관리자로 실행시켜봐
넹!</p>
<p>관리자 창 열고</p>
<pre><code>taskkill /F /PID 5260</code></pre><p>실행 시켰다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/e56c56fd-59fb-49cf-b172-c2e1a528914c/image.png" />
바로 죽었다..!!</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/25eb5ed9-c9bc-4472-afcb-af5e25b01755/image.png" />
다시 실행해보았더니 오류없이 잘 작동하는 것을 확인할 수 있었다!
다시한번 그 친구에게 압도적 감사를 표하면서 게시글을 마치도록 하겠습니다.</p>
<hr />
<h2 id="출처">출처</h2>
<ul>
<li><a href="https://jin2rang.tistory.com/entry/Spring-Boot-%EC%85%8B%ED%8C%85%ED%95%98%EA%B8%B0-startspringio">Spring Boot 셋팅하기</a></li>
<li><a href="https://ttl-blog.tistory.com/761">도커를 사용하여 간단한 SpringBoot 어플 실행하기</a></li>
<li><a href="https://jin2rang.tistory.com/entry/Spring-Boot-Import-projects?category=976390">Spring Boot - import projects</a></li>
<li><a href="https://diary-developer.tistory.com/9">이클립스 설치 및 스프링부트 사용하기</a></li>
<li><a href="https://fernweh6990.tistory.com/155">Eclipse에 Gradle+Springboot 환경 구축하기</a></li>
<li><a href="https://jisooo.tistory.com/entry/Spring-%EB%B9%8C%EB%93%9C-%EA%B4%80%EB%A6%AC-%EB%8F%84%EA%B5%AC-Maven%EA%B3%BC-Gradle-%EB%B9%84%EA%B5%90%ED%95%98%EA%B8%B0">Maven과 Gradle 비교하기</a> </li>
</ul>