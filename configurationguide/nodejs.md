# Node.JS

## 에이전트 기능제어 {#user-content-에이전트-기능제어-1}

### enabled

전체 기능을 활성화 합니다. false인 경우에도 서버와 최소한의 통신을 유지하기 위한 정보는 전송됩니다.

* Default : \[**true**\]
* Type : Boolean

### transaction_enabled

트랜잭션 추적 기능을 활성화 합니다. Hitmap에 기록되는 트랜잭션 정보가 해당합니다.

* Default : \[**true**\]
* Type : Boolean \(enabled=false 인 경우 false\)

### counter_enabled

성능 카운터 추적 기능을 활성화합니다. 액티브트랜잭션 수, 사용자 수, JVM 자원 사용량, Process CPU 사용량 및 DB Pool 사용량 정보등이 해당됩니다.

* Default : \[**true**\]
* Type : Boolean \(enabled=false 인 경우 false\)

### stat_enabled

통계정보 추적 기능을 활성화합니다. 5 분단위로 수집되는 트랜잭션, SQL, HTTPCALL, UserAgent, Client IP 등의 통계 데이터등이 해당됩니다.

* Default : \[**true**\]
* Type : Boolean \(enabled=false 인 경우 false\)

### license

에이전트 설치시 서버로부터 부여받은 라이센스를 지정합니다. 라이센스에는 에이전트가 속한 프로젝트와 보안 통신을 위한 암호키를 포함하고 있습니다.

* Default : \[**NONE**\]
* Type : String

### encrypt_level

와탭 에이전트는 서버로 데이터 전송시 데이터 속성에 따라 선택적으로 암호화를 하므로 높은 보안을 유지하면서도 성능상 이점을 가지고 있습니다. 이와 별개로 데이터 유형에 상관없이 일괄적인 암호화 정책을 적용하려는 경우 당 옵션을 사용할 수 있습니다.

| Note | 1 - 암호화 전송 기능 사용안함 2 - SQL파라미터, Plain Text와 같은 민감한 속성에 대하여 암호화 전송 3 - 모든 항목에 대하여 암호화 전송 |
| :--- | :--- |


* Default : \[**2**\]
* Type : encrypt\_level \[1\|2\|3\]

## 에이전트 네트워크 설정 {#user-content-에이전트-네트워크-설정}

### whatap_server_host

에이전트가 수집한 데이터를 전송할 서버를 지정합니다. 수집서버 이중화로 2개 이상의 IP를 가진 경우 콤마\(,\)로 분리하여 지정할 수 있습니다. 지정된 IP 에는 수집서버 proxy 데몬이 리스닝 상태로 서비스 되어야 합니다.

* Default : \[**127.0.0.1,127.0.0.1**\]
* Type : ip\_address

### whatap_server_port

수집서버 PORT 를 지정합니다. 포트는 하나만 지정할 수 있으므로 whatap\_server\_host 에 지정된 수집서버들은 동일 PORT 를 사용해야 합니다.

* Default : \[**6600**\]
* Type : tcp\_port

### tcp_so_timeout

수집서버와 통신하는 TCP세션의 Socket Timeout 값을 지정합니다.

* Default : \[**60000**\]
* Type : MiliSecond

### tcp_connection_timeout

수집서버와 통신하는 TCP세션의 Connection Timeout 값을 지정합니다.

* Default : \[**5000**\]
* Type : MiliSecond

### net_send_max_bytes

수집서버로 데이터를 전송할 때 한번에 전송되는 최대 크기를 지정합니다.

* Default : \[**5242880**\]
* Type : Byte

### net_send_queue1_size

프로파일 정보와 액티브스택을 제외한 나머지 데이터 전송에 사용될 Queue의 크기를 지정 합니다. 설정된 크기가 10 이하인 경우 10으로 지정됩니다.

* Default : \[**256**\]
* Type : Int

### net_send_queue2_size

프로파일 정보와 액티브스택 데이터 전송에 사용될 Queue의 크기를 지정 합니다. 설정된 크기가 10 이하인 경우 10으로 지정됩니다.

* Default : \[**512**\]
* Type : Int

## 프로파일링 옵션 {#user-content-프로파일링-옵션}

### profile_basetime

트랜잭션이 설정된 값 이하의 시간내에 종료된 경우 프로파일 정보를 수집하지 않습니다. 단, 5 분단위로 최초 호출된 URL, 에러가 발생한 트랜잭션에 대한 프로파일 정보는 수집됩니다.

* Default: 500
* Type : MiliSecond

### profile_http_header_enabled

프로파일 내역에 http 헤더 정보를 기록하고자 할 때 사용합니다.

* Default : \[**false**\]
* Type : Boolean

### profile_http_header_url_prefix

프로파일 내역에 http 헤더 정보를 기록할 대상 URL의 prefix를 정의 할 때 사용합니다.

* Default : \[**/**\]
* Type : String

### profile_http_parameter_enabled

프로파일 내역에 http 파라미터 정보를 기록하고자 할 때 사용합니다. 파라미터는 별도 보안키를 입력해야 조회 할 수 있습니다.

| Note | 보안 키는 WAS서버 ${WHATAP\_AGENT\_HOME}/paramkey.txt 파일내에 6자리로 지정합니다. paramkey.txt 파일이 존재하지 않는 경우 랜덤 값으로 자동 생성됩니다. |
| :--- | :--- |


* Default : \[**false**\]
* Type : Boolean

### profile_http_parameter_url_prefix

프로파일 내역에 http 파라미터 정보를 기록할 대상 URL의 prefix를 정의 할 때 사용합니다.

* Default : \[**/**\]
* Type : String

