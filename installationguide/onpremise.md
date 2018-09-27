# 설치형 서버

## 안내사항

수집 서버가 설치될 장비의 IP 및 수집 규모에 따른 라이센스 발급을 진행합니다.  
라이센스 발급은 license@whatap.io 에 필요사항을 기술하여 요청합니다.

* 설치 환경 식별을 위한 명칭: 고객사 + 사업명
* 고객사 담당자: 이름, 전화번호, 이메일
* 라이선스 시작일
* 라이선스 종료일: 종료일 0시에 제한되므로 종료일 + 1로 요청
* 인프라 모니터링 대상 코어 수/에이전트 수: 코어 또는 에이전트 수 \(정식 라이센스는 에이전트 수 기준임\)
* 어플리케이션 모니터링 대상 코어 수/에이전트 수 \(정식 라이센스는 코어 수 기준임\)

이벤트 알림을 위한 설정은 계약 완료 시점 이후 별도의 절차로 진행합니다. 단 본 문서에는 이벤트 알림용 notihub 서버와 관련한 사항도 기술합니다.

### 수집 서버 권장 사양

#### 수집서버 \(설치형, SaaS형의 경우 불필요\)

* OS : Ubuntu / CentOS 안정화 버전
* CPU : 4Core 이상 \(최소 2Core\)
* Memory : 16G 이상 \(최소 8G\)
* Disk : 200G 이상 \(100TPS 기준 1GB/\)

<table>
  <thead>
    <tr>
      <th style="text-align:center">구분</th>
      <th style="text-align:center">데이터 보관기간</th>
      <th style="text-align:center">Disk 용</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:center">Infra
        <br />Monitoring</td>
      <td style="text-align:center">1 년</td>
      <td style="text-align:center">8.2G / Year
        <br />(1EA * Raw Data 30일 * 100M) + (Summary Data 14M * 365일)</td>
    </tr>
    <tr>
      <td style="text-align:center">
        <p>Application</p>
        <p>Monitoring</p>
      </td>
      <td style="text-align:center">30 일</td>
      <td style="text-align:center">
        <p>30G / 월</p>
        <p>(1EA * 30일 * 1Gb)</p>
      </td>
    </tr>
  </tbody>
</table>* JDK : Oracle JDK 1.7 이상
* 높은 File I/O로 인한 운영체제 file descriptor 설정 조정 

### 방화벽 오픈

* 에이전트 설치대상 -&gt; 수집 서버 \(TCP 6600 포트\)
* 모니터링 PC -&gt; 수집 서버 \(TCP 8080 포트\)

### 파일 디스크립터 설정의 상향 조정

시스템의 파일 디스크립터 설정을 상향 조정합니다.  
sysctl.conf 파일 내용에 fs.file-max = 999999 설정을 추가합니다.

```bash
 $ vi /etc/sysctl.conf fs.file-max = 999999
```

추가한 설정을 적용합니다.

```bash
$ sysctl -p
```

추가한 설정을 적용합니다.

```bash
$ sysctl -a | grep file-max fs.file-max = 999999
```

설치형 서버를 실행할 사용자에 대해 파일 디스크립터 설정을 상향 조정합니다.  
/etc/security/limits.conf 파일에 사용자 또는 그룹 이름으로 soft, hard 설정을 상향 조정합니다.  
사용자 계정은 그대로 사용하고, 그룹은 앞에 @를 붙여서 설정합니다.

```bash
 vi /etc/security/limits.conf
 ${사용자 계정 또는 @그룹명} soft nofile 999999
 ${사용자 계정 또는 @그룹명} hard nofile 999999
```

## 설치 작업 절차

### 설치 파일 및 라이센스 업로드

단일 서버에 구성하는 경우, 최소형 패키지를 활용하며 향후 확장성을 고려할 때 확장형 패키지를 활용하여 설치를 진행합니다. JDK 및 와탭 모니터링 패키지를 설치 대상 서버에 업로드 하고 압축을 해제합니다.

* 최소형 패키지: whatap\_single-\#.\#.\#.\#\#\#\#.tar
* 확장형 패키지: whatap\_multi-\#.\#.\#.\#\#\#\#.tar
* Oracle JDK 1.7 이상
* 라이센스 파일: 텍스트 파일로 준

와탭 모니터링 패키지를 압축 해제하면 whatap\_package 라는 디렉토리로 압축이 해제됩니다.   
본 문서에서 이후 해당 경로를 $WHATAP\_PACKAGE로 기술합니다.

### JDK 설치

Oracle JDK 1.7 이상의 버전이 사전에 설치되어 있는 경우 이를 활용합니다. 설치되어 있지 않은 경우, JDK를 설치합니다.   
본 문서에서 이후 JDK 설치 경로를 $JDK로 기술합니다.

