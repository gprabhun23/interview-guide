### **1. What is ASP.NET Web API?**  
- ASP.NET Web API is a framework for building HTTP services that can be consumed by a broad range of clients like browsers, mobile devices, and other applications.  
- It supports RESTful services, which means it can return data based on HTTP verbs (GET, POST, PUT, DELETE).  
- It can return data in various formats such as JSON, XML, and plain text, making it highly flexible.  
- I used ASP.NET Web API to create RESTful endpoints for a cloud-based storage solution, which allowed multiple client apps to interact with the service.  

```csharp
public class ProductsController : ApiController  
{  
    public IEnumerable<Product> Get()  
    {  
        return productService.GetAllProducts();  
    }  
}
```

### **2. What is the difference between ApiController and Controller?**  
- ApiController is specifically designed for building RESTful services, whereas Controller is used for handling MVC web applications.  
- ApiController automatically serializes the data to JSON or XML format, while Controller returns views.  
- The routing mechanism differs; ApiController uses attribute routing, whereas Controller uses conventional routing.  
- I used ApiController in a microservices project for building stateless APIs, which were consumed by Angular front-end applications.  

```csharp
[Route("api/products")]  
public class ProductsController : ApiController  
{  
    [HttpGet]  
    public IEnumerable<Product> GetAll() { /* logic */ }  
}
```

### **3. What are the main return types supported in Web API?**  
- Web API supports various return types, such as IHttpActionResult, HttpResponseMessage, and strongly typed objects.  
- IHttpActionResult simplifies unit testing and provides flexibility in returning HTTP responses.  
- HttpResponseMessage allows greater control over the response, including headers and status codes.  
- I used IHttpActionResult in an e-commerce application to handle errors gracefully and standardize HTTP responses.  

```csharp
public IHttpActionResult GetProduct(int id)  
{  
    var product = productService.GetProduct(id);  
    if (product == null)  
        return NotFound();  
    return Ok(product);  
}
```

### **4. What are the advantages of using ASP.NET Web API?**  
- It is lightweight and ideal for building RESTful services.  
- It supports multiple media types like JSON, XML, and plain text.  
- It integrates seamlessly with .NET framework and supports Dependency Injection (DI).  
- I utilized Web API in a banking application to expose RESTful endpoints for internal systems and third-party integrations.  

```csharp
public IHttpActionResult GetAccounts()  
{  
    var accounts = accountService.GetAllAccounts();  
    return Ok(accounts);  
}
```

### **5. Which status code is used for all uncaught exceptions by default?**  
- By default, Web API returns status code **500 Internal Server Error** for uncaught exceptions.  
- This can be customized using exception filters.  
- Exception handling can be improved using middleware or global exception filters.  
- I implemented a custom exception filter in a financial application to log errors and provide user-friendly messages.  

```csharp
public class CustomExceptionFilter : ExceptionFilterAttribute  
{  
    public override void OnException(HttpActionExecutedContext context)  
    {  
        // Log exception and return custom response  
        context.Response = new HttpResponseMessage(HttpStatusCode.InternalServerError);  
    }  
}
```

### **6. Explain the usage of HttpResponseMessage.**  
- HttpResponseMessage is used to create a detailed HTTP response with status codes, headers, and content.  
- It provides flexibility when returning custom messages or setting headers.  
- It is useful when you need to manipulate the response before sending it to the client.  
- I used HttpResponseMessage to set custom headers in a reporting module, which enhanced client-side caching.  

```csharp
public HttpResponseMessage GetReport(int id)  
{  
    var response = Request.CreateResponse(HttpStatusCode.OK, reportService.GetReport(id));  
    response.Headers.Add("Custom-Header", "value");  
    return response;  
}
```

### **7. What new features are introduced in ASP.NET Web API 2.0?**  
- Attribute Routing for better control over URL patterns.  
- IHttpActionResult for simplified responses and improved testability.  
- CORS support for handling cross-origin requests.  
- I used attribute routing in an enterprise project to create clean, readable URLs for RESTful endpoints.  

```csharp
[Route("api/orders/{id}")]  
public IHttpActionResult GetOrder(int id)  
{  
    var order = orderService.GetOrderById(id);  
    return Ok(order);  
}
```

