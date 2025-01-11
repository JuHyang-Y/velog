<p>오랜만에 돌아왔습니다!
오늘은 GitHub의 readme에 대해 제가 공부한 내용과 이것을 꾸미는 방법을 설명해드리도록 하겠습니다.</p>
<hr />
<h1 id="readme">README?</h1>
<h2 id="정의">정의</h2>
<p>주변에서 GitHub에 코드를 올려서 관리해야한다고 하고, readme를 작성해주라고 하고...
대체 그 readme가 무엇인지 도통 알 수 없었다..
readme는 쉽게 <strong>설명서 또는 안내문</strong> 이라고 이해할 수 있었는데, 내가 등록한 Repository에 대한 설명(ex. 프로젝트에 대한 설명)을 작성하는 곳이다.</p>
<p>readme.md라는 확장자를 사용하는데, 작성형식(?)은 의외로 velog작성법이랑 유사한 것 같아서 작성하는 내내 좀 익숙했다.
나의 경우 초반에 readme를 작성하지 않고 repository를 만들었는데, 그냥 일반 .txt파일을 만들고 나중에 확장자를 .md로 바꾸니 readme로 설정이 되었다.</p>
<h2 id="필요성">필요성</h2>
<p>readme에는 무슨 내용이 들어가야 하나...? 싶어서 공부를 했다.</p>
<h3 id="readme를-작성하는-이유">readme를 작성하는 이유</h3>
<p>이유는 2가지였는데,</p>
<ul>
<li>나중에 코드를 회고할 때</li>
<li>다른 사람들이 해당 repository를 확인했을 때 조금 더 쉽게 프로그램을 이해할 수 있게 하기 위해
라는 이 두 가지로 생각해 볼 수 있었다. (약간 주석다는 이유와 비슷하다고 느낌)</li>
</ul>
<h3 id="들어갈-내용">들어갈 내용</h3>
<p>그럼 어떤 내용이 들어가야 좋을까? 생각을 해봤을 때</p>
<ul>
<li>프로젝트 소개</li>
<li>개발 기간</li>
<li>개발 환경</li>
<li>기술 스택</li>
<li>프로젝트 구성</li>
<li>프로젝트 버전 내용</li>
<li>... 등
을 작성하면 좋을 거 같다 생각을 했는데, 정해진 양식은 없기에 원하는 내용을 추가하거나 생략해서 작성했다.</li>
</ul>
<h2 id="꾸미기aka-리꾸">꾸미기(AKA 리꾸)</h2>
<p>그런데, 이 readme가 작성하다보니깐 좀더 깔끔하게 꾸미고 싶은 욕구가 샘솟았습니다.
그래서 몇 가지 방법을 찾았다.</p>
<h3 id="readme-편집">readme 편집</h3>
<p>readme를 가지고 있지 않다면 GitHub 화면에서 
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/6524dc8b-76dd-42e7-acb9-88a1f68ec22b/image.png" />
이런 화면을 볼 수 있다.</p>
<p>저기에 Add a README를 클릭하여 readme를 작성하거나 확장자를 readme.md로 한 뒤
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/fd8ab122-38f1-4a87-ab0d-73da30d2fce9/image.png" />
이 화면에서 연필 모양의 버튼을 클릭하여 readme를 편집할 수 있었다.</p>
<p>다 편집한 뒤 어떻게 보이는 지 미리 보고 싶을 땐 Edit file 옆의 Preview를 툴러 확인할 수 있다.</p>
<h3 id="기술-아이콘-뱃지">기술 아이콘 뱃지</h3>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/d73bd78f-5f28-40f7-b1aa-471181868af6/image.png" />
이런 식으로 사용 기술을 적을 때 뱃지를 사용하면 더 눈에 잘 들어오게 작성할 수 있는데, 
<a href="https://simpleicons.org/">Simple Icons</a>
이 사이트에서 아이콘의 이름과 색상코드를 가져올 수 있었다.</p>
<p>예시) python</p>
<pre><code>&lt;img src=&quot;https://img.shields.io/badge/python-3776AB?style=for-the-badge&amp;logo=python&amp;logoColor=white&quot;&gt;</code></pre><p>좀 더 풀어서 설명하자면</p>
<pre><code>&lt;img src=&quot;https://img.shields.io/badge/기술아이콘이름-색상코드('#' 붙은 거 지우고 넣어야 됨)?style=for-the-badge&amp;logo=기술아이콘이름&amp;logoColor=글자색&quot;&gt;</code></pre><p>이 경우에는 html 문법을 사용하는데, velog처럼 마크다운 형식만을 취하다가 여기서는 달리 나와서 조금 당황했지만 꾸미고나니 깔끔해서 보기 나중에는 재미가 붙었던 것 같다.
만약 옆으로 붙여서 넣는게 아니라 다음줄로 넘겨서 작성하고 싶다면 <code>&lt;br&gt;</code> 태그를 넣어주면 된다.</p>
<h3 id="이모지">이모지</h3>
<p>이모티콘도 넣어주고 싶었는데, 이 방법은 노션이랑 똑같은 방법으로 넣을 수 있었다.
나는 보통 <code>. + window</code> 또는 <code>ㅁ + 한자</code> 이 조합을 사용해서 넣었는데, 안먹어서 찾아보았더니 <code>:이모지이름</code> 의 방법으로 작성할 수 있었다.
:book → 📖</p>
<p><a href="https://inpa.tistory.com/entry/MarkDown-%F0%9F%93%9A-Emoji-%EC%9D%B4%EB%AA%A8%ED%8B%B0%EC%BD%98-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0">마크다운 emoji 이모티콘 사용하는 방법</a>
이 사이트를 참고하여 원하는 이모지 이름을 찾을 수 있었다.</p>
<h3 id="사진-영상-첨부">사진, 영상 첨부</h3>
<p>그리고 사진이랑 영상을 넣고 싶었는데, 바로 붙여넣기가 안되길래 또 찾아보았다.(영 귀찮다..)</p>
<h4 id="사진">사진</h4>
<p>순서는 </p>
<ol>
<li>GitHub repository 에 들어가면 있는 Code버튼 바로 옆의 Issues 버튼을 클릭한다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/b4149619-e29e-47e1-b1cc-b204cc3454f9/image.png" /></li>
<li>그 다음 New issue를 누른다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/b474a4d7-4107-4b18-b308-046ea139222f/image.png" /></li>
<li>업로드 하고자 하는 이미지를 Add a description 란에 드래그 해준다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/8fb9c79c-f3d2-44d8-9202-6f424987e71e/image.png" /></li>
<li>그럼 나중에 <code>[사진이름](링크)</code>이런 형식의 문자열이 나온다.</li>
<li>문자열을 복사해서 readme 안에 붙여넣기를 하면 preview로 확인했을 때 이미지가 보이는 것을 확인할 수 있다!</li>
</ol>
<h4 id="영상">영상</h4>
<p>영상의 경우에는 같은 방법을 사용해도 되지만, readme파일에 바로 업로드가 가능한 것 같았다.
여기에는 최대 10MB의 크기만 올라가는데 내가 올리고 싶은 영상의 크기가 커서 압축을 해주었다.</p>
<p><a href="https://www.freeconvert.com/gif-compressor">GIF Compressor</a>
mp4형식도 안된다고 해서 gif형식으로 변환해서 압축을 했는데, 최근에는 mp4형식으로도 업로드가 되는 거 같다...ㅎㅎ</p>
<h2 id="마무리">마무리</h2>
<p>이 외에도 다양한 방법이 존재하나, 내가 이번에 주로 사용한 방식을 기록했다. 나머지 방법은 velog나 notion과 작성방법이 비슷해서 따로 남기진 않았다.</p>
<p>개인적으로 GitHub에 대해서 아무것도 몰랐던 사람으로, 이번 기회에 조금씩 친해져 가는 것(?) 같은 기분이 들었는데, 착각이려나..?
 왜냐면 GitHub는 코드 관리때문에 history가 남는데, 이를 위해서 public으로 전환 시 중요한 정보(ex. 인증키)는 미리 검토하고 업로드 해야 한다는... 기초적인 지식을 몰랐던 개큰 바보 였기에...
pycache를 지우고 올려줘야 한다던지... 정말 아무것도 몰랐던 나부랭이에서 성장한 기분이었다!</p>
<hr />
<h1 id="출처">출처</h1>
<ul>
<li><a href="https://velog.io/@gmlstjq123/Readme.md-%ED%8C%8C%EC%9D%BC-%EC%9E%91%EC%84%B1%EB%B2%95">Readme.md 파일 작성법</a></li>
<li><a href="https://jjinueng.tistory.com/entry/Github-%EA%B9%83%ED%97%88%EB%B8%8C-%EB%A6%AC%EB%93%9C%EB%AF%B8-%EA%BE%B8%EB%AF%B8%EA%B8%B0-%EC%B4%9D%EC%A0%95%EB%A6%AC-README-A-to-Z">깃허브 리드미 꾸미기 총정리 README A to Z</a></li>
<li><a href="https://inpa.tistory.com/entry/MarkDown-%F0%9F%93%9A-Emoji-%EC%9D%B4%EB%AA%A8%ED%8B%B0%EC%BD%98-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0">마크다운 emoji 이모티콘 사용하는 방법</a></li>
<li><a href="https://worthpreading.tistory.com/83">Github Readme에 이미지 올리기</a></li>
</ul>