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

# ASP.Net Core MVC

## Models

Models are classes that contain the entites of the project (Poco classes) and the classes that manages data (repositroy classes), we access the database through model classes to fetch any needed data to display for the user

![image](https://github.com/user-attachments/assets/8a03de41-742e-45a3-bf5e-870850c86301)

```cshap
namespace BethanysPieShop.Models
{
    public class Pie
    {
        public int PieId { get; set; }
        public string Name { get; set; } = string.Empty;
        public string? ShortDescription { get; set; }
        public string? LongDescription { get; set; }
        public string? AllergyInformation { get; set; }
        public decimal Price { get; set; }
        public string? ImageUrl { get; set; }
        public string? ImageThumbnailUrl { get; set; }
        public bool IsPieOfTheWeek { get; set; }
        public bool InStock { get; set; }
        public int CategoryId { get; set; }
        public Category Category { get; set; } = default!;
    }
}
```

![image](https://github.com/user-attachments/assets/fbae6ca9-edb6-4c1b-a398-f1fdc8445246)

Repositroy classes must implement an interface, and we can use it's methods through that interface via dep injection that we can add through 3 methods

![image](https://github.com/user-attachments/assets/4e8765e7-6ed2-4846-8377-be4fced3ca89)

- AddScoped: Maps the class to the interface, whenever the interface is "instaniated", we will get an instance of the mapped class, the instance stays per scope (per http request)

- AddTransient: A new instance of the service is created each time it is requested.

- AddSingleton: A single instance of the service is created and shared across the entire application lifecycle.

AddScoped is the most used, and the dependencies are added to the services DI container in program.cs

## Controller

Controllers are the center of the project, they interact with models and views depending on user interactions, and it has no database knowledge

![image](https://github.com/user-attachments/assets/2c49e9aa-1c96-477c-a5cb-60b32b57b335)

```csharp
using BethanysPieShop.Models;
using BethanysPieShop.ViewModels;
using Microsoft.AspNetCore.Mvc;

namespace BethanysPieShop.Controllers
{
    public class PieController : Controller
    {
        private readonly IPieRepository _pieRepository;
        private readonly ICategoryRepository _categoryRepository;

        public PieController(IPieRepository pieRepository, ICategoryRepository categoryRepository)
        {
            _pieRepository = pieRepository;
            _categoryRepository = categoryRepository;
        }

        public IActionResult List()
        {
            PieListViewModel piesListViewModel = new PieListViewModel(_pieRepository.AllPies, "Cheese cakes");
            return View(piesListViewModel);
        }
    }
}
```

The List() method will return a view (discussed in a second) with the address /pie/list

## Views

They represent the pages that the user can interact with, they are html templates (cshtml) that use razor code to display dynamic data that is passed to it from the controller (that took it from the model)

![image](https://github.com/user-attachments/assets/22d26999-ca34-42bb-b591-4c01d6b6dde5)

We can pass data to views in different ways

- ViewBag

We can pass what is known as a view bag to the view as defined in the example here

![image](https://github.com/user-attachments/assets/c7169bd8-c633-43ee-b203-c28bffb25eea)

![image](https://github.com/user-attachments/assets/c8c7f6e3-42cf-43ab-bd2a-aea3083ea391)

![image](https://github.com/user-attachments/assets/34e44ba7-990e-4b7b-847c-ec89ceb63c8d)

- Strongly Typed Views

We simply pass on what we want to dispaly, list of pies here for example, then in the view we can map the model to contain the list (more examples coming)

![image](https://github.com/user-attachments/assets/764e9050-7ebf-411f-9287-54017f45a38e)

![image](https://github.com/user-attachments/assets/780ece16-69cc-43af-b184-5a9a49816a7e)

- View Models

View models idea is similar to "Dtos" in apis, we construct a class that contains what we want to present to the user for a specific page, for example we can define  view model for the list page we mentioned before

```csharp
using BethanysPieShop.Models;

namespace BethanysPieShop.ViewModels
{
    public class PieListViewModel
    {
        public IEnumerable<Pie> Pies { get; }
        public string? CurrentCategory { get; }

        public PieListViewModel(IEnumerable<Pie> pies, string? currentCategory)
        {
            Pies = pies;
            CurrentCategory = currentCategory;
        }
    }
}
```

Then instaniate the view model in the controller pass the instance to the view

```csharp
        public IActionResult List()
        {
            //ViewBag.CurrentCategory = "Cheese cakes";

            //return View(_pieRepository.AllPies);

            PieListViewModel piesListViewModel = new PieListViewModel(_pieRepository.AllPies, "Cheese cakes");
            return View(piesListViewModel);
        }
```

in the view, we can simply then map the @model keyword

```csharp
@model PieListViewModel

<h1>@Model.CurrentCategory</h1>
```

and then do as before

```csharp
@model PieListViewModel

<h1>@Model.CurrentCategory</h1>

<div class="row row-cols-1 row-cols-md-3 g-4">

    @foreach (var pie in Model.Pies)
    {
        <div class="col">
            <div class="card pie-card">
                <img src="@pie.ImageThumbnailUrl" class="card-img-top" alt="@pie.Name">
                <div class="card-body pie-button">
                    <h4 class="d-grid">
                    </h4>

                    <div class="d-flex justify-content-between mt-2">
                        <h2 class="text-start">
                            <a class="pie-link">@pie.Name</a>
                        </h2>
                        <h5 class="text-nowrap">
                            @pie.Price.ToString("c")
                        </h5>
                    </div>
                </div>
            </div>
        </div>
    }

</div>
```


## Layput.cshtml

Layouts are html/razor code that you want to see in all pages, but dont want to repeat in every view file (respect DRY)

Layout file

![image](https://github.com/user-attachments/assets/cf6b90d9-f643-4c0c-8015-25c1f62794d3)

then we can call layouts in each file 

![image](https://github.com/user-attachments/assets/d6ad9ae5-4fdd-469c-9ef0-8278a8be98a7)

Or use what is known is a "_ViewStart.cshtml"

## _ViewStart.cshtml

Any code in this view file will be presented in every page, so simply calling the layout in that file will resut in adding it to every page

```csharp

@{
    Layout = "_Layout";
}
```

## _ViewImports.cshtml

We can add imports to it so we dont have to repeat them in every view file

```csharp

@using BethanysPieShop.Models
@using BethanysPieShop.ViewModels

```

## Routing

There are 2 approaches for routing in asp.net core MVC

- Conventional Approach

The route is configured to bt the address/{ControllerName}/{ActionMethod}

For example, the routings here are 

https://localhost/Pie/List

and https://localhost/Pie/Details/{id}

- Attribute based approach

...

The default controller is called HomeController, and the default action method is called Index

So having a HomeController with an Index method with a view returned will result in the home page (first page when opening the website) having that said view

- Tag Helpers

They are used to navigate between pages using html anchor elements (<a>)

```csharp

<a asp-controller="Home" asp-action="Index" class="nav-link">Home</a>

<a asp-controller="Pie" asp-action="List" class="nav-link">Pies</a>
```

to import tag helpers

```csharp
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```

## Partial Views

They are like views except they arent called by the controller or passed data through it, the can be used as a shared file by other views

```csharp

@model Pie
<div class="col">
    <div class="card pie-card">
        <img src="@Model.ImageThumbnailUrl" class="card-img-top" alt="@Model.Name">
        <div class="card-body pie-button">
            <h4 class="d-grid">
                <a class="btn btn-secondary" 
                   asp-controller="ShoppingCart" 
                   asp-action="AddToShoppingCart"
                   asp-route-pieId="@Model.PieId"> + Add to cart</a>
            </h4>
            
            <div class="d-flex justify-content-between mt-2">
                <h2 class="text-start">
                    <a asp-controller="Pie"
                       asp-action="Details"
                       asp-route-id="@Model.PieId"
                       class="pie-link">@Model.Name</a>
                </h2>
                <h5 class="text-nowrap">
                    @Model.Price.ToString("c")
                </h5>
            </div>
        </div>
    </div>
</div>
```

For example, this partial view displays the information for one pie, we can add this partial view in a page that displays all pies + in a one that displays top 10 pies.

## Sessions

In ASP.NET, sessions are used to store user-specific data across multiple HTTP requests. Since HTTP is a stateless protocol (i.e., each request is independent and does not retain information from previous requests), sessions provide a way to maintain user-specific information between requests.

When a session is created, a unique session ID is generated for the user.
This session ID is typically stored in a cookie on the user's browser (ASP.NET_SessionId by default) or passed as part of the URL (if cookies are disabled).

The session ID acts as a key to retrieve the user's session data on the server.
Session data is stored in server-side storage (e.g. SQL Server).

This is particularly suitable if we want the user to interact with the server without having to log in, but sessions dont live for long and the user will have a new session id soon enough.

## Forms
...
