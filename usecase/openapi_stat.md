---
description: >-
  수집중인 모니터링 정보를 별도로 활용하거나, 서버의 Scale Up/Out의 자동화를 위해 적용하고자 하는 경우 Open API를 통해 해당
  정보를 추출할 수 있는 기능을 제공합니다. 관리 > 프로젝트 관리에서 프로젝트 정보 영역의 API Token 값을 Open API 호출 시
  HTTP Header 정보로 전송하여 수집된 정보를 획득할 수 있습니다.
---

# 오픈API - 통계

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/exception" %}
{% api-method-summary %}
Exception List
{% endapi-method-summary %}

{% api-method-description %}
Exception 발생 내역을 얻는다.   
조회범위는 1일을 초과 할 수 없으며 Path Parameter 가 없는 경우 최근 5분간의 정보를 반환한다.  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="stime" type="string" %}
 조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="etime" type="string" required=false %}
 조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}

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

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/httpc" %}
{% api-method-summary %}
HttpClient List
{% endapi-method-summary %}

{% api-method-description %}
HTTP 외부 호출 내역을 얻는다.   
조회범위는 1일을 초과 할 수 없으며 Path Parameter 가 없는 경우 최근 5분간의 정보를 반환한다.  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="stime" type="string" %}
 조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="etime" type="string" required=false %}
 조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}

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

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/remote" %}
{% api-method-summary %}
Remote IP List
{% endapi-method-summary %}

{% api-method-description %}
접속 IP 내역을 얻는다.   
조회범위는 1일을 초과 할 수 없으며 Path Parameter 가 없는 경우 최근 5분간의 정보를 반환한다.  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="stime" type="string" %}
 조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="etime" type="string" required=false %}
 조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}

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

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/sql" %}
{% api-method-summary %}
SQL List
{% endapi-method-summary %}

{% api-method-description %}
수행된 SQL 리스트를 얻는다.   
조회범위는 1일을 초과 할 수 없으며 Path Parameter 가 없는 경우 최근 5분간의 정보를 반환한다.  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="stime" type="string" %}
 조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="etime" type="string" required=false %}
 조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}

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

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/transaction" %}
{% api-method-summary %}
Transaction List
{% endapi-method-summary %}

{% api-method-description %}
수행된 트랜잭션 리스트를 얻는다.    
조회범위는 1일을 초과 할 수 없으며 Path Parameter 가 없는 경우 최근 5분간의 정보를 반환한다.  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="stime" type="string" %}
 조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="etime" type="string" required=false %}
 조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}

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

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/thread_count" %}
{% api-method-summary %}
Thread Count
{% endapi-method-summary %}

{% api-method-description %}
Trhead Count 를 얻는다.   
조회범위는 1일을 초과 할 수 없으며 Path Parameter 가 없는 경우 최근 5분간의 정보를 반환한다.  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="stime" type="string" %}
 조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="etime" type="string" required=false %}
 조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="avg" type="string" required=false %}
 stime, etime 구간 평균값을 얻고자 할때 사용
{% endapi-method-parameter %}

{% api-method-parameter name="oids" type="string" required=false %}
 에이전트를 특정하는 경우 사용
{% endapi-method-parameter %}

{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="x-whatap-pcode" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="x-whatap-token" type="string" required=true %}

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
