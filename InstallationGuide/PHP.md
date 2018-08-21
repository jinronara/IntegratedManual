### PHP 애플리케이션 모니터링 {#user-content-php-애플리케이션-모니터링}

#### 에이전트 실행 및 모니터링 개요 {#user-content-에이전트-실행-및-모니터링-개요-1}

와탭 PHP 애플리케이션 모니터링은 PHP 기반 웹 애플리케이션 서버 모니터링 서비스를 제공합니다.

**에이전트 설치 방식 개요**

PHP 모니터링 서비스를 사용하기 위해서는 모니터링 대상 애플리케이션에 모니터링 에이전트를 설치해야 합니다. 설치 방식은 리눅스 패키지 설치로 가능합니다.

* 와탭 저장소\(Repository\)를 설치합니다.
* whatap-php 리눅스 패키지를\(yum, apt-get\) 설치합니다.
* 설정 스크립트를 실행합니다.
* Apache 또는 PHP-FRPM을 재시작 합니다.

설정 스크립트를 통해서 트레이서는 PHP 확장 모듈\(PHP Extension module\)로 등록되고, 에이전트는 whatap-php 서비스\(Service\)로 실행됩니다.[![490](https://github.com/jinronara/deleteme_2/raw/master/images/490.png)](https://github.com/jinronara/deleteme_2/blob/master/images/490.png)

**구성 파일**

모니터링 정보를 수집하기 위한 트레이서, 수집된 정보를 서버에 전송하기 위한 에이전트, 트레이서와 에이전트를 서버에 동적으로 적용하기 위한 설치 스크립트 파일로 구성됩니다.

PHP 모니터링 서비스를 구성하는 각 파일의 역할은 다음과 같습니다.

| 파일명 | 설명 |
| :--- | :--- |
| whatap\_\#\_\#.so | 트레이서 PHP 확장 모듈\(PHP Extension module\)로 추가 되어 정보를 수집하고 수집된 정보를 에이전트로 전송하는 라이브러리입니다. |
| whatap-php\(whatap\_php\) | 에이전트, 트레이서에서 UDP로 전달된 정보를 수집서버로 전송하는 프로그램입니다. |
| /etc/init.d/whatap-php | 서비스 스크립트 |
| whatap\_php | 서비스 실행파일 |
| whatap.ini | 애플리케이션 서버의 데이터를 수집하는 PHP 확장 모듈\(PHP Extension module\)의 설정 정보, 수집서버의 주소와 서버의 프로젝트 라이선스 키가 입력되는 파일입니다. |
| whatap-install-\#.log | 설치 과정에 대한 로그 파일입니다. \(/usr/whata/php/logs\) |
| whatap-boot-\#.log | 에이전트 로그 파일 입니다. \(/usr/whata/php/logs\) |
| install.sh | 웹 애플리케이션 서버에 트레이서를 적용하기 위한 쉘 스크립트입니다. |
| Whatap.php \(sample.php\) | PHP 소스코드에서 사용할 API 레퍼런스 클래스 \(/usr/whatap/php/lib/Whatap.php\) 및 예제 소스 파일\(sample.php\) 입니다. |

**에이전트 이름 식별**

와탭은 모니터링 정보 수집 대상인 애플리케이션 서버 식별을 위한 정보로 기본적으로 애플리케이션 서버로부터 수집한 정보를 활용합니다. 기본적으로 활용하는 정보는 애플리케이션 서버 종류, 애플리케이션 서버의 IP, 서비스 포트를 조합하여 애플리케이션 서버를 고유 식별자로 사용하게 되며 필요에 따라 사용자가 지정한 명칭을 사용하거나 패턴을 변경하여 사용하는 것도 가능합니다. 이때에는 꼭 고유한 값이어야 합니다.

애플리케이션 서버로부터 추출한 정보를 활용하는 이유는 애플리케이션 서버 정지, 네트워크 단절 또는 에이전트 문제로 인한 수집 서버와 에이전트의 통신 단절 상태가 복구되었을 경우, 재 접속된 에이전트로부터 송신되는 정보가 기존 에이전트로부터 송신된 정보와의 연속성을 유지하기 위해서 입니다. 와탭이 애플리케이션 서버를 식별하기 위해 사용하는 기본 패턴은 다음과 같습니다.

* default: {type}-{ip2}-{ip3}-{process}

기본 패턴에 대한 변경은 whatap.ini에서 설정에서 가능합니다.

object\_name default: {type}-{ip2}-{ip3}-{process}

| 설정 | 설명 |
| :--- | :--- |
| Type | app\_name |
| Ip\# | Ip를 .으로 나누었을 때 \#번째 자리\(0부터\) |
| Process | app\_process\_name |
| hostname | 호스트 명 |

#### 에이전트 설치/실행/업데이트/중지 {#user-content-에이전트-설치-실행-업데이트-중지-2}

**공통**

**프로젝트 생성**

서버를 등록하기 위해 우선 프로젝트를 생성합니다. 추가 버튼을 선택하면 아래와 같이 프로젝트 생성 창이 나타납니다. PHP 아이콘을 선택한 뒤, 희망하는 프로젝트명과 데이터 서버 지역\(Region\), 소속하게 될 그룹을 선택한 뒤 프로젝트를 생성합니다.[![500](https://github.com/jinronara/deleteme_2/raw/master/images/500.png)](https://github.com/jinronara/deleteme_2/blob/master/images/500.png)

이후, 생성된 프로젝트를 클릭하여 관리 화면에 진입합니다.[![510](https://github.com/jinronara/deleteme_2/raw/master/images/510.png)](https://github.com/jinronara/deleteme_2/blob/master/images/510.png)

**라이선스 발급**

[![520](https://github.com/jinronara/deleteme_2/raw/master/images/520.png)](https://github.com/jinronara/deleteme_2/blob/master/images/520.png)

프로젝트 관리화면에서는 우선적으로 라이선스를 발급 받습니다. 라이선스 키는 프로젝트별로 귀속되기 때문에, 유출되거나 배포되어서는 안됩니다. 반드시 본인 프로젝트에 서버를 등록할 때에만 이용하시기 바랍니다.

**에이전트 설치**

**패키지 설치**

**RedHat/CentOS**

* 패키지 저장소\(Repository\) 등록

와탭 저장소\(Repository\)를 등록합니다.

```text
$ sudo rpm -Uvh http://repo.whatap.io/centos/5/noarch/whatap-repo-1.0-1.noarch.rpm
```

* 패키지 설치

아래 명령어를 통해 패키지를 설치합니다.

```text
$ sudo yum install whatap-php
```

* PHP 확장 모듈\(PHP Extension module\) 및 whatap-php서비스\(Service\) 등록 PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\)를 자동으로 설치할 경우에 아래와 같이 적용합니다

```text
$ sudo /usr/whatap/php/install.sh
Input license key
xxxxxxxxxxxxxxxx                          # 발급된 라이선스 key 입력

Input whatap.server.host
192.x.x.x                                  # 발급된 서버 IP 입력
```

PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\)를 자동으로 인식하지 못하는 경우 아래와 같이 선택 설치를 진행해야 합니다. 주로 Apache 명령어\(apachectl, httpd, apache2\) 및 PHP 명령어\(CLI\)가 기본 경로\($PATH\)에 설정 되어 있지 않거나, 여러 개의 PHP가 설치되어 PHP 명령어\(CLI\)가 여러 개일 경우에 \(php5, php70, php-zts, zts-php…\) 실제로 적용하고 있는 버전을 선택하여 진행합니다.

```text
$ sudo /usr/whatap/php/install.sh manual

Input license key
xxxxxxxxxxxxxxxx                            # 발급된 라이선스 key 입력

Input whatap.server.host
192.x.x.x                                    # 발급된 서버 IP 입력

Input : which apache or php-fpm ex)/usr/sbin/httpd, /usr/sbin/apache2, /usr/sbin/php-fpm ...
/usr/sbin/httpd                             # apache 및 php-fpm 명령어 위치 입력

Input : which php ex) /usr/bin/php, /usr/bin/php5, /usr/bin/php70 ...
/usr/bin/php5                                # php 명령어 위치 입력
```

**Debian/Ubuntu**

* 패키지 저장소\(Repository\) 등록

와탭 저장소\(Repository\)를 등록합니다.

```text
$ wget http://repo.whatap.io/debian/release.gpg -O -|sudo apt-key add -
$ wget http://repo.whatap.io/debian/whatap-repo_1.0_all.deb
$ sudo dpkg -i whatap-repo_1.0_all.deb
$ sudo apt-get update
```

* 패키지 설치

  ```text
  $ sudo apt-get install whatap-php
  ```

* PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\) 등록

PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\)를 자동으로 설치할 경우에 아래와 같이 적용합니다

```text
$ sudo /usr/whatap/php/install.sh

Input license key
xxxxxxxxxxxxxxxx                               # 발급된 라이선스 key 입력

Input whatap.server.host
192.x.x.x                                       # 발급된 서버 IP 입력
```

PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\)를 자동으로 인식하지 못하는 경우 아래와 같이 선택 설치를 진행해야 합니다. 주로 Apache 명령어\(apachectl, httpd, apache2\) 및 PHP 명령어\(CLI\)가 기본 경로\($PATH\)에 설정 되어 있지 않거나, 여러 개의 PHP가 설치되어 PHP 명령어\(CLI\)가 여러 개일 경우에 \(php5, php70, php-zts, zts-php…\) 실제로 적용하고 있는 버전을 선택하여 진행합니다.

```text
$ sudo /usr/whatap/php/install.sh manual

Input license key
xxxxxxxxxxxxxxxx                          # 발급된 라이선스 key 입력

Input whatap.server.host
192.x.x.x                                  # 발급된 서버 Ip 입력

Input : which apache or php-fpm ex)/usr/sbin/httpd, /usr/sbin/apache2, /usr/sbin/php-fpm ...
/usr/sbin/httpd                           # apache 및 php-fpm 명령어 위치 입력

Input : which php ex) /usr/bin/php, /usr/bin/php5, /usr/bin/php70 ...
/usr/bin/php5                             # php 명령어 위치 입력
```

**패키지 설치 확인**

**PHP 확장 모듈**

PHP 추가 INI 경로에 whatap.ini 생성되어 있는지 확인합니다.

```text
$ find / | grep whatap.ini
```

PHP 확장 모듈\(PHP Extension module\) 경로에 whatap.so 파일 생성되어 있는지 확인합니다.

```text
$ find / | grep whatap.so
```

PHP 확장 모듈\(PHP Extension module\) 실행되고 있는지 확인합니다.

```text
$ sudo php -m

[PHP Modules]
bz2
calendar
Core
ctype
curl
date
…
whatap                  # whatap 모듈 실행 확인
…
[Zend Modules]
```

whatap-php 서비스\(Service\) 상태를 확인합니다.

```text
$ service whatap-php status
```

**실행**

**애플리케이션 재기동**

설치가 완료된 후 Apache 또는 PHP-FPM서비스\(Service\)를 재시작 하면 설정된 PHP 확장 모듈\(PHP Extension module\) whatap.so 파일이 로딩됩니다.

**whatap-php 서비스\(Service\) 재시작**

whatap-php 서비스\(Service\)가 실행 중이지 않거나 오류가 발생한 경우 재시작 합니다.

```text
$ sudo service whatap-php restart
```

**업데이트**

패키지 업데이트는 기존 설정을 유지한 채로 PHP 모니터링 서비스를 업데이트합니다. 0.2.7 이후 버전부터 정상적인 업데이트가 지원됩니다. 이전 버전은 삭제 후 설치를 진행해야 합니다.

**Redhat/CentOS**

패키지 정보 갱신을 위해 캐시 정보를 삭제합니다.

```text
$ yum clean all
```

Apache 또는 PHP-FPM서비스\(Service\)를 중지합니다.

whatap-php 패키지를 업데이트 합니다. $ yum update whatap-php

Apache 또는 PHP-FPM서비스\(Service\)를 시작합니다

**Debian/Ubuntu**

패키지 정보 갱신을 위해 캐시 정보를 갱신합니다.

```text
$ sudo apt-get update
```

Apache 또는 PHP-FPM서비스\(Service\)를 중지합니다.

whatap-php 패키지를 업데이트 합니다.

```text
$ sudo apt-get install --only-upgrade whatap-php
```

Apache 또는 PHP-FPM서비스\(Service\)를 시작합니다

**중지**

**일시 중지**

**PHP 확장 모듈\(PHP Extension module\) 중지**

whatap.ini 파일의 ‘extension=’ 구문을 주석처리 합니다.

수동 설정으로 php.ini 에 직접 설정한 경우도 동일하게 ‘extension=’ 구문을 주석처리 합니다. 주석은 세미콜론\( ; \) 으로 설정합니다.

```text
$ sudo vi whatap.ini

extension=whatap.so

;주석
;extension=whatap.so
```

**whatap-php 서비스\(Service\) 중지**

```text
$ sudo service whatap-php stop
```

**에이전트 삭제**

설치 스크립트를 이용하여 트레이서\(PHP Extension module\) 및 whatap-php 서비스\(Service\)를 삭제합니다.

이후 패키지\(yum, apt-get\) 삭제를 진행하고 필요에 따라서 /usr/whatap/php 아래에 로그 파일 및 기타 파일을 삭제합니다.

**PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\) 삭제**

```text
$ /usr/whatap/php/install.sh remove
```

**패키지 삭제**

* Redhat/CentOS

  ```text
  $ sudo yum remove whatap-php
  ```

* Debian/Ubuntu

  ```text
  $ sudo apt-get purge whatap-php
  ```

* /usr/whatap/php 디렉토리 삭제

#### 로그 {#user-content-로그}

**로그파일 종류**

로그파일은 2가지로 종류는 다음과 같습니다.

* whatap-boot-\[DATE\].log : 데이터 수집 로그
* whatap-install-\[DATE\].log : install.sh 실행 로그

**정상 동작 확인**

애플리케이션 서버를 기동 또는 재기동 한 뒤, 애플리케이션 서버 로그 및 에이전트 로그를 확인하여 PHP 모니터링 서비스의 정상 기동 여부를 확인합니다.apache/error\_log

```text
[Fri Nov 24 11:13:03 2017] [notice] Apache/2.2.15 (Unix) DAV/2 PHP/5.4.45 configured -- resuming normal operations
[Fri Nov 24 15:24:09 2017] [notice] caught SIGTERM, shutting down
[Fri Nov 24 15:24:09 2017] [notice] suEXEC mechanism enabled (wrapper: /usr/sbin/suexec)
[Fri Nov 24 15:24:09 2017] [notice] Digest: generating secret for digest authentication ...
[Fri Nov 24 15:24:09 2017] [notice] Digest: done
WA001 Whatap APM started
```

/usr/whatap/php/logs/whatap-boot-xxx.log

```text
2017/11/27 15:49:15 [WA214] Config: /etc/php.d/whatap.ini
2017/11/27 15:49:15
2017/11/27 15:49:15 ## OPEN LOG FILE  boot  0.3.0.20170929   20171127 06:49:15.44 ##
2017/11/27 15:49:15
2017/11/27 15:49:15 [WA827] 0xc4204ba460
2017/11/27 15:49:15 [WA214] Config: /etc/php.d/whatap.ini
2017/11/27 15:49:15 [WA171] PCODE=1234569399OID=-1182161871ONAME=d54FPHP-3-15-httpd
2017/11/27 15:49:15 [WA174] Net TCP: Connect to121.134.69.246:6600
2017/11/27 15:49:16 [WA632] Net UDP: Try to.... localhost:6600
2017/11/27 15:49:16 [WA635] Net UDP: Listener localhost:6600
```

#### 설치 에러 대응 {#user-content-설치-에러-대응-2}

**PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\) 수동 설정**

PHP 확장 모듈\(PHP Extension module\) , whatap-php 서비스\(Service\) 설치 및 선택 설치\(install.sh \)가 정상적으로 이루어 지지 않을 경우 수동으로 설정하는 방법을 설명합니다. PHP 컴파일\(Compile\) 설치 등의 이유로 환경 정보를 확인 할 수 없는 경우 사용합니다.

**whatap.ini 생성**

```text
$ cp /usr/whatap/php/template.ini /usr/whatap/php/whatap.ini
$ vi /usr/whatap/php/whatap.ini

# 상단에 내용 추가
; Enable whatap extension module
extension=whatap.so
whatap.license=            # 발급된 라이선스 key
whatap.server.host=        # 발급된 서버 IP
whatap.app_name=           # 웹서버 구분 APHP, FPHP (apache : APHP, php-fpm : FPHP)
whatap.app_process_name=   # apache, php-fpm 의 프로세스 이름(httpd,php-fpm)
```

| 설정 | 설명 |
| :--- | :--- |
| whatap.license | 프로젝트 &gt; 관리 &gt; 에이전트 설치 페이지에서 발급된 라이선스 키를 확인할 수 있습니다. |
| whatap.server.host | 프로젝트 &gt; 관리 &gt; 에이전트 설치 페이지에서 발급된 서버 IP를 확인할 수 있습니다. |
| whatap.app\_name | Apache 서버는 ‘APHP’, php-fpm 은 ‘FPHP’를 사용합니다. |
| whatap.app\_process\_name | Apache 또는 php-fpm 의 실행 프로세스 이름 설정으로 정확한 프로세스명 입력하면, 해당 프로세스에 대한 사용 메모리를 수집합니다. 예\) httpd, apach2, php-fpm, php-fpm 등. |

