## I. Settings (주 관리자)
- 다음은 Main 관리자가 해야 하는 영역이다. 
- 우선 드라이브와 구글 코랩을 마운트할 수 있도록 다음 코드를 순서대로 실행한다.

```terminal
# Mount Google Drive
from google.colab import drive # import drive from google colab

ROOT = "/content/drive"     # default location for the drive
print(ROOT)                 # print content of ROOT (Optional)
drive.mount(ROOT)           # we mount the google drive at /content/drive
```

```markdown
/content/drive
Go to this URL in a browser: https://accounts.google.com/o/oauth2/auth?client_id=947318989803-6bn6qk8qdgf4n4g3pfee6491hc0brc4i.apps.googleusercontent.com&redirect_uri=urn%3aietf%3awg%3aoauth%3a2.0%3aoob&response_type=code&scope=email%20https%3a%2f%2fwww.googleapis.com%2fauth%2fdocs.test%20https%3a%2f%2fwww.googleapis.com%2fauth%2fdrive%20https%3a%2f%2fwww.googleapis.com%2fauth%2fdrive.photos.readonly%20https%3a%2f%2fwww.googleapis.com%2fauth%2fpeopleapi.readonly

Enter your authorization code:
··········
Mounted at /content/drive
```

- 현재 경로를 확인한다.

```terminal
%pwd
%cd drive/'My Drive'/'Colab Notebooks'
```

```markdown
/content/drive/My Drive/Colab Notebooks
```

- 해당 경로에 `hkit301`폴더를 만드는 것을 추천한다. `mkdir`를 통해서 만들수도 있기도 하지만, 터미널 명령어가 약한 분들을 위해서 사전에 미리 폴더를 만드는 것을 추천한다. 
- `hkit301`로 이동한다. 

```terminal
%cd hkit301
```
```markdown
/content/drive/My Drive/Colab Notebooks/hkit301
```

- 이제 본인의 `git` 계정에 연동하도록 한다.
  + step 1. `git config --global user.name "your_username"`
  + step 2. `git config --global user.email "your_email_address"`
 
```terminal
!git config --global user.name "chloevan"
!git config --global user.email "j2hoon85@gmail.com"
```

- 이제 프로젝트 `Repo`를 다운로드 받는다.
```terminal
!git clone https://github.com/hkit301/kaggle.git
```

```markdown
Cloning into 'kaggle'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
```

- 각각의 파일 작성이 다 끝나면 아래와 같이 코드를 입력한다.

