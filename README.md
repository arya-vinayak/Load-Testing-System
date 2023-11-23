# **GoLoadTester**

GoLoadTester is a comprehensive load testing system built using GoLang. It is designed to stress-test and evaluate the performance and scalability of your applications. This system uses Sarama for Kafka integration and Gin for creating endpoints.

## **Prerequisites**

Before running GoLoadTester, ensure that you have the Go compiler, toolchain, and runtime environment installed. Additionally, for Kafka integration on macOS, you can use Homebrew to install Kafka and its dependencies:

```bash
bashCopy code
$ brew install java
$ brew install kafka

```

Start Zookeeper and Kafka services in separate terminals:

**Start Zookeeper:**

```bash
bashCopy code
zookeeper-server-start /opt/homebrew/etc/kafka/zookeeper.properties

```

**Start Kafka:**

```bash
bashCopy code
$ kafka-server-start /opt/homebrew/etc/kafka/server.properties

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
    
    ./driverNodes
    
    ```
    
    This simulates load by sending requests to the test server using multiple driver nodes.
    

## **Dependencies**

- Sarama: Go implementation of the Kafka protocol.
- Gin: HTTP web framework for creating endpoints.

## **Future Updates**

An update with a customizable GUI is planned for early 2024.

## **Contact**

For questions or support, please contact [aryavinayak2003@gmail.com](mailto:aryavinayak2003@gmail.com).
