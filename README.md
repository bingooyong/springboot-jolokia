# JMX Http Proxy


1. Run On Docker
注意：需要设置环境变量 `JOLOKIA_JSR160_PROXY_ENABLED=true`，开启Proxy Mode模式

```bash
docker build -t gobars/spring-boot-jolokia .
docker run -p 8080:8080 --env JOLOKIA_JSR160_PROXY_ENABLED=true gobars/spring-boot-jolokia
```

2.  替换 {{JMX_IP}}，{{JMX_PORT}}
```bash
curl --location --request POST 'http://location:8080/actuator/jolokia' --header 'Content-Type: application/json' -d '{
    "type": "READ",
    "mbean": "java.lang:type=Threading",
    "attribute": "ThreadCount",
    "target": {
        "url": "service:jmx:rmi:///jndi/rmi://{{JMX_IP}}:{{JMX_PORT}}/jmxrmi"
    }
}'
```