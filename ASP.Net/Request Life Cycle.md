# Request Life Cycle

## Middleware

Middleware component forms the basic building block of application HTTP pipeline. These are a series of components that are combined to form a request pipeline in order to handle any incoming request.

Middleware component forms the basic building block of the application'a HTTP pipeline. These are aseries of components that are combined to form a request pipeline in order to handle any incoming request. Whenever a new request comes, it is passed to the first middleware component. The component then decides, whether to generate a response after handling that incoming request or to pass it to the next component. The response is sent back along these components, once the request has been handled.

## Routing

Routing is a middleware component that implements MVC framework. The routing Middleware component decides how an incoming request can be mapped to Controllers and actions methods, with the help of convention routes and attribute routes.

Routing is a middleware component that implements MVC framework. In ASP.NET Core, the routing system is used to handle MVC URLs. The routing Middleware component decides how an incoming request can be mapped to Controllers and actions methods, with the help of convention routes and attribute routes. Routing bridges middleware and MVC framework by mapping incoming request to controller action methods.

- Convention routing

This routing type uses application wide patterns to match a different URL to various controller action methods. Convention routes represent default possible routes that can be defined with the help of controller and action methods.

- Attribute routing

This type of routing is implemented through attributes and applied directly to a specific controller or action method.

![image](https://github.com/user-attachments/assets/79b54f4e-849e-4d17-baa9-e62a1749acf4)

## Controller Initialization

At this stage of ASP.NET MVC Core Request Life Cycle, the process of initialization and execution of controllers takes place. Controllers are responsible for handling incoming requests. The controller selects the appropriate action methods on the basis of route templates provided.

At this stage, the process of initialization and execution of controllers takes place. Controllers are responsible for handling incoming requests which is done by mapping request to appropriate action method. The controller selects the appropriate action methods (to generate response) on the basis of route templates provided. A controller class inherits from controller base class. A controller class suffix class name with the Controller keyword.

The MVC RouteHandler is responsible for selecting an action method candidate in the form of action descriptor. The RouteHandler then passes the action descriptor into a class called Controller action invoker. The class called Controller factory creates instance of a controller to be used by controller action method. The controller factory class depends on controller activator for controller instantiation.

After action method is selected, instance of controller is created to handle request. Controller instance provides several features such as action methods, action filters and action result. The activator uses the controller type info property on action descriptor to instantiate the controller by name. once the controller is created, the rest of the action method execution pipeline can run.

The controller factory is the component that is responsible for creating controller instance. The controller factory implements an interface called IControllerFactory. This interface contains two methods which are called CreateController and ReleaseController.

![image](https://github.com/user-attachments/assets/279fc4ba-63b6-43c2-99de-7b043386ac64)

**Action Method Execution Process**

- Authorization Filters 

Authorization filters authorize or deny any incoming request.

In ASP.NET Core MVC, there is an attribute called Authorize. Authorize is a filter, which can be applied to an action and it will be called by a MVC Core framework before and after that action or its result are executed.

These filters are used to provide security to application, including user authorization. If authorize attribute is applied to an action method, before the action is executed, the attribute will check if the current user is logged in or not. If not it will redirect the user to the login page. Authorization filters authorize or deny any incoming request.


- Controller Creation

Instantiate Controller object.

- Model Binding

Model Binding bind incoming request to Action method parameters.

Model binding maps incoming request to action method parameters. Action method parameters are inputs for an action method. Using data values acquired from HTTP request, model binding creates objects that an action method takes as an argument.

The model binders are the components which provide data values from incoming request to invoke action methods. The model binders search for these data values under three scenarios which are

Form data values
Routing variables
Query strings
Each of these sources are examined in sequence until and unless an argument value is found.

- Action Filters

OnActionExecuting method is always called before the action method is invoked.

- Action Method Execution 

Action method inside controller classes executes logic to create Action Result. Action method returns action results to generate response.

- Action Filters 

OnActionExecuted method called is always called after the action method has been invoked.

Action filters are used to execute tasks instantly before and after action method execution is performed. In order to apply some logic to action methods, without having to add extra code to the controller class, action filters can be used either above the action method itself or above the Controller class.

## Action method execution

After the controllers are initialized, the action methods are executed and returns a view which contains Html document to be returned as response to the browser.

Action methods return objects that implements the IActionResult interface from the Microsoft.AspNetCore.Mvc namespace. The various types of response from the controller such as rendering a view or redirecting the client to another URL, all these responses are handled by IActionResult object, commonly known as action result.

When an an action result is returned by a specific action method, MVC calls its ExecuteResultAsync method, which generates response on behalf of the action method. The ActionContext argument provides context data for generating the response, including the HttpResponse object.

Controllers contain Action methods whose responsibility is to generate a response to an incoming request. An action method is any public method inside a controller that responds to incoming requests.

## Result Execution

During this stage of ASP.NET MVC Core Request Life Cycle, result i.e. the response generated to the original HTTP request, is executed. If an action method returns a view result, the MVC view engine renders a view and returns the HTML response. If result is not of view type, then action method will generate its own response.

The action method returns action result. This action result is the base class for all action results in asp.net mvc. Depending on the result of an action method, it will return an instance of one of the classes that derive from action result.

![image](https://github.com/user-attachments/assets/ba4121e5-5baf-451b-881a-ee213aa98def)

![image](https://github.com/user-attachments/assets/658b3554-91c4-4a5f-823b-15dcb3c48ae5)