### 실행 파일 편집

$WHATAP\_PACKAGE/bin 하위에는 쉘 스크립트가 존재합니다. 스크립트에 실행 권한을 부여합니다.

```bash
$ cd $WHATAP_PACKAGE/bin
$ chmod +x *.sh
```

이후 쉘 스크립트를 편집하여 JAVA\_HOME 경로를 지정합니다.  
\(예시 front.sh\)

{% code-tabs %}
{% code-tabs-item title="front.sh" %}
```bash
#!/usr/bin/env bash
SERVICE_NAME=front.apm
JAVA_HOME=$JDK
SERVER_HOME=cd ..;pwd LIB_HOME=$SERVER_HOME/lib CONF_PATH=$SERVER_HOME/conf
EXE_JAR=ls $LIB_HOME/*.${SERVICE_NAME}.boot* | sort | tail -1 $JAVA_HOME/bin/java -Djava.security.egd=/dev/./urandom -Dwhatap.log.path=. -Xmx512m -jar $EXE_JAR
```
{% endcode-tabs-item %}
{% endcode-tabs %}

최소형 설치의 경우 front.sh, keeper.sh, yard.sh, proxy.sh 가 사용되고, 확장형 설치의 경우 eureka.sh, account.sh, front.sh / keeper.sh, yard.sh, proxy.sh, gateway.sh 가 사용됩니다.  
부가적으로 이벤트 알림 설정을 추가할 경우 notihub.sh가 사용됩니다.

### 설정편집

$WHATAP\_PACKAGE/lib 하위에는 어플리케이션 라이브러리\(jar\), $WHATAP\_PACKAGE/conf 하위에는 설정 파일\(conf\)이 존재합니다.   
실행 파일 편집시 개행코드로 인한 문제 발생 시에는 vi에디터에서 :set ff=unix 로 지정하고 편집합니다.

각 설정 파일에는 필수로 설정해야 하는 정보를 수정합니다.

| 구분 | 파일명 | 항목명 | 설정 |
| :--- | :--- | :--- | :--- |
| 최소형 | account.conf | owner | ifconfig/ipconfig로 식별 가능한 IP |
|  |  | license | 발급받은 서버 라이센스 |
|  | front.conf | region.proxy.address | 에이전트가 데이터를 전송하게 될 수집 서버의 IP |
|  |  | admin.password | 사이트 관리자 계정 패스워드 \(초기값 : admin\) |
|  | notihub.conf | mail.host | SMTP 연계를 통한 초대 메일 및 알람발송 등 적용 시 |
|  |  | mail.port |  |
|  |  | mail.username |  |
|  |  | mail.password |  |
|  |  | mail.sender |  |
|  |  | mail.smtp.auth |  |
|  |  | mail.smtp.ssl.enable |  |
|  |  | mail.smtp.starttls.enable |  |
|  |  | mail.smtp.starttls.required |  |
|  |  | smsformat |  |
|  |  | smssender | 이벤트 알림 중 문자 발송 시 고객사 커스터마이징 설정을 지정 |
|  |  | smsformat |  |
| 확장형 | account.conf | owner | ifconfig/ipconfig로 확인 가능한 account 서버 IP |
|  |  | license | 발급받은 서버 라이센스 |
|  |  | eureka.addr | eureka 서버 접근 정보 |
|  |  | eureka.hostname | eureka에 등록할 명칭\(복수의 서버가 동일 명칭을 가질 수 있음\) |
|  |  | eureka\_client\_ip\_address | gateway에서 접근 가능한 account 서버 IP |
|  |  | region.id | 첫 번째 리전의 ID |
|  |  | region.name |  |
|  |  | region.proxy.address | 첫 번째 리전의 proxy IP\(복수 지정 가능\) |
|  |  | mail.host | SMTP 연계를 통한 초대 메일 적용 시 |
|  |  | mail.port |  |
|  |  | mail.username |  |
|  |  | mail.password |  |
|  |  | mail.sender |  |
|  |  | mail.smtp.auth |  |
|  |  | mail.smtp.ssl.enable |  |
|  |  | mail.smtp.starttls.enable |  |
|  |  | mail.smtp.starttls.required |  |
|  | front.conf | eureka.addr | eureka 서버 접근 정보 |
|  |  | eureka.hostname | eureka에 등록할 명칭\(복수의 서버가 동일 명칭을 가질 수 있음\) |
|  |  | eureka\_client\_ip\_address | front 서버 IP |
|  |  | admin.password | 사이트 관리자 계정 패스워드 \(초기값 : admin\) |
|  | yard.conf | keeper | yard에서 접근 가능한 keeper 서버 IP:Port |
|  |  | server.name | keeper에 등록할 이름\(서버 단위\) |
|  |  | net\_noti\_ip | yard에서 접근 가능한 noti 서버 IP |
|  | proxy.conf | keeper | proxy에서 접근 가능한 keeper 서버 IP:Port |
|  |  | server.name | keeper에 등록할 이름\(서버 단위\) |
|  | gateway.conf | eureka.addr | eureka 서버 접근 정보 |
|  |  | eureka.hostname | eureka에 등록할 명칭\(복수의 서버가 동일 명칭을 가질 수 있음\) |
|  |  | eureka\_client\_ip\_address | account/front 에서 접근 가능한 gateway 서버 IP |
|  |  | keeper | gateway에서 접근 가능한 keeper 서버 IP:Port |
|  |  | region.name | region 명 첫 번째 region명은 account.conf에서 지정한 region.name과 일치해야 함 두 번째 이후 region명은 사이트 관리자 페이지에서 지정한 region명과 일치해야 함 |
|  | notihub.conf | eureka.addr | eureka 서버 접근 정보 |
|  |  | eureka.hostname | eureka에 등록할 명칭\(복수의 서버가 동일 명칭을 가질 수 있음\) |
|  |  | eureka\_client\_ip\_address | noti 서버 IP |
|  |  | keeper | noti에서 접근 가능한 keeper 서버 IP:Port |
|  |  | mail.host | 이벤트 알람 중 SMTP 통한 메일발송 기 적용 시 |
|  |  | mail.port |  |
|  |  | mail.username |  |
|  |  | mail.password |  |
|  |  | mail.sender |  |
|  |  | mail.smtp.auth |  |
|  |  | mail.smtp.ssl.enable |  |
|  |  | mail.smtp.starttls.enable |  |
|  |  | mail.smtp.starttls.required |  |
|  |  | smsformat |  |
|  |  | smssender | 이벤트 알림 중 문자 발송 시 고객사 커스터마이징 설정을 지정 |
|  |  | smsformat |  |

