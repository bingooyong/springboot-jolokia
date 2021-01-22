# JMX Http Proxy
1.  设置环境变量，开启Proxy Mode模式

```bash
export JOLOKIA_JSR160_PROXY_ENABLED=true
```

2.  替换KAFKA_IP，KAFKA_JMX_PORT

```bash
curl --location --request POST 'http://location:10000/actuator/jolokia' --header 'Content-Type: application/json' -d '{
    "type": "READ",
    "mbean": "java.lang:type=Threading",
    "attribute": "ThreadCount",
    "target": {
        "url": "service:jmx:rmi:///jndi/rmi://KAFKA_IP:KAFKA_JMX_PORT/jmxrmi"
    }
}'
```