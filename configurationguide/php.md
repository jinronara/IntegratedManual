# PHP

## 에이전트 기능제어 {#user-content-에이전트-기능제어-2}

### whatap.stat_enabled

통계정보 추적 기능을 활성화합니다. 5 분단위로 수집되는 트랜잭션, SQL, HTTPCALL, UserAgent, Client IP 등의 통계 데이터등이 해당됩니다.

* Default : \[**true**\]
* Type : Boolean

### whatap.license

에이전트 설치시 서버로부터 부여받은 라이센스를 지정합니다. 라이센스에는 에이전트가 속한 프로젝트와 보안 통신을 위한 암호키를 포함하고 있습니다.

* Default : \[**NONE**\]
* Type : String

## PHP Extension 기능제어 {#user-content-php-extension-기능제어}

### whatap.ext.error_enabled

PHP 확장 모듈\(PHP Extension module\) 에서 오류\(Error\) 정보를 수집하는 기능을 활성화 합니다. PHP 컴파일 설치로 php.ini 에 ‘\[whatap\]’ 항목이 있으면 whatap.ini가 아닌 php.ini 에 추가합니다.

* Default : \[**true**\]
* Type : Boolean
* remark: 재기동 필요 \(Apache 및 PHP-FPM\)

### whatap.ext.exception_enabled

PHP 확장 모듈\(PHP Extension module\) 에서 예외 처리\(Exception\) 정보를 수집하는 기능을 활성화 합니다. PHP 컴파일 설치로 php.ini 에 \[whatap\] 항목이 있으면 whatap.ini가 아닌 php.ini 에 추가합니다.

* Default : \[**true**\]
* Type : Boolean
* remark: 재기동 필요 \(Apache 및 PHP-FPM\)

## 수집 서버 연결 설정 {#user-content-수집-서버-연결-설정}

### whatap.server.host

에이전트가 수집한 데이터를 전송할 서버를 지정합니다. 수집서버 이중화로 2개 이상의 IP를 가진 경우 콤마\(,\)로 분리하여 지정할 수 있습니다. 지정된 IP 에는 수집서버 proxy 데몬이 리스닝 상태로 서비스 되어야 합니다.

* Default : \[**127.0.0.1,127.0.0.1**\]
* Type : ip\_address

### whatap.server.port

수집서버 PORT 를 지정합니다. 포트는 하나만 지정할 수 있으므로 whatap\_server\_host 에 지정된 수집서버들은 동일 PORT 를 사용해야 합니다.

* Default : \[**6600**\]
* Type : tcp\_port

### whatap.tcp_so_timeout

수집서버와 통신하는 TCP세션의 Socket Timeout 값을 지정합니다.

* Default : \[**60000**\]
* Type : MiliSecond

### whatap.tcp_connection_timeout

수집서버와 통신하는 TCP세션의 Connection Timeout 값을 지정합니다.

* Default : \[**5000**\]
* Type : MiliSecond

### whatap.net_send_max_bytes

수집서버로 데이터를 전송할 때 한번에 전송되는 최대 크기를 지정합니다.

* Default : \[**5242880**\]
* Type : Byte

### whatap.net_send_buffer_size

데이터 전송을 하기 위해 가지고 있는 최대 바이트 크기입니다.

* Default: \[**1024**\]
* Type: byte

## 내부 UDP 서버 연결 설정 {#user-content-내부-udp-서버-연결-설정}

### whatap.net_udp_port

와탭 에이전트는 트레이서에서 UDP를 통해 수집한 데이터를 수집서버로 전송합니다. 처음 UDP서버의 포트를 지정할 수 있다. 기본값으로 제공되는 6600포트가 사용 중일 때 이 옵션을 사용합니다. PHP 컴파일 설치로 php.ini 에 \[whatap\] 항목이 있으면 whatap.ini가 아닌 php.ini 에 추가합니다.

* Default : \[**6600**\]
* Type : tcp\_port
* remark: 재기동 필요 \(Apache 및 PHP-FPM\)

## 프로파일링 옵션 {#user-content-프로파일링-옵션-1}

### whatap.profile_step_max_count