**PHP 명령어\(CLI\) 경로 확인**

```text
$ which php

/usr/bin/php
```

**whatap-php 서비스\(Service\) 환경 변수 설정**

$WHATAP\_PHP\_BIN 환경 변수에 PHP CLI 명령어의 경로를 설정합니다.

```text
$ sudo vi /etc/init.d/whatap-php

export WHATAP_PHP_BIN=         # PHP 명령어 위치(/usr/bin/php)
```

**PHP API 버전 확인**

$WHATAP\_PHP\_BIN 환경 변수에 PHP CLI 명령어의 경로를 설정합니다.

```text
$ sudo php -i | grep 'PHP API'

PHP API => 20100412
```

**PHP ZTS\(Zend Thread Safe\) 지원 여부 확인**

apache

```text
$ sudo apachectl -V | grep MPM

Server MPM: Prefork       	# ZTS 지원 안함
Server MPM: Worker       	# ZTS 지원
```

PHP-FPM

```text
$ sudo php-fpm -i | grep Thread

Thread Safety => disabled       	# ZTS 지원 안함
Thread Safety => enabled       	# ZTS 지원
```

**PHP 확장 모듈\(PHP Extension module\) 경로 확인 및 설정**

**PHP 확장 모듈\(PHP Extension module\) 경로 확인**