### **8. What exactly is OAuth (Open Authorization)?**  
- OAuth is a protocol for authorization, allowing users to grant third-party access to their resources without sharing credentials.  
- It uses access tokens instead of credentials to access APIs.  
- OAuth supports different flows like authorization code, implicit, and client credentials.  
- I implemented OAuth in a SaaS application to allow external partners to securely access APIs.  

```csharp
services.AddAuthentication("OAuth").AddJwtBearer("OAuth", options =>  
{  
    options.TokenValidationParameters = new TokenValidationParameters  
    {  
        ValidateIssuer = true,  
        ValidateAudience = true  
    };  
});
```

### **9. Explain the difference between WCF RESTful Service and ASP.NET Web API.**  
- WCF supports both SOAP and RESTful services, while Web API is built specifically for RESTful services.  
- WCF requires more configuration and is heavyweight compared to Web API.  
- Web API is more flexible, supporting multiple media types like JSON and XML out of the box.  
- I migrated a legacy WCF REST service to Web API to simplify maintenance and improve performance in a healthcare application.  

```csharp
public class ProductService : IProductService  
{  
    public IEnumerable<Product> GetAllProducts() { /* logic */ }  
}
```

### **10. What is Attribute Routing in ASP.NET Web API 2.0?**  
- Attribute Routing allows you to define routes directly on controller actions using attributes.  
- It provides more control and flexibility over URL patterns compared to conventional routing.  
- Attribute Routing supports parameters and constraints for cleaner URL management.  
- I used attribute routing in a microservices project to create RESTful APIs with descriptive URLs.  

```csharp
[Route("api/customers/{id:int}")]  
public IHttpActionResult GetCustomer(int id)  
{  
    var customer = customerService.GetCustomerById(id);  
    return Ok(customer);  
}
```

### **11. Is it true that ASP.NET Web API has replaced WCF?**  
- Web API has not entirely replaced WCF; it depends on the use case.  
- WCF is still suitable for scenarios requiring SOAP, security, and reliable messaging.  
- Web API is preferred for building RESTful services with lightweight communication.  
- I used WCF for internal SOAP services and Web API for external-facing REST APIs in a finance system.  

```csharp
public class MyWcfService : IService  
{  
    public string GetData(int value) { return $"You entered: {value}"; }  
}
```

### **12. What are the differences between Web API and Web API 2?**  
- Web API 2 introduced Attribute Routing, making it easier to define custom routes.  
- It added CORS support, allowing cross-origin requests.  
- The IHttpActionResult interface was introduced for cleaner and more testable code.  
- I used Web API 2 to manage CORS in a multi-client project that required API access from different domains.  

```csharp
[EnableCors(origins: "*", headers: "*", methods: "*")]  
public class ProductsController : ApiController  
{  
    public IEnumerable<Product> GetProducts() { return productService.GetAll(); }  
}
```

### **13. Explain the difference between MVC and ASP.NET Web API.**  
- MVC is designed for web applications that return HTML views, while Web API is for creating RESTful services that return data.  
- MVC controllers inherit from the Controller class, while Web API controllers inherit from ApiController.  
- Web API supports content negotiation, returning data in JSON, XML, etc., based on client needs.  
- I used MVC for a user-facing web portal and Web API for exposing data to mobile apps in a logistics project.  

```csharp
public class HomeController : Controller  
{  
    public ActionResult Index() { return View(); }  
}
```

### **14. Compare WCF and ASP.NET Web API.**  
- WCF is versatile, supporting SOAP, TCP, and HTTP protocols, while Web API only supports HTTP.  
- WCF requires configuration for REST services, whereas Web API is RESTful by default.  
- Web API is lightweight and easier to use for simple RESTful services.  
- I used Web API in a project requiring mobile-friendly JSON responses and WCF for internal secure messaging.  

```csharp
public class MyService : IService  
{  
    public string GetMessage() { return "Hello WCF"; }  
}
```

### **15. Name types of Action Results in Web API 2.**  
- OkResult (200 OK)  
- NotFoundResult (404 Not Found)  
- BadRequestResult (400 Bad Request)  
- I used NotFoundResult in an e-commerce project to handle missing product IDs gracefully.  

