# ASP.NET Core

ASP.Net core came out with .Net core in 2016, it's a cross platform open source web framework that can be used to web apps and services.

![image](https://github.com/user-attachments/assets/92aa250a-f5ab-47d0-a29f-853a56c31201)

We can build different types of applications using ASP.Net including

- Server Side Rendering: Where the user makes an HTTP Request and we return a dynamic HTML Content to the user, like ASP.Net core MVC

- Services: API Projects that the user can send a request to and then get content, typically in JSON, used commonly by front end developers to integrate with Backend

- Client Side Rendering: New type of projects that when the user sends a request, the server returns an application that the user can run on their side, and any needed JSON files for the application to work will be sent by the server

![image](https://github.com/user-attachments/assets/d19a13b5-cc7e-4bc5-b3d8-fbd544e8947c)

## ASP.Net Core Architecture

The bottom architucture platform represents ASP.Net core, while the top ones represents applications platforms that can be built using ASP.Net core.

ASP.Net Core MVC Refers to the Model View Controller Architecture pattern that existed well before ASP.Net core itself, Where the Model represents the entities in the application, Controller for handling API Requests and the view for front end options.

Razor and Blazor pages are front end options for ASP.Net core, they came out since the front end options had some issues in ASP.Net core MVC

And ASP.Net Web APIS (and minimal apis) refer to the services application we talked about.
![image](https://github.com/user-attachments/assets/cdc69ed3-d49c-4e49-82d9-4e404674505e)

## Program.cs File

![image](https://github.com/user-attachments/assets/446d6e33-0dcf-4edf-8d4a-3a52bfa35f52)

When running 

```csharp
var builder = WebApplication.CreateBuilder(args);
```

An ASP.Net core server known as Kestrel is ran, this server is used for handling requests coming from different users for different applications

Program.cs file exists in all asp.net core project templates whether its mvc, razor pages,....

It has 2 Main Tasks

Setting up dependencies and Middleware pipeline.

![image](https://github.com/user-attachments/assets/8254fec0-4e93-4a8a-a896-bed2f39a6855)

Through the Services DI container in program.cs, we can map interfaces to classes that we want to depend on to avoid tight coupling the code (and respecting dependency inversion principle of SOLID)

```csharp
builder.Services.AddControllersWithViews();
```
![image](https://github.com/user-attachments/assets/9a88539d-f527-4e44-8d35-6471d8f8f7e5)

For the Middleware pipeline, we can build it layer by layer using the "app" variable we defined.

```csharp
var app = builder.Build();
```
For example

```csharp
app.UseStaticFiles();
```
app.UseStaticFiles adds a middleware layer that is in charge of routing static files (like images) when they are requested, when the request is recieved, it goes to thorugh the HTTP Redirects Middleware and then to the Static Files middleware which then returns the static file to the user.

The pipeline is shortcircuited, it didnt reach the endpoint middle ware which is responsible for returning (json) content, which improves the performance. 

The order of setting up middleware layers **does matter**

![image](https://github.com/user-attachments/assets/ebd41ad9-e826-450f-95e6-e1a6180ea99a)

