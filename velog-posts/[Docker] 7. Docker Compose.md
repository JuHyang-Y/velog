<h2 id="버전-기록">버전 기록</h2>
<p>docker compose 를 이용해서 웹을 배포해보려 한다.
우선, 로컬 환경 버전이다.</p>
<ul>
<li><p><strong>GPU 환경</strong>(모델 학습할 때만 사용)
  PyTorch 2.3.1 (Python 3.10.13, CUDA 11.8, cuDNN 8.9.7)</p>
</li>
<li><p><strong>FastAPI 환경</strong>
  Anaconda 가상환경- 실행 명령어 : conda activate MR
  python : 3.10.13 → torch 2.4.1+cpu / ultralytics 8.3.9
  FastAPI version : 0.115.0
  FastAPI CLI version : 0.0.5</p>
</li>
<li><p><strong>Spring Boot 환경</strong>
  Project : Maven
  Language : Java
  Spring Boot : 3.3.4
  Project Metadata 나머지는 다 기본값
  Project Metadata - Packaging : Jar
  Project Metadata - Java : 17</p>
</li>
<li><p><strong>MariaDB</strong> </p>
</li>
</ul>
<p>10.5</p>
<h2 id="docker-desktop-확인-및-wsl설치">docker desktop 확인 및 wsl설치</h2>
<p>docker compose를 위해 docker desktop 설치가 필요하다.
나는 저번에 설치를 완료했기 때문에,</p>
<p>cmd화면에서</p>
<pre><code>docker -v
docker-compose -v</code></pre><p>를 입력하여 두개의 버전을 확인했다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/e1176b4a-9c68-42cd-8c52-f73492db2202/image.png" /></p>
<p>그리고 설치를 위해서 wsl을 다운 받았어야 했는데, 
Microsoft Store에도 접근이 안되고,
powershell에서 
wsl -- install 도 액세스가 거부되었다고 뜨는 것이다...
아니 어떻게 다운을 받아서 compose를 하라는 거야...
시작부터 안되면 어쩌라는 거야....</p>
<p>이렇게 하는 도중 선생님께 도움을 요청하였더니 바로 해결이 되었는데,
Powershell에서 </p>
<pre><code>wsl --install --web-download Ubuntu-22.04</code></pre><p>를 입력했더니 Ubuntu 22.04 LTS가 설치 되었따...
뭐야..</p>
<p>ubuntu가 실행이 되어서 sudo apt-get update 를 실행했다.</p>
<h2 id="docker-file과-build">Docker File과 build</h2>
<h3 id="spring-boot-docker-file만들기">Spring boot docker file만들기</h3>
<p>spring boot에서 docker compose기능을 사용하기 위해서는 dependency를 추가해야한다고 한다. pom.xml에서 이 의존성을 추가한다.</p>
<pre><code>&lt;dependency&gt;
     &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
     &lt;artifactId&gt;spring-boot-docker-compose&lt;/artifactId&gt;
     &lt;optional&gt;true&lt;/optional&gt;
&lt;/dependency&gt;</code></pre><p>도커에 올릴 .jar파일을 만들기로 했다.
저번에 gradle로 만들었는데, maven으로 바꾸면서 다시 시도하였다.</p>
<ol>
<li>cmd에 들어가서 pom.xml 파일이 있는 경로까지 이동한다.</li>
<li>maven의 경우 아래의 명령어를 입력하여 .jar 파일을 만든다.<pre><code>./mvnw package &amp;&amp; java -jar target/gs-spring-boot-docker-0.1.0.jar</code></pre><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/4c6c72d3-3d7c-450d-b507-3c896f020e69/image.png" /></li>
</ol>
<p>파일이 만들어진 것도 확인했다
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/d3821f84-a324-4c0d-a7db-6f1d9af960b1/image.png" /></p>
<p>그런 뒤 root파일에서 그냥 file형식으로
dockerfile을 생성해준다.</p>
<pre><code>FROM openjdk:17-jdk-alpine

