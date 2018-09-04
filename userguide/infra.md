# 관리 {#user-content-관리-1}

와탭 Infra 모니터링 서비스는 다수의 서버를 프로젝트로 그룹화 하여 관리합니다.

[![1170](https://github.com/jinronara/IntegratedManual/raw/master/images/1170.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1170.png)

## 에이전트 설치

[![1180](https://github.com/jinronara/IntegratedManual/raw/master/images/1180.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1180.png)

와탭 콘솔의 프로젝트 그룹에서 추가 버튼을 누릅니다.

[![1190](https://github.com/jinronara/IntegratedManual/raw/master/images/1190.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1190.png)

INFRA STRUCTURE 아이콘 선택 후 각 입력란에 해당하는 정보를 입력하고 전송 버튼을 눌러 프로젝트를 추가합니다.

### Linux

새롭게 생성한 인프라 모니터링 프로젝트를 클릭하여 아래와 같은 에이전트 설치 화면에 진입합니다.

* 해당 화면은 프로젝트 관리 → 에이전트 설치 부분에서 확인 가능합니다.

[![1200](https://github.com/jinronara/IntegratedManual/raw/master/images/1200.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1200.png)

#### 패키지 저장소\(Repository\) 추가

에이전트 설치 페이지에서 상위에 위치한 OS탭에서 서버 OS와 동일한 탭을 클릭합니다.

설치 페이지에 존재하는 “와탭 저장소\(Repository\)를 추가합니다.”의 밑에 있는 명령어를 copy 버튼을 눌러 복사하거나 밑의 명령어를 설치하고자 하는 서버에 입력합니다.Debian / Ubuntu

```text
$ wget http://repo.whatap.io/debian/release.gpg -O -|sudo apt-key add -
$ wget http://repo.whatap.io/debian/whatap-repo_1.0_all.deb
$ sudo dpkg -i whatap-repo_1.0_all.deb
$ sudo apt-get update
```

CentOS / Amazon Linux

```text
$ sudo rpm --import http://repo.whatap.io/centos/release.gpg
$ sudo rpm -Uvh http://repo.whatap.io/centos/5/noarch/whatap-repo-1.0-1.noarch.rpm
```

#### 에이전트 설치

설치 페이지에 존재하는 “서버 모니터 패키지를 설치하십시오.” 밑에 있는 명령어를 copy 버튼을 눌러 복사하거나 밑의 명령어를 설치하고자 하는 서버에 입력합니다.Debian / Ubuntu

```text
$ sudo apt-get install whatap-infra
```

CentOS / Amazon Linux

```text
$ sudo yum install whatap-infra
```

#### 라이선스 등록

설치 페이지에 존재하는 “설정 스크립트를 실행하여 서버 모니터 데몬을 시작하십시오.” 밑에 있는 박스를 클릭하여 라이선스를 발급받습니다. 이후 생성되는 명령어를 copy 버튼을 눌러 복사하거나 아래의 명령어에 라이선스키와 서버 IP를 추가하여 설치하고자 하는 서버에 입력합니다.

```text
$ echo "license=[발급된 라이선스키]" |sudo tee /usr/whatap/infra/conf/whatap.conf
$ echo "whatap.server.host=[할당된 와탭 서버 IP]" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
$ echo "createdtime=`date +%s%N`" |sudo tee -a /usr/whatap/infra/conf/whatap.conf
$ sudo service whatap-infra restart
```

* 설치 페이지에서 발급받은 명령어에는 라이선스 키와 IP가 입력되어 있습니다.
* 데이터 전송을 위해 6600 PORT가 열려 있어야 합니다. \(TCP 아웃바운드\)

### Windows

새롭게 생성한 인프라 모니터링 프로젝트를 클릭하여 아래와 같은 에이전트 설치 화면에 진입합니다.

* 해당 화면은 프로젝트 관리 → 에이전트 설치 부분에서 확인 가능합니다.

[![1210](https://github.com/jinronara/IntegratedManual/raw/master/images/1210.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1210.png)

#### 에이전트 파일 다운로드

에이전트 설치 페이지 상단에 위치한 OS 탭에서 Windows를 클릭합니다. 이후 Whatap\_infra.exe 를 클릭하여 설치파일을 다운로드 합니다.

* 보안상 .exe 형식의 파일이 받아지지 않는 사용자를 위하여 .zip 형식의 파일도 제공됩니다.
* 보안을 위해 브라우저를 통한 직접 설치보단 다운로드 받은 파일 실행을 권장합니다.

#### 에이전트 파일 업로드

다운로드 받은 인프라 에이전트 설치파일을 설치하고자 하는 서버에 접속하여 업로드 합니다.

#### 라이선스 발급

설치 페이지에서 라이선스 키와 IP를 발급받습니다.
[![1220](https://github.com/jinronara/IntegratedManual/raw/master/images/1220.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1220.png)

#### 에이전트 설치

서버에서 업로드 받은 인프라 에이전트 설치파일을 실행합니다.

실행 시 다음과 같은 화면을 볼 수 있습니다. 입력란에 발급받은 라이선스 키와 IP를 입력하고 진행합니다.

[![1230](https://github.com/jinronara/IntegratedManual/raw/master/images/1230.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1230.png)

정상적으로 설치가 완료된 경우 다음과 같은 화면을 볼 수 있으며, 에이전트가 자동적으로 모니터링을 시작합니다. 완료 버튼을 눌러 설치를 완료합니다.

[![1240](https://github.com/jinronara/IntegratedManual/raw/master/images/1240.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1240.png)

* 데이터 전송을 위하여 6600 PORT가 열려 있어야 합니다. \(TCP 아웃바운드\)

## 프로젝트 관리

### 사용자 관리

프로젝트를 생성하였거나 SuperAdmin 권한을 이전 받았을 경우 프로젝트 설정에서 해당 프로젝트의 기본 정보\(이름, 알림 표시 시간대, API토큰\) 입력/수정 및 사용자 초대를 통하여 서버 모니터링 현황을 공유할 수 있습니다.

[![1250](https://github.com/jinronara/IntegratedManual/raw/master/images/1250.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1250.png)

| 이름 | 설명 |
| :--- | :--- |
| 프로젝트 명 | 프로젝트 생성시에 기입한 이름이 들어갑니다. Edit 버튼을 눌러 프로젝트 이름을 변경할 수 있습니다. |
| 애플리케이션 시간대 | 알림 발생시 메일/SMS에 표시되는 시간을 지정할 수 있습니다. 원하는 시간대를 선택한 뒤 Edit버튼을 눌러 이후 발생하는 알림의 표시 시간을 변경할 수 있습니다. |
| 라이선스 키 | 각각의 프로젝트별로 발급되는 라이선스 키입니다. |
| 프로젝트 지역 | 프로젝트에 속한 서버에서 발생하는 데이터를 저장하는 수집 서버의 위치입니다. |
| Api 토큰 | Open API를 사용할 시 사용자를 식별 및 인증하는 문자열입니다. |
| 액티브 회원 | 해당 프로젝트에 등록된 사용자 명단입니다. SuperAdmin 계정의 경우 타 계정의 권한을 변경/삭제할 수 있습니다 |

* 주의: Api 토큰은 노출되지 않도록 사용자가 주의하여 관리하여야 하며, 노출 의심 시 재발급 버튼을 눌러 갱신할 수 있습니다.

## 알림 설정

### 알림 설정 개요

서버 임계 상황에서 알림이 발생 시 Email / SMS / Mobile App으로 알림을 수신할 수 있게 됩니다. 알림 메시지 언어 설정 및 미디어 별 수신 여부 / 수신 시간 / 수신 요일 등을 설정할 수 있습니다.

[![1260](https://github.com/jinronara/IntegratedManual/raw/master/images/1260.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1260.png)

| 이름 | 설명 |
| :--- | :--- |
| 알림 언어 | 알림을 받을 언어를 설정할 수 있습니다. |
| 알림 시간 | 설정한 시간에만 알림이 옵니다. |
| 알림 요일 | 설정한 요일에만 알림이 옵니다. |

### 이메일 알림 설정

알림이 발생한 경우 해당 프로젝트에 등록된 이메일로 알림 메일이 발송됩니다. 만약 알림을 받고 싶지 않은 경우 “이메일로 알림을 받겠습니다.”의 체크를 해제해주시면 됩니다.

### 문자 알림 설정

알림이 발생한 경우 해당 프로젝트에 등록된 휴대폰 번호로 알림 메시지가 발송됩니다. 만약 알림을 받고 싶지 않은 경우 “문자로 알림을 받겠습니다.”의 체크를 해제해주시면 됩니다.

* SMS 알림 기능은 유료 서버에 한정됩니다.

### 모바일 알림 설정

알림이 발생한 경우 해당 프로젝트에 등록된 모바일 APP으로 알림이 발송됩니다. 만약 알림을 받고 싶지 않은 경우 “모바일로 알림을 받겠습니다.”의 체크를 해제해주시면 됩니다.

#### 모바일 앱 설치

Google Play Store, App Store에서 WhaTap을 검색하여 설치합니다.
[![1270](https://github.com/jinronara/IntegratedManual/raw/master/images/1270.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1270.png)

#### 모바일 앱 활용

[![1280](https://github.com/jinronara/IntegratedManual/raw/master/images/1280.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1280.png)

[![1290](https://github.com/jinronara/IntegratedManual/raw/master/images/1290.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1290.png)

[![1300](https://github.com/jinronara/IntegratedManual/raw/master/images/1300.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1300.png)

## 다운 체크 설정

### 다운 체크 개요

같은 내부 네트워크에 존재하는 서버들이 서로의 포트 작동 여부를 확인하여 수집 서버로 전송합니다. 해당 방식은 가용성 기능을 사용할 때 모니터링 서버와 수집 서버간 네트워크 문제로 인하여 발생하는 오탐을 줄이기 위하여 내부 서버 서로 감시를 하여 서버의 다운 여부를 확인하여 수집 서버로 전송합니다.

[![1310](https://github.com/jinronara/IntegratedManual/raw/master/images/1310.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1310.png)

* 탐지 역할을 하는 서버를 선택할 수 있습니다. 클릭 시 드롭다운 메뉴가 나와 현재 서버 목록을 보여줍니다.
* 탐지할 서버를 추가할 수 있습니다.
* 현재 탐지되는 서버의 이름, IP, 포트에 대한 정보를 목록으로 보여줍니다.
* 등록 된 서버를 수정 / 삭제할 수 있습니다.

### 다운 체크 설정

다운 체크 설정 화면에서 추가 혹은 EDIT 버튼을 클릭 시 설정창이 발생합니다.

[![1320](https://github.com/jinronara/IntegratedManual/raw/master/images/1320.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1320.png)

| 이름 | 설명 |
| :--- | :--- |
| 이름 | 클릭시 드롭다운 메뉴가 인프라에 등록된 서버 목록을 보여줍니다. |
| IP | 드롭다운으로 서버를 선택시 자동으로 IP가 추가됩니다. |
| Port | 탐지역할 서버가 확인할 포트를 입력합니다. |
| SSH | RDP Port를 포함한 서버가 작동하면 반드시 접속가능한 Port를 입력하실 수 있습니다. |

# 실시간 모니터링 {#user-content-실시간-모니터링-1}

## 서버 목록

[![1330](https://github.com/jinronara/IntegratedManual/raw/master/images/1330.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1330.png)

1. 등록된 전체 서버들의 상태를 한 눈에 볼 수 있습니다.
2. 일시정지 / 재개 / 해지 하거나 비교하기 위해 서버\(들\)를 선택할 수 있습니다.
3. 서버에 대한 요약 차트를 볼 수 있습니다.
4. 등록된 서버명입니다. 클릭 시 개별 서버에 대한 상세 정보를 확인할 수 있습니다.
5. 선택된 서버들을 한번에 비교하여 볼 수 있습니다.
6. 원하는 서버에 태그를 만들어 해당 태그로 취사 선택하여 확인할 수 있습니다.
7. 등록된 서버들에 대한 정보를 취사 선택하여 확인할 수 있습니다. 컬럼에는 다음과 같은 정보들을 확인할 수 있습니다. 컬럼 및 컬럼 정렬 상태는 저장되어 다음에 접속하였을 때도 계속 유지됩니다.
8. 모니터링 서버를 일시정지 / 재개 / 해지할 수 있습니다.
   * 주의: 해당 기능은 프로젝트의 SuperAdmin과 Admin만 사용할 수 있습니다.
9. 새로운 서버를 등록할 수 있습니다.
10. 서버를 검색할 수 있습니다. 서버 이름, IP를 포함한 키워드를 입력하여 목록에서 원하는 서버만을 볼 수 있습니다.

### 컬럼 데이터**

| 이름 | 설명 |
| :--- | :--- |
| Server Name | 등록된 서버의 Display Name. 서버 상세정보 화면에서 변경할 수 있습니다. |
| OS | 등록된 서버의 운영체제 환경 |
| IP \(Public + Private\) | 외부/내부망 IP 모두 표시 |
| Public IP | 외부망 IP |
| Private IP | 내부망 IP |
| CPU | CPU 사용량\(%\) |
| Memory | Memory 사용량\(%\) |
| Disk\(all\) | 마운드 되어 있는 전체 디스크 현황 |
| Disk\(max\) | 최대 사용량 디스크 현황 |
| Network\(all\) | 연결되어 있는 전체 네트워크 어댑터 현황 |
| Network\(max\) | 최대 사용률 네트워크 현황 |
| CPU Vendor | 가용중인 CPU명 |
| RAM | 메모리 총량 |
| Up Time\(days\) | 서버가 켜진 후 경과한 일수 |
| DISK IO%\(all\) | 디스크 장치들의 사용 시간을 백분율 한 것 전부 출력 |
| DISK IO%\(max\) | 디스크 장치들의 사용 시간을 백분율 한 것 중 최대값 출력 |
| DISK IOPS\(all\) | 디스크 장치들의 IO 초당 사용 횟수를 전부 출력 |
| DISK IOPS\(max\) | 디스크 장치들의 IO 초당 사용 횟수 중 최대값 출력 |
| DISK BPS%\(all\) | 디스크 장치가 IO에 사용한 대역폭 전부 출력 |
| DISK BPS%\(max\) | 디스크 장치가 IO에 사용한 대역폭 중 최대값 출력 |

## 서버 상세 정보

### 상세 정보 개요

[![1340](https://github.com/jinronara/IntegratedManual/raw/master/images/1340.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1340.png)

| 번호 | 이름 | 설명 |
| :--- | :--- | :--- |
| 1 | 운영 체제 | OS 사용 정보 |
| 2 | CPU Usage | CPU 사용량 정보 |
| 3 | Memory Usage | Memory 사용량 정보 |
| 4 | Network | 네트워크 현황 정보 |
| 5 | Disk I/O | Disk I/O 수치 정보 |
| 6 | Server Info | 해당 서버의 운영체제, 화면 명, IP 주소, 와탭 에이전트 정보 |
| 7 | 조회 기간 | 화면상에 보여줄 데이터의 조회 기간을 변경할 수 있습니다. |
| 8 | Process | 해당 서버 내에 돌아가고 있는 프로세스의 리소스 정보 |
| 9 | Alert List | 등록된 서버 내에서 발생했던 최근 알림 기록 |

* CPU / Memory / Network / Disk IO의 경우 우측 See details를 통해 자세한 정보를 확인할 수 있습니다.

조회 기간 상세 설명

* 기본 설정: Real time으로 30분전부터 현재까지의 데이터. 기본 설정으로 세팅되어 있는 경우 5초마다 차트가 흐르며 실시간으로 모니터링이 가능합니다. 각각의 차트 우측에 돌아가고 있는 애니메이션이 활성화가 됩니다.
* 시간값 좌측의 화살표를 클릭하면 선택된 기간만큼의 앞, 혹은 뒤로 이동하며 차트를 조회합니다. 조회 기간 이동 시 선택 된 기간과 관계 없이 Real time 기능은 비활성화 됩니다.
* 가장 좌측에 있는 화살표를 클릭하면 현재 시간으로 돌아갑니다.
* 조회 기간마다 다른 차트 시간 간격을 갖습니다.
  * 30분, 1시간: 5초
  * 3시간, 12시간, 24시간: 5분
  * 7일, 30일: 1시간

### CPU 상세 정보

서버 상세 정보의 CPU Usage 우측 See Details를 통하여 상세 페이지로 들어올 수 있습니다.

[![1350](https://github.com/jinronara/IntegratedManual/raw/master/images/1350.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1350.png)

| 이름 | 설명 | 단위 |
| :--- | :--- | :--- |
| CPU Usage | CPU 사용량 | % |
| CPU Idle | CPU 미 사용량 | % |
| CPU I/O Wait | CPU가 디스크 IO가 완료되는 것을 기다리느라 소비하는 시간 | % |
| CPU Steal | 가상 CPU가 실제 CPU 시간을 기다리느라 소비하는 시간 | % |
| CPU IRQ | CPU가 하드웨어 인터럽트 처리를 위해 소비한 시간 | % |
| CPU SOFTIRQ | CPU가 소프트웨어 인터럽트 처리를 위해 소비한 시간 | % |
| CPU Load | 1분, 5분, 15분 동안 평균적으로 대기하고 있는 프로세스의 수 | 개수 |

### 메모리 상세 정보

서버 상세 정보의 Memory Usage 우측 See Details를 통해 상세 페이지로 들어올 수 있습니다.

[![1360](https://github.com/jinronara/IntegratedManual/raw/master/images/1360.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1360.png)

| 이름 | 설명 | 단위 |
| :--- | :--- | :--- |
| Memory Usage | Windows: Total Memory - Available Memory Linux: Total Memory - \(buffer + cache + free\) CentOS7: 100 - Memory Available | %, Byte |
| Memory Free | Windows: Available Memory Linux: Process가 사용가능한 메모리 중 buffer, cache를 제외한 용량 CentOS7 계열: SWAP 증가 없이 프로세스가 사용할 수 있는 메모리 | % |
| Memory Available | Windows: 시스템 상에서 사용 가능한 메모리 Linux: 사용 가능한 메모리 CentOS: SWAP 증가 없이 프로세스가 사용할 수 있는 메모리 | % |
| Memory Swap Used | Swap 영역 사용량 | %, Byte |
| Memory Page Faults | 메모리 공간에 존재하지 않는 코드나 데이터를 요청 시 발생하는 Soft Page Fault+Hard Page Fault | 개수 |

### 네트워크 상세 정보

서버 상세 정보의 Network 우측 See Details를 통해 상세 페이지로 들어올 수 있습니다.

[![1370](https://github.com/jinronara/IntegratedManual/raw/master/images/1370.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1370.png)

| 번호 | 이름 | 설명 | 단위 |
| :--- | :--- | :--- | :--- |
| 1 | Network Adapter | 연결된 네트워크 어댑터별 상세 정보 |  |
| 2 | Traffic In/Out | Network Interface가 송/수신한 트래픽 대역폭 | bps |
| 3 | Packet In/Out | Network Interface가 송/수신한 패킷 대역폭 | ps |
| 4 | Error In/Out | Network Interface에서 발생한 송/수신 전송 오류 | ps |
| 5 | Dropped In/Out | Network Interface에서 발생한 송/수신 중 처리하지 못하고 timeout이 발생하여 손실 처리된 것 | ps |

### 디스크 상세 정보

서버 상세 정보의 Disk I/O 우측 See Details를 통해 상세 페이지로 들어올 수 있습니다.

[![1380](https://github.com/jinronara/IntegratedManual/raw/master/images/1380.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1380.png)

| 번호 | 이름 | 설명 | 단위 |
| :--- | :--- | :--- | :--- |
| 1 | Disk | 마운트 된 디스크별 상세 정보 |  |
| 2 | Disk I/O | 디스크 장치가 사용중인 시간 | % |
| 3 | IOPS | Read/Write 디스크 장치가 IO를 사용한 초당 횟수 | ps |
| 4 | Disk Bps Read/Write | 디스크 장치가 IO에 사용한 대역폭 | bps |
| 5 | Used Space | 파일 시스템 사용 용량 | %, Byte |
| 6 | Free Space | 사용할 수 있는 파일 시스템 용량 | %, Byte |
| 7 | Queue Length | 대기중인 I/O 요청 수 | 개수 |

### 프로세스 상세 정보
[![1390](https://github.com/jinronara/IntegratedManual/raw/master/images/1390.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1390.png)

1. 정렬 기준: 프로세스들의 정렬 기준 및 개수를 결정할 수 있습니다. CPU / Memory / Name / IO / Count를 기준으로 정렬할 수 있습니다.

[![1400](https://github.com/jinronara/IntegratedManual/raw/master/images/1400.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1400.png)

1. 알림 정책 설정: 개별 프로세스에 대해 Alert 정책을 설정할 수 있습니다. 자세한 내용은 프로세스 알림 정책을 참고하시길 바랍니다.
2. 프로세스 세부 정보: 해당 프로세스 클릭 시 프로세스에 대한 세부정보를 볼 수 있습니다. 자세한 내용은 개별 프로세스 정보를 참고하시길 바랍니다.
3. 더 보기: 현재 화면상에 보이지 않는 프로세스들 역시 확인할 수 있습니다.

#### 개별 프로세스 정보**

각각의 프로세스를 클릭할 경우 개별 프로세스 정보를 확인할 수 있습니다.

[![1410](https://github.com/jinronara/IntegratedManual/raw/master/images/1410.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1410.png)

| 번호 | 이름 | 설명 | 단위 |
| :--- | :--- | :--- | :--- |
| 1 | 프로세스 개요 | \* PID, 프로세스명, CPU/Memory/RSS 사용률 및 사용자 권한을 확인 \* 해당 프로세스가 한 개 이상 실행될 경우 추가적으로 리스트업 \* RSS: 메모리 내부에서 프로세스가 차지하는 메모리의 양 |  |
| 2 | CPU Used\(%\) | 프로세스가 사용한 CPU 시간의 백분율 | % |
| 3 | Memory Used\(%\) | 프로세스가 사용한 메모리 비율 | % |
| 4 | I/O Used \(Bps\) | Windows: File, Network, Device로부터 발생한 IO 대역폭 | bps |
| 5 | IP Used \(Count\) | 같은 이름의 프로세스에서 사용 중인 Listen Port 및 연결 개수 | count |
| 6 | File Used \(Byte\) | 같은 이름의 프로세스에서 Open한 파일 이름과 크기 | byte |

# 대시보드 {#user-content-대시보드}

## Compound Eye

### Compound Eye 개요

Compound Eye는 사용자들에게 와탭 에이전트가 설치된 모든 서버들을 빈틈없이 볼 수 있게 해줍니다.

[![1420](https://github.com/jinronara/IntegratedManual/raw/master/images/1420.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1420.png)

[![1430](https://github.com/jinronara/IntegratedManual/raw/master/images/1430.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1430.png)

하나의 눈\(Eye\) 입니다. 총 5가지의 정보를 제공합니다.

* CPU 사용량
* Memory 사용량
* Disk 사용량
* 네트워크의 Rx \(수신량\)
* 네트워크의 Tx \(송신량\)
  * 특히 네트워크 사용량에서 Rx/Tx 를 추가함으로 DDoS와 같이 외부 공격이 여러 서버에서 일제히 발생하는지 확인할 수 있습니다.

[![1440](https://github.com/jinronara/IntegratedManual/raw/master/images/1440.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1440.png)

서버에 이상 현상이 발생한 경우 개별 아이\(Eye, 눈\)는 색상으로 그 상태를 표현합니다.

* 서버 모니터링이 일시정지 된 상태입니다. 회색으로 표현됩니다.
* 서버가 경고 상태입니다. 주황색으로 표현됩니다.
* 서버가 위험 상태입니다. 빨간색으로 표현됩니다.

추가적으로 서버 위에 마우스를 위치하게 될 경우 개별 정보가 수치화 된 팝업 메시지가 뜨게 되며, 서버 클릭 시 해당 서버의 요약 페이지로 이동하게 되어 서버에 대한 더욱 자세한 내용들을 파악할 수 있습니다.

### Traffic Max Value 옵션

네트워크 환경에 따라 트래픽 양이 변화할 수 있기 때문에 트래픽의 최대값을 조정할 수 있습니다. 희망하는 트래픽 최대값을 설정하면 값에 따라 Rx/Tx 그래프가 변경됩니다.

[![1450](https://github.com/jinronara/IntegratedManual/raw/master/images/1450.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1450.png)

## 가용성

가용성 기능은 여러 서버들의 서버 상태 기록을 그래프로 보여 한눈에 파악할 수 있도록 합니다.

[![1460](https://github.com/jinronara/IntegratedManual/raw/master/images/1460.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1460.png)

가용성 차트는 다운 체크에서 추가한 IP들의 가용성 차트를 표시합니다. 기본으로 오늘 날짜의 00:00부터 현재까지의 가용성 차트를 표시합니다. 1일, 7일, 30일 등 범위를 지정할 수 있으며 화살표 클릭으로 차트의 날짜를 변경할 수 있습니다.

# 알림 정책 {#user-content-알림-정책}

## 알림 정책 설정

### 알림 정책 개요

서버 및 프로세스 알림 정책을 생성, 수정, 삭제할 수 있습니다.

[![1470](https://github.com/jinronara/IntegratedManual/raw/master/images/1470.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1470.png)

| 이름 | 설명 |
| :--- | :--- |
| 추가 | 해당 정책을 추가할 수 있습니다. |
| COPY | 다른 인프라에 해당 정책을 복사할 수 있습니다. |
| 이름 프로세스명 로그 규칙명 | 해당 정책의 이름을 표시합니다 |
| 요약 | 지정된 정책을 간략하게 보여줍니다. |
| 서버 대수 | 해당 정책을 사용하는 서버의 수를 표시합니다. |

### 모니터링 알림 정책

서버의 재시작 여부, 에이전트의 통신 장애 지속시간, 자원 사용량에 따라 알림 발생 여부를 설정할 수 있습니다.

[![1480](https://github.com/jinronara/IntegratedManual/raw/master/images/1480.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1480.png)

| 이름 | 설명 |
| :--- | :--- |
| 통신 장애 알림 | 지정된 지속기간 동안 에이전트가 반응이 없을 경우 알림 발생 여부를 설정합니다. |
| CPU Memory Swap | CPU, Memory, SWAP 메모리 등의 사용률에 대한 알림을 설정합니다. |
| Disk | 디스크 사용량과 I/O 사용량을 기반으로 알림을 설정합니다. |
| Network | 네트워크 사용량과 관련한 알림을 설정합니다. 트래픽 양과 초당 패킷을 기준으로 설정할 수 있습니다. |
| 지속시간 | 해당 시간 이후 서버의 상태가 Warning, Fatal로 변경됩니다. |

* 주의 : 하나의 서버는 하나의 알림 정책만을 할당 받을 수 있습니다.

### 프로세스 알림 정책

#### 프로세스 알림 정책 설정

특정 프로세스에 대한 알림 정책을 설정할 수 있습니다.

[![1490](https://github.com/jinronara/IntegratedManual/raw/master/images/1490.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1490.png)

1. 프로세스명: 선택한 프로세스명이 표기됩니다.
2. Enable as Project-Wide: 해당 프로젝트에 있는 모든 서버들에 해당 알람 정책을 적용합니다.
3. Count: 해당 프로세스의 개수 증감에 대하여 알림을 설정할 수 있습니다. 좌측의 경우 최저치 알림 / 우측의 경우 최대치 알림입니다.
   * 만약 프로세스가 슬라이더 좌측보다 적어지면 알림이 발생하고, 반대로 슬라이더 우측보다 많아지면 알림이 발생합니다.
4. CPU: CPU 사용량에 따라 알림을 설정할 수 있습니다.
5. Memory: 메모리 사용량에 따라 알림을 설정할 수 있습니다.
6. 알림 정책 적용: 해당 프로세스에 대한 알림을 단일 서버가 아닌 다중 서버에 대한 정책으로 설정할 수 있습니다.
7. 임계값 지속 시간: 해당 설정된 임계값의 지속시간 이후 서버 상태가 Warning 혹은 Fatal로 변경됩니다.

### 로그 알림 정책

로그 정책은 애플리케이션에서 발생하는 여러 로그들의 감시 설정을 편리하게 관리할 수 있도록 만들어졌습니다.

#### 로그 알림 정책 설정

[![1500](https://github.com/jinronara/IntegratedManual/raw/master/images/1500.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1500.png)

1. 해당 정책의 이름을 지정합니다.
2. 새로운 규칙을 생성합니다.
3. 지정된 규칙을 삭제합니다.
4. 삭제하거나 적용될 규칙을 선택합니다.
5. 적용될 서버를 선택합니다.

##### 파일 로그

[![1510](https://github.com/jinronara/IntegratedManual/raw/master/images/1510.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1510.png)

파일 로그를 감시하기 위해 파일 경로, 키워드를 입력할 수 있습니다. \* 파일 경로: 감시할 파일의 경로 \* 키워드: 해당 파일의 로그에서 해당 키워드가 발생시 알림을 발생시킵니다. \* 위험도: 알림이 발생하였을 때 위험도를 지정합니다.

##### 이벤트 로그

[![1520](https://github.com/jinronara/IntegratedManual/raw/master/images/1520.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1520.png)

이벤트 로그를 감시하기 위해 로그명, 수준을 선택할 수 있으며, 이벤트 소스, 이벤트 ID, 키워드를 입력할 수 있습니다. 각각의 빈칸에는 아래의 사진들에서 지정된 영역에 해당하는 값들 중에서 모니터링 하고자 하는 값을 골라 기입하시면 됩니다.

[![1530](https://github.com/jinronara/IntegratedManual/raw/master/images/1530.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1530.png)

[![1540](https://github.com/jinronara/IntegratedManual/raw/master/images/1540.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1540.png)

* 위험도: 알림이 발생했을 때 해당 알림의 위험도를 지정할 수 있습니다.
* 이벤트 로그는 Windows 환경에서만 사용 가능합니다.

## 알림 내역

해당 프로젝트에 등록된 모든 서버에서 발생한 모든 알림 내역 리스트를 볼 수 있으며, 서버명을 기준으로 검색할 수 있습니다.

[![1550](https://github.com/jinronara/IntegratedManual/raw/master/images/1550.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1550.png)

| 이름 | 설명 |
| :--- | :--- |
| 발생시간 | 알림 발생시간 |
| 위험도 | Fatal\(위험\) 혹은 Warning\(경고\)로 표시됩니다. |
| 서버명 | 서버 이름 |
| 설명 | 알림 정책에서 설정한 값을 바탕으로 발생한 알림 설명 |
| 스냅샷 | 발생한 알림에 대한 CPU, Memory, Disk, Network에 대한 스냅샷 정보 |
| 현재상태 | 해당 알림의 현재 상태 |
| 처리내역 | 알림에 대한 처리내역 |

## 알림 상세 정보
알림 내역에서 하나의 알림을 선택 시 상세 정보 페이지로 이동합니다.

[![1560](https://github.com/jinronara/IntegratedManual/raw/master/images/1560.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1560.png)

1. 개요: 발생한 알림에 대한 개요를 확인할 수 있습니다.
2. 발생한 시점의 전후로 5분씩의 CPU, Memory, Disk, Network 차트를 보여줍니다. 알림에 해당하는 부분의 Severity\(위험도\)를 표시하고 있습니다.
3. 알림에 해당하는 프로세스 정보를 상위로부터 10개를 보여주고 있으며, View all 링크를 클릭시 모든 프로세스 정보를 확인할 수 있습니다.
   * 해당 화면에서도 각각의 프로세스에 대한 알림 정책을 설정할 수 있습니다.
4. 알림에 대한 처리 내역 리스트를 보여줍니다. Acknowledge Add버튼을 눌러 처리내역을 추가적으로 기입 후 저장할 수 있습니다.

# 보고서 {#user-content-보고서-1}

## 일일 보고서 \(전체 요약\)

하루 동안 수집한 데이터를 토대로 보고서를 작성해 보여줍니다.

[![1570](https://github.com/jinronara/IntegratedManual/raw/master/images/1570.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1570.png)

* 보고서를 작성할 데이터 기간을 설정합니다. 시간 설정 버튼을 눌러 시작~종료 시간을 설정할 수 있습니다.
* 이메일 수신을 체크면 매일 오전 중 일일 보고서를 이메일로 전달 받을 수 있습니다.
* 인쇄 버튼을 누르면 해당 보고서를 인쇄할 수 있습니다.
* 프로젝트 이름, 서버 대수, 알림 개수를 보여줍니다.
  * Change rate는 전날 대비 증감폭입니다.
* 서버 이름, CPU/메모리 평균, 알림 개수를 요약해서 보여줍니다.
* 당일 발생한 알림의 발생 시간, 위험도, 서버명, 설명, 스냅샷을 최대 50개까지 보여줍니다.

## 주간 보고서

일주일 동안 수집한 데이터를 토대로 보고서를 작성해 보여줍니다.

[![1580](https://github.com/jinronara/IntegratedManual/raw/master/images/1580.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1580.png)

* 보고서를 작성할 데이터 기간을 설정합니다.
* 내보내기 버튼을 누를 경우 .CSV 형식으로 보고서를 저장합니다.
* 인쇄 버튼을 누를 경우 해당 보고서를 인쇄할 수 있습니다.
* 서버 이름, CPU Avg\(%\), Memory Avg\(%\)를 요약해서 보여줍니다.   ==== 주간 보고서 \(디스크\) 일주일간 수집한 데이터 중 디스크만 추출하여 보고서를 작성해 보여줍니다.

[![1590](https://github.com/jinronara/IntegratedManual/raw/master/images/1590.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1590.png)

* 보고서를 작성할 데이터 기간을 설정합니다, 설정한 날짜의 이후 7일간의 데이터를 보여줍니다.
* 내보내기 버튼을 누를 경우 .CSV 형식으로 보고서를 저장합니다.
* 인쇄 버튼을 누를 경우 해당 보고서를 인쇄할 수 있습니다.
* 서버 이름, Disk\(%\)를 요약해서 보여줍니다.   ==== 월간 보고서 한달 동안 수집한 데이터를 토대로 보고서를 작성해 보여줍니다.

[![1600](https://github.com/jinronara/IntegratedManual/raw/master/images/1600.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1600.png)

* 보고서를 작성할 데이터 기간을 설정합니다.
* 내보내기 버튼을 누를 경우 .CSV 형식으로 보고서를 저장합니다.
* 인쇄 버튼을 누를 경우 해당 보고서를 인쇄할 수 있습니다.
* 서버 이름, CPU Avg\(%\), Memory Avg\(%\)를 요약해서 보여줍니다.

## 월간 보고서 \(디스크\)

한달간 수집한 데이터 중 디스크 정보만 추출하여 월간 보고서를 작성하여 보여줍니다.

[![1610](https://github.com/jinronara/IntegratedManual/raw/master/images/1610.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1610.png)

* 보고서를 작성할 데이터 기간을 설정합니다. 설정한 기간 이후의 1달간 데이터를 보고서로 작성합니다.
* 내보내기 버튼을 누를 경우 .CSV 형식으로 보고서를 저장합니다.
* 인쇄 버튼을 누를 경우 해당 보고서를 인쇄할 수 있습니다.
* 서버 이름, 사용 경로, Disk\(%\)를 요약해서 보여줍니다.

## 월간 보고서 \(애플리케이션 상세\)

한달간 수집한 데이터를 토대로 애플리케이션 별 월간 보고서를 작성하여 보여줍니다.

[![1620](https://github.com/jinronara/IntegratedManual/raw/master/images/1620.png)](https://github.com/jinronara/IntegratedManual/blob/master/images/1620.png)

* 보고서를 작성할 데이터 기간을 설정합니다.
* 내보내기 버튼을 누를 경우 .CSV 형식으로 보고서를 저장합니다.
* 인쇄 버튼을 누를 경우 해당 보고서를 인쇄할 수 있습니다.
* CPU
  * SYS
  * USR
  * STEAL
  * NICE
  * IRQ
  * SOFT\_IRQ
* MEMORY
  * MEMORY
  * SWAP
* DISK I/O
* Network
