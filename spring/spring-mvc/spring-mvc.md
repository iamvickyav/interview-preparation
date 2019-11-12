## Spring MVC

* **“Model View Controller”** web framework built on the Servlet API 
* Lets you create @Controller or @RestController beans to handle incoming HTTP requests

### Front Controller Pattern in Spring MVC

Spring MVC designed around the front controller pattern where a central Servlet, the DispatcherServlet, provides a shared algorithm for request processing, while actual work is performed by configurable delegate components

| **More about Front Controller Design pattern** |
| ------------- |
| https://www.geeksforgeeks.org/front-controller-design-pattern/|

The DispatcherServlet, as any Servlet, **needs to be declared and mapped according to the Servlet specification by using Java configuration or in web.xml**. In turn, the DispatcherServlet uses Spring configuration to discover the delegate components it needs for request mapping, view resolution, exception handling

### DispatcherServlet

* Expects a WebApplicationContext (an extension of a plain ApplicationContext)

* Delegates to special beans to process requests and render the appropriate responses


| **Special Beans** | **Usage** |
| ------------- | ---------|
| HandlerMapping | Map a request to a handler along with a list of interceptors for pre- and post-processing E.g. **RequestMappingHandlerMapping** |
| HandlerAdapter | Help the DispatcherServlet to invoke a handler mapped to a request |
| ViewResolver | Resolve logical String-based view names returned from a handler to an actual View |
|MultipartResolver | Abstraction for parsing a multi-part request  |


### Interceptor - HandlerInterceptor

* preHandle(..): Before the actual handler is executed

* postHandle(..): After the handler is executed

* afterCompletion(..): After the complete request has finished

**Note:** postHandle is less useful with @ResponseBody and ResponseEntity methods for which the response is written and committed within the HandlerAdapter and before postHandle. In that case use **ResponseBodyAdvice**

```
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LocaleChangeInterceptor());
        registry.addInterceptor(new ThemeChangeInterceptor()).addPathPatterns("/**");
        registry.addInterceptor(new SecurityInterceptor()).addPathPatterns("/secure/*");
    }
}
```

### Exceptions - HandlerExceptionResolver

If an exception occurs during request mapping or is thrown from a request handler (such as a @Controller), the DispatcherServlet delegates to a chain of HandlerExceptionResolver

### ViewResolver

View technologies in Spring MVC is pluggable, whether you decide to use Thymeleaf, Groovy Markup Templates, JSPs, or other technologies

Let you render models in a browser without tying you to a specific view technology. ViewResolver provides a mapping between view names and actual views

**InternalResourceViewResolver** - used for JSP
**UrlBasedViewResolver** - for redirect (redirect: prefix in a view name) & for forwarding (forward: prefix)

### Multipart Resolver

When a POST with content-type of multipart/form-data is received, the resolver parses the content and wraps the current HttpServletRequest as MultipartHttpServletRequest

### Inbuilt Filters - 

| Form Data | Forwarded Headers | Shallow ETag | CORS |
| --------- | ----------------- | ------------ | ---- |
| FormContentFilter | ForwardedHeaderFilter | ShallowEtagHeaderFilter | CorsFilter |
| To intercept HTTP PUT, PATCH, and DELETE requests with a content type of application/x-www-form-urlencoded | As a request goes through proxies (such as load balancers) the host, port, and scheme may change. E.g X-Forwarded-Host, X-Forwarded-Port, X-Forwarded-Proto, X-Forwarded-Ssl, and X-Forwarded-Prefix. This filter removes them | The ShallowEtagHeaderFilter filter creates a “shallow” ETag by caching the content written to the response and computing an MD5 hash from it. The next time a client sends, it does the same, but it also compares the computed value against the If-None-Match request header and, if the two are equal, returns a 304 (NOT_MODIFIED) | Cross-Origin Resource Sharing |

### Controller 

@Controller

* stereotype - indicates role 
* allows auto-detection. Spring detects @Component classes in the classpath and auto-registering bean definitions for them
* Auto detection needs @ComponentScan or <context:component-scan/>

@RestController

* Composed annotation of @Controller and @ResponseBody 
* @ResponseBody - indicates every method inherits the type-level @ResponseBody annotation and, therefore, writes directly to the response body versus view resolution and rendering with an HTML template