### 로그 경로 변경

실행 시 로그는 $WHATAP\_PACKAGE /logs/{server명}.log 로 출력됩니다.   
로그를 외부 경로에 출력할 경우 다음과 같이 지정합니다.

```bash
$ cd $WHATAP\_PACKAGE
$ rmdir logs
$ ln -s {외부경로} logs
$ cd javam/server
$ ln -s {외부경로} logs
```

### 실행

서버 실행은 $WHATAP\_PACKAGE /bin/control.sh를 통해 실행하게 됩니다.   
최소형 설치본의 경우 $WHATAP\_PACKAGE /bin/start.sh, $WHATAP\_PACKAGE /bin/stop.sh 파일을 통해서도 실행/정지가 가능합니다.

#### control.sh 를 통한 실행

control.sh를 통해 최소형 서버 실행 시에는 다음의 명령을 통해 실행하게 됩니다.

* ./control.sh keeper start
* ./control.sh front start
* ./control.sh yard start
* ./control.sh proxy start
* ./control.sh notihub start \(이벤트 알림 설정 시\)

확장형 서버 실행 시에는 front를 구성한 서버에서 다음의 명령을 실행합니다.

* ./control.sh eureka start
* ./control.sh account start
* ./control.sh front start
* ./control.sh notihub start

yard 구성 서버에서 다음의 명령을 실행합니다.

* ./control.sh keeper start
* ./control.sh yard start
* ./control.sh proxy start
* ./control.sh gateway start

control.sh 실행 시 다음과 같이 메뉴를 선택하여 작업을 수행할 수도 있습니다.

{% code-tabs %}
{% code-tabs-item title="\(예시\) 사용법 출력 " %}
```bash
$ cd $WHATAP_PACKAGE/bin
$ ./control.sh
-------------------------------------------------------------------------
[ Usage ] ./control.sh [ service_name [ command ]]
./control.sh menu
./control.sh all (stop/status)
./control.sh single (status/start/stop/restart)
./control.sh (multi-front/mf) (status/start/stop/restart)
./control.sh (multi-yard/my) (status/start/stop/restart)
./control.sh front (status/start/stop/restart)
./control.sh proxy (status/start/stop/restart)
./control.sh yard (status/start/stop/restart)
./control.sh keeper (status/start/stop/restart)
./control.sh notihub (status/start/stop/restart)
./control.sh eureka (status/start/stop/restart)
./control.sh gateway (status/start/stop/restart)
./control.sh account (status/start/stop/restart)
/apps/whatap/bin/admin_console.sh
-------------------------------------------------------------------------
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="\(예시\) 메뉴 선택형 모드" %}
```bash
./control.sh menu
############################
Select type 
############################
1. service start/stop
2. start-single
3. restart-single
4. start-multi
5. restart-multi
6. status-all
7. stop-all
       
