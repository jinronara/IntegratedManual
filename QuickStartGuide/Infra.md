### 인프라 모니터링 {#user-content-인프라-모니터링}

본 가이드는 사용자가 와탭 인프라스트럭처 모니터링 서비스\(이하 인프라 모니터링\)를 사용 중인 Ubuntu 16.04 서버에 설치하고 확인하는 내용을 다룹니다. 별도의 세부적인 설정을 필요로 하는 확장팩 모니터링, 알림정책 등의 설정을 위해서는 사용자 가이드를 참조해주시기 바랍니다.

#### 설치 환경 {#user-content-설치-환경-3}

* OS: Linux Ubuntu 16.04

#### 에이전트 설치 절차 {#user-content-에이전트-설치-절차-4}

인프라 모니터링을 사용하기 위해서는 모니터링 대상 서버에 모니터링 에이전트를 설치해야 합니다. 인프라 모니터링 에이전트는 리눅스의 경우 와탭 저장소\(Repository\)를 통해, 윈도우의 경우 와탭 웹사이트에서 다운받을 수 있으며, 홈페이지에서 발급 받은 라이선스 키를 입력하여 등록할 수 있습니다.

**프로젝트 생성**

[![20](https://github.com/jinronara/deleteme_2/raw/master/images/20.png)](https://github.com/jinronara/deleteme_2/blob/master/images/20.png)

서버를 등록하기 위해 우선 프로젝트를 생성합니다. 추가 버튼을 선택하면 아래와 같이 프로젝트 생성 창이 나타납니다. INFRA 아이콘을 선택한 뒤, 희망하는 프로젝트명과 데이터 서버 지역\(Region\), 소속하게 될 그룹을 선택한 뒤 프로젝트를 생성합니다.[![160](https://github.com/jinronara/deleteme_2/raw/master/images/160.png)](https://github.com/jinronara/deleteme_2/blob/master/images/160.png)

**라이선스 발급**

[![170](https://github.com/jinronara/deleteme_2/raw/master/images/170.png)](https://github.com/jinronara/deleteme_2/blob/master/images/170.png)

프로젝트 관리화면에서는 우선적으로 라이선스를 발급 받습니다. 라이선스 키는 프로젝트별로 귀속되기 때문에, 유출되거나 배포되어서는 안됩니다. 반드시 본인 프로젝트에 서버를 등록할 때에만 이용하시기 바랍니다.

**에이전트 설치 절차**

**패키지 저장소\(Repository\) 등록**

아래 명령어를 복사하여 실행합니다.

```text
$ wget http://repo.whatap.io/debian/release.gpg -O -|sudo apt-key add -
$ wget http://repo.whatap.io/debian/whatap-repo_1.0_all.deb
$ sudo dpkg -i whatap-repo_1.0_all.deb
$ sudo apt-get update
```

정상적으로 저장소\(Repository\)가 등록되면 아래와 같은 화면을 볼 수 있습니다. 확인 후 sudo apt-get update를 통해 리스트를 업데이트합니다.

```text
(중략)
-                   100%[===================>]   1.69K  --.-KB/s    in 0s

2017-11-07 11:13:43 (517 MB/s) - written to stdout [1735/1735]

OK
root@ubuntu:~# wget http://repo.whatap.io/debian/whatap-repo_1.0_all.deb
--2017-11-07 11:13:44--  http://repo.whatap.io/debian/whatap-repo_1.0_all.deb
Resolving repo.whatap.io (repo.whatap.io)... 210.122.7.70
Connecting to repo.whatap.io (repo.whatap.io)|210.122.7.70|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1988 (1.9K) [application/x-debian-package]
Saving to: ‘whatap-repo_1.0_all.deb’

whatap-repo_1.0_all 100%[===================>]   1.94K  --.-KB/s    in 0s

2017-11-07 11:13:44 (526 MB/s) - ‘whatap-repo_1.0_all.deb’ saved [1988/1988]

root@ubuntu:~# sudo dpkg -i whatap-repo_1.0_all.deb
(데이터베이스 읽는중 ...현재 67273개의 파일과 디렉터리가 설치되어 있습니다.)
Preparing to unpack whatap-repo_1.0_all.deb ...
Unpacking whatap-repo (1.0) over (1.0) ...
whatap-repo (1.0) 설정하는 중입니다 ...
root@ubuntu:~# sudo apt-get update
```

* 정상적으로 whatap-repo이 설정되었을 apt 목록에 [http://repo.whatap.io](http://repo.whatap.io/) 가 추가된 것을 확인할 수 있습니다. 만약 정상적으로 표시되지 않았다면 설치 명령어와 네트워크 설정을 확인해주시기 바랍니다.

**에이전트 설치**

아래 명령어를 복사하여 에이전트를 설치합니다.

```text
$ sudo apt-get install whatap-infra
```

**라이선스키 등록**

설치가 완료된 후, 웹사이트에서 발급받은 라이선스키와 수집서버를 등록한 뒤 에이전트를 재시작합니다.

```text
$ echo "license=[발급된 라이선스 키] " |sudo tee /usr/whatap/infra/conf/whatap.conf
$ echo "whatap.server.host=[발급된 서버 아이피]" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
$ echo "createdtime=`date +%s%N`" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
sudo service whatap-infra restart
```

* 만약 정상적으로 에이전트가 설치되지 않았거나, 설치되었지만 데이터가 수집되지 않는다면, 방화벽 설정을 확인해 보시기 바랍니다. 와탭 에이전트의 경우 수집 서버와의 통신을 위해 수집 서버에 대한 TCP 아웃바운드 6600 포트가 오픈되어 있어야 합니다.

**모니터링 확인**

[![180](https://github.com/jinronara/deleteme_2/raw/master/images/180.png)](https://github.com/jinronara/deleteme_2/blob/master/images/180.png)

에이전트가 정상적으로 등록되면 서버 메뉴에서 등록된 에이전트를 확인할 수 있습니다.

* 시스템 모니터링 지표\(CPU, Memory, Disk, Network\) 수집 주기는 5초, 프로세스 모니터링 지표 수집 주기는 20초입니다.