# 애플리케이션 JAR 파일 경로 설정
ARG JAR_FILE=target/*.jar

# JAR 파일 복사
COPY ${JAR_FILE} app.jar

# 애플리케이션 실행
ENTRYPOINT [&quot;java&quot;,&quot;-jar&quot;,&quot;/app.jar&quot;]

# 필요 포트 공개
EXPOSE 8443</code></pre><p>나의 경우 https를 사용할 때 propertise에서 port 번호를 8443으로 지정해줬기 때문에 필요 포트를 같이 작성해주었다.</p>
<p>docker파일이 다 작성되면 cmd창에 아래의 명령어를 입력한다.</p>
<pre><code>docker build -t DockerHub아이디/제목:태그 .
docker run -p 8443:8443 DockerHub아이디/제목:태그</code></pre><p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/beee529a-9f18-4c7f-ae07-e8bf1c079a46/image.png" />
실행된 것을 확인한 후에</p>
<p><code>https://localhost:8443/index</code>를 입력하여 결과가 뜨는지 확인한다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/1804ebd6-75c6-4d97-9939-068a460ebd7c/image.png" /></p>
<p>오우 실행되었다!</p>
<h3 id="fastapi-docker-file-만들기">FastAPI docker file 만들기</h3>
<p>spring boot와 마찬가지로 root 폴더에 docker file을 만든다.
놀랍게도 pycharm에서 하고 있는데 dockerfile 형식을 지원한다.ㅋㅋㅋㅋㅋ
내가 eclipse에서 발견을 하지 못한 것인가..?</p>
<pre><code>FROM python:3.10.13
# 작업 디렉토리 생성
WORKDIR /app

# 필요한 파일 복사
COPY requirements.txt .

# 패키지 설치
RUN pip install --no-cache-dir -r requirements.txt

# 애플리케이션 코드 복사
COPY . .

# FastAPI 실행 명령어
CMD [&quot;uvicorn&quot;, &quot;app.main:app&quot;, &quot;--port&quot;, &quot;8000&quot;, &quot;--ssl-certfile&quot;, &quot;app/cert.pem&quot;, &quot;--ssl-keyfile&quot;, &quot;app/key.pem&quot;]

# 필요 포트 공개
EXPOSE 8000</code></pre><p>이렇게 작성하고, </p>
<p>requirements.txt가 없어서 어떻게 하지 했는데,
프롬프트 창에서</p>
<pre><code>pip freeze &gt; requirements.txt</code></pre><p>를 입력하면 내가 사용하고 있는 패키지들이 기록이 된다.
이제 docker이미지를 빌드해보도록 하겠다.</p>
<p>cmd창에서 fastapi가 있는 경로로 이동 후 </p>
<pre><code>docker build -t 이미지이름:태그 .
docker run -p 8000:8000 이미지이름:태그</code></pre><p>를 입력하여 실행이 되는 지 확인했다.</p>
<p><strong>(중요) Docker 이미지 빌드할 때 이미지 제목 형식은 &quot;DockerHub아이디/제목:태그&quot; 형식으로 build 해야 Hub에 푸시할 수 있다.</strong></p>
<h4 id="주의">주의</h4>
<p>처음에 FastAPI이미지를 빌드하는데, 바로 run이 실행되지 않고 run ~~ bash로 들어가서 uvicorn명령어를 실행시켜줘야만 친구가 돌아가는 것이다.</p>
<p>dockerfile에서 문제가 발생한 것 같은데 아무리 수정해도 바뀌지 않아서 너무 답답했었는데, 이미지를 빌드할 때 캐시가 남아있어서 아무리 바꿔봐도 같은 문제가 반복되었던 것 같다.</p>
<p>멘토님께 문제에 대해 물어봤더니, no cache를 써보라고 하셨고, 명령어를 사용했더니 해결이 되었다!!</p>
<pre><code>docker build --no-cache -t 이미지이름:태그 .</code></pre><p>이 명령어를 통해서 기존 빌드에 사용된 캐시를 사용하지 않고 이미지를 빌드 할 수 있다.</p>
<h2 id="docker-compose">Docker compose</h2>
<h3 id="docker-hub-push">docker hub push</h3>
<p>먼저 docker hub에 아까 만든 이미지들과 이름이 같은 Repositories들을 만들어준다.</p>
<p>그런 뒤,</p>
<pre><code>docker push 이미지이름:태그</code></pre><p>를 입력해준다.(태그는 따로 지정하지 않으면 latest로 들어간다.)
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/898489a8-2c3b-4a73-bea5-f47941071eea/image.png" /></p>
<p>사진을 보면 hub에 올라간 것을 확인할 수 있다.</p>
<h3 id="docker-compose-여부">docker compose 여부</h3>
<p>docker compose가 있는지 확인하기 위해</p>
<pre><code>docker-compose -v</code></pre><p>를 입력하여 확인해준다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/b7892c56-4e8e-4b67-88d0-a5233403de68/image.png" /></p>
<h3 id="docker-composeyml파일-만들기">docker compose.yml파일 만들기</h3>
<p>yml파일을 만드려고 하는데, 위치를 어디에 만들어야하지? 고민이 되었다.
그러나 Docker Hub에 이미지를 올렸다면, yml파일 위치는 크게 상관이 없다고 한다!
docker-compose.yml</p>
<pre><code>version: &quot;3.8&quot;
services:
  spring-boot:
    image: 이미지이름:태그
    ports:
      - &quot;포트 번호&quot;

  fastapi:
    image: 이미지이름:태그
    ports:
      - &quot;포트 번호&quot;
</code></pre><p>을 만들어서 저장하였다.
그런데, 이렇게만 지정하면 내가 저장한 데이터 저장할 데이터들이 모두 삭제가 된다.</p>
<p>그래서 더 찾아보았더니 volume이라는 개념이 존재했다.
컨테이너 내부의 데이터를 외부로 링크를 걸어주는 기능이라고 한다.</p>
<h3 id="volume추가">Volume추가</h3>
<p>docker의 volume을 만들어보도록 하자</p>
<pre><code>docker volume create 볼륨이름</code></pre><p>잘 만들어졌는지 확인하려면
<code>docker volume ls</code> 를 입력해서 확인하면 된다.</p>
<p>그리고 yml파일에 volume을 추가해준다.</p>
<pre><code>version: &quot;3.8&quot;
services:
  spring-boot:
    image: 이미지이름:태그
    ports:
      - &quot;포트 번호&quot;
    volumes:
      - 볼륨이름:docker volume컨테이너 경로 # Docker Volume을 컨테이너 경로에 마운트

  fastapi:
    image: 이미지이름:태그
    ports:
      - &quot;포트 번호&quot;

volumes:
  볼륨이름:
    driver: local</code></pre><p>그리고 나는 이 과정에서 spring boot에 지정해주었던 경로가 바뀌어서 jar파일을 다시 만들고, 이미지도 다시 빌드하여 compose를 해줬다.</p>
<h3 id="docker-compose-1">docker compose</h3>
<p>이제 진짜 진짜 진짜로 docker compose를 할 차례이다.
먼저, yml파일을 만들었던 위치로 이동하여 cmd(or PowerShell)를 실행시키고 docker hub의 로그인을 실행해준다.</p>
<pre><code>docker login</code></pre><p>그 후 hub에 올라갔던 이미지를 토대로 compose를 해준다.</p>
<pre><code># 이미지 다운로드 및 실행
docker-compose up -d

# 실행 상태 확인
docker-compose ps

# 로그 확인
docker-compose logs</code></pre><p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/25bcb396-344a-4c5b-956b-803c9f0c7445/image.png" />
도커 desktop을 확인해보면, docker-compose 밑에 두개의 컨테이너가 돌아가고 있는 것을 확인할 수 있다.</p>
<hr />
<h2 id="출처">출처</h2>
<ul>
<li><a href="https://docs.docker.com/compose/">dockerdocs</a></li>
<li><a href="https://languagestory.tistory.com/126">윈도우 환경에서 docker, docker-compose 설치하기</a></li>
<li><a href="https://youtu.be/cMyoSkQZ41E?si=M5PyXGg75XgkDFOB">Run Docker in Windows</a></li>
<li><a href="https://spring.io/guides/gs/spring-boot-docker">Spring Boot with Docker</a></li>
<li><a href="https://fastapi.tiangolo.com/deployment/docker/#docker-cache">FastAPI in Containers - Docker</a></li>
<li><a href="https://hello-judy-world.tistory.com/57">Docker, Docker compose를 이용한 개발 환경 구축</a></li>
<li><a href="https://ohju.tistory.com/607">캐시를 이용한 이미지 빌드</a></li>
</ul>