<p>간단한 SpringBoot코드를 입력하고, Docker에 올려보도록 하겠다.
SpringBoot는 eclipse에서 실행되었습니다.</p>
<hr />
<h2 id="springboot-프로젝트-만들기">SpringBoot 프로젝트 만들기</h2>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/eb366e4d-7536-4671-a1dd-35b30324eb42/image.png" />
SpringBoot가 잘 돌아가고 있는지 확인해줍니다.
프로젝트 우클릭 -&gt; Run As -&gt; Spring Boot App</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/c72e8655-22cc-4c02-b919-c8426a47f801/image.png" />
src/main/java안 package 안에 HomeController.java 파일을 만들어줍니다.</p>
<pre><code class="language-java">package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HomeController {
    @GetMapping(&quot;/&quot;)
    public String index() {
        return &quot;Hello World&quot;;
    }
}</code></pre>
<p>간단하게 코드를 선언해줍니다!</p>
<p>cmd 관리자로 열어주고</p>
<pre><code>netstat -aon | findstr :8080</code></pre><p>포트에 돌아가고 있는게 확인해준 뒤 없으면 실행시켜주고!
있으면</p>
<pre><code>taskkill /F /PID 실행되고 있는 친구 이름</code></pre><p>종료시켜준 뒤 실행시켜줍니다!
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/1e752e88-539b-4d59-9729-d7606b0c7b13/image.png" />
그럼 이렇게 실행되는 것을 확인할 수 있습니다!</p>
<p>스프링.. 감이 올락말락...
<del>뭔가 프로젝트가 다 끝날 때가 되어서야 &quot;아</del>! 이렇게 하는 거구나?&quot; 싶을 것 같은 이 기분..ㅋㅋㅋ~~</p>
<h2 id="docker에-올릴-jar파일-만들기">Docker에 올릴 Jar파일 만들기</h2>
<h3 id="jar-파일-만들기오류">Jar 파일 만들기(오류)</h3>
<p>도커에 올리기 위해서 jar파일을 만들어야 한다
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/161d7f7f-2285-4a4a-b43c-31d6fcda88c1/image.png" />
프로젝트 우클릭 -&gt; Run as -&gt; Run Configurations... 를 누르고</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/5f939085-eae1-4f24-a97c-59ab2b16930d/image.png" />
Gradle Task 선택... 넌 또 뭐가 문제니 증말...</p>
<ul>
<li>해결 해보기1
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/51f5dd85-53eb-4998-8934-0cd597c94fd6/image.png" />
프로젝트 우클릭 -&gt; Gradle -&gt; Refresh Gradle Project</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/562276ca-6676-4e3c-a5f3-a0826bb633ba/image.png" />
cmd를 사용해서 프로젝트가 있는 경로에 접근</p>
<pre><code>gradlew clean build</code></pre><blockquote>
<p>저같은 경우에는 C폴더에 바로 올려놓아서 C파일까지 이동했습니다!</p>
</blockquote>
<pre><code>- 파일 경로 찾아가기 
cd 파일경로
- 바로 뒤에있는 파일로 이동하기
cd ..</code></pre><p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/c353a4aa-2c7b-4400-96ec-97ace61893da/image.png" />
Project - clean
프로젝트 클린 작업을 실행해줍니다
저는 Clean all projects를 선택했습니다!</p>
<p>다시 Gradle을 실행하면..?! 안되네요...ㅎㅎㅎㅎ</p>
<ul>
<li>해결해보기2
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/c83c1830-ceb6-4481-867b-058cdd028d3f/image.png" />
project 우클릭 Properties 선택</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/7e0a2834-c80b-4330-9a9b-15290b617986/image.png" />
Java Compiler와 
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/51213076-2d43-4bf6-8024-f9b3ea188a90/image.png" />
Project Facets의 Java버전이 동일한지 확인하기!</p>
<p>이미 동일하니 Pass!!!</p>
<ul>
<li>해결해보기3
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/e214a610-49ba-4683-b81a-0936499cb73b/image.png" />
프로젝트의 Gradel 버전 확인하기
방금 봤던 화면에서 Gradle에 들어가서 자바 버전별 호환되는 Gradle버전인지 확인한다.
<a href="https://docs.gradle.org/7.3/release-notes.html#java17">Gradle페이지</a>
17부터는 7.3이상은 다 지원해주는 것 같은데 왜... 일단..!! 8.10.2에서 7.3.3으로 맞춰본다</li>
</ul>
<p>안되는데?</p>
<p>아하... 방금 다시 cmd 창에서 Gradlew build 기록을 보는데 Gradle 8.10.2는 Java 23지원을 한다고... 짜식이... 근데 왜 7.3.3으로 바꿨는데 안되지?</p>
<h3 id="jar파일-생성하기cmd">Jar파일 생성하기(CMD)</h3>
<p>cmd에서 해보기로 했다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/8ac93e4c-b903-449e-adcc-3ff7d36541b5/image.png" />
프로젝트가 있는 폴더로 이동한다</p>
<pre><code>cd 프로젝트 경로</code></pre><pre><code>gradlew build</code></pre><p>입력하고 보니 BUILD SUCCESSFUL 이 뜬 것을 확인할 수 있다.
해결이 되었다!!</p>
<h3 id="jar파일-실행해보기">Jar파일 실행해보기</h3>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/fe24484e-9585-4d0d-84b9-3ea044964d75/image.png" />
파일에 들어있는 파일명 확인하고 cmd에서 실행해보도록 하겠다.
현재 경로 프로젝트가 들어있는 경로!</p>
<pre><code>cd build/libs</code></pre><p>폴더로 이동하고 </p>
<pre><code>java -jar jar파일명.jar</code></pre><p>를 입력한다</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/9ea1d193-0da2-43b9-8234-e4aca107b227/image.png" />
서버에서 프로젝트가 동작하는 것을 확인했다!!!
진짜 뭐 하나 쉽게 넘어가지 않고... 눈물이 흐르는 것 같다...</p>
<h2 id="docker-파일-만들기">Docker 파일 만들기</h2>
<ul>
<li>이클립스
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/b2736c10-4bb2-459d-ad13-e2f6d75c646b/image.png" />
Dockerfile을 생성해줍니다!(위치는 상관없음)</li>
</ul>
<p><a href="https://spring.io/guides/gs/spring-boot-docker">Docker를 사용한 Spring Boot</a>를 참고해서 이미지를 빌드해보도록 하겠습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/e3cc86fe-73ae-4074-bbd2-55fb09176464/image.png" />
Gradel버전을 7.5이상이 필요해서 버전업을 시켜줍니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/9292b0f6-aa44-4109-af96-c152bfbb199d/image.png" />
제가 사용하고 있는 JDK 17의 경우 7.3 이상부터 지원을 하기 때문에 7.5로 버전을 바꿔줍니다.</p>
<p>그리고 Dockerfile에 </p>
<pre><code class="language-dockerfile">FROM openjdk:17-jdk-alpine
ARG JAR_FILE=gradle/wrapper/*.jar
COPY ${JAR_FILE} gradle-wrapper.jar
ENTRYPOINT [&quot;java&quot;,&quot;-jar&quot;,&quot;/gradle-wrapper.jar&quot;]</code></pre>
<p>를 입력하고 cmd나 다른 터미널 창에서</p>
<pre><code>docker build --build-arg JAR_FILE=build/libs/\*.jar -t springio/gs-spring-boot-docker .</code></pre><p>를 실행하면 된다.
이때 docker desktop이 실행되어있어야한다!</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/7ee47af9-29ab-4b79-8701-5ed209469724/image.png" />
build가 성공적으로 된 것을 확인할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/a76a9b6a-47ad-406a-be46-a2892a5bd3eb/image.png" />
docker desktop에서 확인하면 image가 만들어져있는 것을 확인할 수 있다!</p>
<hr />
<h2 id="출처">출처</h2>
<ul>
<li><a href="https://jin2rang.tistory.com/entry/Spring-Boot-View-%EA%B8%B0%EC%B4%88-%ED%99%98%EA%B2%BD%EC%84%A4%EC%A0%95-thymeleaf">Spring Boot - Welcome Page 만들기</a></li>
<li><a href="https://da2uns2.tistory.com/entry/Docker-%EB%8F%84%EC%BB%A4%EC%97%90-Spring-Boot-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0">도커에 Spring Boot 구축하기</a></li>
<li><a href="https://ttl-blog.tistory.com/761#SpringBoot%20%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%20%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0-1">도커를 사용하여 간단한 SpringBoot 어플 실행하기</a><ul>
<li><a href="https://kitty-geno.tistory.com/109">Spring Boot | Gradle, Jar 빌드&amp;배포하기</a></li>
<li><a href="https://zluoy.tistory.com/entry/SpringBoot-Gradle-Error-Gradle%EC%9D%B4-%EC%A0%81%EC%9A%A9%EC%9D%B4-%EB%90%98%EC%A7%80-%EC%95%8A%EC%9D%84-%EB%95%8C-Library-Import-Error-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-Import-%EC%95%88%EB%90%A0-%EB%95%8C#google_vignette">Gradle Error ( Gradle이 적용이 되지 않을 때. ) / Library Import Error ( 라이브러리 Import 안될 때. )
출처: https://zluoy.tistory.com/entry/SpringBoot-Gradle-Error-Gradle이-적용이-되지-않을-때-Library-Import-Error-라이브러리-Import-안될-때 [dev_eunz:티스토리]</a></li>
</ul>
</li>
<li><a href="https://velog.io/@kekim20/Spring-Boot-%EB%B9%8C%EB%93%9C%ED%95%98%EC%97%AC-jar%ED%8C%8C%EC%9D%BC-%EC%83%9D%EC%84%B1%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0">빌드하여 jar파일 생성/실행하기</a></li>
<li><a href="https://spring.io/guides/gs/spring-boot-docker">Docker를 사용한 Spring Boot</a></li>
<li><a href="https://adjh54.tistory.com/214">Gradel 버전 확인 및 변경 방법</a></li>
</ul>