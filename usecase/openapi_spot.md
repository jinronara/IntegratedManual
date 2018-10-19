---
description: >-
  수집중인 모니터링 정보를 별도로 활용하거나, 서버의 Scale Up/Out의 자동화를 위해 적용하고자 하는 경우 Open API를 통해 해당
  정보를 추출할 수 있는 기능을 제공합니다. 관리 > 프로젝트 관리에서 프로젝트 정보 영역의 API Token 값을 Open API 호출 시
  HTTP Header 정보로 전송하여 수집된 정보를 획득할 수 있습니다.
---

# 오픈API - 실시간

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/act\_agent" %}
{% api-method-summary %}
Active Agent
{% endapi-method-summary %}

{% api-method-description %}
활성화 상태인 에이전트 수 를 얻는다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
활성화 상태인 에이전트 수 를 반환한다
{% endapi-method-response-example-description %}

```javascript
1
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/inact\_agent" %}
{% api-method-summary %}
Inactive Agent
{% endapi-method-summary %}

{% api-method-description %}
비활성화 상태인 에이전트 수 를 얻는다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
비활성화 상태인 에이전트 수를 반환한
{% endapi-method-response-example-description %}

```text
0
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/host" %}
{% api-method-summary %}
Hosts Count
{% endapi-method-summary %}

{% api-method-description %}
물리 호스트 수를 얻는다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
프로젝트내의 물리 호스트 수를 반환한다.
{% endapi-method-response-example-description %}

```text
1
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/cpucore" %}
{% api-method-summary %}
Cpu Core Count
{% endapi-method-summary %}

{% api-method-description %}
Cpu Core 수를 얻는다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
프로젝트내의 Cpu Core 수 합계를 반환환다.
{% endapi-method-response-example-description %}

```text
1
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/txcount" %}
{% api-method-summary %}
Transaction Count
{% endapi-method-summary %}

{% api-method-description %}
5초내 종료된 트랜잭션 수를 얻는다
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
직전 5초내 종료된 트랜잭션 수를 반환한다.
{% endapi-method-response-example-description %}

```text
10
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/tps" %}
{% api-method-summary %}
TPS
{% endapi-method-summary %}

{% api-method-description %}
현재 TPS 를 구한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/user" %}
{% api-method-summary %}
User Count
{% endapi-method-summary %}

{% api-method-description %}
최근 5분간 집계된 고유 사용자 수를 구한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/actx" %}
{% api-method-summary %}
Active Transaction Count
{% endapi-method-summary %}

{% api-method-description %}
액티브 트랜잭션 수를 구한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/rtime" %}
{% api-method-summary %}
Average Response Time
{% endapi-method-summary %}

{% api-method-description %}
현재 평균 응답시간을 구한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/cpu" %}
{% api-method-summary %}
CPU Usage
{% endapi-method-summary %}

{% api-method-description %}
현재 CPU 사용률을 구한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/threadpool\_active" %}
{% api-method-summary %}
Active ThreadPool Count
{% endapi-method-summary %}

{% api-method-description %}
사용중인 Thread Pool 수를 구한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/threadpool\_queue" %}
{% api-method-summary %}
Queuing ThreadPool Count
{% endapi-method-summary %}

{% api-method-description %}
큐잉중인 Thread Pool 수를 구한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/dbc\_count" %}
{% api-method-summary %}
DB Connection Pool Count
{% endapi-method-summary %}

{% api-method-description %}
전체 DB Connection Pool 수를 구한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/dbc\_active" %}
{% api-method-summary %}
DB Connection Pool Active Count
{% endapi-method-summary %}

{% api-method-description %}
사용중인 DB Connection Pool 수를 구한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
 대상 프로젝트 코드 사
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
 관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/dbc\_idle" %}
{% api-method-summary %}
DB Connection Pool Idle Count
{% endapi-method-summary %}

{% api-method-description %}
Idle 상태의 DB Connection Pool 수를 구한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}
대상 프로젝트 코드 사용
{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}
관리 - 프로젝트 관리 메뉴를 통해 확인된 Token 사용
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

