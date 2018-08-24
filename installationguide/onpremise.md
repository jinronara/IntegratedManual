# 설치형 서버

### 안내사항

수집 서버가 설치될 장비의 IP 및 수집 규모에 따른 라이센스 발급을 진행합니다.   
라이센스 발급은 license@whatap.io에 필요사항을 기술하여 요청합니다. 

* 설치 환경 식별을 위한 명칭: 고객사 + 사업명 
* 고객사 담당자: 이름, 전화번호, 이메일 
* 라이선스 시작일 
* 라이선스 종료일: 종료일 0시에 제한되므로 종료일 + 1로 요청 
* 인프라 모니터링 대상 코어 수/에이전트 수: 코어 또는 에이전트 수 \(정식 라이센스는 에이전트 수 기준임\) 
* 어플리케이션 모니터링 대상 코어 수/에이전트 수 \(정식 라이센스는 코어 수 기준임\)

이벤트 알림을 위한 설정은 계약 완료 시점 이후 별도의 절차로 진행합니다. 단 본 문서에는 이벤트 알림용 notihub 서버와 관련한 사항도 기술합니다.

### **수집 서버 권장 사양**

#### 방화벽 오픈

* 에이전트 설치대상 -&gt; 수집 서버 \(TCP 6600 포트\)
* 모니터링 PC -&gt; 수집 서버 \(TCP 8080 포트\)

#### 파일 디스크립터 설정의 상향 조정

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

### **설치 작업 절차**

#### 설치 파일 및 라이센스 파일을 설치 대상 서버에 업로드 

단일 서버에 구성하는 경우, 최소형 패키지를 활용하며 향후 확장성을 고려할 때 확장형 패키지를 활용하여 설치를 진행합니다. JDK 및 와탭 모니터링 패키지를 설치 대상 서버에 업로드 하고 압축을 해제합니다. 

* 최소형 패키지: whatap\_single-\#.\#.\#.\#\#\#\#.tar
*  확장형 패키지: whatap\_multi-\#.\#.\#.\#\#\#\#.tar 
* Oracle JDK 1.7 이상
* 라이센스 파일: 텍스트 파일로 준

와탭 모니터링 패키지를 압축 해제하면 whatap\_package 라는 디렉토리로 압축이 해제됩니다. 본 문서에서 이후 해당 경로를 $WHATAP\_PACKAGE로 기술합니다.

#### JDK 설치 

Oracle JDK 1.7 이상의 버전이 사전에 설치되어 있는 경우 이를 활용합니다. 설치되어 있지 않은 경우, JDK를 설치합니다. 본 문서에서 이후 JDK 설치 경로를 $JDK로 기술합니다.

### 실행 파일 편집 

$WHATAP\_PACKAGE/bin 하위에는 쉘 스크립트가 존재합니다. 스크립트에 실행 권한을 부여합니다. 

```bash
$ cd $WHATAP_PACKAGE/bin 
$ chmod +x *.sh
```

이후 쉘 스크립트를 편집하여 JAVA\_HOME 경로를 지정합니다.   
\(예시 front.sh\)

```bash
#!/usr/bin/env bash
SERVICE_NAME=front.apm
JAVA_HOME=$JDK
SERVER_HOME=cd ..;pwd LIB_HOME=$SERVER_HOME/lib CONF_PATH=$SERVER_HOME/conf
EXE_JAR=ls $LIB_HOME/*.${SERVICE_NAME}.boot* | sort | tail -1 $JAVA_HOME/bin/java -Djava.security.egd=/dev/./urandom -Dwhatap.log.path=. -Xmx512m -jar $EXE_JAR
```

최소형 설치의 경우 front.sh, keeper.sh, yard.sh, proxy.sh 가 사용되고, 확장형 설치의 경우 eureka.sh, account.sh, front.sh / keeper.sh, yard.sh, proxy.sh, gateway.sh 가 사용됩니다.   
부가적으로 이벤트 알림 설정을 추가할 경우 notihub.sh가 사용됩니다.

### 설정편집

$WHATAP\_PACKAGE/lib 하위에는 어플리케이션 라이브러리\(jar\), $WHATAP\_PACKAGE/conf 하위에는 설정 파일\(conf\)이 존재합니다. 설정 파일을 편집합니다. 실행 파일 편집 시 개행 코드로 인한 문제 발생 시에는 vi에디터에서 :set ff=unix 로 지정하고 편집합니다.