### Request Mapping

* For mapping path or called as URL Variables

* URI variables are automatically converted to the appropriate type, or TypeMismatchException. int, long, Date etc. supported in default

* Custom type means use DataBinder

```
@GetMapping("/owners/{ownerId}/pets/{petId}")
public Pet findPet(@PathVariable Long ownerId, @PathVariable Long petId) {
    // ...
}
```

### Consumable Media Type

Can narrow request mapping based on Content-Type header in request

`@PostMapping(path = "/pets", consumes = "application/json")`


### Producible Media Type

Can narrow request mapping based on the Accept header in request

`@GetMapping(path = "/pets/{petId}", produces = "application/json")`

### Parameters, headers

`@GetMapping(path = "/pets/{petId}", params = "myParam=myValue")`

`@GetMapping(path = "/pets", headers = "myHeader=myValue")`

### HTTP HEAD Request

If request made for HEAD, will be considered as @GetMapping. Request will be processed but instead of writing the body, the number of bytes are counted and the Content-Length header is set

### Request Parameter values & annotations

| Parameter | Usage |
| --------- | ----------------- |
| HttpServletRequest, MultipartHttpServletRequest | |
|java.io.InputStream| Access to raw request body |
|java.io.OutputStream| Access to raw response body |
| @PathVariable | Access to URI variables |
| @RequestParam | Access to request param |
| @RequestHeader | Access to request header |
| @RequestBody | Access to request body (converted to type using HttpMessageConverter |
| HttpEntity | Access to request body & header (converted to type using HttpMessageConverter |
| java.util.Map, Model, ModelMap | For access to the model |
| @ModelAttribute | Existing attribute |
| Errors, BindingResult | For access to errors from validation from validation of RequestBody |

### Response values & annotations

| Parameter | Usage |
| --------- | ----------------- |
| @ResponseBody | Return value converted using HttpMessageConverter for body |
| HttpEntity<B>, ResponseEntity<B> | Both body & header |
| HttpHeaders | To return response with headers and no body |
| String | View name resolved with ViewResolver |
| View | For rendering together with the implicit model |
| ModelAndView | The view and model attributes; Optional HttpStatus |
| void or returning null | Either Response/OutputStream in method argument solved it already. If Rest, no response body.

### Samples 

```
@PostMapping("/owners/{ownerId}/pets/{petId}/edit")
public String processSubmit(@ModelAttribute Pet pet) { }
```

```
@GetMapping("/demo")
public void handle(@CookieValue("JSESSIONID") String cookie)
```

```
@GetMapping("/demo")
public void handle(
	@RequestHeader("Accept-Encoding") String encoding)
```

```
@GetMapping
public String setupForm(
	@RequestParam("petId") int petId)

```

```
@PostMapping("/accounts")
public void handle(@Valid @RequestBody Account account, BindingResult result)
```

```
@PostMapping("/accounts")
public void handle(HttpEntity<Account> entity)
```

```
@GetMapping("/accounts/{id}")
@ResponseBody
public Account handle()
```

### Validation

You can automatically apply validation after data binding by adding the javax.validation.Valid annotation or Spring’s @Validated annotation

```
@PostMapping("/owners/{ownerId}/pets/{petId}/edit")
public String processSubmit(@Valid @ModelAttribute("pet") Pet pet, BindingResult result)
```

### DataBinder

@InitBinder methods can register controller-specific java.bean.PropertyEditor

```
@Controller
public class FormController {

    @InitBinder 
    protected void initBinder(WebDataBinder binder)
```

### Exceptions

@Controller and @ControllerAdvice classes can have @ExceptionHandler methods to handle exceptions from controller methods

@ControllerAdvice classes to apply them globally

Also extend ResponseEntityExceptionHandler, which provides handling for exceptions that Spring MVC raises

```
@ExceptionHandler({FileSystemException.class, RemoteException.class})
public ResponseEntity<String> handle(IOException ex) {
        // ...
}
```

### HTTP Caching

HTTP caching revolves around the **Cache-Control** response header and, subsequently, conditional request headers (such as Last-Modified and ETag)


Most items taken from https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html










