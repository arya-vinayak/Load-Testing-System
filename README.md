# **GoLoadTester**

GoLoadTester is a comprehensive load testing system built using GoLang. It is designed to stress-test and evaluate the performance and scalability of your applications. This system uses Sarama for Kafka integration and Gin for creating endpoints.

## **Prerequisites**

Before running GoLoadTester, ensure that you have the Go compiler, toolchain, and runtime environment installed. Additionally, for Kafka integration on macOS, you can use Homebrew to install Kafka and its dependencies:

```bash

brew install java
brew install kafka

```

Start Zookeeper and Kafka services in separate terminals:

**Start Zookeeper:**

```bash

zookeeper-server-start /opt/homebrew/etc/kafka/zookeeper.properties

```

**Start Kafka:**

```bash

kafka-server-start /opt/homebrew/etc/kafka/server.properties

```

## **Installation**

Clone the repository:

```bash

git clone https://github.com/arya-vinayak/Load-Testing-System.git
cd Load-Testing-System

```

Build the executable:

```bash

go build

```

## **Usage**

1. **Run HTTP Server:**
    
    ```bash
    
    ./httpServer
    
    ```
    
    This starts the test server. Modify **`httpServer.go`** to adapt the server to your needs.
    
2. **Run Orchestra:**
    
    ```bash
    
    ./Orchestra 
    
    ```
    
    Edit **`Orchestra.go`** and the **`config.yaml`** file to define your test scenarios, target URLs, and other parameters.
    
3. **Run Driver Nodes:**
    
    ```bash
    
    ./driverNode 
    
    ```
    
    This simulates load by sending requests to the test server using multiple driver nodes.
    

## **System Details**

- The orchestrator node and driver node are implemented as separate processes.
- The Orchestrator node and the Driver node communicate via Kafka. The Kafka IP Address and Orchestrator node IP Address are provided as command-line arguments.
- All nodes must possess a unique ID used to register themselves and generate unique IDs as necessary.

## **Functionality**

- **Load Test Types:**
    - Tsunami testing: Set a delay interval between each request, maintaining the gap between each request on each node.
    - Avalanche testing: Send all requests as soon as they are ready in a first-come, first-serve order.
- The system supports target throughput per driver node and stops once responses for all specified requests are received.
- No time bound for test stop; it depends on when all responses are received.

## **Observability**

- The Orchestrator node knows how many requests each driver node has sent, updated at a maximum interval of one second.
- The Orchestrator node displays a dashboard with aggregated {min, max, mean, median, mode} response latency across all nodes and for each node.
- Both the driver node and the orchestrator node have a metrics store.

## **Scalability**

- The system is scalable, supporting a minimum of three (one orchestrator, two driver) and a maximum of nine (one orchestrator, 8 driver) nodes.
- It is possible to change the number of driver nodes between tests.

## **Code Implementation**

### **Orchestrator Node**

- Exposes a REST API to view and control different tests.
- Triggers load tests.
- Reports statistics for a current load test.
- Implements a Runtime controller handling heartbeats from Driver Nodes, coordinating between driver nodes to trigger load tests, and receiving metrics from driver nodes, storing them in the metrics store.

### **Driver Node**

- Sends requests to the target web server as indicated by the Orchestrator node.
- Records statistics for {mean, median, min, max} response time.
- Sends results back to the Orchestrator node.
- Implements a communication layer that talks to the central Kafka instance, implemented around a Kafka Client.

### **Target HTTP Server**

- Implements an endpoint to test (/ping).
- Implements a metrics endpoint to see the number of requests sent and responses sent (/metrics).

## **Future Updates**

An update with a customizable GUI is planned for early 2024.

## **Contact**

For questions or support, please contact [aryavinayak2003@gmail.com](mailto:aryavinayak2003@gmail.com).
