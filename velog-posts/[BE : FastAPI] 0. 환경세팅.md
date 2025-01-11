<p>ViT모델을 Spring Boot와 통신시킬 때 사용할 FastAPI에 대해서 공부하려고 한다.
인프런에서 첫 수업 25% 할인해주길래 88000원강의 66000원에 결제했다!
그런데 동시접속이 안된다니.. 실망쓰~~!</p>
<hr />
<h2 id="환경설정">환경설정</h2>
<h3 id="1-파이썬-설치하기">1. 파이썬 설치하기</h3>
<p>수업에서는 최신 버전의 파이썬을 설치했지만, 나의 경우 이미 깔려있는 파이썬이 있어서 그걸 이용하기로 했다.</p>
<p><a href="https://www.python.org/">https://www.python.org/</a> 파이썬 설치는 링크를 타고 들어가서 하면된다!</p>
<p>파이썬 버전을 확인하는 방법은
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/51a6f6a9-89a4-453a-9f96-fedd38caad9d/image.png" />
cmd창을 연 뒤</p>
<pre><code>python</code></pre><p>을 입력하면 python프롬프트와 함께 python version 이 출력이 된다.
현재는 3.12.4버전이 설치된 것을 확인할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/d42ba73f-8e13-4041-9c39-0b8dace6327b/image.png" />
그런데 우리 팀의 경우 모델을 학원에서 제공해주는 GPU환경에서 만들기 때문에 그 환경의 python과 버전을 맞추기로 했다.
<del>CUDA를 보니 학부연구생 시절 GPU환경 맞추려고 엄청 고생했던 기억이 난다...(따흫)</del>
<del>그 당시 window11에서는 되지 않는다는 것을 몰랐던 나는...</del></p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/7c662920-3407-4ea6-b75d-dfa79a6be692/image.png" />
root에서의 버전충돌을 막기위해서 anaconda에서 가상환경을 만들었다.
그런데 gpu에서 설정할 수 있는 python버전이 gpu버전과 맞지 않아서 prompt에서 다시 재설정을 하기로 했다.</p>
<p>Anaconda Powershell Prompt를 실행시키고</p>
<pre><code>conda activate 가상환경이름</code></pre><p>navigator에서 만든 가상환경을 실행시키고,</p>
<pre><code>conda list</code></pre><p>어떤 것들이 가상환경 안에 설치되어있는지 확인한다.</p>
<pre><code>conda install python=원하는버전</code></pre><p>python을 재설치한 뒤</p>
<pre><code>conda list</code></pre><p>다시 확인을 한다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/16597397-9294-4161-8acb-fef3a1a0a3d1/image.png" /></p>
<p>가상환경의 python버전과 gpu상의 python버전을 맞췄다.</p>
<pre><code>conda deactivate</code></pre><p>가상환경에서 나오고 싶을 때 입력한다.</p>
<h3 id="2-ide-설치하기">2. IDE 설치하기</h3>
<p>Anaconda를 이용하여 진행할 예정이다.</p>
<p>분명 깔았는데, Anaconda navigator가 실행이 되지 않아서 찾아보았다.
Anaconda Powershell Prompt를 실행한 뒤</p>
<pre><code>conda install anaconda-navigator</code></pre><p>실행하여 재설치를 진행하고</p>
<pre><code>anaconda-navigator</code></pre><p>네비게이터를 실행한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/21454525-fafe-461f-b912-5fd7bea70857/image.png" />
네비게이터가 정상적으로 실행된 것을 확인할 수 있었다.</p>
<p>근데 강의에서 PyCharm을 사용했기 때문에, PyCharm을 설치해보도록 하겠습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/215755f5-984a-46f1-a3c5-6d092f8f39f2/image.png" />
install을 누르면 
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/b8ce23d6-4443-4c39-9512-dfc955f4e959/image.png" />
홈페이지로 이동하고 Developer Tools -&gt; pycharm을 누른뒤</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/ec716230-d024-4c62-bc1d-3031ac2017eb/image.png" />
다운로드를 클릭하고 밑으로 내리면 Community Edition이 나온다!
이걸로 다운을 받아준다.</p>
<p>폴더에서 .exe 파일을 실행시켜주고
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/7f62ad1a-a11e-4d38-b69f-81a9e0927a62/image.png" />
설치를 진행해준다.</p>
<p>나머지는 다 기본으로 설정되어있는대로 넘겼다.</p>
<p>단,
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/256885e5-6d40-4f50-8a77-41ec0b0abdcd/image.png" />
설치 옵션은 모두 체크를 눌러서 진행해주었다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/0c7ffd28-122b-4fb1-a084-259d21bf9a72/image.png" />
설치가 완료되었다!</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/8bdfd8b7-3f52-4812-acee-0c644d10add8/image.png" />
아나콘다 환경에서 pycharm community를 실행한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/975e4fb0-6c07-49dd-abff-96ac84ba526f/image.png" />
새로운 프로젝트를 생성해준다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/cf4bdd0c-90bd-40cf-8a69-8afdc9026f1c/image.png" />
이런 화면을 볼 수 있다.
이곳에 FastAPI 애플리케이션을 만들고 테스트를 한다고 한다!</p>
<h2 id="fastapi">FastAPI</h2>
<h3 id="fastapi-설명">FastAPI 설명</h3>
<ul>
<li>FastAPI는 웹 프레임워크, ASGI를 따른다.</li>
<li>파이썬에서 비동기 웹 서버와 웹 애플리케이션 간의 인터페이스 표준</li>
<li>주요 특징<ul>
<li>비동기를 지원한다.</li>
<li>HTTP, WebSocket, gRPC와 같은 다른 프로토콜을 지원한다.</li>
<li>다양한 서버 및 프레임워크와 호환이된다.</li>
</ul>
</li>
</ul>
<h3 id="fastapi-설치">FastAPI 설치</h3>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/1a66d6fb-7167-4afa-b352-6e07e89d085e/image.png" />
PyCharm에서 프로젝트를 우클릭하고 new -&gt; python file을 선택해 파이썬 파일을 만들어준다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/e76d15fe-c87a-4e3d-9830-ae987eb5cca2/image.png" />
파이썬 파일을 만들고 </p>
<pre><code class="language-python">from fastapi import FastAPI</code></pre>
<p>FastAPI를 부르면 설치가 되지않기 때문에, FastAPI를 설치해주어야한다.</p>
<p>터미널 창을 열고</p>
<pre><code>pip install fastapi uvicorn</code></pre><p>fastapi와 uvicorn을 설치해준다.(uvicorn은 ASGI의 서버이다.)
그리고 확인을 하면 정상적으로 실행이 되는 것을 볼 수 있다!</p>
<h3 id="fastapi-실습">FastAPI 실습</h3>
<p>그리고 빠르게 FastAPI를 이용한 실습을 진행하였다.</p>
<pre><code class="language-python"># 어떤 url로 요청이 되었을 때 어떤 함수가 실행될지 실습