각 설정 파일에는 필수로 설정해야 하는 정보를 수정합니다.

| 구분  | 파일명 | 항목명 | 설정  |
| :--- | :--- | :--- | :--- |
| 최소형 | account.conf | owner | ifconfig/ipconfig로 식별 가능한 IP |
|  |  | license | 발급받은 서버 라이센스 |
|  | front.conf | region.proxy.address | 에이전트가 데이터를 전송하게 될 수집 서버의 IP |
|  |  | admin.password | 사이트 관리자 계정 패스워드 \(초기값 : admin\) |
|  | notihub.conf | mail.host  | SMTP 연계를 통한 초대 메일 및 알람발송 등 적용 시  |
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
| 확장형 | account.conf |  |  |

### **실행 확인**

### FAQ



## 

  
  
  
  owner ifconfig/ipconfig로 확인 가능한 account 서버 IP license 발급받은 서버 라이센스 eureka.addr eureka 서버 접근 정보 eureka.hostname eureka에 등록할 명칭\(복수의 서버가 동일 명칭을 가질 수 있음\) eureka\_client\_ip\_address gateway에서 접근 가능한 account 서버 IP region.id 첫 번째 리전의 ID region.name  
region.proxy.address 첫 번째 리전의 proxy IP\(복수 지정 가능\) mail.host SMTP 연계를 통한 초대 메일 발송 등 적용 시 mail.port  
mail.username  
mail.password  
mail.sender  
mail.smtp.auth  
mail.smtp.ssl.enable  
mail.smtp.starttls.enable  
mail.smtp.starttls.required  
front.conf eureka.addr eureka 서버 접근 정보 eureka.hostname eureka에 등록할 명칭\(복수의 서버가 동일 명칭을 가질 수 있음\) eureka\_client\_ip\_address front 서버 IP admin.password 사이트 관리자 계정 패스워드 \(초기값 : admin\) yard.conf keeper yard에서 접근 가능한 keeper 서버 IP:Port server.name keeper에 등록할 이름\(서버 단위\) net\_noti\_ip yard에서 접근 가능한 noti 서버 IP proxy.conf keeper proxy에서 접근 가능한 keeper 서버 IP:Port server.name keeper에 등록할 이름\(서버 단위\) gateway.conf eureka.addr eureka 서버 접근 정보 eureka.hostname eureka에 등록할 명칭\(복수의 서버가 동일 명칭을 가질 수 있음\) eureka\_client\_ip\_address account/front 에서 접근 가능한 gateway 서버 IP keeper gateway에서 접근 가능한 keeper 서버 IP:Port region.name region 명 첫 번째 region명은 account.conf에서 지정한 region.name과 일치해야 함 두 번째 이후 region명은 사이트 관리자 페이지에서 지정한 region명과 일치해야 함 noti.conf eureka.addr eureka 서버 접근 정보 eureka.hostname eureka에 등록할 명칭\(복수의 서버가 동일 명칭을 가질 수 있음\) eureka\_client\_ip\_address noti 서버 IP keeper noti에서 접근 가능한 keeper 서버 IP:Port mail.host 이벤트 알림 중 SMTP를 통한 메일 발송 기능 적용 시 mail.port  
mail.username  
mail.password  
mail.sender  
mail.smtp.auth  
mail.smtp.ssl.enable  
mail.smtp.starttls.enable  
mail.smtp.starttls.required  
smsformat 이벤트 알림 중 문자 발송 시 고객사 커스터마이징 설정을 지정 smssender

1.3.5. 로그 경로 변경 실행 시 로그는 $WHATAP\_PACKAGE /logs/{server명}.log 로 출력됩니다.

로그를 외부 경로에 출력할 경우 다음과 같이 지정합니다. $ cd $WHATAP\_PACKAGE $ rmdir logs $ ln -s {외부경로} logs $ cd javam/server $ ln -s {외부경로} logs

1.3.6. 실행 서버 실행은 $WHATAP\_PACKAGE /bin/control.sh를 통해 실행하게 된다. 최소형 설치본의 경우 $WHATAP\_PACKAGE /bin/start.sh, $WHATAP\_PACKAGE /bin/stop.sh 파일을 통해서도 실행/정지가 가능합니다.

