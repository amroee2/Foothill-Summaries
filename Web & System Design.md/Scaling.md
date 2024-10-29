# Scaling

In software development, scalability is a system’s capacity to adapt to precedented as well as unprecedented increases in workload. For example, the scalability of a database determines how it can adapt to new users joining the system or how it handles integrations.

## Software scalability analysis

Software scalability analysis (scalability testing) is the process of testing the performance of a system or software application. This procedure determines how the system or application responds to structural changes that increase the workload.

Here are the scalability testing attributes to consider:

- Response Time

Response time refers to the time that elapses between a user’s request and the application’s response — the lower the response time, the better the application’s performance. On average, users can tolerate a 5-second response time. Anything above that harms your app’s performance and hampers the user experience.

- Resource usage (network and memory)

This attribute measures the capacity of memory and network bandwidth in use when the application is in full operation.

- Throughput

Throughput is a measurement unit that tracks the number of requests processed within a specific time interval. For instance, web applications measure throughput by the number of queries received or processed in the specified time frame.

- Cost

This attribute determines the price of every transaction carried out by the application.

## When To Scale

- The system prevents you from introducing new technologies

Due to compatibility issues, businesses that rely on legacy systems often struggle to integrate new technologies and automation. As a result, upgrading the software becomes a tedious — if not impossible — task to accomplish.

- The current tech leads to constant interruptions resulting from downtimes

Security issues and internal vulnerabilities like buggy code and conflicting codebases might be disrupting the system. Not only that, any technical failure in monolithic systems affects the entire application — if one module fails, the whole system must be fixed to get things running at a regular pace.

- The system in place costs your company money

Although massive corporations can handle massive spending to address scalability problems, startups and SMBs need to explore ways to limit expenditure while maintaining optimum product performance. If you are spending a fortune just to fix a recurring issue, then it is time to find a scalability model for your system.

## Types of scalability

 - Horizontal scaling

Horizontal scaling (scaling out) involves adding nodes to (or removing nodes from) a system. A node, in this scenario, could be a new computer or server. Essentially, adding more servers to an existing application means that you are scaling it out.

Massive social networks rely on horizontal scalability to increase the capacity to scale workloads and share processing power. Horizontal scaling also lets you keep your existing computing resources online while adding more nodes. However, adding multiple nodes increases the initial costs, since the system becomes more complex to maintain and operate.

- Vertical scaling

Vertical scaling (scaling up) involves adding resources to a single node instead of the entire system. When you scale up your application, you increase its capacity and throughput. Not only that, vertical scaling gives you massive computing power and allows data to live on a single node, albeit within the limits of your server. 

One major drawback to the vertical scalability model is that it follows Amdahl’s law, which states that “the overall performance improvement gained by optimizing a single part of a system is limited by the fraction of time that the improved part is actually used.” In essence, vertical scalability gives you more computing power which diminishes over time due to limited usage. Another major drawback is that vertical scaling exposes your system to a single point of failure, which places your data at risk when failures occur.

![image](https://github.com/user-attachments/assets/1e226890-6633-40ec-a0bf-32b2741f0899)

## Best practices to improve software scalability

- Outline scalability metrics

Before analyzing your application’s scalability potential, outline the fundamental values to measure. Attributes like throughput, resource usage, and response time should top the list of scalability metrics for every software.

- Use cloud storage

- Adopt caching techniques

A cache stores pre-computed results that the application can access without having to process those requests again. As a result, caches allow your application to retrieve data from the database, which reduces the overall response time.
