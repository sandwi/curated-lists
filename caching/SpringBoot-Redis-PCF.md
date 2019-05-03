
## Spring Boot and Redis on Pivotal Cloud Foundary

Spring Boot applications can be configured to use a Redis service on PCF by including the Cloud Connector and Data Redis dependencies in the project.  The following steps should enable the cache in the application:

- Add the cloud connector and redis dependencies
- Cache enable the application with the `@EnableCaching` annotation
- Use the `@Cachable` annotation on methods for which we want data cached

### Add Redis Dependencies to Project

The two dependencies that are central to adding Redis support for a project on PCF are the Data Redis dependency and the Cloud Connector dependency.  A gradle dependency fragment is shown below:

```gradle
dependencies {
	compile('org.springframework.boot:spring-boot-starter-actuator')
	compile 'org.springframework.boot:spring-boot-starter-cloud-connectors'
	compile('org.springframework.boot:spring-boot-starter-data-redis')
	compile('org.springframework.boot:spring-boot-starter-web')
	testCompile('org.springframework.boot:spring-boot-starter-test')
}
```

### Configure Redis in the Application

Create a configuration for a Redis enabled application in the cloud by creating a configuration class that extends the `AbstractCloudConfig` class.  
A simple configuration class for Redis if an application is bound to only one Redis service:

```java
import org.springframework.cache.CacheManager;
import org.springframework.cloud.config.java.AbstractCloudConfig;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.cache.RedisCacheManager;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;


@Configuration
public class RedisCacheConfig extends AbstractCloudConfig {


    /**
     * Connect to the only available Redis service 
     * */
    @Bean
    public RedisConnectionFactory redisFactory() {
        return connectionFactory().redisConnectionFactory();
    }


    @Bean
    RedisTemplate<String, String> redisTemplate() {
        RedisTemplate<String, String> redisTemplate = new RedisTemplate<String, String>();
        redisTemplate.setConnectionFactory(redisFactory());
        return redisTemplate;
    }

    @Bean
    public CacheManager cacheManager(RedisTemplate redisTemplate) {
        return new RedisCacheManager(redisTemplate);
    }
}
```

If an application is bound to multiple Redis services, the redis service name must be specified in the connection factory.

```java
//Connect to the 'market-data-redis-service' Redis service
@Bean
public RedisConnectionFactory redisFactory() {
    return connectionFactory().redisConnectionFactory("market-data-redis-service");
}
```

Also, use the `@EnableCaching` annotation on the Application class in the Spring Boot application.

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cache.annotation.EnableCaching;

@SpringBootApplication
@EnableCaching
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}
}
```



### Annotate Methods which return Data that Should be Cached

In many cases, the data returned by the controller is the data that should be cached.  The `@Cacheable` annotation is used on methods where the returned data should be cached.

A possible key naming strategy is to use SpEL to generate keys based on the method name.  This can be done by using the following annotation `@Cacheable(key = "#root.methodName")`.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.cache.annotation.CacheConfig;
import org.springframework.cache.annotation.Cacheable;
import org.springframework.http.MediaType;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Map;

@CacheConfig(cacheNames = "market-data")
@RestController
public class CacheDemoController {

    @Autowired
    CacheDataService cacheDataService;

    @GetMapping("/")
    public String home() {
        return "home";
    }

    @Cacheable(key = "#root.methodName")
    @GetMapping("/market-data")
    public Map<String, String> testData() {
        Map<String, String> test = cacheDataService.retrieveTestData();
        return test;
    }

    @Cacheable(key = "#root.methodName")
    @GetMapping(value = "market-data/rates", produces = MediaType.APPLICATION_JSON_VALUE)
    public Map<String, String> retrieveDemoData() {
        Map<String, String> demo = cacheDataService.retrieveDummyData();
        return demo;
    }
}
```

### Create the Redis Service in Cloud Foundry

1. Login to cf cli
    - `cf login –a https://api.cfapps.io`
2. Check your target Org and Space, if they are not right target the right org and space
    - `cf target`
3. Check your marketplace to see if you have redis service available
    - `cf marketplace`

#### Create Service instance of `Redis` tile

```cmd
cf create-service p-redis <service-plan-name> <service-instance-name>
```

### Bind the service to the app
To bind the service to the app, we need to mention the Redis service name in the manifest yaml file(s). It might look like the following:

```yaml
applications:
- name: TradingApp
  buildpack: java_buildpack_offline
  disk_quota: 1G
  instances: 1
  memory: 1G
  routes:
  - route: trading-app.cfapps.io
  path: build/libs/app.jar
  services:
  - market-data-redis-service
  env:
    SPRING_PROFILES_ACTIVE: dev
```

## References

- [Redis for PCF](http://docs.pivotal.io/redis/1-11/appdevs.html)
- [Spring Data Redis](https://docs.spring.io/spring-data-redis/docs/current/reference/html/)
- [Spring Boot Cache](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-caching.html)
- [Redis Connection Configuration](https://cloud.spring.io/spring-cloud-connectors/spring-cloud-spring-service-connector.html#_redis)