```text
$ sudo php -i | grep extension_dir

extension_dir => /usr/lib64/php/modules => /usr/lib64/php/modules
```

**PHP 확장 모듈\(PHP Extension module\) 설정**

PHP API 버전, PHP ZTS 지원 여부를 확인하여 환경에 적합한 라이브러리를 선택하여 PHP 확장 모듈\(PHP Extension module\) 경로에 whatap.so 파일명으로 복사합니다.

* PHP ZTS를 지원할 경우 - whatap\_zts\_\[PHP API 버전\].so
* PHP ZTS를 지원하지 않을 경우 - whatap\_\[PHP API 버전\].so

  ```text
  $ sudo cp /usr/whatap/php/modules/x64/whatap_20100412.so /usr/lib64/php/modules/whatap.so
  ```

**whatap-php 서비스\(Service\) 환경 변수 설정**

$WHATAP\_PHP\_EXT\_HOME 환경변수에 PHP 확장 모듈 경로를 설정합니다.

$WHATAP\_PHP\_EXT\_SRC 환경변수에 와탭 라이브러리 전체 파일 경로를 설정합니다.

```text
$ sudo vi /etc/init.d/whatap-php

export WHATAP_PHP_EXT_HOME=   # PHP Extension 경로(/usr/lib64/php/modules)
export WHATAP_PHP_EXT_SRC=    # 와탭 라이브러리 경로 및 파일명
                              # (/usr/whatap/php/modules/x64/whatap_20100412.so)]
```