수집 가능한 프로파일 스텝의 최대 개수를 설정합니다. 수집된 프로파일 스텝 수가 이 값을 초과하면 이후 수집되는 스텝들은 모두 버려집니다.

* Default: \[**1024**\]
* Type : Int

### whatap.profile_step_normal_count

기본 스텝의 수집 가능한 개수를 설정합니다.

* Default: \[**1000**\]
* Type : Int

### whatap.profile_step_heavy_count

기본 스텝의 수집 개수가 초과되면, 실행 시간이 profile\_step\_heavy\_time을 초과하는 스텝만 수집합니다. 해당 스텝의 수집 가능한 개수를 설정합니다. Default 설정일 경우 profile\_step\_normal\_count가 800 이면 최대 200개의 스텝이 수집됩니다.

* Default: \[**1000**\]
* Type : Int

### whatap.profile_step_heavy_time

Heavy한 스텝의 기준을 지정 합니다. 지정된 값보다 수행시간이 긴 경우 profile\_step\_normal\_count 를 초과하는 경우라도 profile\_step\_heavy\_count 이내에서 기록됩니다.

* Default: \[**100**\]
* Type : MiliSecond

### whatap.profile_basetime

트랜잭션이 설정된 값 이하의 시간내에 종료된 경우 프로파일 정보를 수집하지 않습니다. 단, 5 분단위로 최초 호출된 URL, 에러가 발생한 트랜잭션에 대한 프로파일 정보는 수집됩니다.

* Default: 500
* Type : MiliSecond

### whatap.query_string_enabled

트랜잭션 URL의 쿼리 스트링을 함께 수집하는 기능을 활성화합니다. whatap.query\_string\_urls 에 등록된 URL만 적용됩니다.

* Default : \[**true**\]
* Type : Boolean

### whatap.query_string_urls

트랜잭션에서 쿼리 스트링을 수집 할 URL들을 등록합니다.

* Default : \[**NONE**\]
* Type : String

### whatap.profile_sql_param_enabled

프로파일 내역에 SQL 파라미터 정보를 기록하고자 할 때 사용합니다. 파라미터는 별도 보안키를 입력해야 조회 할 수 있습니다.

| Note | 보안 키는 WAS서버 ${WHATAP\_AGENT\_HOME}/paramkey.txt 파일내에 6자리로 지정합니다. paramkey.txt 파일이 존재하지 않는 경우 랜덤 값으로 자동 생성됩니다. |
| :--- | :--- |

* Default : \[**false**\]
* Type : Boolean

### whatap.profile_sql_resource_enabled

프로파일에서 SQL 이 수집될 때 해당 스텝에서 사용한 CPU 와 메모리 사용량을 추적합니다.

* Default : \[**false**\]
* Type : Boolean

### whatap.profile_httpc_resource_enabled

프로파일에서 HTTP Call 스텝이 수집될 때 해당 스텝에서 사용한 CPU 와 메모리 사용량을 추적합니다.

* Default : \[**false**\]
* Type : Boolean

### whatap.profile_http_host_enabled

트랜잭션의 Host 정보를 출력합니다. False일 경우 트랜잭션의 URL에 URI 만 표기하고 True 일 경우 /xxx.aaa.com/URL 형식으로 출력됩니다.

* Default : \[**false**\]
* Type : Boolean

## 사용자 추적 옵션 {#user-content-사용자-추적-옵션-1}

### whatap.trace_user_enabled

실시간 사용자 집계 여부를 지정합니다. 이 값을 활성화 하는 경우 아이피 또는 PHP 기본 쿠키 및 프레임워크 쿠키\(PHPSESSID, ci\_session, Laravel\_session\)를 기준으로 사용자를 추적합니다. PHP 컴파일 설치로 php.ini 에 \[whatap\] 항목이 있으면 whatap.ini가 아닌 php.ini 에 추가합니다.

* Default : \[**true**\]
* Type : Boolean
* remark : 재기동 필요 \(Apache 및 PHP-FPM\)

### whatap.trace_user_using_ip