```csharp
public IHttpActionResult GetProduct(int id)  
{  
    var product = productService.GetProduct(id);  
    if (product == null) return NotFound();  
    return Ok(product);  
}
```

### **16. In OOP, what is the difference between the Repository Pattern and a Service Layer?**  
- The Repository Pattern abstracts database operations, handling CRUD logic.  
- The Service Layer handles business logic and acts as a bridge between controllers and repositories.  
- Using both patterns promotes separation of concerns and clean code architecture.  
- I implemented these patterns in a microservice project to separate data access from business logic.  

```csharp
public class ProductService  
{  
    private readonly IProductRepository _repository;  
    public ProductService(IProductRepository repository) { _repository = repository; }  
    public Product GetProduct(int id) { return _repository.Get(id); }  
}
```

### **17. Why are the FromBody and FromUri attributes needed in ASP.NET Web API?**  
- FromBody is used to bind complex types from the request body.  
- FromUri is used to bind simple types from the query string or URL.  
- Using these attributes provides clarity and flexibility in data binding.  
- I used FromBody to accept JSON payloads in a project where clients submitted data through REST APIs.  

```csharp
public IHttpActionResult Post([FromBody] Product product)  
{  
    productService.AddProduct(product);  
    return Ok();  
}
```

### **18. What is ASP.NET Web API Data?**  
- ASP.NET Web API Data refers to handling data in RESTful APIs, including serialization, model binding, and validation.  
- It uses JSON or XML serializers to convert objects to data formats.  
- Data handling can be customized using formatters and filters.  
- I customized data serialization in a project to handle special date formats for client applications.  

```csharp
config.Formatters.JsonFormatter.SerializerSettings.DateFormatString = "yyyy-MM-dd";  
```

### **19. What's the difference between OpenID and OAuth?**  
- OpenID is used for authentication, verifying user identity.  
- OAuth is for authorization, granting access to resources.  
- They can be used together for secure login and resource access.  
- I implemented both protocols in a project to allow secure login and third-party API access.  

```csharp
services.AddAuthentication("OAuth").AddJwtBearer("OAuth", options => { /* config */ });  
```

### **20. What is a Delegating Handler in ASP.NET Web API?**  
- A Delegating Handler is a custom message handler that processes HTTP requests before they reach the controller.  
- It can be used for tasks like logging, authentication, and modifying requests/responses.  
- Delegating Handlers can be chained together to form a pipeline.  
- I used a Delegating Handler in a project to log API requests for auditing purposes.  

```csharp
public class LoggingHandler : DelegatingHandler  
{  
    protected override async Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)  
    {  
        // Log request  
        var response = await base.SendAsync(request, cancellationToken);  
        return response;  
    }  
}
```

### **21. How to register an exception filter globally?**  
- Exception filters handle exceptions thrown during the execution of an action.  
- To register globally, add the filter to the `GlobalConfiguration.Configuration.Filters` collection.  
- This ensures all controllers and actions use the filter.  
- I registered a global exception filter in a Web API project to log exceptions and return custom error messages.  

```csharp
GlobalConfiguration.Configuration.Filters.Add(new CustomExceptionFilter());
```

### **22. How to return a view from an ASP.NET Web API method?**  
- Web API is designed to return data, not views.  
- However, it is possible by combining Web API with MVC, returning a `ViewResult`.  
- Use a regular MVC controller for actions requiring views.  
- I used this approach in a hybrid application where some endpoints returned JSON, and others returned HTML views.  

```csharp
public ActionResult Index()  
{  
    return View("MyView");  
}
```

### **23. Can we use Web API with ASP.NET Web Forms?**  
- Yes, Web API can be integrated with Web Forms by adding API routes in `Global.asax`.  
- It allows you to create RESTful endpoints in a Web Forms project.  
- Web Forms pages and Web API controllers can coexist.  
- I added Web API to a legacy Web Forms project to expose data to modern front-end clients.  

```csharp
GlobalConfiguration.Configure(WebApiConfig.Register);
```