**whatap.ini 설정**

**PHP 추가 ini 설정 경로 확인**

```text
$ sudo php -i | grep '.ini files'

Scan this dir for additional .ini files => /etc/php.d
```

whatap.ini를 해당 경로에 복사합니다.

```text
$ sudo cp /usr/whatap/php/whatap.ini /etc/php.d/whtap/ini
```

**PHP 추가 ini 설정 경로 확인 불가**

PHP 컴파일\(Compile\) 설치 옵션 ‘--with-config-file-scan-dir=PATH‘이 설정 안된 경우에 발생합니다.

```text
$ sudo php -i | grep '.ini files'

Scan this dir for additional .ini files => (none)
```

whatap.ini 파일 내용을 php.ini 마지막에 추가합니다.

```text
$ php -i | grep 'php.ini'

Loaded Configuration File => /etc/php.ini

$ sudo vi php.ini

# 파일 마지막에 추가
[whatap]
Enable whatap extension module
extension=whatap.so
whatap.ext.error_enabled=true
whatap.ext.exception_enabled=true
whatap.trace_user_enabled=true
whatap.trace_user_using_ip=false
```

이외 옵션은 /usr/whatap/php/whatap.ini 를 사용합니다.

**whatap-php 서비스\(Service\) 환경 변수 설정**