99. Exit
############################
number> {원하는 메뉴 번호를 입력함}

############################
Select command 
############################
1. front start
2. front stop
3. front restart
                
4. proxy start
5. proxy stop
6. proxy restart
                
7. yard start
8. yard stop
9. yard restart
                
10. keeper start
11. keeper stop
12. keeper restart
                
13. notihub start
14. notihub stop
15. notihub restart
                
16. billing start
17. billing stop
18. billing restart
                
19. eureka start
20. eureka stop
21. eureka restart
                
22. gateway start
23. gateway stop
24. gateway restart
                
25. account start
26. account stop
27. acdount restart
                
0. menu
99. Exit
############################
number> {원하는 메뉴 번호를 입력함}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 실행 확인

기동 완료 여부는 서버의 포트 리스닝 여부와 로그를 확인합니다.

#### 포트 리스닝 확인

구성 환경에 따른 서버의 포트 리스닝 여부를 체크합니다.

```bash
$ netstat -na \| grep {체크 대상 포트} \| grep LISTEN
```

**최소형**

![](../.gitbook/assets/single_port.png)

| 어플리케이션 서버 |  포트 |  프로토콜  | 용도 |
| :--- | :--- | :--- | :--- |
| front \(+account\) | 8080 | HTTP | 모니터링 사이트 |
| keeper | 6789 | TCP/UDP | 서버 정보 수신 |
| yard | 7710 | TCP | 모니터링 데이터 조회 |
|  | 6610 | TCP | 모니터링 데이터 저장 |
| proxy | 6600 | TCP | 에이전트 데이터 수신 |
| notihub | 6500 | TCP/UDP | 이벤트 알림 |

                     

**확형**

![](../.gitbook/assets/multi_port.png)



| 어플리이션 서버 |  포트 |  프로토콜  | 용도 |
| :--- | :--- | :--- | :--- |
| eureka | 6761 | TCP | 서버 위치 관리 |
| account | 18080 | HTTP | 계정 관 |
| front | 8080 | HTTP | 모니터링 사이트 |
| gateway | 8800 | TCP | 리전 요청 수 |
| keeper | 6789 | TCP/UDP | 서버 정보 수신 |
| yard | 7710 | TCP | 모니터링 데이터 조회 |
|  | 6610 | TCP | 모니터링 데이터 저장 |
| proxy | 6600 | TCP | 에이전트 데이터 수신 |
| notihub | 6500 | TCP/UDP | 이벤트 알림 |

**로그 확인** 

실행 시 로그는 $WHATAP\_PACKAGE /logs 하위에 출력되므로, 본 경로의 로그를 확인하여 이상 로그 출력 여부를 점검합니다. 서버 초기 기동 시의 상호 접속 실패로 인한 로그는 이상 로그로 간주하지 않습니다. 

| 설치 형태 구분 | 어플리케이션 로그 |
| :--- | :--- |
| 최소형/확장형 | front.log |
|  | keeper.log |
|  | yard.log |
|  | proxy.log |
|  | notihub.log |
| 확장형 | eureka.log |
|  | gateway.log |

      

**실행 화면 확인** 

front 서버의 기동이 정상 완료되면, admin@whatap.io / admin 계정으로 로그인 합니다.   
본 계정은 와탭 수집 서버 관리용으로 사용되는 계정으로, 수집 서버 관리용으로만 사용합니다. 본 계정으로는 프로젝트를 생성하지 않습니다.

화면 우상단의 계정메뉴\(이메일 클릭시 노출\)에서 사이트 관리를 선택하여 각 화면에 표시되는 내용을 확인합니다. 하기의 메뉴가 노출됩니다.

* SERVERS: 서버 관리 현황 
* ACCOUNTS: 계정 관리 
* PROJECTS: 프로젝트 생성 현황 
* NOTICE: 공지사항 등록 관리 \(설치형에서는 사용불가\) 
* REGIONS: 수집 서버 관리 리전 정보 
* MAIL: 최소형 설치 시 메일 설정 변경 
* SITELOGO: 설치형 제품의 로고 변경 옵션

### 점검 

이후 점검은 신규 계정을 생성하여 진행합니다. 최소 점검 사항은 다음과 같습니다. 

* 계정 생성 : 로그인 페이지 하단의 계정 생성 링크 또는 사이트 관리자 메뉴의 ACCOUNTS를 통해 계정을 생성합니다. 사이트 관리자 메뉴를 통해 계정을 생성하는 경우, 패스워드에 대한 제약이 존재하지 않습니다. 
* 프로젝트 생성 : 새로 생성한 계정으로 프로젝트를 생성하여 프로젝트 생성 시 이상 현상이 발생하지 않는지 확인합니다. 
* 프로젝트 라이선스 발급 : 프로젝트 카드 클릭 시의 설치 안내 페이지에서 라이선스 발급 버튼을 클릭하고, 이상 현상 발생 여부를 확인합니다. 
* 에이전트를 적용하고 기능 체크를 수행합니다.