1.3.6.1. control.sh 를 통한 실행 control.sh를 통해 최소형 서버 실행 시에는 다음의 명령을 통해 실행하게 됩니다.  ./control.sh keeper start  ./control.sh front start  ./control.sh yard start  ./control.sh proxy start  ./control.sh noti start \(이벤트 알림 설정 시\)

확장형 서버 실행 시에는 front를 구성한 서버에서 다음의 명령을 실행합니다.  ./control.sh eureka start  ./control.sh account start  ./control.sh front start

yard 구성 서버에서 다음의 명령을 실행합니다.  ./control.sh keeper start  ./control.sh yard start  ./control.sh proxy start  ./control.sh gateway start  ./control.sh noti start

control.sh 실행 시 다음과 같이 메뉴를 선택하여 작업을 수행할 수도 있습니다. \(예시\) 사용법 출력 $ cd $WHATAP\_PACKAGE/bin

### $ ./control.sh

\[ Usage \] ./control.sh \[ service\_name \[ command \]\] ./control.sh menu ./control.sh start-multi ./control.sh restart-multi ./control.sh start-single ./control.sh restart-single ./control.sh stop-all ./control.sh status-all ./control.sh front \(status/start/stop/restart\) ./control.sh proxy \(status/start/stop/restart\) ./control.sh yard \(status/start/stop/restart\) ./control.sh keeper \(status/start/stop/restart\) ./control.sh noti \(status/start/stop/restart\) ./control.sh billing \(status/start/stop/restart\) ./control.sh eureka \(status/start/stop/restart\) ./control.sh gateway \(status/start/stop/restart\) ./control.sh account \(status/start/stop/restart\)

### ./admin\_console.sh

\(예시\) 메뉴 선택형 모드 ./control.sh menu

Select type

1. service start/stop
2. status-all
3. start-multi
4. stop-all
5. restart-multi
6. start-single
7. restart-single
8. Exit

   number&gt;{원하는 메뉴 번호를 입력함}

Select command

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
13. noti start
14. noti stop
15. noti restart
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
28. restart-all
29. menu
30. Exit

    number&gt;{원하는 메뉴 번호를 입력함}

1.3.7. 실행 확인 기동 완료 여부는 서버의 포트 리스닝 여부와 로그를 확인합니다.

1.3.7.1. 포트 리스닝 확인 구성 환경에 따른 서버의 포트 리스닝 여부를 체크합니다. $ netstat -na \| grep {체크 대상 포트} \| grep LISTEN

1.3.7.1.1. 최소형

어플리케이션 서버 포트 프로토콜 용도 front \(+account\) 8080 HTTP 모니터링 사이트 keeper 6789 TCP/UDP 서버 정보 수신 yard 7710 TCP 모니터링 데이터 조회 6610 TCP 모니터링 데이터 저장 proxy 6600 TCP 에이전트 데이터 수신 noti 6500 TCP/UDP 이벤트 알림

1.3.7.1.2. 확장형

어플리케이션 서버 포트 프로토콜 용도 eureka 6761 TCP 서버 위치 관리 account 18080 HTTP 계정 관리 front 8080 HTTP 모니터링 사이트 gateway 8800 TCP 리전 요청 수신 keeper 6789 TCP/UDP 서버 정보 수신 yard 7710 TCP 모니터링 데이터 조회 6610 TCP 모니터링 데이터 저장 proxy 6600 TCP 에이전트 데이터 수신 noti 6500 TCP/UDP 이벤트 알림

1.3.7.2. 로그 확인 실행 시 로그는 $WHATAP\_PACKAGE /logs 하위에 출력되므로, 본 경로의 로그를 확인하여 이상 로그 출력 여부를 점검합니다. 서버 초기 기동 시의 상호 접속 실패로 인한 로그는 이상 로그로 간주하지 않습니다. 설치 형태 구분 어플리케이션 로그 최소형/확장형 front.log keeper.log yard.log proxy.log noti.log 확장형 eureka.log gateway.log

1.3.7.3. 실행 화면 확인 front 서버의 기동이 정상 완료되면, admin@whatap.io / admin 계정으로 로그인 합니다. 본 계정은 와탭 수집 서버 관리용으로 사용되는 계정으로, 수집 서버 관리용으로만 사용합니다. 본 계정으로는 프로젝트를 생성하지 않습니다.