$WHATAP\_CONFIG\_HOME 환경변수에 whatap.ini 경로를 설정합니다.

PHP 추가 ini 경로를 확인 할 수 없는 경우 whatap.ini를 생성한 /usr/whatap/php 경로를 설정합니다.

```text
$ sudo vi /etc/init.d/whatap-php

export WHATAP_CONFIG_HOME=      # whatap.ini 경로(/etc/php.d)
```

**서비스 재시작**

Apache 및 PHP-FPM 서비스\(Service\)를 재시작 합니다.

whatap-php 서비스\(Service\)를 재시작 합니다.

**Error: Not found PHP API**

PHP 명령어\(CLI\)를 찾지 못하는 경우 발생합니다.

PHP 명령어\(CLI\)의 위치를 정확히 찾고, ‘PHP 확장 모듈\(PHP Extension module\) 및 whatap-php 서비스\(Service\) 선택 설치’ 항목을 진행합니다.PHP API 버전 정보 확인

```text
$ sudo php -i | grep 'PHP API'

PHP API => 20100412
```

**Error: Not found PHP ini directory**

PHP 환경 중 ‘Scan this dir for additional .ini files’ 항목의 값을 확인 하지 못하는 경우 발생합니다. PHP 컴파일\(Compile\) 설치 옵션 ‘--with-config-file-scan-dir=PATH’ 이 설정 안된 경우에 해당 환경정보가 없습니다. PHP 명령어의\(CLI\) 경로를 정확히 찾고, ‘PHP 확장 모듈\(PHP Extension module\) 및 whata-php 서비스\(Service\) 수동 설정’ 항목을 진행합니다.