## 확장형 설치 예제

### 환경

예제에 사용 되는 환경은 다음과 같습니다. 

<table>
  <thead>
    <tr>
      <th style="text-align:left">호스트명</th>
      <th style="text-align:left">항목</th>
      <th style="text-align:left">내</th>
      <th style="text-align:left">비</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">vmsvr01</td>
      <td style="text-align:left">용도</td>
      <td style="text-align:left">front 서버</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">vmsvr01</td>
      <td style="text-align:left">OS</td>
      <td style="text-align:left">X86 Linux</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">vmsvr01</td>
      <td style="text-align:left">IP</td>
      <td style="text-align:left">192.168.122.21</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">vmsvr01</td>
      <td style="text-align:left">구동 서비스</td>
      <td style="text-align:left">
        <p>Eureka</p>
        <p>Front</p>
        <p>Account</p>
        <p>Notihub</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">vmsvr02</td>
      <td style="text-align:left">용도</td>
      <td style="text-align:left">yard 서버</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">vmsvr02</td>
      <td style="text-align:left">OS</td>
      <td style="text-align:left">X86 Linux</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">vmsvr02</td>
      <td style="text-align:left">IP</td>
      <td style="text-align:left">192.168.122.22</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">vmsvr02</td>
      <td style="text-align:left">구동 서비스</td>
      <td style="text-align:left">
        <p>Keeper
          <br />Gateway</p>
        <p>Proxy</p>
        <p>Yard</p>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>### 설치 절차

예제 환경의 설치 절차는 다음과  같습니다. 방화벽, JDK 와 같은 제반 환경은 사전 구성되어 있어야 합니다.  

#### Front 서버 설치

1.설치 파일 업로드

```bash
whatap@vmsvr01:/apps$ ls -alrt
합계 769828
drwxr-xr-x 25 root   root        4096  8월 14 17:15 ..
drwxr-xr-x  2 whatap whatap      4096  9월 27 12:08 .
-rw-r--r--  1 whatap whatap 788295680  9월 27 12:08 whatap_multi-1.1.4.2092.tar
```

2. 압축 해제 

```bash
whatap@vmsvr01:/apps$ tar -xvf whatap_multi-1.1.4.2092.tar
```

3. 실행 파일 권한 추가

```bash
whatap@vmsvr01:/apps/whatap/bin$ chmod +x *sh
```

4. Linux 환경에서 불필요 파일 제거

```bash
whatap@vmsvr01:/apps/whatap/bin$ rm -f *.bat *.exe *solaris.sh
```

5. Yard 관련 모듈 제거 - \(선택사항\)

_운영 과정에서 발생 할 수 있는 오류요소 제거를 위해 Front 에서 사용 되지 않는 실행 파일을 삭제합니다._ 

```bash
whatap@vmsvr01:/apps/whatap/bin$ rm -f gateway.sh keeper.sh *yard* proxy.sh billing.sh billing.sh adaptor.sh start.sh stop.sh noti.sh
```

6. Account 설정

{} 내 항목을 아래 값으로 변경합니다. 

| 항목 | 값 |
| :--- | :--- |
| {EUREKA\_IP\_accessable\_from\_ACCOUNT} | 192.168.122.21 |
| {ACCOUNT} | ACCOUNT |
| {ACCOUNT\_IP\_accessable\_from\_GATEWAY} | 192.168.122.21 |
| {FIRST\_REGION\_ID/NAME} | REGION-01 |
| {FIRST\_REGION\_DISPLAY\_NAME} | REGION-01 |
| {PROXY\_IPs\_accessable\_from\_AGENTS} | 192.168.122.22 |
| {ip address can be showed by ifconfig/ipconfig} | 192.168.122.21 |
| {server license} | 발급된 라이센스  |

