<p>오늘은 velog를 GitHub와 연동을 시킬 것이다.
이 둘을 연동시키면 velog에 글을 쓰면 GitHub에 잔디가 심어진다고 해서 도전하게 되었다.
시간 있을 때 잔디 많이 심어둬야지...</p>
<hr />
<h2 id="repository-생성">repository 생성</h2>
<p>GitHub에서 repository를 생성해준다.
이때 <strong>public</strong>으로 만들어줘야한다!
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/12ebe15f-5b1c-49c6-89b6-ef4228054a73/image.png" /></p>
<h2 id="폴더-및-파일-생성">폴더 및 파일 생성</h2>
<pre><code>velog/
├── .github/
│   └── workflows/
│       └── update_blog.yml
├── scripts/
│   └── update_blog.py
└── ...</code></pre><p>이 와 같은 구조의 폴더를 만들어준다.</p>
<p>이 파일을 생성하는 방법은 간단하다.
나의 경우에는 GitHub에서 파일을 만들었다.
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/a6366aca-a2c1-4ad3-8510-ee1307d92ecd/image.png" /></p>
<ol>
<li><ul>
<li>버튼을 누르고, create new file을 클릭한다.</li>
</ul>
</li>
<li>Name your file에 <code>.github/workflows/update_blog.yml</code>을 입력하면 자동으로 그에 맞는 폴더를 만들어준다.</li>
<li>1번을 다시 실행하고 Name your file에 <code>scripts/update_blog.py</code>을 입력한다.</li>
<li>2번과 3번에서 각각 내용을 작성한 뒤 Commit changes를 누른다.</li>
</ol>
<p>이렇게 하면 쉽게 저 구조의 폴더를 만들 수 있다!</p>
<h2 id="github-action-작성">github action 작성</h2>
<p>update_blog.yml에 들어 갈 내용</p>
<pre><code class="language-yml">name: Update Blog Posts


on:
  push:
      branches:
        - [1.브랜치이름]  # 또는 워크플로우를 트리거하고 싶은 브랜치 이름
  schedule:
    # 테스트를 원한다면, `한국 표준시 = UTC + 9` 참고해서 시간 수정한 후 테스트해보기
    - cron: '0 0 * * *'  # 매일 자정에 실행, UTC 협정 세계시 기준 (한국 시간 기준 오전 9시)
    - cron: '0 15 * * *' # 매일 자정에 실행, 한국 시간 기준 (UTC 15:00)

jobs:
  update_blog:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout
      uses: actions/checkout@v2

    - name: Push changes
      run: |
        git config --global user.name 'github-actions[bot]'
        git config --global user.email 'github-actions[bot]@users.noreply.github.com'
        git push https://${{ secrets.GH_PAT }}@github.com/[2.깃허브아이디]/velog.git

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.x'

    - name: Install dependencies
      run: |
        pip install feedparser gitpython

    - name: Run script
      run: python scripts/update_blog.py</code></pre>
<p>브랜치 이름은 update_blog.yml파일 Github에서 작성할 때 
<img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/5914b9ce-3063-437a-823b-304b7b4b73f5/image.png" />
여기서 in 뒤에 보고 수정하면 된다. 나같은 경우에는 main으로 지정했다!</p>
<p>update_blog.py에 들어 갈 내용
<strong><em>velog 아이디 확인 잘 하기</em></strong></p>
<pre><code class="language-python">import feedparser
import git
import os

# 벨로그 RSS 피드 URL
# example : rss_url = 'https://api.velog.io/rss/@rimgosu'
rss_url = 'https://api.velog.io/rss/@[본인벨로그아이디]'

# 깃허브 레포지토리 경로
repo_path = '.'

# 'velog-posts' 폴더 경로
posts_dir = os.path.join(repo_path, 'velog-posts')

# 'velog-posts' 폴더가 없다면 생성
if not os.path.exists(posts_dir):
    os.makedirs(posts_dir)

# 레포지토리 로드
repo = git.Repo(repo_path)

# RSS 피드 파싱
feed = feedparser.parse(rss_url)

