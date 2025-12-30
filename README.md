# Enterprise Network Design & Signal Analysis Portfolio

1. Project Overview: This project demonstrates the design and implementation of a segmented departmental network infrastructure alongside a technical analysis of digital signal quantization1. The goal was to establish a functional, secure network with inter-departmental communication and verified application services.

2. Network Architecture: The network utilizes a Star Topology centered around a Cisco switch.
• Segmentation: The organization is divided into four logical departments: Admin, Sales, Marketing, and IT.
• Inter-VLAN Routing: Implemented "Router-on-a-Stick" using 802.1Q encapsulation to allow secure communication between subnets.
3. Technical Implementation:
   VLAN & IP Schema

   ### VLAN Configuration
| Department | VLAN | Gateway | Ports |
| :--- | :--- | :--- | :--- |
| Marketing | 10 | 192.100.30.1 | Fa0/4, Fa0/5 |
| Admin | 20 | 192.100.30.33 | Fa0/2, Fa0/3 |
| IT | 30 | 192.100.30.65 | Fa0/6, Fa0/7, Fa0/10 |
| Sales | 40 | 192.100.30.97 | Fa0/8, Fa0/9 |

  Application Services: 
  • Web Hosting: A Sales web application is hosted at http://192.100.30.98
  • DNS Resolution: Configured a DNS server at 192.100.30.66 to resolve the local domain sales.carscity.local.
  
4. Verification & Analysis:
   Connectivity Tests: Success was verified through internal and cross-departmental pings:
   • Intra-VLAN: Marketing PC to Gateway (192.100.30.1) — Success.
   • Inter-VLAN: Admin PC to IT Server (192.100.30.66) — Success.
   
 - Protocol Deep-Dive (PDU Analysis)

   I performed deep-packet inspection at the switch to verify the OSI model encapsulation:
   • Layer 2: Ethernet II framing with Source/Destination MAC addresses.
   • Layer 3: IP routing from IT Server to IT PC.
   • Layer 4/7: UDP transport for DNS queries resolving sales.carscity.local.
   
6. Engineering Analysis: Signal Quantization

   A study was conducted on converting analog signals to digital outputs, comparing 3-bit and 8-bit precision.
   • 3-bit depth: Resulted in 8 levels, showing visible rounding errors (signal fidelity loss).
   • 8-bit depth: Utilized 256 levels for significantly higher precision and signal accuracy.

7. How to Run the Simulation
   
   i. Download and Install: Ensure you have Cisco Packet Tracer installed.
   ii. Open Project: Download the .pkt file from this repository and open it.
   iii. Verify Services:
     - Open any departmental PC (e.g., Marketing PC).
     - Go to Desktop > Web Browser and enter http://192.100.30.98.
     - Open the Command Prompt and type nslookup sales.carscity.local to verify DNS resolution.
   iv. Test Connectivity: Use the ping command to test communication between different VLANs (e.g., pinging from Admin PC to IT Server).
