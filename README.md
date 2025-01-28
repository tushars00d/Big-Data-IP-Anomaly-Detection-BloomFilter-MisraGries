# Big-Data-IP-Anomaly-Detection-BloomFilter-MisraGries
A scalable and efficient real-time IP anomaly detection system leveraging Bloom Filters and the Misra-Gries Algorithm to identify malicious traffic, detect heavy hitters, and dynamically update blacklists with minimal memory usage
Here's a structured and professional README template for your project, complete with placeholders for analysis graphs and detailed explanations of the **Bloom Filter** and **Misra-Gries Algorithm** concepts. 

## Overview

This project presents a scalable, efficient, and real-time approach to detecting anomalous IP addresses in network traffic. By combining **Bloom Filters** with the **Misra-Gries Algorithm**, we provide a memory-efficient solution capable of identifying suspicious IPs, heavy hitters, and dynamically updating blacklists. This approach is ideal for applications in cybersecurity, DDoS prevention, and enterprise network monitoring.

---

## Workflow of the Project

The project workflow systematically processes incoming IP addresses through a multi-stage detection pipeline:

1. **Initial IP Check**:
   - Incoming IP addresses are first checked against the **Bad IP Bloom Filter**.
   - If a match is found, the IP is immediately classified as **Prohibited** and restricted from entering the system.

2. **Safe IP Check**:
   - IPs that pass the Bad IP Bloom Filter are then checked against the **Good IP Bloom Filter**.
   - If a match is found, the IP is considered **Safe**, and the system does not track its further entries to save memory and processing power.

3. **Risky IP Tagging**:
   - IPs that do not match either the Bad or Good Bloom Filter are classified as **Risky**.
   - The system begins tracking their occurrences in the data stream.

4. **Heavy Hitter Detection**:
   - The **Misra-Gries Algorithm** is applied to the **Risky IPs** to count their occurrences and identify **Heavy Hitters** (frequently appearing IPs that exceed a predefined threshold).
   - These heavy hitters are considered **Hazardous** and flagged for further action.

5. **Blacklist Update**:
   - Hazardous IPs identified as heavy hitters are dynamically added to the **Bad IP Bloom Filter**.
   - This ensures that future occurrences of these IPs are immediately blocked, improving the system's adaptability and security.

6. **Result Aggregation and Storage**:
   - The system aggregates results into four classifications:
     - **Prohibited IPs**: Detected in the Bad IP Bloom Filter.
     - **Safe IPs**: Detected in the Good IP Bloom Filter.
     - **Risky IPs**: Neither in the Good nor Bad filters, tracked for analysis.
     - **Heavy Hitters**: Risky IPs identified by the Misra-Gries Algorithm as frequent offenders.
   - The updated **Bad IP Bloom Filter** is persisted for future use.

---

## Features
- **Real-Time IP Anomaly Detection**: Immediate identification of malicious IPs.
- **Scalable and Efficient**: Handles large datasets with minimal memory overhead.
- **Dynamic Blacklist Updates**: Ensures continuous threat adaptability.
- **Performance Benchmarking**: Demonstrates superior speed and memory efficiency compared to traditional methods.

---

## Project Workflow

1. **Data Acquisition**: Simulated IP traffic is ingested as a continuous stream.
2. **Preprocessing**: Validates data and initializes Bloom Filters.
3. **IP Classification**:
   - **Safe**: Found in Good IP Bloom Filter.
   - **Risky**: Not found in any filter; analyzed further.
4. **Detection**:
   - Identifies heavy hitters using the **Misra-Gries Algorithm**.
   - Updates blacklist dynamically.
5. **Visualization**: Provides insights through comparison graphs.

---

## Key Concepts

### Bloom Filter
A **Bloom Filter** is a space-efficient probabilistic data structure that is used to test whether an element is a member of a set. It can result in false positives but guarantees no false negatives.