# 각 글을 파일로 저장하고 커밋
for entry in feed.entries:
    # 파일 이름에서 유효하지 않은 문자 제거 또는 대체
    file_name = entry.title
    file_name = file_name.replace('/', '-')  # 슬래시를 대시로 대체
    file_name = file_name.replace('\\', '-')  # 백슬래시를 대시로 대체
    # 필요에 따라 추가 문자 대체
    file_name += '.md'
    file_path = os.path.join(posts_dir, file_name)

    # 파일이 이미 존재하지 않으면 생성
    if not os.path.exists(file_path):
        with open(file_path, 'w', encoding='utf-8') as file:
            file.write(entry.description)  # 글 내용을 파일에 작성

        # 깃허브 커밋
        repo.git.add(file_path)
        repo.git.commit('-m', f'Add post: {entry.title}')

# 변경 사항을 깃허브에 푸시
repo.git.push()</code></pre>
<h2 id="pat-권한-받기">PAT 권한 받기</h2>
<ol>
<li>작성 뒤 다시 GitHub 계정에 들어간다.</li>
<li>계정 이미지를 눌렀을 때 나오는 사이드바 Settings를 눌러준다.(repository의 Settings 아님)</li>
<li>내려서 &lt;&gt; Developer Settings 클릭</li>
<li>Personal access tokens (classic) 클릭</li>
<li>Generate new token(classic) 클릭</li>
<li>Note 작성 뒤, repo와 workflow를 선택</li>
<li>Getnerate new token 클릭</li>
<li>토큰 복사(다시 안보이기 때문에 꼭 복사해두기)</li>
<li>velog repository 들어가서 Settings 누르기</li>
<li>Secrets and variables - Actions - Secrets - New repository secret 순으로 클릭</li>
<li>Name에 <code>GH_PAT</code>,  Secret에 <code>발급받았던 토큰</code> 입력</li>
<li>Add Secret 클릭</li>
</ol>
<h2 id="외부-권한-부여">외부 권한 부여</h2>
<ol>
<li>velog repository에 다시 들어간다.</li>
<li>Settings 클릭</li>
<li>Actions에서 General 클릭</li>
<li>Allow all actions and reusable workflows, require approval for all outside collaborators, read and write permissions, Allow GitHub Actions to create and approve pull requests 선택해주고 각각 save버튼을 눌러준다.</li>
</ol>
<h2 id="확인">확인</h2>
<p><img alt="" src="https://velog.velcdn.com/images/ju_hyanghyang/post/1c05556a-4b0a-419d-af3b-6e908d36de2c/image.png" />
완성하면 velog-posts라는 이름의 폴더가 생기고 내가 그동안 업로드했던 게시글들이 .md라는 이름으로 올라가는 것을 확인할 수 있다!</p>
<hr />
<h2 id="출처">출처</h2>
<ul>
<li><a href="https://velog.io/@ryuneng2/GitHub-velog%EC%99%80-GitHub-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0-velog-%EA%B8%80-%EC%9E%91%EC%84%B1-%EC%8B%9C-%EC%9E%90%EB%8F%99%EC%9C%BC%EB%A1%9C-%EA%B9%83%ED%97%88%EB%B8%8C%EC%97%90-%EC%BB%A4%EB%B0%8B%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95">[GitHub] velog와 GitHub 연동하기 (velog 글 작성 시, 자동으로 깃허브에 커밋하는 방법)</a></li>
<li><a href="https://velog.io/@sooozi/velog%EC%99%80-github-%EC%97%B0%EB%8F%99-%EB%B2%A8%EB%A1%9C%EA%B7%B8-%EA%B8%80%EC%93%B0%EA%B3%A0-%EC%9E%94%EB%94%94%EC%8B%AC%EA%B8%B0">velog와 github 연동 : 벨로그 글쓰고 잔디심기</a></li>
<li><a href="https://velog.io/@rimgosu/velog-%EA%B8%80-%EC%9E%91%EC%84%B1-%EC%8B%9C-%EC%9E%90%EB%8F%99%EC%9C%BC%EB%A1%9C-github%EC%97%90-%EC%BB%A4%EB%B0%8B%ED%95%98%EA%B8%B0">velog 글 작성 시, 자동으로 github에 커밋하기</a></li>
</ul>