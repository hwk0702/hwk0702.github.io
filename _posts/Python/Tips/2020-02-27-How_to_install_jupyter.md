---

layout: post

title: "Jupyter notebook"

date: 2020-02-27 17:28:07

categories: [Python/Tips]

description:

image: /img/jupyter.png

published: true

canonical_url:

---

Jupyter notebook 설치 및 실행 방법
==================================

-	본 설치 방법은 Linux 기반 설치 방법입니다.

#### Anaconda의 jupyter notebook을 이용시에 [0번 목차](#0-anaconda-설치-및-실행-일반-python에서-jupyter-notebook-이용-시에는-생략) 부터

#### Anaconda 설치 없이 jupyter notebook을 이용시에는 [1번 목차](#1-pip-사용) 부터 따라서 진행하시면 됩니다.

---

0. Anaconda 설치 및 실행 (일반 python으로 jupyter notebook 이용 시에는 생략)
----------------------------------------------------------------------------

#### Anaconda 설치 파일 다운로드

아래의 코드를 입력하여 Anaconda 설치 파일을 다운 받습니다. 설치 전에 아나콘다 버전을 확인 후에 다운 받아 주시길 바랍니다.

```
wget https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
```

그 후 bash 쉘 스크립트 명령으로 설치를 진행합니다.

```
bash ./Anaconda3-2019.10-Linux-x86_64.sh
```

#### Anaconda 실행

설치가 완료되면 아래의 명령어로 Anaconda를 실행 시킬 수 있습니다.

```
source ~/.bashrc
```

#### Anaconda 업데이트

아래의 명령어들로 Anaconda를 업데이트 할 수 있습니다.

```
conda updata conda
```

```
conda updata anaconda
```

```
conda updata -n base conda
```

#### Anaconda의 python 패키지 전체 업데이트

```
conda update -all
```

---

1. PIP 사용
-----------

#### PIP 설치

pip가 설치되어 있지 않은 경우 아래의 명령어를 사용하여 설치 할 수 있습니다.

```
sudo apu intall python-pip
```

```
sudo apu intall python3-pip
```

#### PIP 업데이트

```
pip install --upgrade pip
```

```
python -m pip install --upgrade pip
```

---

2. Jupyter notebook
-------------------

#### Jupyter notebook 설치

-	***Anaconda를 설치 한 경우***

Anaconda 설치 시 Jupyter notebook은 기본으로 설치가 됩니다. 하지만 가상환경 내에 jupyter를 설치하고자 할 때 다음과 같은 명령어를 사용하시면 됩니다.

```
conda install jupyter notebook
```

-	***Anaconda를 설치하지 않고 일반 python으로 실행시키는 경우***

Anaconda를 따로 설치하지 않고 jupyter notebook을 사용하고자 할 때 다음과 같은 명령어를 사용하시면 됩니다.

```
pip install jupyter
```

#### 로컬에서 Jupyter notebook 실행(default)

로컬에서 Jupyter notebook을 실행 할 경우 아래와 같은 명령어를 실행하면 Jupyter notebook을 실행 시킬 수 있습니다.

```
jupyter notebook
```

Anaconda를 통해서 실행 시에는 반드시 Anaconda를 실행시키고 명령어를 입력하여야 합니다. 실행 시 아래와 같이 localhost:8888로 접속 가능합니다. (원격 접속 불가능)

<img src='/img/jupyter_notebook_local.PNG'>

#### 원격으로 Jupyter notebook 접속

1.	포트 방화벽 해제하기

아래의 명령어로 열고자 하는 포트의 방화벽을 해제합니다. 포트포워딩도 필수로 해주어야 합니다.

```
sudo ufw allow [port]
```

1.	config 파일 만들기

아래의 명령어를 실행하면 /home/username/.jupyter 디렉토리에 jupyter_notebook_config.py 파일이 생성됩니다.

```
jupyter notebook --generate-config
```

1.	서버 비밀번호 생성

```
Ipython
```

위 코드로 실행되는 Ipython 프롬포트 환경에서 다음 코드를 순서대로 실행합니다.

```python
ln [1]: from notebook.auth import passwd

ln [2]: passwd()
Enter password: # 패스워드를 입력합니다.
verify password: # 패스워드를 재입력합니다.
Out[2]: 'sha1:12j30t94230g208ehdsflhsdgt3908' # 이런 식으로 입력한 비밀번호를 암호화 하여 반환합니다.
```

암호화된 비밀번호를 복사합니다.

1.	환경설정하기

/home/username/.jupyter 디렉토리에 가서 jupyter_notebook_config.py을 실행시킵니다.

```
vi jupyter_notebook_config.py
```

vi, vim에서 수정시 i를 누르고 수정합니다. 코드를 수정하는 부분은 #을 제거하여 주석처리를 제거합니다.

```python
# 코드 맨 위 코드 추가
c = get_config()

# 외부 접속 허용하기
c.NotebookApp.allow_origin = '*'

# 작업 경로 설정
c.NotebookApp.notebook_dir = '원하는/작업경로를/입력해/주세요'

# 아이피 설정
c.NotebookApp.ip = '사용할.아이피를.입력해.주세요'

# 포트 설정
c.NotebookApp.port = '사용할 포트번호 네자리를 입력해주세요, 초기값은 8888 입니다.'

# 비밀번호 설정
c.NotebookApp.password = u'복사해둔 암호화된 비밀번호 sha1:12j30t94230g208ehdsflhsdgt3908 를 여기에 입력해주세요'

# 시작시 브라우저 실행여부
c.NotebookApp.open_browser = False
```

수정이 완료하였으면 :wq 를 누르고 저장합니다.

아래 코드로 jupyter notebook을 실행 시킵니다.

```
jupyter notebook --config jupyter_notebook_config.py
```

설정한 ip 주소와 포트 번호로 접속합니다.

```
[ip address]:[port num]
```

<img src='/img/jupyter_notebook_login.PNG'>

위와 같이 원격으로 접속이 되면 설정했던 비밀번호로 로그인하시면 됩니다.

---

3. Jupyter notebook extensions
------------------------------

Jupyter notebook extensions란 jupyter notebook의 다양한 확장 기능을 모아 놓은 것입니다.

#### Jupyter notebook extensions 설치하기

아래의 명령어를 입력하여 설치합니다.

```
pip install jupyter_contrib_nbextensions && jupyter contrib nbextension install
```

Permission denied: '/usr/local/share/jupyter/nbextensions' 이 뜰 경우 아래 코드를 입력하세요.

```
pip install jupyter_contrib_nbextensions && jupyter contrib nbextension install --user
```

설치가 완료되면 아래와 같이 Nbextensions 탭이 생깁니다. diable 박스 체크를 해제해주고 원하시는 기능들을 체크해서 사용하시면 됩니다.

<img src='/img/jupyter_notebook_extensions.PNG'>

#### 추천 기능

-	Table of Conents: 마크다운 헤더 수준에 따른 목차 생성
-	Autopep8: 자동 코드정리기능
-	Variable inspector: 변수들을 트래킹 하는 익스텐션
-	ExecuteTime: 셀이 돌아가는 시간 측정
-	Hide input all: 코드부분을 숨기고 결과만 보여줍니다.

---
