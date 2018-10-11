# 오픈API

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/act\_agent" %}
{% api-method-summary %}
Get act\_agent
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
Cake successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
    "name": "Cake's name",
    "recipe": "Cake's recipe name",
    "cake": "Binary cake"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a cake matching this query.
{% endapi-method-response-example-description %}

```javascript
{
    "message": "Ain't no cake like that."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://apm.whatap.io" path="/open/api/inact\_agent" %}
{% api-method-summary %}
Get inact\_agent
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

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