# FastAPI를 호출한다.
from fastapi import FastAPI

# FastAPI 클래스를 이용하여 앱 객체를 만든다.
app = FastAPI()

# root 경로에 대해 get방식으로 요청하면 아래에 있는 함수를 실행하라
# async는 비동기 형식으로 처리하라는 의미
# 요청 방식 : get, post, put
@app.get(&quot;/&quot;)
async def read_root():
    return {&quot;Hello&quot;:&quot;World&quot;} # json형식으로 반환


# 경로에 {}를 넣으면 경로에 값이 포함되는 것을 의미 -&gt; 경로매개변수 또는 패스베리어블
# q는 일반 매개변수(쿼리매개변수)라 한다.
# get방식은 일반매개변수를 받을 수 있다. -&gt; 기본값을 지정할 수 도 있다.
@app.get(&quot;/item/{item_id}&quot;)
async def read_item(item_id: int, q: str=None): # 뒤에 전달되는 변수를 지정
    return {&quot;item_id&quot;:item_id, 'q':q}
</code></pre>
<h3 id="fastapi-실행">FastAPI 실행</h3>
<ol>
<li>메뉴에서 실행</li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/50c5a41c-32f5-4759-b892-b291712c5819/image.png" />
메뉴에서 -&gt; 실행(RUN) -&gt; 파일이름.py(main.py)를 눌러서 실행시킨다.</p>
<ol start="2">
<li>터미널에서 실행
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/4f767bf7-8baf-426d-ad07-2e906f695231/image.png" /><pre><code>uvicorn 파일이름:app --reload</code></pre></li>
</ol>
<p>--reload를 같이 입력하면 서버가 바뀌었을 때 자동으로 재실행을 해준다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/955197a0-6200-447f-8dc1-a8f71a86517c/image.png" />
링크의 기본 경로로 들어가면 확인할 수 있는 화면
연결된 링크로 들어가면 아래와 같은 화면이 뜨는 것을 확인할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/73091add-b7a0-4531-9f06-20058e72885d/image.png" />
그리고 하나 더 만들어주었던 페이지에 접속했을 때도 정상적으로 작동하는 것을 확인할 수 있다.
경로에 값을 입력하고 ?는 쿼리파라미터를 전송할 때 url뒤에 붙여서 사용한다.</p>
<hr />
<h2 id="출처">출처</h2>
<ul>
<li><a href="https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%ED%8C%8C%EC%9D%B4%EC%8D%AC-ai-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8/dashboard">자바 스프링 부트 프로젝트와 파이썬 AI 프로젝트 연결하기</a></li>
<li><a href="https://www.inflearn.com/community/questions/898715/%EB%A7%A5%EC%97%90%EC%84%9C-%EC%84%A4%EC%B9%98-%EC%99%84%EB%A3%8C-%ED%9B%84-%EC%95%84%EB%82%98%EC%BD%98%EB%8B%A4-%EB%84%A4%EB%B9%84%EA%B2%8C%EC%9D%B4%ED%84%B0-%EC%8B%A4%ED%96%89%EC%9D%B4-%EC%95%88%EB%90%A9%EB%8B%88%EB%8B%A4-%E3%85%A0%E3%85%A0">아나콘다 네비게이터 실행 안될 때</a></li>
<li><a href="https://oceanlightai.tistory.com/25">python 기초(가상환경에 파이썬 설치하기)</a></li>
</ul>