{% code-tabs %}
{% code-tabs-item title="/apps/whatap/conf/account.conf" %}
```bash
# Eureka
# eureka.addr=http://whatap:1qaz$RFV@{EUREKA_IP_accessable_from_ACCOUNT}:6761/eureka/
# eureka.hostname={ACCOUNT}
# eureka_client_ip_address={ACCOUNT_IP_accessable_from_GATEWAY}
eureka.addr=http://whatap:1qaz$RFV@192.168.122.21:6761/eureka/
eureka.hostname=ACCOUNT
eureka_client_ip_address=192.168.122.21
ribbon_protocol=http
prefer_ip_address=true

# Region Proxy
#region.id={FIRST_REGION_ID/NAME}
#region.name={FIRST_REGION_DISPLAY_NAME}
#region.proxy.address={PROXY_IPs_accessable_from_AGENTS}
region.id=REGION-01
region.name=REGION-01
region.proxy.address=192.168.122.22
prefer_ip_address=true

# DB
# Relative path from Home or Absolute path
h2.file.path=./db
db_driver=org.h2.Driver
h2_auto_server=true
h2_bind_address=127.0.0.1
jpa_ddl_auto=update
db_name=account
db_name_project=account

# Admin Account
domain=apm.whatap.io
database.init=true
admin.email=admin@whatap.io
admin.password=admin

# License
owner=192.168.122.21
license=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
{% endcode-tabs-item %}
{% endcode-tabs %}

7. Front 설정

{} 내 항목을 아래 값으로 변경합니다. 

| 항목 | 값 |
| :--- | :--- |
| {EUREKA\_IP\_accessable\_from\_FRONT} | 192.168.122.21 |
| {FRONT} | FRONT |
| {FRONT\_IP} | 192.168.122.21 |

{% code-tabs %}
{% code-tabs-item title="/apps/whatap/conf/front.conf" %}
```bash
# Eureka
#eureka.addr=http://whatap:1qaz$RFV@{EUREKA_IP_accessable_from_FRONT}:6761/eureka/
#eureka.hostname={FRONT}
#eureka_client_ip_address={FRONT_IP}
eureka.addr=http://whatap:1qaz$RFV@192.168.122.21:6761/eureka/
eureka.hostname=FRONT
eureka_client_ip_address=192.168.122.21
ribbon_protocol=http
prefer_ip_address=true

# Front Control
standalone=false
domain=apm.whatap.io
whatap.admin=admin@whatap.io
loginable=true
sessionTimeoutSecs=-1
login_footer_visible=false

# NotiHub
notihub.enable=true
```
{% endcode-tabs-item %}
{% endcode-tabs %}

8. Notihub 설정

{} 내 항목을 아래 값으로 변경합니다. 

| 항목 | 값 |
| :--- | :--- |
| {EUREKA\_IP\_accessable\_from\_FRONT} | 192.168.122.21 |
| {NOTIHUB} | NOTIHUB |
| {NOTIHUB\_IP} | 192.168.122.21 |

{% code-tabs %}
{% code-tabs-item title="/apps/whatap/conf/notihub.conf" %}
```bash
# Eureka
eureka.enable=true
#eureka.addr=http://whatap:1qaz$RFV@{EUREKA_IP_accessable_from_NOTI}:6761/eureka/
#eureka.hostname={NOTIHUB}
#eureka_client_ip_address={NOTIHUB_ADDRESS}
eureka.addr=http://whatap:1qaz$RFV@192.168.122.21:6761/eureka/
eureka.hostname=NOTIHUB
eureka_client_ip_address=192.168.122.21
ribbon_protocol=http
prefer_ip_address=true

# H2 DB
# Relative path from Home or Absolute path
h2.file.path=./db
h2_auto_server=true
db_driver_event=org.h2.Driver
h2_bind_address=0.0.0.0

jpa_show_sql=false
jpa_generate_ddl=true
jpa_ddl_auto=update

# Mail
mail.sender=no-reply@whatap.io
mail.smtp.debug=false
mail.host=
mail.username=
mail.password=
mail.smtp.protocol=smtp
mail.port=25
mail.smtp.auth=true
mail.smtp.ssl.enable=false
mail.smtp.starttls.enable=true
mail.smtp.starttls.required=true
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Yard 서버 설치

1.설치 파일 업로드

```bash
whatap@vmsvr02:/apps$ ls -alrt
합계 769828
drwxr-xr-x 25 root   root        4096  8월 14 17:15 ..
drwxr-xr-x  2 whatap whatap      4096  9월 27 12:08 .
-rw-r--r--  1 whatap whatap 788295680  9월 27 12:08 whatap_multi-1.1.4.2092.tar
```

2. 압축 해제 

```bash
whatap@vmsvr02:/apps$ tar -xvf whatap_multi-1.1.4.2092.tar
```

3. 실행 파일 권한 추가

```bash
whatap@vmsvr02:/apps/whatap/bin$ chmod +x *sh
```

4. Linux 환경에서 불필요 파일 제거

```bash
whatap@vmsvr02:/apps/whatap/bin$ rm -rf *.bat *.exe *solaris.sh
```

5. Front 관련 항목 제거 - \(선택사항\)

_운영 과정에서 발생 할 수 있는 오류요소 제거를 위해 Yard 에서 사용 되지 않는 실행 파일을 삭제합니다._ 

```bash
whatap@vmsvr02:/apps/whatap/bin$ rm -f account.sh eureka.sh adaptor.sh billing.sh noti* start.sh *front.sh
```

6. Gateway 설정

