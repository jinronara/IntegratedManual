# 멀티 트랜잭션 추적

 왜 필요한가?

뭘 할 수 있는가? 

어떻게 설정 하는가? 

{% code-tabs %}
{% code-tabs-item title="출발지 whatap.conf" %}
```text
stat_mtrace_enabled=true
stat_domain_enabled=true
mtrace_spec=v1.0
mtrace_rate=100
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="나머지 whatap.conf" %}
```text
stat_mtrace_enabled=true
stat_domain_enabled=true
mtrace_spec=v1.0
```
{% endcode-tabs-item %}
{% endcode-tabs %}