화면 우상단의 계정메뉴\(이메일 클릭시 노출\)에서 사이트 관리를 선택하여 각 화면에 표시되는 내용을 확인합니다. 하기의 메뉴가 노출됩니다.  SERVERS: 서버 관리 현황  ACCOUNTS: 계정 관리  PROJECTS: 프로젝트 생성 현황  NOTICE: 공지사항 등록 관리 \(설치형에서는 사용불가\)  REGIONS: 수집 서버 관리 리전 정보  MAIL: 최소형 설치 시 메일 설정 변경  SITELOGO: 설치형 제품의 로고 변경 옵션

1.3.8. 점검 이후 점검은 신규 계정을 생성하여 진행합니다. 최소 점검 사항은 다음과 같습니다.  계정 생성 : 로그인 페이지 하단의 계정 생성 링크 또는 사이트 관리자 메뉴의 ACCOUNTS를 통해 계정을 생성합니다. 사이트 관리자 메뉴를 통해 계정을 생성하는 경우, 패스워드에 대한 제약이 존재하지 않습니다.  프로젝트 생성 : 새로 생성한 계정으로 프로젝트를 생성하여 프로젝트 생성 시 이상 현상이 발생하지 않는지 확인합니다.  프로젝트 라이선스 발급 : 프로젝트 카드 클릭 시의 설치 안내 페이지에서 라이선스 발급 버튼을 클릭하고, 이상 현상 발생 여부를 확인합니다.  에이전트를 적용하고 기능 체크를 수행합니다.

1.4. FAQ 1.4.1. 라이선스 만기 및 연장 요청 라이선스 만기 시, 사이트에 라이선스 만기임을 알리는 페이지가 표시됩니다. 라이선스 만기는 매시 라이선스의 사용기간 및 사용량을 체크하여 라이선스 허용치를 초과 여부를 통해 결정합니다.

라이선스 연장 요청 절차는 최초 발급 시와 동일하며, 연장 요청임을 명시하여 요청합니다.

1.4.2. 재설치 설정 오류 혹은 설정 변경을 통해 문제를 해결할 수 없는 경우, 재설치 하는 과정을 안내합니다.

재설치 시, 기존 모니터링 정보는 폐기합니다.  로그 삭제 $ cd $WHATAP\_PACKAGE $ rm -rf logs/\*

 모니터링 데이터 삭제 $ cd $WHATAP\_PACKAGE $ rm -rf yardbase/\*

 DB 삭제 $ cd $WHATAP\_PACKAGE $ rm -rf db/\*.db

이후 재설치 과정은 신규 설치 과정과 동일합니다.

1.4.3. 사이트 관리자 패스워드 사이트 관리자 계정\(admin@whatap.io\) 은 변경 불가합니다. 사이트 관리자 계정의 패스워드는 front.conf의 admin.password 를 통해 설정 가능합니다.

1.4.4. 포트 변경 어플리케이션 서버는 디폴트로 지정된 포트가 사전 점유되어 있는 경우, 포트 번호를 +1씩 증가시켜 가용한 포트를 활용합니다. 임의로 포트를 지정하여 사용해야 할 경우 다음의 옵션을 적용합니다.

파일 설정 용도 디폴트 front.conf web.port 사이트 접근 8080 proxy.conf data.port 모니터링 데이터 수신 \(서버측\) 6600 whatap.conf whatap.server.port 모니터링 데이터 전송\(에이전트\) 6600

1.4.5. 설치 자원 Google Drive 및 AWS S3를 통해 제공 \(라이선스 요청 시 별도 제공\)

1.4.6. 문의처 서영일 \(yiseo@whatap.io, 010.3255.6480\) 이병우 \(bulee@whatap.io, 010.8250.1525\)

Host파일에

121.166.140.134 wiki.whatapkvm.io

[http://wiki.whatapkvm.io/whatap\_single.tar](http://wiki.whatapkvm.io/whatap_single.tar)

[http://wiki.whatapkvm.io/tomcat85.tar.gz](http://wiki.whatapkvm.io/tomcat85.tar.gz)

[http://wiki.whatapkvm.io/jemeter.tar.gz](http://wiki.whatapkvm.io/jemeter.tar.gz)

[http://톰켓서버IP:8080/petstore/sleep.jsp](http://톰켓서버IP:8080/petstore/sleep.jsp)

