# Springcloud

## Springcloud组件的作用

### 1.Eureka：服务注册与发现，用于服务管理。

### 2.Feign：web调用客户端，能够简化HTTP接口的调用。

### 3.Ribbon：基于客户端的负载均衡。

### 4.Hystrix：熔断降级，防止服务雪崩。

### 5.GateWay：网关路由，提供路由转发、请求过滤、限流降级等功能。

### 6.Config：配置中心，分布式配置管理。

### 7.Sleuth：服务链路追踪

### 8.Admin：健康管理

### 9.alibaba的Nacos可以实现上面的多个功能（服务注册，服务配置，服务总线）



## Eureka流程

### 1.先在C:\Windows\System32\drivers\etc\hosts.ice文件中添加127.0.0.1 eureka7001.com，127.0.0.1 eureka7002.com
### 2.在引入maven依赖，再配置yml文件，再写代码

### 3.@EnableEurekaClient 只对 Eureka 注册中心有效,而 @EnableDiscoveryClient 对 Eureka、Zookeeper、Consul 等注册中心都有效

### 4.从 SpringCloud Edgware 版本开始, @EnableEurekaClient 和 @EnableDiscoveryClient 注解都可以省略了,只需要在 pom.xml 中引入依赖、在application.yml 上进行相关配置,就可以将微服务注册到注册中心上

## Hystrix(豪猪)

### 1.分为服务降级，服务熔断，服务限流

### 2.服务降级：服务器忙，请稍后再试，不让客户端等待并立刻返回一个友好提示，fallback，哪些情况会触发降级：1.程序运行异常。2.超时。3.服务熔断并触发降级服务。4.线程池/信号量打满也会导致服务降级

### 3.服务熔断：类比保险丝达到最大服务访问后，直接拒绝访问，拉闸限电，然后调用服务降级的方式并返回友好提示

### 4.服务限流：秒杀高并发等操作，严禁一窝蜂的过来拥挤，大家排队，一秒钟N个，有序进行

### 5.关于降级和熔断：1.调用失败会触发降级，而降级会调用fallback方法   2.但无论如何降级的流程一定会先调用正常方法再调用fallback方法   3假如单位时间内调用失败次数过多，也就是降级次数过多，则触发熔断   4熔断以后就会跳过正常方法直接调用fallback方法  5所谓“熔断后服务不可用”就是因为跳过了正常方法直接执行fallback