# ASP.NET Web API

ASP.NET Web API is a framework for building RESTful services on the .NET platform. It allows for easy creation of HTTP services that can be consumed by a wide range of clients, including browsers, mobile applications, and desktop applications.

## Program.cs

```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container
builder.Services.AddControllers();
builder.Services.AddDbContext<MyDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));

// Configure logging
builder.Services.AddLogging(logging =>
{
    logging.ClearProviders();
    logging.AddConsole();
});

// Build the app
var app = builder.Build();

// Configure the middleware pipeline
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}

app.UseHttpsRedirection();
app.UseAuthorization();

app.MapControllers();

app.Run();
```

## Controllers

Controllers in Web API serve as the main entry point for handling HTTP requests. Each controller is responsible for processing incoming requests and returning the appropriate response, usually in JSON format. Controllers typically interact with services or repositories to perform CRUD operations on data.

```csharp
[ApiController]
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    private readonly IProductService _productService;

    public ProductsController(IProductService productService)
    {
        _productService = productService;
    }

    [HttpGet]
    public async Task<IActionResult> GetAllProducts()
    {
        var products = await _productService.GetAllAsync();
        return Ok(products);
    }

    [HttpPost]
    public async Task<IActionResult> AddProduct(ProductDto productDto)
    {
        var createdProduct = await _productService.AddAsync(productDto);
        return CreatedAtAction(nameof(GetAllProducts), new { id = createdProduct.Id }, createdProduct);
    }
}
```

Entity Framework Core has built-in logging that integrates seamlessly with ASP.NET Core’s logging infrastructure. This means that by default, EF Core logs queries, warnings, errors, and performance issues without requiring additional configuration.

Key Points about Automatic Logging:
Integrated with ILogger: EF Core logs messages via the ASP.NET Core ILogger interface, which supports logging to different outputs (Console, Debug, File, etc.).
Log Categories: EF Core logs important information like SQL queries executed, connection lifecycle events, and critical exceptions.
Log Level Configuration: You can configure the log level (e.g., Debug, Information, Error) in appsettings.json or via Program.cs to control the verbosity of logs.

## appsettings.json
```csharp
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=myServerAddress;Database=myDataBase;User Id=myUsername;Password=myPassword;"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

![image](https://github.com/user-attachments/assets/e916c8c8-cb11-40db-a6bc-81a4037e7a2e)


## DB Context

```csharp
﻿using FirstProject.Controllers;
using FirstProject.DAL;
using FirstProject.Models;
using Microsoft.EntityFrameworkCore;
using System.Data.Common;

namespace FirstProject.DsConn
{
    public class FirstContext : DbContext
    {
        public FirstContext(DbContextOptions<FirstContext> op) : base(op) { }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            base.OnModelCreating(modelBuilder);
            modelBuilder.Entity<Guest>().ToTable("Guest", "HotelManagementSystem");
            modelBuilder.Entity<Hotel>().ToTable("Hotel", "HotelManagementSystem");
            modelBuilder.Entity<HotelDetail>().ToTable("HotelDetail", "HotelManagementSystem");
            modelBuilder.Entity<Reservation>().ToTable("Reservation", "HotelManagementSystem");
            modelBuilder.Entity<Room>().ToTable("Room", "HotelManagementSystem");
            modelBuilder.Entity<RoomDetail>().ToTable("RoomDetail", "HotelManagementSystem");
            modelBuilder.Entity<Feedback>().ToTable("Feedback", "HotelManagementSystem");

        }

        public DbSet<Guest> Guests { get; set; }
        public DbSet<Hotel> Hotels { get; set; }
        public DbSet<HotelDetail> HotelDetails { get; set; }
        public DbSet<Reservation> Reservations { get; set; }
        public DbSet<Room> Rooms { get; set; }
        public DbSet<RoomDetail> RoomDetails { get; set; }
        public DbSet<Feedback> Feedbacks { get; set; }

    }
}

```

![image](https://github.com/user-attachments/assets/79763da3-a118-49f4-a652-308d1125fe60)
