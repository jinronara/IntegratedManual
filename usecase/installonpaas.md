---
description: PaaS 환경에서 Whatap Agent 설치를 설명합니다.
---

# PaaS설치

PaaS 환경은 별도의 Shell을 제공하지 않으므로 어플리케이션에 Whatap Agent 와 설정을 포함하여 배포합니다. 

## IBM BlueMix

IBM BlueMix 는 컨테이너로 WebSphere Liberty 환경을 제공합니다. Liberty는 WebSphere Application Server 와 다른 경량화 환경으로 Spring Boot 가 동작하는 방식과 유사합니다. 

BlueMix 환경의 사용법은 아래 가이드를 확인 해 주세요   
[https://console.bluemix.net/docs/apps/index.html](https://console.bluemix.net/docs/apps/index.html)

### Java

설정 환경 예제 입니다.   
가이드에 따라 환경 구성시 로컬 개발환경에서 생성되는 파일들은 아래와 같습니다. 

```bash
whatap@vmwas01:/apps/bluemix/java-helloworld$ ls -alrt
합계 64
drwxrwxr-x 3 whatap whatap  4096 10월 29 13:13 ..
-rw-rw-r-- 1 whatap whatap  1079 10월 29 13:13 .classpath
-rw-rw-r-- 1 whatap whatap  1184 10월 29 13:13 .project
-rw-rw-r-- 1 whatap whatap    39 10월 29 13:13 .gitignore
-rw-rw-r-- 1 whatap whatap   151 10월 29 13:13 CONTRIBUTING.md
drwxrwxr-x 2 whatap whatap  4096 10월 29 13:13 .settings
-rw-rw-r-- 1 whatap whatap  2823 10월 29 13:13 pom.xml
-rw-rw-r-- 1 whatap whatap   122 10월 29 13:13 manifest.yml
-rw-rw-r-- 1 whatap whatap  3522 10월 29 13:13 README.md
-rw-rw-r-- 1 whatap whatap 11323 10월 29 13:13 LICENSE
drwxrwxr-x 3 whatap whatap  4096 10월 29 13:13 src
drwxrwxr-x 2 whatap whatap  4096 10월 29 13:13 target
drwxrwxr-x 8 whatap whatap  4096 10월 29 13:13 .git
drwxrwxr-x 6 whatap whatap  4096 10월 29 15:26 .
```

${APP\_HOME}에서 src/main/resources/whatap-agent/ 디렉토리를 생성하고 jar 파일, conf 파일을 복사 합니다. 

```text
$ mkdir -p src/main/resources/whatap-agent/
```

```text
$ cp /apps/whatap/whatap.agent.tracer-1.5.4.jar src/main/resources/whatap-agent/
$ cp /apps/whatap/whatap.conf src/main/resources/whatap-agent/
```

whatap.conf 설정은 PaaS 가 아닌 환경과 동일하게 적용합니다.   
단, 적용 후 에이전트명 식별에 어려움이 있을 수 있으므로 상황에 맞는 oname 정책을 적용 합니다. 

manifest.yml 파일에 옵션을 추가 합니다. yml 파일은 공백, 들여쓰기 기준을 잘 맞춰야 합니다.  

{% code-tabs %}
{% code-tabs-item title="manmifest.yml" %}
```text
---
applications:
- name: sample-java-helloworld
  random-route: true
  memory: 256M
  path: target/JavaHelloWorldApp.war
  #여기서부터 추가됩니다. 
  env:
    JAVA_OPTS: "-javaagent:/{APPLICATION_DIR}/WEB-INF/classes/whatap-agent/whatap.agent.tracer-1.5.4.jar -Dorg.osgi.framework.bootdelegation=whatap.* "
```
{% endcode-tabs-item %}
{% endcode-tabs %}



