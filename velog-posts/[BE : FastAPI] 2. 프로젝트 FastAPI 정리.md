<p>1게시글은 강의 내용을 정리했기 때문에 비공개로 처리를 했습니다.</p>
<p>프로젝트가 끝나고 코드를 까먹기 전에 코드 작성했던 것들을 정리해보려고 한다.
나는 FastAPI를 이용하여서 모델 서버를 구축했었다.</p>
<hr />
<h2 id="기본설정">기본설정</h2>
<h3 id="fastapi-파일-구조기본만">FastAPI 파일 구조(기본만)</h3>
<pre><code>FastAPI
├─ app
│  ├─ cert.pem
│  ├─ func.py
│  ├─ key.pem
│  ├─ main.py
│  ├─ vit_func.py
│  ├─ __init__.py
│  └─ routers
│     ├─ dicom_upload_con_test.py
│     ├─ vit_cam.py
│     └─ __init__.py
├─ csv
├─ json
├─ models
├─ MONAI
├─ runs
│  └─ adamw_weight_updated_imagnet_uni_224_bs128_1e-4
├─ .dockerignore
├─ Dockerfile
├─ model.py
├─ requirements.txt
├─ myopenssl.cnf
└─ resnet.py</code></pre><h2 id="모듈화">모듈화</h2>
<h3 id="함수-모듈화">함수 모듈화</h3>
<p> 처음 fastapi에 올릴 모델 코드를 받았을 때, 코드가 너무 길어 가독성이 떨어졌었다.
그래서 함수가 선언된 부분을 분리하였다.
(나의 경우에는 func.py에 모델에 있다.)
분리한 함수 폴더는 함수를 불러올 .py와 같은 위치에 있는 것이 아닌 <strong>main.py와 같은 위치</strong>에 있어야 사용이 가능했다.</p>
<h3 id="router-모듈화">Router 모듈화</h3>
<p> 함수를 모듈화 시켰지만 모든 엔드포인트를 main.py에 넣어서 여전히 코드가 너무 길었다.
springboot에서는 @Controller또는 @RestController를 설정하여 기능별로 엔드포인트를 나눌수 있었는데, FastAPI에서는 어떻게 해야하는 지 알 수 가 없었다.
 방법을 찾아보던 중, FastAPI는 router를 이용하여서 나눌 수 있다는 사실을 알게 되었다.</p>
<p>그래서 기능별로 파일을 나누어주었다.</p>
<p>기능별로 파일을 나누고 기존에는
<code>from fastapi import FastAPI</code> 로 라이브러리를 호출하고
<code>app = FastAPI()</code>로 정의한 뒤 엔드포인트를 정의했는데, </p>
<p>router를 사용해 나누니
<code>from fastapi import APIRouter</code>로 라이브러리를 호출하고
<code>router = APIRouter()</code>로 정의한 뒤 기존 app을 사용하여 정의했던 엔트포인트를 router로 변경해주었다.
그리고 라우터로 엔드포인트를 지정할 때 파일에 있는 라우터에는 같은 이름의 tags이름을 지정해주었다. </p>
<h2 id="router-실행">Router 실행</h2>
<p>Router을 사용하여 모듈화를 시켰는데,
<code>uvicorn 파일이름:app --reload</code>라는 명령어를 사용해서 이전에는 실행시켰는데, 라우터로 나눈 파일들은 어떻게 한번에 돌릴 수 있을까? 고민했다.</p>
<p>나의 경우에는 main.py에 FastAPI를 부르고 라우터를 등록해주었다.
main.py에서는 <code>from fastapi import FastAPI</code>로 라이브러리를 호출하고 <code>app = FastAPI()</code>로 정의했다.
그런 뒤 모듈화시킨 라우터 파일도 불러왔다.</p>
<p>불러온 라우터를 등록을 했는데,
<code>app.include_router(라우터파일이름.router, tags=[&quot;라우터정의할 때 적은 태그이름&quot;])</code>을 사용해 적어주었다.
이때 더 prefix를 사용하면 경로를 더 명확하게 설정해줄 수 있다.</p>
<p>그리고
<code>uvicorn app.main:app --host 0.0.0.0 --port 8000 --ssl-certfile=&quot;app/cert.pem&quot; --ssl-keyfile=&quot;app/key.pem&quot;</code>
이 명령어를 사용하여서 한번의 실행으로 두개의 라우터를 실행해주었다.
이렇게 설정해주면 모든 네트워크 인터페이스에서 8000번 포트로 접속할 수 있다.</p>
<h2 id="cors-에러-해결">CORS 에러 해결</h2>
<p>fastapi를 실행할 때 certfile(인증서)과 keyfile(개인키)을 왜 설정한 이유는 CORS에러를 해결하기 위해서 사용했기 때문이다. </p>
<h3 id="cors란">CORS란?</h3>
<p>브라우저가 다른 도메인에 요청을 보낼 때 보안상의 이유로 접근을 제한하는 것이다.
나의 경우 java web server에서 python ai server로 요청을 보내기 때문에 이를 지정하는 일이 필요했다.</p>
<p>이전 http로 웹서버를 돌릴 때는 필요하지 않지만 https로 통신을 시도하면서 발생하였다.
이때 https로 통신하려면 인증서를 통해 서버의 신뢰성을 검증하는데, 적절하다 판단되지 않으면 cors에러가 발생이 된다.</p>
<h3 id="자체-인증서-발급">자체 인증서 발급</h3>
<p>나는 자체 인증서인 <strong>SSL(Self-Signed Certificate)</strong>을 사용하였다.
자체 인증서는 서버 운영자가 자체적으로 생성한 인증서로, 브라우저나 다른 클라이언트가 기본적으로 신뢰하지 않기때문에 공개 환경에서는 부적합하다. 하지만, 개발환경에서는 간단히 https를 활성화 할 수 있는 방법이기 때문에 나는 SSL 인증서를 생성하였다.</p>
<p>이 인증서들은 main.py와 같은 위치에 있어야 한다.</p>
<h3 id="cors-헤더-추가">CORS 헤더 추가</h3>
<p>그리고 나는 main.py에 CORSMiddleware를 추가하였다.</p>
<pre><code class="language-python">from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

origins = [&quot;https://example.com&quot;] # 허용할 출처 설정

app.add_middleware(
    CORSMiddleware,
    allow_origins=[&quot;*&quot;], # 허용할 출처 목록, &quot;*&quot;는 모두 허락하겠다는 의미
    allow_credentials=True,
    allow_methods=[&quot;*&quot;], # GET, POST 등과 같은 메서드
    allow_headers=[&quot;*&quot;],
)</code></pre>
<p>이를 통해서 cors에러를 해결할 수 있었다!</p>