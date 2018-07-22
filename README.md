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
1. facade模块，因此执行
```
cd /seckill-facade-goodes
mvn clean
mvn install 

```

2. service模块  
由于添加了web.xml，service模块可以使用jetty运行
```
mvn jetty:run
```
也可以用测试类运行：dubbo.test.DubboProvider 里面的main方法

3. frontend模块    
```
mvn jetty:run  
```

## zk
cd /usr/local/zookeeper
tail -f zookeeper.out  #查看zookeeper是否有服务注册上来