{} 내 항목을 아래 값으로 변경합니다. 

| 항목 | 값 |
| :--- | :--- |
| {EUREKA\_IP\_accessable\_from\_GATEWAY} | 192.168.122.21 |
| {GATEWAY} | GATEWAY |
| {GATEWAY\_IP\_accessable\_from\_ACCOUNT} | 192.168.122.22 |
| {KEEPER\_IP\_accessable\_from\_GATEWAY} | 192.168.122.22 |
| {REGION\_NAME\_displayed\_by\_SiteAdminPage} | REGION-01 |

{% code-tabs %}
{% code-tabs-item title="/apps/whatap/conf/gateway.conf" %}
```bash
# Eureka
#eureka.addr=http://whatap:1qaz$RFV@{EUREKA_IP_accessable_from_GATEWAY}:6761/eureka/
#eureka.hostname={GATEWAY}
#eureka_client_ip_address={GATEWAY_IP_accessable_from_ACCOUNT}
eureka.addr=http://whatap:1qaz$RFV@192.168.122.21:6761/eureka/
eureka.hostname=GATEWAY
eureka_client_ip_address=192.168.122.22
prefer_ip_address=true

# Keeper
#keeper={KEEPER_IP_accessable_from_GATEWAY}:6789
keeper=192.168.122.22:6789

# Account 의 Region Value
#region.name={REGION_NAME_displayed_by_SiteAdminPage}
region.name=REGION-01
```
{% endcode-tabs-item %}
{% endcode-tabs %}

7. Proxy 설정

{} 내 항목을 아래 값으로 변경합니다. 

| 항목 | 값 |
| :--- | :--- |
| {KEEPER\_IP\_accessable\_from\_PROXY} | 192.168.122.22 |
| {PROXY-01} | PROXY-01 |

{% code-tabs %}
{% code-tabs-item title="/apps/whatap/conf/proxy.conf" %}
```bash
# Keeper
#keeper={KEEPER_IP_accessable_from_PROXY}:6789
#server.name={PROXY-01}
keeper=192.168.122.22:6789
server.name=PROXY-01
secure_file_name=secure.conf

# Self Monitoring
selfmon.enabled=false
```
{% endcode-tabs-item %}
{% endcode-tabs %}

8. Yard 설정

{} 내 항목을 아래 값으로 변경합니다. 

| 항목 | 값 |
| :--- | :--- |
| {KEEPER\_IP\_accessable\_from\_YARD} | 192.168.122.22 |
| {YARD-01} | YARD-01 |
| notihub=127.0.0.1:6500 | notihub=192.168.122.21:6500 |

