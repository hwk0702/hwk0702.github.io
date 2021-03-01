---

layout: post

title: "Docker Tensorflow"

date: 2020-04-20 18:36:07

categories: [Tips]

description:

image: /img/docker_tensorflow.png

published: true

canonical_url:

tags: [도커, Docker, 텐서플로우, Tensorflow, Tensorflow GPU, Pycharm, 파이썬, Python]
---

Tensorflow Docker 환경 구축 방법
================================

-	본 설치 방법은 Linux 기반 세팅 방법입니다.

- GPU 버전 Tensorflow Docker를 설치하실 때는 [2번 목차](#2-gpu-기반-tensorflow-docker-환경) 부터

- Pycharm에서 Docker 원격 접속은 [3번 목차](#3-pycharm에서-원격으로-docker-접속) 부터 보시면 됩니다.

---

## 0. Docker 설치 및 사용 방법


Docker 설치 및 사용 방법은 https://github.com/jeonghoonkang/keti_data_proc/tree/master/docker 에 설명이 되어 있습니다. 참고 바랍니다.

---

## 1. CPU 기반 tensorflow Docker 환경


#### 1. Tensorflow 공식 이미지를 가져와서 컨테이너에 올립니다.

```bashrc
sudo docker run -it -p 8888:8888
-v ${HOME}/code:/notebooks tensorflow/tensorflow [command]
```

-	-i: interactive, -t: tty keep stdin open / allocate a terminal (옵션을 주지 않으면 컨테이너 안에서의 터미널을 볼 수 없습니다.)

-	-v: volume (== --mount or --bind) 호스트의 파일시스템과 격리된 도커 컨테이너의 파일시스템을 이어주는 역할 컨테이너는 휘발성이기 때문에 작업하고 저장한 파일들은 호스트에서 직접 접근할 수 없고, 컨테이너가 내려간 상태에서 삭제되면 같이 삭제.

<img src='/img/docker_tensorflow_volume.PNG'>

-	이미지 이름의 형식은 <repo>/<image_name>:<tag_name> 입니다. tag name이 주어지지 않을 경우 default는 ‘latest’

-	[COMMAND]가 주어지지 않을 경우 tensorflow 이미지의 디폴트 실행 프로그램은 **Jupyter notebook**

#### 2. 실행 후

<img src='/img/docker_tensorflow_1.PNG'>

-	tensorflow/tensorflow:latest 이미지를 컨테이너로 올리면, 컨테이너에서 Jupyter notebook이 컨테이너의 8888번 포트에서 디폴트로 실행됩니다.

-	현재 터미널의 상태는 컨테이너에 attach 되어 있는 상태입니다. Ctrl + c로 Jupyter 서버를 중지시키면 자기 할 일을 마친 컨테이너는 바로 정지되기 때문에, attach 상태에서 호스트 쉘로 서버를 중지하지 않 고 돌아가려면 **Ctrl + p, Ctrl + q** 를 차례대로 입력하면 됩니다.(Escape sequence)

-	Jupyter notebook 접속

<img src='/img/docker_tensorflow_2.PNG'>

-	컨테이너의 8888 포트와 로컬의 8888 포트를 이전에 -p 옵션으로 포워딩 해 주었으니, 로컬의 브라우 저에서 8888 포트로 접속할 수 있습니다.

-	콘솔에 보이는 token=[abcdabcd …] 문자열을 복사해 붙여줍니다. 최초 1회만 확인하며, 외부에서 접속하는 ip가 바뀌면 다시 입력해 주어야 합니다. 비밀번호를 설정할 수도 있습니다.

#### 3. 그 외 커맨드

-	Container 내부 쉘 접속:

```bashrc
docker exec -it <container_id> /bin/bash
```

-	컨테이너 변경사항을 이미지에 커밋:

```bashrc
docker commit <container_id> <image_id>:<tag>
```

-	이후에 Tensorboard 실행을 염두해 처음에 컨테이너의 포트를 하나 더 열어주시는 것 도 좋습니다. (docker run -it -p 8888:8888 -p 8889:6006 tf/tf:latest)

---

## 2. GPU 기반 tensorflow Docker 환경


-	Overview

```mermaid
graph LR
A(Nvidia Graphics Driver) --> B(Docker)
B --> C(Nvidia-docker2)
C --> D(DONE!)
```

#### 1. 하드웨어에 맞는 그래픽 드라이버를 설치

```bashrc
ubuntu-drivers devices
```

gpu에 맞는 드라이버를 확인하실 수 있습니다.

<img src='/img/ubuntu_drivers.PNG'>

```bashrc

sudo ubuntu-drivers autoinstall
```

위 코드로 recommended driver 바로 설치하고, 재부팅 후 아래 코드로 확인

```bashrc

nvidia-smi
```

<img src='/img/nvidia_smi.PNG'>

#### 2. nvidia-docker2 설치

1.	nvidia-docker1이 이미 설치되어 있다면 제거

```bashrc

docer volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker

sudo apt-get purge -y nvidia-docker
```

2.	apt-key에 package repository를 추가하고 apt-get update

```bashrc

curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -

distribution=$(. /etc/os-release;echo $ID$VERSION_ID)

curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee / etc/apt/sources.list.d/nvidia-docker.list

sudo apt-get update
```

3.	nvidia-docker2 설치

```bashrc
sudo apt-get install -y nvidia-docker2

sudo pkill -SIGHUP dockerd
```

1.	테스트

```bashrc

docker run --runtime=nvidia --rm nvidia/cuda nvidia-smi
```

#### 3. Tensorflow-gpu 공식 이미지를 가져와서 컨테이너에 올립니다.

<img src='/img/docker_tensorflow_gpu_1.PNG'>

그리고 실행시킨 gpu 컨테이너의 jupyter notebook 안에서 gpu를 잘 인식하는지 확인

```python
from tensorflow.python.client import device_lib
def get_available_gpus():
    return [x.name for x in device_lib.list_local_devices()]

get_available_gpus()
```

<img src='/img/docker_tensorflow_gpu_2.PNG'>

---

## 3. pycharm에서 원격으로 docker 접속

Pycharm 원격 접속은 Pycharm professional 버전에서만 사용 가능합니다.

#### 1. default runtime을 설정

```bashrc

sudo vim /etc/docker/daemon.json
```

위의 코드를 입력하여 daemon.json 파일을 연다. “default-runtime”: “nvidia” 이 부분이 없을텐데 아래와 같이 추가해준다.

```vi

1 {
2     "default-runtime": "nvidia",
3     "runtimes": {
4         "nvidia": {
5             "path": "nvidia-container-runtime",
6             "runtimeArgs": []
7         }
8     }
9 }

```

그 다음, 아래와 같은 명령으로 도커 서비스를 다시 시작한다.

```bashrc

sudo service docker stop

sudo service docker restart
```

#### 2. docker.service 파일 수정

아래 명령을 통해 docker.service 파일을 수정한다.

```bashrc

sudo vim /lib/systemd/system/docker.service
```

ExecStart로 시작하는 줄 끝에 -H tcp://0.0.0.0:[port번호] 부분을 추가한다.

```
ExecStart=usrbindocker daemon -H fd:/ -H tcp://0.0.0.0:2375
cs
```

그 다음, 파일의 변경사항을 저장하고 아래와 같은 명령으로 변경된 사항을 반영한다.

```bashrc
systemctl daemon-reload
sudo service docker restart
```

3. Remote Docker 세팅

pycharm에서 file -> setting을 열고 docker 설정을 합니다.

<img src='/img/pycharm_docker_1.PNG'>

tcp socket에서 Engine API URL에 서버 IP와 설정한 port로 연결합니다.

밑에 Connection successful이 뜨면 연결이 된겁니다.

4. Interpreter 설정

setting -> Project -> Project Interpreter로 들어갑니다.

<img src='/img/pycharm_docker_2.PNG'>

위와 같이 세팅한 Docker에서 이미지를 설정합니다.

5. path mappings

로컬에서 작성한 파일과 Docker상의 파일이 같아야하므로 맵핑을 해주어야 합니다.

<img src='/img/pycharm_docker_3.PNG'>

위와 같이 로컬에서의 경로와 Docker 상의 경로를 지정해줍니다.

6. 실행 결과

```python
from tensorflow.python.client import device_lib
def get_available_gpus():
    return [x.name for x in device_lib.list_local_devices()]

get_available_gpus()
```

<img src='/img/pycharm_docker_4.PNG'>

위와 같이 뜨면 성공입니다.
