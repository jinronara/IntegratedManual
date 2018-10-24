---
description: >-
  수집중인 모니터링 정보를 별도로 활용하거나, 서버의 Scale Up/Out의 자동화를 위해 적용하고자 하는 경우 Open API를 통해 해당
  정보를 추출할 수 있는 기능을 제공합니다. 관리 > 프로젝트 관리에서 프로젝트 정보 영역의 API Token 값을 Open API 호출 시
  HTTP Header 정보로 전송하여 수집된 정보를 획득할 수 있습니다.
---

# 오픈API - 통계

> API 에서 사용되는 Unix Epoch Time 은 Milisecond 단위 입니다.  \(13자리\)

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/exception/{stime}/{etime}" %}
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
{% api-method-parameter name="{stime}" type="string" %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=false %}
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

```text
{
"records": [
{
"oids": "[-1459620666]",
"time": 1535557500000,
"classHash": -1811136020,
"count": 14,
"service": "/account/delete/dept/daegu",
"class": "java.sql.SQLException(0)",
"serviceHash": 1900616259,
"snapSeq": "6068699991557528332",
"msg": "Sql Exception"
},
(중략)
],
"total": 2063
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/httpc/{stime}/{etime}" %}
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
{% api-method-parameter name="{stime}" type="string" %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=false %}
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

```text
{
"records": [
{
"Sum": 22628,
"Port": 10002,
"Url": "/remote/account/save/employee/kwangju",
"Host": "127.0.0.1",
"Max": 1815,
"Stdev": "247.95",
"Actived": 0,
"Avg": 1131,
"HostHash": -675813464,
"Min": 1002,
"Error": 0,
"Total": 20,
"UrlHash": -243814510
},
(중략)
],
"total": 4923
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/remote/{stime}/{etime}" %}
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
{% api-method-parameter name="{stime}" type="string" %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=false %}
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

```text
{
"records": [
{
"count": 86,
"city": "Winnipeg",
"country": "CA (CANADA)",
"ip": "140.193.83.68"
},
(중략)
],
"total": 1000
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/sql/{stime}/{etime}" %}
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
{% api-method-parameter name="{stime}" type="string" %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=false %}
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

```text
{
"records": [
{
"time_max": 4164,
"dbcHash": 450678784,
"db": "jdbc:mysql://localhost:3306,localhost:3310/fake",
"time_min": 0,
"fetch_count": 0,
"hash": 796628118,
"fetch_time": 0,
"sql_crud": 0,
"count_total": 5224,
"count_error": 0,
"sql": "update table set x=# where key=#",
"time_sum": 581391,
"time_avg": 111,
"time_std": "240.79",
"count_actived": 0
},
(중략)
],
"total": 130
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/transaction/{stime}/{etime}" %}
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
{% api-method-parameter name="{stime}" type="string" %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=false %}
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

```text
{
"records": [
{
"time_max": 44735,
"sql_fetch_time": 363,
"sql_time": 2628663,
"count": 10743,
"error": 29,
"sql_count": 22635,
"hash": -1485863373,
"sql_fetch": 6741607,
"httpc_avg": 1084,
"cpu_avg": 0,
"time_sum": 19911778,
"time_avg": 1853,
"httpc_count": 7072,
"service": "/account/save/employee/seoul",
"mem_avg": 0
},
(중략)
],
"total": 1080
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/thread\_count/{stime}/{etime}/{avg}/{oids}" %}
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
{% api-method-parameter name="{stime}" type="string" %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=false %}
조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{avg}" type="string" required=false %}
stime, etime 구간 평균값을 얻고자 할때 사용
{% endapi-method-parameter %}

{% api-method-parameter name="{oids}" type="string" required=false %}
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

```text
{
"pcode": 1234570141,
"type": "thread_count",
"stime": 1536050400000,
"etime": 1536050700000,
"interval": 300,
"data": [
{
"oname": "8080",
"oid": -1234257485,
"data": []
},
(중략)
{
"oname": "TC-29-96-8082",
"oid": 1482741919,
"data": []
}
]
}

# 범위를 지정하는 경우 
{
"pcode": 1234570141,
"type": "thread_count",
"stime": 1536050100000,
"etime": 1536050700000,
"interval": 300, <= data point 간격
"data": [
{
"oname": "8080",
"oid": -1234257485,
"data": [
[
1536050100000, <= 시계열 timestamp
95.2
],
[
1536050400000,
85.3
],
[
1536050700000,
91.43
]
]
},
(중략)
{
"oname": "TC-29-96-8082",
"oid": 1482741919,
"data": [
[
1536050100000,
98.11
],
[
1536050400000,
81.44
],
[
1536050700000,
90.05
]
]
}
]
}

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/thread\_daemon/{stime}/{etime}/{avg}/{oids}" %}
{% api-method-summary %}
Daemon Thread Count
{% endapi-method-summary %}

{% api-method-description %}
Daemon Thread Count 를 얻는다.  
조회범위는 1일을 초과 할 수 없으며 Path Parameter 가 없는 경우 최근 5분간의 정보를 반환한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{stime}" type="string" %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=false %}
조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{avg}" type="string" required=false %}
stime, etime 구간 평균값을 얻고자 할때 사용
{% endapi-method-parameter %}

{% api-method-parameter name="{oids}" type="string" required=false %}
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

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/thread\_peak\_count/{stime}/{etime}/{avg}/{oids}" %}
{% api-method-summary %}
Thread Peak Count
{% endapi-method-summary %}

{% api-method-description %}
Thread Peak Count 를 얻는다.  
조회범위는 1일을 초과 할 수 없으며 Path Parameter 가 없는 경우 최근 5분간의 정보를 반환한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{stime}" type="string" %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=false %}
조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{avg}" type="string" required=false %}
stime, etime 구간 평균값을 얻고자 할때 사용
{% endapi-method-parameter %}

{% api-method-parameter name="{oids}" type="string" required=false %}
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

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/threadpool\_active/{stime}/{etime}/{avg}/{oids}" %}
{% api-method-summary %}
Active Thread Pool Count
{% endapi-method-summary %}

{% api-method-description %}
Active Thread Pool Count 를 얻는다.  
조회범위는 1일을 초과 할 수 없으며 Path Parameter 가 없는 경우 최근 5분간의 정보를 반환한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{stime}" type="string" %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=false %}
조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{avg}" type="string" required=false %}
stime, etime 구간 평균값을 얻고자 할때 사용
{% endapi-method-parameter %}

{% api-method-parameter name="{oids}" type="string" required=false %}
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

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/threadpool\_queue/{stime}/{etime}/{avg}/{oids}" %}
{% api-method-summary %}
Thread Pool Queue Count
{% endapi-method-summary %}

{% api-method-description %}
Thread Pool Queue Count 를 얻는다.  
조회범위는 1일을 초과 할 수 없으며 Path Parameter 가 없는 경우 최근 5분간의 정보를 반환한다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{stime}" type="string" %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=false %}
조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{avg}" type="string" required=false %}
stime, etime 구간 평균값을 얻고자 할때 사용
{% endapi-method-parameter %}

{% api-method-parameter name="{oids}" type="string" required=false %}
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

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/tx\_caller/{stime}/{etime}/{oids}/filter/{filterkey}/{filterval}" %}
{% api-method-summary %}
Tx Caller
{% endapi-method-summary %}

{% api-method-description %}
Caller 호출 통계를 조회한다. 조회범위는 1일을 초과 할 수 없다. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{stime}" type="string" required=true %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=true %}
조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{oids}" type="string" required=false %}
에이전트를 특정하는 경우 사용
{% endapi-method-parameter %}

{% api-method-parameter name="filter" type="string" required=false %}
Filter 조건을 지정하는 경우 사용
{% endapi-method-parameter %}

{% api-method-parameter name="{filterkey}" type="string" required=false %}
Filter 로 사용할 Key 를 지정   
  
\[caller\_pcode\|caller\_spec\|caller\_url\|spec\|url\]
{% endapi-method-parameter %}

{% api-method-parameter name="{filterval}" type="string" required=false %}
Filter 로 사용할 값 을 지정 Key 가 caller\_url, url 인 경우 BASE64 인코딩값을 사용   
  
\[caller\_pcode value \|caller\_spec value \|caller\_url value \|spec value \|url value \]
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

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/tx\_domain/{stime}/{etime}/{oids}/filter/{filterkey}/{filterval}" %}
{% api-method-summary %}
Tx Domain
{% endapi-method-summary %}

{% api-method-description %}
도메인 호출 통계를 조회한다. 조회범위는 1일을 초과 할 수 없다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{stime}" type="string" required=true %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=true %}
조회 끝 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{oids}" type="string" required=false %}
에이전트를 특정하는 경우 사용
{% endapi-method-parameter %}

{% api-method-parameter name="filter" type="string" required=false %}
Filter 조건을 지정하는 경우 사용
{% endapi-method-parameter %}

{% api-method-parameter name="{filterkey}" type="string" required=false %}
Filter 로 사용할 Key 를 지정   
  
\[domain\|url\]
{% endapi-method-parameter %}

{% api-method-parameter name="{filterval}" type="string" required=false %}
Filter 로 사용할 값 을 지정 Key 가 url 인 경우 BASE64 인코딩값을 사용   
  
\[domain value \|url value \]
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

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/json/fullgclog/{stime}/{etime}" %}
{% api-method-summary %}
FullGC Log
{% endapi-method-summary %}

{% api-method-description %}
Full GC 로그를 조회한다. 조회범위는 1일을 초과 할 수 없다.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{stime}" type="string" required=true %}
조회 시작 시간 \(Unix epoch time\)
{% endapi-method-parameter %}

{% api-method-parameter name="{etime}" type="string" required=true %}
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

```text
{
"pcode": 1,
"stime": 1538983800000,
"etime": 1539070200000,
"data": [
{
"oid": 832254513,
"oname": "SEO2",
"count": [
[
1538983800000,
1
]
],
"logs": [
"2018-10-08T16:33:09.001-0900: 79.812: [Full GC (System.gc()) 47269K->14801K(448000K),
0.0537298 secs]"
]
},
{
"oid": -1453518268,
"oname": "0-1-9780-seo",
"count": [
[
1538983800000,
2
]
],
"logs": [
"2018-10-08T16:32:57.009-0900: 32.382: [Full GC (System.gc()) 26874K->14816K(94720K),
0.0463841 secs]",
"2018-10-08T16:33:02.435-0900: 37.807: [Full GC (System.gc()) 15040K->13556K(94720K),
0.0557387 secs]"
]
}
]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

