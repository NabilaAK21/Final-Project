# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology
_TODO: Fill out the information below._

The following machines were identified on the network:
- Windows 10 Hypervisor
  - **Operating System**: Windows 10 Pro
  - **Purpose**: Hypervisor
  - **IP Address**:192.168.1.1
- ELK
  - **Operating System**:Uuntu Linux
  - **Purpose**:SIEM/IDS - ELK Stack
  - **IP Address**:192.168.1.100
- Etc.

### Description of Targets
_TODO: Answer the questions below._

The target of this attack was: `Target 1` (TODO: IP Address: 192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

* Excessive HTTP Errors
* HTTP Request Size MOnitor
* CPU Usage Monitor

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Name of Alert 1
_TODO: Replace `Alert 1` with the name of the alert._

Alert 1 is implemented as follows:
  - **Metric**: http.response.status_code > 400
  - **Threshold**: 5 in the last 5 minutes
  - **Vulnerability Mitigated**: The alert will notify the security operations analysts of a potential attack and act according to the incident response plan. This may include blocking the IP or changing authorization credentials.
  - **Reliability**:  High reliability, very few false positives

#### Name of Alert 2
Alert 2 is implemented as follows:
  - **Metric**: http.request.bytes
  - **Threshold**: 3500 in the last 1 minute
  - **Vulnerability Mitigated**: Since this will notify when the http request size is large enough, this can help alert when a DDoS attack is in progress
  - **Reliability**: High reliability, very few false positives

#### Name of Alert 3
Alert 3 is implemented as follows:
  - **Metric**: system.process.cpu.total.pct
  - **Threshold**: 0.5 in last 5 minutes
  - **Vulnerability Mitigated**: This will trigger an alert when CPU usage rises above 50%
  - **Reliability**: Low reliability, since CPU usage is not indicative of an attack, it can trigger when any resource intensive process is running.

_TODO Note: Explain at least 3 alerts. Add more if time allows._

### Suggestions for Going Further (Optional)
_TODO_: 
- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
- Vulnerability 1
  - **Patch**: Require a stronger password policy in the user account settings, or require public key authentication in addition. Update the account password policy in Windows group policy through /etc/security/pwquality.conf or /etc/security/pwquality.conf in Linux
  - **Why It Works**: By having a strong password it will be unlikely to guess. With public key authentication, it will be almost impossible to brute force.
- Vulnerability 2
  - **Patch**: The IT team could implement an intrusion prevention system or intrusion detection system on the network.
  - **Why It Works**: Since DDoS attacks are extremely complex and diverse, it is difficult to implement only one tool to automatically respond to such an attack. With proper baselining, it will be possible for the IPS or IDS to alert or notify based on the fact that they perform deep packet analysis to see if the traffic is legitimate or not.

- Vulnerability 3
  - **Patch**: Implement a host-based intrusion prevention system, a common feature on modern anti-virus programs
  - **Why It Works**: Similar to a network-based IPS, these will perform deep packet analysis to prevent malware from installing or running on the client's computer, which may steal computer resources causing the CPU usage to spike.