**Advantages**:
- **Memory Efficient**: Represents a large dataset compactly.
- **Fast Lookup**: Performs membership checks in constant time.

**How it Works**:
1. Hash each input element using multiple hash functions.
2. Update bits in a fixed-size bit array corresponding to hash outputs.
3. To check membership, rehash the query and verify if all corresponding bits are set.



---

### Misra-Gries Algorithm
The **Misra-Gries Algorithm** identifies frequent elements in a stream using a fixed amount of memory. It is well-suited for detecting "heavy hitters" under memory constraints.

**Steps**:
1. Track a limited number of counters for unique elements.
2. Increment counters for elements in the set, or reduce all counters if full.
3. Extract elements exceeding a frequency threshold as heavy hitters.

**Applications**:
- Identifying top traffic sources in network streams.
- Detecting DDoS attack patterns.



---

## Analysis Graphs
### As Per Dataset
![image](https://github.com/user-attachments/assets/ffd68191-d870-47e7-8f8d-46f57631a77b)

### 1. **Time Comparison**
This graph demonstrates the processing time advantage of our Bloom Filter-based system over traditional brute-force methods.

![image](https://github.com/user-attachments/assets/80ac2e50-5dd9-41d9-97ff-ab887bf895c2)

### 2. **Memory Usage**
Illustrates the significantly reduced memory footprint of our approach compared to traditional systems.

![image](https://github.com/user-attachments/assets/929a7611-4f48-40b2-94c4-7cab719348b7)


### 3. **Accuracy Comparison**
Highlights the accuracy trade-off (minor false positives) for the memory and speed benefits.

![image](https://github.com/user-attachments/assets/dcf56960-0464-4969-ab56-fd3aa6553f08)


Here are the tables for direct copying:

### Feature Comparison: Traditional vs. Bloom Filter + Misra-Gries

| **Feature**                      | **Traditional Approach**        | **Bloom Filter + Misra-Gries**      |
|----------------------------------|---------------------------------|-------------------------------------|
| **Scalability**                  | Limited                         | High                                |
| **Memory Usage**                 | High                            | Low                                 |
| **Processing Time**              | Longer                          | Faster                              |
| **False Positives**              | None                            | Minor (tunable error rate)          |
| **Real-Time Detection**          | No                              | Yes                                 |
| **Blacklist Updates**            | Static                          | Dynamic                             |

---

### Performance Metrics

| **Metric**                       | **Traditional Approach**        | **Bloom Filter Approach**          |
|----------------------------------|---------------------------------|------------------------------------|
| **Processing Time**              | 0.04 seconds                    | 0.03 seconds                      |
| **Memory Usage**                 | 17 KB                           | 14 KB                              |
| **Detection Accuracy**           | 98%                             | 92%                                |

Feel free to use or adapt these!

---

## Getting Started

### Prerequisites
- Python 3.10 or higher
- Libraries: `pandas`, `matplotlib`, `pybloom-live`

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/username/repo-name.git
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Run the project:
   ```bash
   python main.py
   ```

### Usage
- Replace the dataset file (`IP_dataset.csv`) with your own network traffic data.
- Adjust parameters like `BLOOM_FILTER_SIZE` and `ERROR_RATE` in the configuration.

---

## Results
- **Processing Time**: 0.03 seconds (Bloom Filter) vs. 0.04 seconds (Traditional).
- **Memory Usage**: 14 KB (Bloom Filter) vs. 17 KB (Traditional).
- **Accuracy**: 92% (Bloom Filter) vs. 98% (Traditional).

---

## Contribution Guidelines
We welcome contributions! Please follow these steps:
1. Fork the repository.
2. Create a new branch: `git checkout -b feature-name`.
3. Commit changes: `git commit -m "Description of changes"`.
4. Push to the branch: `git push origin feature-name`.
5. Open a pull request.

---

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Contact

For any inquiries or feedback, please contact the project maintainer:

https://www.linkedin.com/in/raj-tyagi-83765b21b/