실시간 사용자의 구분을 IP로 하고자 하는 경우 설정합니다. 이 데이터는 Real Time User에서 확인 가능합니다. false 일 경우 PHP 기본 쿠키 및 프레임워크 쿠키\(PHPSESSID, ci\_session, Laravel\_session\)를 기준으로 사용자 구분을 합니다. PHP 컴파일 설치로 php.ini 에 \[whatap\] 항목이 있으면 whatap.ini가 아닌 php.ini 에 추가한다.

* Default : \[**false**\]
* Type : Boolean
* remark : 재기동 필요 \(Apache 및 PHP-FPM\)

### whatap.trace_user_header_ticket

사용자의 구분을 HTTP 헤더의 특정 값으로 구분하고 싶을 때 사용 할 HTTP 키를 지정합니다. 단, trace\_user\_using\_ip 배타적으로 설정을 동시에 적용할 수 없다. HTTP키를 찾지 못하는 경우 Cookie를 기준으로 사용자를 구분합니다. PHP 컴파일 설치로 php.ini 에 \[whatap\] 항목이 있으면 whatap.ini가 아닌 php.ini 에 추가합니다.

* Default : \[**false**\]
* Type : Boolean
* remark : 재기동 필요 \(Apache 및 PHP-FPM\)

### whatap.trace_user_set_cookie

사용자의 구분을 하기 위해 쿠키에 “WHATAP” 키 이름으로 사용자 구분 값을 설정한다. trace\_user\_using\_ip 설정 되는 경우 반영되지 않습니다. trace\_user\_header\_ticket이 설정되는 경우 header key를 찾지 못하는 경우 설정됩니다. HTTP키를 찾지 못하는 경우 Cookie를 기준으로 사용자를 구분합니다. PHP 컴파일 설치로 php.ini 에 \[whatap\] 항목이 있으면 whatap.ini가 아닌 php.ini 에 추가합니다.

* Default : \[**false**\]
* Type : Boolean
* remark : 재기동 필요 \(Apache 및 PHP-FPM\)

### whatap.profile_http_header_enabled

HTTP 헤더의 이름 과 값을 수집합니다. 최대 20개를 수집하며 파라메터 이름과 값은 최대 256 byte 까지 수집됩니다.

* Default : \[**false**\]
* Type : Boolean
* remark : 재기동 필요 \(Apache 및 PHP-FPM\)

### whatap.trace_http_client_ip_header_key

Client IP(Remote IP)의 정보를 특정 HTTP 헤더의 값으로 변경하여 설정하는 기능입니다.
Proxy(프락시) 환경에서 X-Forwarded-For 헤더 값을 Client IP 로 설정할 수 있습니다.

* Default : \[**NONE**\]
* Type : String
* remark : 재기동 필요 \(Apache 및 PHP-FPM\)

## 트랜잭션 추적 옵션 {#user-content-트랜잭션-추적-옵션-1}

### whatap.trace_active_transaction_slow_time

수집 정보를 확인하는 대시보드의 엑티브트랜잭션 아크이퀄라이저 그래프에서 노란색 구간으로 표기될 수 있는 트랜잭션 응답 시간의 기준을 지정합니다. 트랜잭션의 응답시간이 지정 시간을 초과할 경우 Slow 액티브트랜잭션의 개수에 포함됩니다.

* Default : \[**3000**\]
* Type : MiliSecond

### whatap.trace_active_transaction_very_slow_time

수집 정보를 확인하는 대시보드의 엑티브트랜잭션 아크이퀄라이저 그래프에서 빨간색 구간으로 표기될 수 있는 트랜잭션 응답 시간의 기준을 지정합니다. 트랜잭션의 응답시간이 지정 시간을 초과할 경우 경고가 발행됩니다.

* Default : \[**8000**\]
* Type : MiliSecond

### whatap.trace_active_transaction_lost_time

트랜잭션의 종료를 기다리는 제한 시간. 5분안에 트랜잭션이 끝나지 않는 경우 트랜잭션을 정보를 더이상 수집하지 않습니다. 트랜잭션의 프로파일 정보에서 “Lost Connection”를 확인할 수 있습니다.
* Default : \[**30000**\]
* Type : MiliSecond

### whatap.trace_normalize_enabled

