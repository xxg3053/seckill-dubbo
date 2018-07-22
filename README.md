# 使用dubbo改造seckill项目

原项目：https://github.com/xxg3053/seckill 

## 模块划分
seckill-common-parent
seckill-facade-goods
seckill-service-goods
seckill-web-frontend

## 冲突
项目本身日志使用的logback，但zk使用的log4j
```xml
<dependency>
    <groupId>org.apache.zookeeper</groupId>
    <artifactId>zookeeper</artifactId>
    <exclusions>
        <exclusion>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

## QA
1. seckill-web-frontend启动报错：      

2. Serialized class org.seckill.dto.Exposer must implement java.io.Serializable    
dubbo传输需要实现 Serializable

3. SeckillServiceImpl添加@service注解需要命名    
@Service("seckillService")

## 运行
先运行service模块，在运行frontend模块 
mvn jetty:run 