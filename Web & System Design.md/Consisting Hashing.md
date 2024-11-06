# Consistent Hashing

Consistent hashing is a technique used in distributed systems to distribute data across multiple nodes (e.g., servers, databases) in a way that minimizes data movement when nodes are added or removed. 

## How does it work

In consistent hashing, both the nodes and data items are mapped to a virtual "ring" or circular space. Each node is assigned a position on this ring based on a hash of its identifier (e.g., an IP address or hostname). Each data item is also assigned a position on this ring by hashing its key.

When data is mapped to a ring:

- Each data item is stored on the first node that appears on the ring at or after the item's position (moving clockwise).

- If nodes are added or removed, only a portion of the data items need to be moved to rebalance the ring, minimizing data migration. This is a major benefit over traditional hashing, where changes can lead to a large reshuffle.

**Key Benefits of Consistent Hashing**

- Scalability: Nodes can be added or removed with minimal impact on the distribution of data across the remaining nodes.

- Load Balancing: Data is more evenly distributed among nodes, avoiding hotspots.

- Fault Tolerance: Losing a node doesn't affect data on other parts of the ring; only data mapped to that node is affected.

**Example in Practice**

In a distributed cache:

- Suppose there are three cache servers, each positioned on a consistent hashing ring.

- A cache key is mapped to a position on the ring.

- The data is stored in the first server clockwise from that position.

- If a new cache server is added, only some keys near its position need to move to it, reducing data reshuffling.
