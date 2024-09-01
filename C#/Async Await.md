# Async Await

Async and Await in C# are used for asynchronous programming, which allows you to perform tasks without blocking the main thread. 

async: The async keyword is used to define an asynchronous method. It tells the compiler that the method can contain await expressions and that it might perform asynchronous operations.

await: The await keyword is used inside an async method to pause its execution until the awaited task completes. This allows other operations to run concurrently while waiting.

- Non-blocking: When you await a task, the control returns to the caller method, allowing the application to remain responsive.
- Continuations: Once the awaited task completes, the method resumes execution from the point where it was paused.

**Example**

```
using AirportTicketBookingSystem.Models;
using AirportTicketBookingSystem.Utilties;
using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace AirportTicketBookingSystem.Airport_Repository
{
    public class FlightsRepository
    {
        public async static Task ExportToCsvAsync()
        {
            try
            {
                StringBuilder csvContent = new StringBuilder();
                csvContent.AppendLine("FlightId,DepartureDate,DeparetureCountry,DestinationCountry,DepartureAirport,ArrivalAirport");

                foreach (var flight in Utilities.flights)
                {
                    csvContent.AppendLine($"{flight.FlightId},{flight.DepartureDate},{flight.DepartureCountry},{flight.DestinationCountry},{flight.DepartureAirport},{flight.ArrivalAirport}");
                }
                string filePath = Path.Combine("./flights.csv");
                await File.WriteAllTextAsync(filePath, csvContent.ToString());
                Console.WriteLine("Flights exported to flights.csv");
            }
            catch (Exception e)
            {
                Console.WriteLine(e.Message);
            }
        }
        public async static Task ImportFromCsvAsync()
        {
            try
            {
                string filePath = Path.Combine("./flights.csv");

                string[] lines = await File.ReadAllLinesAsync(filePath);

                for (int i = 1; i < lines.Length; i++)
                {
                    string line = lines[i];
                    string[] values = line.Split(',');

                    if (values.Length == 6)
                    {
                        Flight flight = new Flight(Convert.ToInt32(values[0]), DateTime.Parse(values[1]), values[2], values[3], values[4], values[5]);

                        // Validate the flight object
                        var context = new ValidationContext(flight, serviceProvider: null, items: null);
                        var results = new List<ValidationResult>();

                        bool isValid = Validator.TryValidateObject(flight, context, results, true);

                        if (isValid)
                        {
                            Utilities.flights.Add(flight);
                        }
                        else
                        {
                            foreach (var validationResult in results)
                            {
                                Manager.errorMessages.Add($"Line {i + 1}: {validationResult.ErrorMessage}");
                            }
                        }
                    }
                    else
                    {
                        Manager.errorMessages.Add($"Line {i + 1}: Invalid line format: {line}");
                    }
                }

                if (Manager.errorMessages.Any())
                {
                    Console.WriteLine("The following errors were found:");
                    foreach (var errorMessage in Manager.errorMessages)
                    {
                        Console.WriteLine(errorMessage);
                    }
                }
                else
                {
                    Console.WriteLine("Flights imported successfully from flights.csv");
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"An error occurred while reading the file: {e.Message}");
            }
        }
    }
}
```
```
        public static List<Flight> flights = new List<Flight>();
        public static void PrintMenu()
        {
            _ = GenerateFlights();
            Console.Clear();

            while (true)
            {
                try
                {
                    Console.WriteLine("Welcome!\nYou Are?\n1-Manager\n2-Passenger\n3-Exit");

                    int op = Convert.ToInt32(Console.ReadLine());
                    switch (op)
                    {
                        default:
                            Console.WriteLine("Invalid Option"); PrintMenu();
                            break;
                        case 1:
                            ManagerUtilities.PrintMenu();
                            break;
                        case 2:
                            PassengerUtilities.PrintMenu();
                            break;
                        case 3:
                            return;
                    }
                }
                catch (Exception e)
                {
                    Console.WriteLine(e.Message);
                }
            }
        }
        public async static Task GenerateFlights()
        {
            await FlightsRepository.ImportFromCsvAsync();
        }
```
Despite the ImportFromCsvAsync being called first, the menu was printed before the flights were imported, this is due to the fact that the working on the method stopped on the await line and it proceeded to print the menu and then go back once the await line was done.

```
Welcome!
You Are?
1-Manager
2-Passenger
3-Exit
Flights imported successfully from flights.csv
```
