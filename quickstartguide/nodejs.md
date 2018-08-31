본 가이드는 사용자가 Linux Ubuntu 16.04 환경에서 Node.js와 Express를 기반으로 생성된 애플리케이션 서버를 구동하고 있을 때 와탭 Node.js 모니터링을 설치하는 방법에 대해 다룹니다. 별도의 세부적인 가이드를 필요로 하는 여타 다른 프레임워크를 이용하는 경우 사용자 가이드를 참고해주시기 바랍니다. 와탭 Node.js APM 모니터링 서비스를 사용하기 위해서는 모니터링 대상 애플리케이션에 모니터링 에이전트를 설치해야 합니다. 와탭 Node.js APM 모니터링 에이전트는 npm 서비스를 통해 다운받을 수 있으며, 홈페이지에서 발급 받은 라이선스 키를 입력하여 등록할 수 있습니다.

# 설치 환경 {#user-content-설치-환경-1}

* OS: Linux Ubuntu 16.04
* Framework: Express
* Node.js Version: v5.1.1
* NPM Version: v3.3.12

# 프로젝트 생성

![](https://github.com/jinronara/IntegratedManual/tree/93fdbbf61f0cb8cedae22fdbf4c1e9e88904c19c/QuickStartGuide/.gitbook/assets/20.png)

서버를 등록하기 위해 우선 프로젝트를 생성합니다. 추가 버튼을 선택하면 아래와 같이 프로젝트 생성 창이 나타납니다. Java 아이콘을 선택한 뒤, 희망하는 프로젝트명과 데이터 서버 지역\(Region\), 소속하게 될 그룹을 선택한 뒤 프로젝트를 생성합니다.

![](https://github.com/jinronara/IntegratedManual/tree/93fdbbf61f0cb8cedae22fdbf4c1e9e88904c19c/QuickStartGuide/.gitbook/assets/80.png)

이후, 생성된 프로젝트를 클릭하여 관리 화면에 진입합니다

# 라이선스 발급

![](https://github.com/jinronara/IntegratedManual/tree/93fdbbf61f0cb8cedae22fdbf4c1e9e88904c19c/QuickStartGuide/.gitbook/assets/40.png)

프로젝트 관리화면에서는 우선적으로 라이선스를 발급 받습니다. 라이선스 키는 프로젝트별로 귀속되기 때문에, 유출되거나 배포되어서는 안됩니다. 반드시 본인 프로젝트에 서버를 등록할 때에만 이용하시기 바랍니다.

# 에이전트 설치

와탭 Node.js 모니터링 서비스는 npm을 통하여 설치할 수 있습니다. 우선, 설치할 애플리케이션 프로젝트의 최상위 폴더로 이동 한 후, 아래의 npm 명령어를 통하여 와탭 Node.js 모니터링 을 설치합니다.

```text
$ npm install whatap –save
```

설치 후 node\_module 아래 whatap 이라는 디렉토리가 생성된 것을 확인하실 수 있습니다. 이 과정에서 생성된 node\_modules/whatap/whatap.conf 파일을 애플리케이션의 최상위 폴더에 복사합니다.

```text
$ cp ./node_modules/whatap/whatap.conf ./
```

# 라이선스 및 수집 서버 설정

whatap.conf 파일을 열어 프로젝트 생성시 발급 받은 라이선스와 수집서버 정보를 입력한 후 저장합니다.

```text
$ echo "license={라이선스 키}" >> whatap.conf
$ echo "whatap.server.host={수집서버 정보}" >> whatap.conf
```

# 애플리케이션 기동 옵션 추가

Node.js 애플리케이션 실행 시 가장 먼저 실행되는 파일에 다음과 같이 입력합니다.

```text
var WhatapAgent = require('whatap').NodeAgent;

Express를 사용하는 경우 app.js 최상위에 추가하시면 됩니다.
var WhatapAgent = require('whatap').NodeAgent;

var express = require('express');
var path = require('path');
var favicon = require('serve-favicon');
var logger = require('morgan');
var cookieParser = require('cookie-parser');
var bodyParser = require('body-parser');
var https = require('https');
var fs = require('fs');
```

# 로그 확인

Node.js 애플리케이션을 시작 혹은 재시작을 하면 다음과 같이 와탭 로고와 표시되며 모니터링이 시작됩니다.

```text
20171127 03:08:17 [WHATAP-203] Config file reloaded
20171127 03:08:17 [WHATAP-101] Finish initialize configuration...
20171127 03:08:17 [WHATAP-110] [pcode=2870,SECURE_KEY=f20b4f2ea1fcd53fe0b05cab562665df]
20171127 03:08:17 [WHATAP-170] [WhaTap Agent] now waiting for starting......
20171127 03:08:22 [WHATAP-180] Try to connect to {"host":"52.78.209.94","port":6600,"agent":false}
20171127 03:08:22 [WHATAP-168] OID: -962721665 ONAME: NODE-0-191-8080 IP: 172.17.0.191
 _      ____       ______NODE-AGENT
| | /| / / /  ___ /_  __/__ ____
| |/ |/ / _ \/ _ `// / / _ `/ _ \
|__/|__/_//_/\_,_//_/  \_,_/ .__/
                          /_/
Just Tap, Always Monitoring
WhaTap Node Agent version 0.1.26, 20170626
```

# 모니터링 확인

{text 모니터링 확인에 대한 부분 확인 필요}
