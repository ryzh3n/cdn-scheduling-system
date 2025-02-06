# Auto-Scheduling System 4.0: From Concept to Implementation

## 📌 Introduction

> Before continue reading, make sure you understand the fundamentals of a CDN system. [Read here](https://github.com/ryzh3n/cdn-scheduling-system/blob/main/introduction.md)

CDN (**Content Delivery Network**) optimization is crucial for ensuring **low latency, high availability, and optimal performance**. However, CDNs often face these challenges:

- **Uneven Load Distribution** → Some nodes are overloaded while others are underutilized.
- **Network Instability & Attacks** → Nodes can fail due to network outages or DDoS attacks.
- **Complex Resource Management** → Different ISPs, regions, and networks require dynamic adjustments.

To solve these problems, **Auto-Scheduling System 4.0** employs **real-time monitoring, intelligent decision-making, and automated scheduling** to dynamically adjust CDN node allocation.


## 🛠 System Workflow

The system operates in **four core stages**:

1. **Observation** – Continuously monitoring CDN nodes.
2. **Analysis** – Evaluating conditions and determining necessary actions.
3. **Execution** – Automatically applying scheduling adjustments.
4. **Review** – Logging events and refining scheduling strategies.

### 🔄 **Workflow Overview**

```
User requests website
↓
DNS resolves to a CDN node
↓
CDN node serves the request
↓
System monitors node performance & traffic
↓
If issues are detected, triggers a strategy → executes scheduling actions
↓
Adjusts DNS resolution, isolates nodes, or modifies routes
↓
Logs results & refines strategies
```

Let's break down each phase in detail.


## 🔍 1. Observation (Monitoring)

💡 **The system continuously collects real-time data from all CDN nodes.**

### 📡 **Data Sources**
| **Source**        | **Data Collected**                  |
|------------------|----------------------------------|
| **Elasticsearch** | Logs request volume (QPS), response times, error rates |
| **Prometheus**   | Monitors CPU, memory, bandwidth, network traffic |
| **MySQL**        | Stores node information (location, ISP, bandwidth) |

### 📊 **Key Monitoring Metrics**
| **Metric**     | **Purpose** |
|--------------|-----------|
| CPU Usage   | Prevent overload and maintain performance |
| Bandwidth Usage | Ensure network capacity is balanced |
| QPS (Queries Per Second) | Detect traffic spikes and redistribute requests |
| DDoS Detection | Identify attack patterns and mitigate risks |

### 🚨 **Example Triggers**
- If **CPU > 80%**, the node might be overloaded.
- If **QPS increases by 500% in 10 seconds**, it might be a DDoS attack.
- If **RTT (Round Trip Time) spikes**, network instability may be present.


## 🤖 2. Analysis (Decision-Making)

💡 **The system evaluates data and determines the necessary actions.**

When an anomaly is detected, the **Monitoring Strategy**:
- **Assigns status labels** (e.g., `"CPU Overload"`, `"Under Attack"`).
- **Evaluates node health** (Can it continue serving traffic?).
- **Determines necessary scheduling actions** (e.g., rerouting requests, isolating nodes).

### 🔍 **State Evaluation**
| **Status**     | **Trigger Condition**      | **Possible Action** |
|--------------|------------------|----------------|
| Normal       | CPU < 70%, QPS normal | No action required |
| Overloaded   | CPU > 80%, QPS high | Reduce traffic, reroute requests |
| Under Attack | DDoS detected | Trigger isolation strategy |
| Offline      | No response from node | Reroute traffic, mark as inactive |

### 🏷 **Dynamic Tagging System**
Each node is dynamically assigned **labels**:
- `CPU_Overload` → High CPU usage
- `QPS_High` → Excessive request volume
- `Under_Attack` → Possible DDoS attack detected
- `Isolated` → Node temporarily removed from service


## ⚙️ 3. Execution (Scheduling Actions)

💡 **The system executes predefined actions based on strategy evaluations.**

The core logic is handled by the **Action Strategy Module**, which determines:

### ✅ **DNS Resolution Adjustments**
- **Add new records** → Increase CDN node availability.
- **Modify existing records** → Redirect traffic to more stable nodes.
- **Delete records** → Remove unstable or compromised nodes.

### ✅ **Node Management**
- **Add new nodes** → Deploy additional nodes from a reserve pool.
- **Revert nodes** → Move underutilized nodes back to the shared pool.

### ✅ **Node Isolation**
- **Direct Isolation** → Isolate nodes experiencing CPU overload or attacks.
- **Reverse Isolation** → Redirect unaffected traffic to more stable nodes.
- **Complete Isolation** → Separate all traffic across multiple nodes to mitigate risks.

### 🔀 **Example Scenario**
- If **Node `A` is overloaded**, the system may:
  - Redirect part of its traffic to Nodes `B` and `C`.
  - If the issue persists, remove Node `A` from the DNS records.


## 📜 4. Review (Logging & Optimization)

💡 **All scheduling actions are logged for future analysis and optimization.**

### 📖 **Log Types**
- **Monitoring Logs** → Records performance changes.
- **Scheduling Logs** → Tracks executed scheduling decisions.
- **User Actions** → Logs manual configuration changes.
- **System Errors** → Captures anomalies or failures.

### 📝 **Example Log Entries**
| **Time** | **Action** | **Impact** |
|---------|----------|--------|
| 10:00  | `CPU_Overload` detected | Node `103.99.50.50` flagged |
| 10:05  | Traffic redistributed | Load reduced on `103.99.50.50` |
| 10:10  | Node returns to normal | Scheduling complete |


## 🏗 System Architecture & Modules

### 🔧 **4.1 Key Components**
1. **Monitoring System**
   - Uses **Elasticsearch**, **Prometheus**, and **MySQL** for data collection.
   - Detects anomalies based on real-time metrics.

2. **Decision Engine**
   - Implements **monitoring strategies** to evaluate node health.
   - Dynamically assigns **labels** to indicate node status.

3. **Action System**
   - Executes **DNS adjustments**, **node reassignments**, and **traffic routing**.
   - Integrates an **isolation mechanism** for security threats.

4. **Logging & Reporting**
   - Captures all scheduling activities.
   - Provides insights for continuous optimization.

### 💾 **4.2 Technology Stack**
| **Component**     | **Technology** |
|------------------|--------------|
| **Backend**      | Python (FastAPI), Go |
| **Database**     | MySQL, Elasticsearch, ClickHouse |
| **Monitoring**   | Prometheus + Grafana |
| **Message Queue** | Kafka, RabbitMQ |
| **Containerization** | Docker, Kubernetes |
| **API Gateway**  | OpenResty (Nginx + Lua) |


## 🎯 Conclusion

🚀 **Auto-Scheduling System 4.0** optimizes CDN node distribution dynamically through:
1. **Real-time monitoring** to detect performance issues.
2. **Intelligent decision-making** to assess node health.
3. **Automated scheduling actions** to redistribute traffic efficiently.
4. **Logging and continuous optimization** to refine strategies.

### ✅ **Key Benefits**
- **Improved CDN Performance & Reliability**
- **Reduced Operational Costs**
- **Real-time DDoS Mitigation**
- **Seamless Scaling & Automation**

### 🔮 **Future Enhancements**
- Integrate **AI-based anomaly detection**.
- Improve **predictive load balancing models**.

💡 If you find this project useful, **Star ⭐️ and Contribute**! 🚀