```terminal
# Clone github repository setup
# import join used to join ROOT path and MY_GOOGLE_DRIVE_PATH
from os.path import join  

# path to your project on Google Drive
MY_GOOGLE_DRIVE_PATH = 'My Drive/Colab Notebooks/'

# replace with your github username
GIT_USERNAME = "hkit301"

# definitely replace with your
GIT_TOKEN = "99a6e6cee0faacc6c2b360ba50378a6e5e067fbd" # this is temporary, whenever you add, need to get token number

# Replace with your github repository in this case we want 
# to clone deep-learning-v2-pytorch repository
GIT_REPOSITORY = "kaggle"

PROJECT_PATH = join(ROOT, MY_GOOGLE_DRIVE_PATH)

# It's good to print out the value if you are not sure 
print("PROJECT_PATH: ", PROJECT_PATH)  

# In case we haven't created the folder already; we will create a folder in the project path 
# !mkdir "{PROJECT_PATH}"    

#GIT_PATH = "https://{GIT_TOKEN}@github.com/{GIT_USERNAME}/{GIT_REPOSITORY}.git" this return 400 Bad Request for me
GIT_PATH = "https://" + GIT_TOKEN + "@github.com/" + GIT_USERNAME + "/" + GIT_REPOSITORY + ".git"
print("GIT_PATH: ", GIT_PATH)
```
- `GIT_TOKEN`은 매번 변동하기 때문에 꼭 다시 발급받을 것을 권한다.
	+ 참조할 것: [깃허브 Access Token](https://chloevan.github.io/settings/colab_drive_github_settings/#1-%EA%B9%83%ED%97%88%EB%B8%8C-access-token)

```markdown
PROJECT_PATH:  /content/drive/My Drive/Colab Notebooks/
GIT_PATH:  https://99a6e6cee0faacc6c2b360ba50378a6e5e067fbd@github.com/hkit301/kaggle.git
```

- 이제 아래 코드를 순차적으로 입력한 후 `git push`를 진행한다.

```terminal
!git remote set-url origin "{GIT_PATH}"
!git add *
!git commit -m "commit"
!git push
```

## II. Branch 생성 및 이동 
- 우선 `kaggle` 폴더로 이동한다.  

```bash
%cd kaggle
!ls
```

### (1) 브랜치 생성 (주 사용자만 해당)
- 브랜치 이름을 생성한다. 
- 브랜치 이름은 슬래시(/)를 사용하여 계층적인 구조로 만들어서 사용할 수 있으며, 작성 규칙은 다음과 같다. 
  + 기호(-)로 시작할 수 없다. 
  + 연속적인 마침표(..)를 포함할 수 없다. 
  + 빈간, 공백 문자, 물결(~), 캐럿(^), 물음표(?), 별표(*), 대괄호([]) 등은 포함할 수 없다. 
  + 브랜치 이름은 중복해서 사용할 수 없다. 
- 브랜치 생성 방법은 아래 코드와 같다. 

```bash
!git branch hajin # jongmin or seongsik
```

### (2) 브랜치 확인
- 브랜치 목록을 확인하는 방법은 매우 간단하다. 

```bash
!git branch 
```
```
  hajin
  jongmin
* master
  seongsik
```
- 여기에서 `별표(*)`는 현재 선택된 브랜치를 의미한다.
- 브랜치의 세부 사항을 확인하기 위해서는 `git branch -v`를 실행한다. 

```bash
!git branch -v
```
```bash
  hajin    cc21763 commit
  jongmin  cc21763 commit
* master   cc21763 commit
  seongsik cc21763 commit
```

### (3) 브랜치 이동 및 작업 예제
- checkout 명령어는 호텔에서 퇴실할 때의 체크아웃을 떠올리면 이해하기 쉬울 것이다. 
- 지금 현재 `master` 상태에서 이제 각각의 브랜치로 이동하도록 한다. 
- 이 때, 중요한 것은 팀프로젝트이지만, 각각의 폴더로 이동 후 `git checkout` 을 실행하는 것을 권한다. 
- 우선 `hajin`의 예를 들면 다음과 같다. 
  + 먼저 구글 코랩 `CELL`안에서 `%cd hajin` 실행하여 이동한다. 
  
```bash
%cd hajin/
!ls
```

- 실제로 이동이 되었는지 확인한다. 

```bash
%pwd
```

- 이제 `git checkout hajin`을 실행한다.
```bash
!git checkout hajin
```
```markdown
M	hkit301.ipynb
D	setting.ipynb
D	sungsik/sungsik_WBS.md
Switched to branch 'hajin'
```
- `Switched to branch 'hajin'`으로 변경된 것을 확인할 수 있다. 
- 변경된 브랜치에서 작업하면 된다. 
- 간단하게 `temp.ipynb`를 생성했다. 


### (4) 원격 저장소에 push 하기
- 현재 로컬에서만 `branch`를 생성한 상태이기 때문에 아래 명령을 입력해서 upstream branch로 만들어준다. 
- master의 remote 정보를 새로운 브랜치에도 그대로 가져온다.

```bash
!git push --set-upstream origin hajin
```
```markdown
Total 0 (delta 0), reused 0 (delta 0)
remote: 
remote: Create a pull request for 'hajin' on GitHub by visiting:
remote:      https://github.com/hkit301/kaggle/pull/new/hajin
remote: 
To https://github.com/hkit301/kaggle.git
 * [new branch]      hajin -> hajin
Branch 'hajin' set up to track remote branch 'hajin' from 'origin'.
```

- 이렇게 한번 `upstream`을 진행한 이후에는 `git add .`와 `git commit -m "your_message"` 명령어만 입력하면 된다. 

```bash
!git add .
!git commit -m "hajin commit"
```

```markdown
[hajin e91d409] hajin commit
 1 file changed, 1 insertion(+)
 create mode 100644 hajin/temp.ipynb
```

### (4) 브랜치 병합 및 마지막 커밋(주 사용자가 실행)
- 이제 `checkout master`로 들어간 이후에 병합과 최종 push를 진행한다.
- `git merge`를 할 때에는 꼭 자신의 `branch 이름`을 명기해야 한다. 
  + `!git merge hajin`
  + `!git merge jongmin`
  + `!git merge seongsik`
  
```bash
!git checkout master
!git merge hajin
```

```markdown
M	hkit301.ipynb
D	setting.ipynb
D	sungsik/sungsik_WBS.md
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
Updating cc21763..e91d409
Fast-forward
 hajin/temp.ipynb | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 hajin/temp.ipynb
```

- 이제 최종적인 `push`만 남았다. 

```bash
!git push origin master
```

```markdown
Counting objects: 4, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 593 bytes | 148.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/hkit301/kaggle.git
   cc21763..e91d409  master -> master
```