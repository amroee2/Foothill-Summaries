# Measuring Performance

Network performance is commonly measured in 3 ways:

- Bandwidth: the maximum amount of data (bits) that can be transmitted per a unit of time.
- Throughput: the actual number of data that was transmitted per a unit of time.
- Latency (Delay): the time it takes a packet to be sent from the sender to the reciever.

It's like a road 

A road can have 100 cars at the same time (bandwidth), but only 20 cars are crossing it (throughput), and each car takes 3 minutes to reach that end of the road (latency)

# Availability 

System availability (also known as equipment availability or asset availability) is a metric that measures the probability that a system is not failed or undergoing a repair action when it needs to be used.

![image](https://github.com/user-attachments/assets/a53b9c4d-e298-47c0-9446-798f9eb8e29c)

For example, let’s say you’re trying to calculate the availability of a critical production asset. That asset ran for 200 hours in a single month. That asset also had two hours of unplanned downtime because of a breakdown, and eight hours of downtime for weekly PMs. That equals 10 hours of total downtime.

Here is how to calculate the availability of that asset:

Availability = 200 ÷ (200 + 10)

Availability = 200 ÷ 210

Availability = 0.952

Availability = 95.2%

**World-class availability is considered to be 90% or higher.**

The more a system is available, the more work it does and the more revenue is generated, this means that availabiltiy is a very important factor for measuring a system performance.

Asset reliability refers to the probability of an asset performing without failure under normal operating conditions over a given period of time. This does not include unplanned downtimes.

For example, an asset that never experiences unplanned downtime is 100 percent reliable but if it is shut down every 10 hours for routine maintenance, it would only be 90 percent available. System availability and asset reliability go hand-in-hand because if an asset is more reliable, it’s also going to be more available.

5 ways to increase system availability

- Design a system with failure in mind

Everything fails at some point so the best way to optimize system availability is to plan on when and how your assets will fail. When building your system, consider availability concerns during all aspects of your system design and construction.

- Mitigate risk

Keeping a system highly available requires removing the risk of the system failing. In many situations, the reason for the failure could have been identified beforehand as a risk and addressed accordingly. Identifying risk is one of the best ways to ensure availability.

- Monitor availability

It’s difficult to know if there is a problem in your system unless you can see the consequences of the problem. Make sure your assets are properly tested and monitored so that you can see how they perform from internal and external perspectives throughout the production process.

- Create a standard protocol for responding to availability issues

Monitoring systems aren’t much use if action isn’t taken to fix the issues identified. To be most effective in maintaining system availability, establish processes and procedures that your team can follow to help diagnose issues and easily fix common failure scenarios. For example, if an asset becomes unresponsive, you might have a set of steps for workers to go through that might include tasks such as running a test to help diagnose where the problem is or rebooting the equipment.

- Optimize your preventive maintenance program

Preventive maintenance is regular and routine maintenance performed on physical assets to reduce the chances of equipment failure and unplanned machine downtime.