### **24. Explain briefly Cross-Origin Resource Sharing (CORS).**  
- CORS is a security feature that allows or restricts resources from being requested from a different domain.  
- It requires server-side configuration to enable cross-origin requests.  
- Web API 2 has built-in support for CORS using the `EnableCors` attribute.  
- I enabled CORS in a multi-client project to allow requests from multiple domains.  

```csharp
[EnableCors(origins: "http://example.com", headers: "*", methods: "*")]  
public class ProductsController : ApiController  
{  
    public IEnumerable<Product> GetProducts() { return productService.GetAll(); }  
}
```

### **25. Explain advantages/disadvantages of using HttpModule vs Delegating Handler.**  
- HttpModule processes requests at the IIS pipeline level, affecting all incoming requests.  
- Delegating Handler operates within the Web API pipeline and is specific to Web API requests.  
- Delegating Handlers are more flexible and easier to configure for API-specific logic.  
- I used Delegating Handlers in a project to implement custom authentication for APIs without affecting the entire application.  

```csharp
public class CustomHandler : DelegatingHandler  
{  
    protected override async Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)  
    {  
        // Custom logic  
        return await base.SendAsync(request, cancellationToken);  
    }  
}
```

### **26. Explain briefly OWIN (Open Web Interface for .NET) self-hosting.**  
- OWIN decouples web applications from the server, allowing self-hosting without IIS.  
- It provides a lightweight, flexible way to host Web APIs.  
- Self-hosting is useful for console applications and Windows services.  
- I used OWIN self-hosting to run a background task API in a Windows service.  

```csharp
WebApp.Start<Startup>("http://localhost:9000");
```

### **27. Could you clarify what is the best practice with Web API error management?**  
- Use exception filters to handle exceptions centrally.  
- Return meaningful HTTP status codes for different error types.  
- Log errors for diagnostics and monitoring.  
- I implemented global error handling in a financial application to ensure consistent error responses across APIs.  

```csharp
public class GlobalExceptionFilter : ExceptionFilterAttribute  
{  
    public override void OnException(HttpActionExecutedContext context)  
    {  
        context.Response = new HttpResponseMessage(HttpStatusCode.InternalServerError);  
    }  
}
```

### **28. What is the difference between WCF, Web API, WCF REST, and Web Service?**  
- WCF supports SOAP and multiple protocols, Web API is REST-focused and HTTP-only.  
- WCF REST requires configuration, whereas Web API is RESTful by default.  
- Traditional Web Services (ASMX) are legacy SOAP-based services.  
- I chose Web API for a project requiring lightweight, JSON-based communication and WCF for SOAP interoperability.  

```csharp
[ServiceContract]  
public interface IService  
{  
    [OperationContract]  
    string GetData(int value);  
}
```

### **29. Why should I use IHttpActionResult instead of HttpResponseMessage?**  
- IHttpActionResult simplifies unit testing by abstracting the HTTP response creation.  
- It provides a cleaner, more readable API by encapsulating response details.  
- It allows built-in helper methods like `Ok()`, `NotFound()`, etc.  
- I used IHttpActionResult in a project to streamline controller code and improve readability.  

```csharp
public IHttpActionResult GetProduct(int id)  
{  
    var product = productService.GetProduct(id);  
    if (product == null) return NotFound();  
    return Ok(product);  
}
```

### **30. How to restrict access to a Web API method to specific HTTP verbs?**  
- Use HTTP method attributes like `[HttpGet]`, `[HttpPost]`, etc.  
- This enforces the correct HTTP verb for each action.  
- Combining with routing provides fine-grained control over API behavior.  
- I used verb restrictions in a project to separate read and write operations in a RESTful service.  

```csharp
[HttpGet]  
public IEnumerable<Product> GetProducts() { return productService.GetAll(); }
```

### **31. How can we provide an alias name for an ASP.NET Web API action?**  
- Use the `[ActionName]` attribute to give an action a different name in the route.  
- This helps avoid name conflicts and improves API readability.  
- Aliases are useful for creating user-friendly endpoints.  
- I used action aliases in a project to create intuitive, readable API routes.  

```csharp
[ActionName("List")]  
public IEnumerable<Product> GetAllProducts() { return productService.GetAll(); }
```


