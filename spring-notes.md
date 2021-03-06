* https://github.com/keeplearningandtrying/testing-spring-boot-applications/blob/master/script.adoc
* https://github.com/keeplearningandtrying/tdd-with-spring-boot/blob/master/CHEATSHEET.md
* https://spring.io/blog/2016/04/15/testing-improvements-in-spring-boot-1-4
* https://spring.io/blog/2016/08/30/custom-test-slice-with-spring-boot-1-4
* https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-understanding-auto-configured-beans - see appendix C and D
* https://springframework.guru/unit-testing-spring-mvc-spring-boot-1-4-part-1/
* https://github.com/spring-projects/spring-boot/issues/11392
* https://github.com/spring-projects/spring-data-examples - see how spring boot autoconfiguration can be used to test regular spring components
* https://docs.spring.io/spring-boot/docs/current/reference/html/test-auto-configuration.html

Favor AsserJ for fluent assertion. See xxxxxx for details
Favor mockito as mocking framework

How to unit test exception
How to capture console output

Spring and Spring Boot Test


https://spring.io/guides/gs/testing-web/



@RunWith(SpringRunner.class)
@SpringBootTest

* The @SpringBootTest annotation tells Spring Boot to go and look for a main configuration 
class (one with @SpringBootApplication for instance), and use that to start a Spring application context

@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)

The port is not really needed as we can directly use TestRestTemplate (see https://github.com/keeplearningandtrying/testing-spring-boot-applications/blob/master/src/test/java/sample/ApplicationIntegrationTest.java)


(
@RunWith(SpringRunner.class)
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
@AutoConfigureTestDatabase



)


@RunWith(SpringRunner.class)
@SpringBootTest
@AutoConfigureMockMvc


to not start the server at all, but test only the layer below that, where Spring 
handles the incoming HTTP request and hands it off to your controller.

the full Spring application context is started, but without the server.


(
https://github.com/keeplearningandtrying/testing-spring-boot-applications/blob/master/src/test/java/sample/web/UserVehicleControllerApplicationTest.java

@RunWith(SpringRunner.class)
@SpringBootTest
@AutoConfigureMockMvc
@AutoConfigureTestDatabase

Annotation that can be applied to a test class to configure a test database to use instead of any application defined or auto-configured DataSource.
)





@RunWith(SpringRunner.class)
@WebMvcTest

pring Boot is only instantiating the web layer, not the whole context. 

Using this annotation will disable full auto-configuration and instead apply 
only configuration relevant to MVC tests (i.e. @Controller, @ControllerAdvice, 
@JsonComponent Filter, WebMvcConfigurer and HandlerMethodArgumentResolver beans 
but not @Component, @Service or @Repository beans).

By default, tests annotated with @WebMvcTest will also auto-configure Spring Security 
and MockMvc (include support for HtmlUnit WebClient and Selenium WebDriver). For more 
fine-grained control of MockMVC the @AutoConfigureMockMvc annotation can be used. 

@WebMvcTest is the web test slice in Spring Boot 1.4. When it is present, you instruct 
Spring Boot that a web environment is required and that only the specified controller(s) 
should be instantiated. 


Test repository

@DataJpaTest

Annotation that can be used in combination with @RunWith(SpringRunner.class) for a typical JPA test. Can be used when a test focuses only on JPA components.

Using this annotation will disable full auto-configuration and instead apply only configuration relevant to JPA tests.

By default, tests annotated with @DataJpaTest will use an embedded in-memory database (replacing any explicit or usually auto-configured DataSource). The @AutoConfigureTestDatabase annotation can be used to override these settings. 

https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/autoconfigure/orm/jpa/DataJpaTest.html




Test calling a remote rest service

@RestClientTest

RemoteVehicleDetailsService 

https://github.com/keeplearningandtrying/testing-spring-boot-applications/blob/master/src/test/java/sample/service/RemoteVehicleDetailsServiceTest.java




Security test

https://docs.spring.io/spring-security/site/docs/current/reference/html/test-method.html


/// follow up
@JdbcTest

https://github.com/spring-projects/spring-boot/blob/master/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jdbc/JdbcTemplateAutoConfiguration.java

https://spring.io/blog/2013/10/30/empowering-your-apps-with-spring-boot-s-property-support

https://geowarin.github.io/understanding-spring-boot.html

@import - https://www.mkyong.com/spring3/spring-3-javaconfig-import-example/


Spring Boot 1.4 now defines a spring-boot-test-autoconfigure module that provides a collection of 
test-related auto-configurations. These auto-configurations are composable and can help you crafting 
your own infrastructure easily. 

@ImportAutoConfiguration
@EnableAutoConfiguration
@PropertyMapping
@PropertySource
@EnableConfigurationProperties

https://stackoverflow.com/questions/43653655/what-is-difference-between-importautoconfiguration-and-import
You would use @ImportAutoConfiguration when you don't want to enable the default autoconfiguration with @EnableAutoConfiguration. As you probably know, @EnableAutoConfiguration attemps to configure beans that are located on your classpath eg tomcat-embedded.jar. Whereas @ImportAutoConfiguration only runs the configuration classes that you provided in the annotation.

@SpringJUnit4ClassRunner 
https://github.com/spring-projects/spring-framework/blob/master/spring-test/src/main/java/org/springframework/test/context/junit4/SpringJUnit4ClassRunner.java

https://github.com/spring-projects/spring-boot/tree/master/spring-boot-project/spring-boot-test/src/main/java/org/springframework/boot/test/context


@PropertyMapping - https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/autoconfigure/properties/PropertyMapping.html
Example 
 * https://github.com/keeplearningandtrying/testing-with-spring-boot/blob/master/src/main/java/com/example/external/dealer/DealerService.java
 * https://github.com/keeplearningandtrying/testing-with-spring-boot/blob/master/src/test/java/com/example/external/dealer/DealerServiceEndpoint.java
 
 * Sample boot application configuration file with log setting - https://github.com/spring-cloud/spring-cloud-skipper/blob/3c48f51c31387d034170aacc611bc316c1aa5a2c/spring-cloud-skipper-server-core/src/main/resources/application.yml
 
 * BrokerRunning - https://github.com/spring-projects/spring-amqp/blob/master/spring-rabbit-junit/src/main/java/org/springframework/amqp/rabbit/junit/BrokerRunning.java
 
 * RabbitTemplateIntegrationTests  - https://github.com/spring-projects/spring-amqp/blob/master/spring-rabbit/src/test/java/org/springframework/amqp/rabbit/core/RabbitTemplateIntegrationTests.java
 