## 사용자 추적 옵션 {#user-content-사용자-추적-옵션}

### trace_user_enabled

실시간 사용자 집계 여부를 지정합니다.

| Note | 사용자 추적 옵션이 중복 설정 된 경우 동작 우선순위 1. trace\_user\_using\_ip 2. user\_header\_ticket |
| :--- | :--- |


* Default : \[**true**\]
* Type : Boolean

### trace_user_cookie_limit

사용자 집계를 위해 쿠키를 발행하는 경우 기존 쿠키가 너무 많다면 쿠키 오버플로어가 발생 할 수 있습니다. 이를 회피하기 위해 limit 를 지정합니다.

* Default: \[**2048**\]
* Type : Int

### trace_user_using_ip

실시간 사용자 집계시 IP 를 기반으로 합니다.

* Default : \[**true**\]
* Type : Boolean

### trace_http_client_ip_header_key

Remote Address 를 http header의 특정 key값으로 대체합니다.

| Note | WEB/WAS 앞에 L4와 같은 로드밸런서가 위치한 경우 Client의 IP가 아닌 L4의 IP가 Remote Address가 되는 경우가 있습니다. 이 상황에서 실제 Client IP정보가 http header에 특정 key 값으로 기록되는 경우라면 해당 key로 대체 할 수 있습니다. |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String
* Ex : trace\_http\_client\_ip\_header\_key=x-fowarded-for

### user_header_ticket

HTTP Header 의 특정 값으로 사용자 수를 집계하고자 하는 경우 해당 Key값을 지정합니다.

* Default : \[**NONE**\]
* Type : String

## 트랜잭션 추적 옵션 {#user-content-트랜잭션-추적-옵션}

### trace_background_socket_enabled

트랜잭션이 아닌 백그라운드 쓰레드에 의한 소켓이 오픈될 때도 이를 기록합니다.

* Default : \[**true**\]
* Type : Boolean

### trace_transaction_name_header_key

트랜잭션의 이름 끝부분에 지정한 http header key에서 추출한 값을 추가합니다.

* Default : \[**NONE**\]
* Type : String

### trace_service_port_enabled

트랜잭션의 이름에 port 번호를 추가한다.

* default: false

### trace_active_transaction_yellow_time

액티브 트랜잭션의 아크이퀄라이저에서 노란색으로 표현할 기준을 지정 합니다.

* Default: \[**3000**\]
* Type : MiliSecond

### trace_active_transaction_red_time

액티브 트랜잭션의 아크이퀄라이저에서 빨간색으로 표현할 기준을 지정 합니다.

* Default: \[**8000**\]
* Type : MiliSecond

### trace_normalize_urls

정규화 할 트랜잭션 URL 패턴을 정의 한다. 호출 URL 패턴을 파싱하여 패스파라미터를 제거합니다.

| Note | ex\) /a/{v}/b 라고 선언하면 a/123/b ⇒ a/{v}/b 로 치환한다 여러 개를 등록할 때는 콤마\(,\)를 사용합니다. 치환패턴 정리 후 보완필요 |
| :--- | :--- |


* Default : \[**NONE**\]
* Type : String

### trace_normalize_enabled

트랜잭션 URL 을 파싱하여 정규화하는 기능을 활성화합니다.

| Note | false 로 변경시 패스파라미터 파싱이 비활성화됩니다. 이 경우 통계데이터의 의미가 약화됨으로 디버그 용도로만 잠시 사용하는 것이 좋습니다. |
| :--- | :--- |


* Default : \[**true**\]
* Type : Boolean

### trace_auto_normalize_enabled

트랜잭션 URL 정규화할때 패턴값을 어노테이션에서 추출하여 자동으로 파싱하는 기능을 활성화합니다.

* Default : \[**true**\]
* Type : Boolean

### web_static_content_extensions

스태틱 컨텐츠임을 판단하는 확장자를 지정합니다. 여기에 설정된 확장자를 가진 트랜잭션들은 프로파일 추적과 카운팅이 제외됩니다.

* Default : \[**js, htm, html, gif, png, jpg, css, swf, ico**\]
* Type : String

### profile_error_sql_time_max

SQL 수행후 수행시간이 여기서 지정한 값을 초과하면 TOO SLOW 에러로 처리됩니다.

* Default : \[**30000**\]
* Type : MiliSecond

## 로그 옵션 {#user-content-로그-옵션}

### log_rotation_enabled

에이전트 로그파일을 일자별로 관리하는 기능을 활성화 합니다.

* Default : \[**true**\]
* Type : Boolean

### log_keep_days

로그파일 보관기간을 지정합니다.

* Default : \[**7**\]
* Type : Day

## 운영 설정 {#user-content-운영-설정}

### active\_stack\_second

액티브 스택을 추적하는 간격을 지정합니다.

| Warning | 값을 바꾸는 것을 권장하지 않습니다. |
| :--- | :--- |


* Default : \[**10**\]
* Type : Seconds

### counter_netstat_enabled

NET STAT 상태별 건수를 모니터링합니다. ESTABLISH, CLOSE\_WAIT, FIN\_WAIT 등 상태별 건수를 수집합니다.

* Default : \[**false**\]
* Type : Boolean

### realtime_user_thinktime_max

실시간 사용자 측정시 동일 사용자로 인정되는 최대 호출간격을 지정합니다.

* Default : \[**300000**\]
* Type : MiliSeconds

### time_sync_interval_ms

에이전트와 서버간 시간 동기화 주기를 지정합니다. 동기화 하지 않을 경우 0으로 지정합니다.

* Default : \[**300000**\]
* Type : MiliSeconds
