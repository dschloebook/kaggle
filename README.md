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

