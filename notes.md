https://github.com/keeplearningandtrying/testing-spring-boot-applications/blob/master/script.adoc
https://github.com/keeplearningandtrying/tdd-with-spring-boot/blob/master/CHEATSHEET.md



Favor AsserJ for fluent assertion. See xxxxxx for details

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