```text
$ sudo php -i | grep '.ini files'

Scan this dir for additional .ini files => (none)
```

**응답 시간 분포도 \(히트맵\)에 트랜잭션이 표시되지 않는 경우**

CPU, Memory의 그래프는 표기 되지만 응답 시간 분포도\(히트맵\)가 표기 되지 않는 현상은 에이전트가 수집서버와 정상적으로 연결 되었지만, 트레이서가 정상적으로 PHP 확장 모듈\(PHP Extension module\)로 적용되지 않았거나, 설정 후 Apache 및 PHP-FRPM 서비스\(Service\)를 재시작 하지 않은 경우에 발생합니다.

**PHP 확장 모듈\(PHP Extension module\) 확인**

```text
$ sudo php -m

 [PHP Modules]
bz2
calendar
Core
ctype
curl
date
…
whatap                 # 와탭 모듈 로드 확인
…
[Zend Modules]
```

PHP 확장 모듈\(PHP Extension module\) 적용을 확인 한 경우 Apache 및 PHP-FRPM 서비스\(Service\)를 재시작 합니다. 적용이 안된 경우는 정상 설치 되지 않은 것으로 whatap.so 또는 whatap.ini 파일 경로가 PHP 환경과 일치하는 지 확인합니다. ‘PHP 명령어\(CLI\) 경로 확인,’ PHP 확장 모듈\(PHP Extension module\) 경로 확인’, ‘PHP 추가 ini 설정 경로 확인’ 을 확인합니다.

#### FAQ {#user-content-faq-2}

#### 제약 사항 {#user-content-제약-사항-2}

#### 호환성 목록 {#user-content-호환성-목록-1}

**운영체제**

* Redhat/CentOS 64bit 6.x 이상
* Ubuntu 64bit 12.04 이상

**PHP**

* 5.2, 5.3, 5.4, 5.5, 5.6, 7.0, 7.1
* Non Tread Safe 방식 지원
* Tread Safe 방식 지원
