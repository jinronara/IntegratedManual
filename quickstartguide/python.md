본 가이드는 사용자가 와탭 Python 모니터링 서비스를 사용 중인 Python 애플리케이션 서버에 설치하고 확인하는 내용을 다룹니다. 별도의 세부적인 설정을 필요로 하는 프레임워크/옵션을 사용하는 경우 설치 가이드를 참고해주시기 바랍니다.

# 설치 환경 {#user-content-설치-환경-2}

* 운영체제
  * CentOs 6 이상\(64bit\)
  * Ubuntu 14 이상\(64bit\)
* Python 버전
  * Python 2.7이상 & Python 3.3이상
  * WSGI Application
* Network 포트
  * 와탭 서버 연결을 위한 6600 Port 허용
  * 서버 내부 UDP 통신을 위한 6600 Port 사용

# 에이전트 설정 파일 {#user-content-에이전트-설정-파일}

whatap.conf은 에이전트 설정 기본 필수 파일입니다. 에이전트와 관련된 옵션은 모두 whatap.conf에서 설정이 가능합니다. 애플리케이션 서버의 데이터를 수집하는 수집서버의 주소와 서버의 프로젝트의 라이선스 키는 필수 옵션입니다. 이때, 라이선스키와 수집서버의 주소는 프로젝트를 생성하여 발급 및 확인이 가능합니다. 다음과 같은 옵션은 필수 조건입니다.

* license=\[라이선스 키\]
* whatap.server.host=\[수집서버 주소\]

다음은 부가 옵션입니다. 설정을 하지 않더라고 모니터링 데이터는 수집하나, 프로세스에 대한 CPU, Memory등을 계산할때 사용되는 값입니다. 또한 기본으로 설정되는 에이전트 식별 체계에 따라 식별에 어려움이 있으므로 해당 옵션 설정을 권장합니다.

* app\_name=XXXX \# 애플리케이션 명
  * ex\)django, flask ..
* app\_process\_name=XXXX \# 애플리케이션의 프로세스명
  * ex\)uwsgi, gunicorn ..

# 에이전트 설치 절차 {#user-content-에이전트-설치-절차-3}

와탭 python 모니터링 서비스를 사용하기 위해서는 모니터링 대상 애플리케이션에 모니터링 에이전트를 설치해야 합니다. 와탭 Python 모니터링 에이전트는 Python Package Index\(pip\)를 통해 와탭 -python 패키지를 설치 합니다. 홈페이지에서 발급 받은 라이선스 키를 입력하여 등록할 수 있습니다.

## 프로젝트 생성

![](https://github.com/jinronara/IntegratedManual/tree/93fdbbf61f0cb8cedae22fdbf4c1e9e88904c19c/QuickStartGuide/.gitbook/assets/20.png)

![](https://github.com/jinronara/IntegratedManual/tree/93fdbbf61f0cb8cedae22fdbf4c1e9e88904c19c/QuickStartGuide/.gitbook/assets/140.png)

이후, 생성된 프로젝트를 클릭하여 관리 화면에 진입합니다

## 라이선스 발급

![](https://github.com/jinronara/IntegratedManual/tree/93fdbbf61f0cb8cedae22fdbf4c1e9e88904c19c/QuickStartGuide/.gitbook/assets/150.png)

프로젝트 관리화면에서는 우선적으로 라이선스를 발급 받습니다. 라이선스 키는 프로젝트별로 귀속되기 때문에, 유출되거나 배포되어서는 안됩니다. 반드시 본인 프로젝트에 서버를 등록할 때에만 이용하시기 바랍니다.

## 에이전트 설치

### 에이전트 기본 경로 설정

로그와 설정파일 경로를 위한 $WHATAP\_HOME 경로를 지정해 주세요. ‘whatap’ 디렉토리를 새로 생성하는것을 권장합니다.

```text
$ export WHATAP_HOME=[PATH]
```

### 라이선스 키 및 수집서버 설정

다음 명령어를 실행하면 $WHATAP\_HOME에 지정한 경로에 바로 whatap.conf 파일이 생성 및 설정 됩니다.

```bash
$ whatap-setting-config
 --host [HOST_ADDR]
 --license [LICENSE_KEY]
 --app_name [APPLICATION_NAME]
 --app_process_name [APP_PROCESS_NAME ex]uwsgi, gunicorn..]
```

### 설정 확인

다음과 같이 설정파일이 잘 생성되어 있는지 확인 해 주세요.

```text
$ cat $WHATAP_HOME/whatap.conf
```

### 코드 사용

WHATAP\_AGENT시작 커맨드와 함께 애플리케이션 서버를 재시작해주세요.

```text
$ whatap-start-agent [YOUR_APPLICATION_START_COMMAND]
```

### 애플리케이션 재 시작

애플리케이션 서버가 실행되면 애플리케이션의 모니터링 정보를 수집하기 시작합니다.

### 로그 확인

서비스 재시작시 정상적으로 로그가 뜨는 화면을 통해 정상 구동 여부를 확인합니다. whatap-python 패키지를 설치한 후 에이전트 사용안내에 따라 애플리케이션 서버를 재시작 하면 다음과 같은 로그를 확인할 수 있습니다.

에이전트 등록 후 수집과 관련된 로그는 $WHATAP\_HOME/logs 디렉토리에서 확인 할 수 있습니다.whatap-hook.log / whatap-boot-\[DATE\].log

```text
_      ____       ______Python-AGENT
| | /| / / /  ___ /_  __/__ ____
| |/ |/ / _ \/ _ `// / / _ `/ _ \
|__/|__/_//_/\_,_//_/  \_,_/ .__/
                          /_/
Just Tap, Always Monitoring
WhaTap Python Agent version 0.1.33, 20171017

WHATAP_HOME: /Users/kimjihye/workspace/whatap/python-sample/whatap
Config: /Users/kimjihye/workspace/whatap/python-sample/whatap/whatap.conf
Logs: /Users/kimjihye/workspace/whatap/python-sample/whatap/logs
```

### 모니터링 확인

![](https://github.com/jinronara/IntegratedManual/tree/93fdbbf61f0cb8cedae22fdbf4c1e9e88904c19c/QuickStartGuide/.gitbook/assets/110.png)