트랜잭션 URL을 변환하여 일반화하는 기능을 활성화 합니다.

* Default : \[**true**\]
* Type : Boolean

### whatap.trace_normalize_urls

트랜잭션 URL을 변환하고 일반화할 대상 URL을 지정합니다. 호출 URL패턴을 변환하여 패스 파라미터를 제거합니다. 예를 들어 “/a/{v}/b” 라고 설정하면 해당 형식으로 호출되는 트랜잭션 URL은 “/a/{v}/b” 형식으로 변환됩니다. 여러 개를 등록 할 때는 콤마\(,\)를 사용합니다.

* Default : \[**NONE**\]
* Type : String

### whatap.trace_httpc_normalize_enabled

외부 HTTP 호출\(HTTP Call\) URL을 변환하고 일반화하는 기능을 활성화 합니다.

* Default : \[**true**\]
* Type : Boolean

### whatap.trace_httpc_normalize_urls

외부 HTTP 호출하는 URL을 변환하고 일반화할 대상 URL을 지정합니다 호출 URL 패턴을 변환하여 패스 파라미터를 제거합니다. 예를 들어 “/a/{v}/b” 라고 설정하면 해당 형식으로 호출되는 트랜잭션 URL은 “/a/{v}/b” 형식으로 변환됩니다. 여러 개를 등록 할 때는 콤마\(,\)를 사용합니다.

* Default : \[**NONE**\]
* Type : String

### whatap.trace_sql_normalize_enabled

SQL문에서 리터럴 부분을 추출하여 SQL문을 정규화 하는 기능을 활성화 합니다. 리터럴 부분은 "\#"으로 표기됩니다.

* Default : \[**true**\]
* Type : Boolean

## 에이전트 명명 옵션 {#user-content-에이전트-명명-옵션}

### whatap.object_name

애플리케이션을 식별하는 에이전트 이름\(ONAME\)체계입니다. ONAME을 토대로 OID가 생성됩니다.

* Default : \[**{type}-{ip2}-{ip3}-{process}**\]
* Type : String
* remark: 재기동 필요 \(Apache 및 PHP-FPM\)

| 명칭 | 설명 |
| :--- | :--- |
| {type} | whatap.app\_name 에 설정된 값을 사용합니다. |
| {ip\#} | IP를 나누었을 때 \#번째 자리를 사용합니다. |
| {process} | whatap.app\_process\_name 에 설정된 값을 사용합니다. |
| {hostname} | 서버 호스트명을 사용합니다. |

### whatap.app_name

애플리케이션을 식별하는 에이전트 이름\(ONAME\)체계에 사용되는 애플리케이션 명. object\_name의 {type}에 해당하는 값이다.

* Default : \[**NONE**\]
* Type : String
* remark: 재기동 필요 \(Apache 및 PHP-FPM\)

### whatap.app_process_name

애플리케이션을 식별하는 에이전트 이름\(ONAME\)체계에 사용되는 애플리케이션 프로세스 명. 애플리케이션 서버의 CPU, Heap Memory등을 수집할 대상 프로셋를 설정합니다. object\_name의 {process}에 해당하는 값이다.

* Default : \[**NONE**\]
* Type : String
* remark: 재기동 필요 \(Apache 및 PHP-FPM\)

## 로그 옵션 {#user-content-로그-옵션-1}

### whatap.log_keep_days

로그파일 보관기간을 설정합니다

* Default : \[**7**\]
* Type : Day

## 운영 설정 {#user-content-운영-설정-1}

### whatap.realtime_user_thinktime_max

실시간 사용자 측정시 동일 사용자로 인정되는 최대 호출간격을 지정합니다.

* Default : \[**300000**\]
* Type : MiliSeconds

### whatap.text_reset

와탭 에이전트는 한번 보낸 텍스트유형 데이터는 hash 처리되므로 다음날까지 재전송하지 않습니다. 이전 설정값과 다른 값을 설정하는 경우 재전송 합니다.

| Note | 트랜잭션 URL, SQL String 등이 텍스트유형 데이터에 해당합니다. |
| :--- | :--- |

* Default : \[**0**\]
* Type : Int