{% code-tabs %}
{% code-tabs-item title="/apps/whatap/conf/yard.conf" %}
```bash
# Keeper
keeper={KEEPER_IP_accessable_from_YARD}:6789
server.name={YARD-01}

# Port
web.port=7710
data.port=6610

# Self Monitoring
selfmon.enabled=false

# Noti
#net_noti_ip={NOTI_IP_accessable_from_YARD}
#net_noti_port=6500

# NotiHub
notihub_enabled=true
#notihub=127.0.0.1:6500
notihub=192.168.122.21:6500
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 기동

#### Front 서버 기동

1.Eureka, Front, Account 기동

```bash
whatap@vmsvr01:/apps/whatap/bin$ ./control.sh eureka start
whatap@vmsvr01:/apps/whatap/bin$ ./control.sh front start
whatap@vmsvr01:/apps/whatap/bin$ ./control.sh account start
```

또는

```bash
whatap@vmsvr01:/apps/whatap/bin$ ./start_front.sh
```

2. Notihub 기동

```bash
whatap@vmsvr01:/apps/whatap/bin$ ./control.sh notihub start
```

#### Yard 서버 기동

1.Keeper, Gateway, Proxy, Yard 기동

```bash
whatap@vmsvr02:/apps/whatap/bin$ ./control.sh keeper start
whatap@vmsvr02:/apps/whatap/bin$ ./control.sh gateway start
whatap@vmsvr02:/apps/whatap/bin$ ./control.sh proxy start
whatap@vmsvr02:/apps/whatap/bin$ ./control.sh yard start
```

또는

```bash
whatap@vmsvr02:/apps/whatap/bin$ ./start_yard.sh
```

### 설치 확인

브라우저에서 http://192.168.122.21:8080 에 admin@whatap.io 로 접속 후 확인합니다. 

1.우측 상단의 계정명 클릭해 "사이트 관리" 메뉴로 이동

![](../.gitbook/assets/2018-09-27-3.08.19.png)

  
2. 등록항목 확인 및 REGION-01 정보 확인

NOTIHUB, REGION-01, FRONT, ACCOUNT 항목이 보여지는지 확인 후 REGION-01의 화살표 버튼을 클릭해 이

![](../.gitbook/assets/2018-09-27-3.11.52.png)

3. REGION-01 세부 정보 확인

KEEPER, PROXY, YARD 정보가 확인되면 정상

![](../.gitbook/assets/2018-09-27-3.17.40.png)

## FAQ 

### 라이선스 만기 및 연장 요청 

라이선스 만기 시, 사이트에 라이선스 만기임을 알리는 페이지가 표시됩니다. 라이선스 만기는 매시 라이선스의 사용기간 및 사용량을 체크하여 라이선스 허용치를 초과 여부를 통해 결정합니다.  
라이선스 연장 요청 절차는 최초 발급 시와 동일하며, 연장 요청임을 명시하여 요청합니다.

### 재설치 

설정 오류 혹은 설정 변경을 통해 문제를 해결할 수 없는 경우, 재설치 하는 과정을 안내합니다.  
재설치 시, 기존 모니터링 정보는 폐기합니다. 

* 로그 삭제 

```bash
$ cd $WHATAP_PACKAGE $ rm -rf logs/*
```

* 모니터링 데이터 삭제 

```bash
$ cd $WHATAP_PACKAGE $ rm -rf yardbase/*
```

* DB 삭제 

```bash
$ cd $WHATAP_PACKAGE $ rm -rf db/*.db
```

이후 재설치 과정은 신규 설치 과정과 동일합니다.

### 사이트 관리자 패스워드 

사이트 관리자 계정\(admin@whatap.io\) 은 변경 불가합니다.   
사이트 관리자 계정의 패스워드는 front.conf의 admin.password 를 통해 설정 가능합니다.

### 포트 변경 

어플리케이션 서버는 디폴트로 지정된 포트가 사전 점유되어 있는 경우, 포트 번호를 +1씩 증가시켜 가용한 포트를 활용합니다. 임의로 포트를 지정하여 사용해야 할 경우 다음의 옵션을 적용합니다.

| 파일 | 설정 | 용도 | 디폴트 |
| :--- | :--- | :--- | :--- |
| front.conf | web.port | 사이트 접근 | 8080 |
| proxy.conf | data.port | 모니터링 데이터 수신 \(서버측\) | 6600 |
| whatap.conf | whatap.server.port | 모니터링 데이터 전송\(에이전트\)  | 6600 |

### 설치 파일 다운로드 

문의처로 요청시 Google Drive 및 AWS S3를 통해 제공 \(라이선스 요청 시 별도 제공\)

### MySQL DB 사용

수집된 모니터링 데이터는 RDB 를 사용하지 않고 와탭 만의 독자적인 저장구조를 가지지만 이외 계정 정보, 구성 정보, 알림 발송 이력은 내장 DB인 H2를 사용합니다. 이를 MySQL DB로 변경하는 방법 입니다. 

1.계정 정보 및 구성 정보의 MySQL 사용

${WHATAP\_HOME}/conf/account.conf 에서 DB 항목을  다음과 같이 변경합니다. 

_MySQL에서 account 명의 DB와 CRUD 권한이 있는 {whatap\_dbuser} 가 존재 해야 합니다._ 

{% code-tabs %}
{% code-tabs-item title="/apps/whatap/conf/account.conf" %}
```bash
...

# DB
# Relative path from Home or Absolute path
#h2.file.path=./db
#db_driver=org.h2.Driver
#h2_auto_server=true
#h2_bind_address=127.0.0.1
#jpa_ddl_auto=update
#db_name=account
#db_name_project=account

# DB for MySQL
db_driver=com.mysql.jdbc.Driver
jdbc_url=jdbc:mysql://127.0.0.1:3306
db_username={whatap_dbuser}
db_password={whatap_dbpassword}
db_name=account
db_name_project=account

...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

2. 알람발송 이력의 MySQL 사용

${WHATAP\_HOME}/conf/notihub.conf 에서 DB 항목을 다음과 같이 변경합니다.

{% code-tabs %}
{% code-tabs-item title="/apps/whatap/conf/notihub.conf" %}
```bash
...

# H2 DB
# Relative path from Home or Absolute path
#h2.file.path=./db
#h2_auto_server=true
#db_driver_event=org.h2.Driver
#h2_bind_address=0.0.0.0

db_driver_event=com.mysql.jdbc.Driver
jdbc_url_event=jdbc:mysql://192.168.122.201:3306
db_username_event=whatap
db_password_event=userpassword
db_name_event=account

...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

3. 관련 서비스를 재기동 합니다. 

```bash
$ ./control.sh account restart
$ ./control.sh notihub restart
```

### 문의처 

송재진 \(jjsong@whatap.io, 010.7288.3384\)  
박명규 \(mkpark@whatap.io, 010.8972.4012\)

