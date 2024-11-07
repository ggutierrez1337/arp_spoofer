# ARP Spoofer

<h2>Description</h2>
This Python project demonstrates how to perform ARP (Address Resolution Protocol) spoofing and how to restore the ARP tables after an attack. The script uses Scapy, a Python library used for packet manipulation and network analysis. ARP spoofing, also known as ARP poisoning, allows an attacker to intercept traffic between a victim and the network gateway, enabling man-in-the-middle (MITM) attacks. The project also includes functionality to restore the network to its original state once the attack is stopped.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Python</b>
- <b>Scapy (package)</b> 
- <b>Time (package)</b>

<h2>Environments Used </h2>

- <b>Kali Linux</b> 
- <b>PyCharm</b>

<h2>Skills Learned</h2>

<ol>
        <li><b>Network Protocols:</b> Understanding <code>ARP</code>, <code>IP</code>, and <code>MAC</code> addresses, and how they interact in local networks.</li>
        <li><b>Scapy Library:</b> Using Scapy for crafting and sending packets, as well as interacting with network protocols.</li>
        <li><b>MITM Attacks:</b> Implementing and understanding the concept of man-in-the-middle attacks by manipulating ARP tables.</li>
        <li><b>Packet Analysis:</b> Understanding the components of ARP and Ethernet frames, and how data is transmitted across the network.</li>
        <li><b>Error Handling:</b> Implementing graceful shutdowns with <code>try-except</code> blocks to handle keyboard interrupts and restore network integrity.</li>
    </ol>

<h2>Program Walthrough</h2>

<ol>
        <li><b>Setting Up Port Forwarding:</b> Before running the script, port forwarding must be enabled on the Kali machine with the command:
            <pre><code>echo > 1 /proc/sys/net/ipv4/ip_forward</code></pre>
        </li>
        <li><b>Get MAC Address Function:</b> The <code>get_mac()</code> function sends an ARP request to the target IP, asking for its MAC address. It returns the MAC address of the target.</li>
        <li><b>Spoofing Function:</b> The <code>spoof()</code> function creates an ARP packet with the attacker's MAC address, pretending to be the router (or any spoofed source). This packet is then sent to the target device, making it believe the attacker is the router.</li>
        <li><b>Restore Function:</b> The <code>restore()</code> function sends ARP packets to restore the MAC addresses to their original state, fixing the ARP tables of both the target and the gateway.</li>
        <li><b>Main Attack Loop:</b> The script continuously sends spoofing packets to both the target and the gateway, creating a MITM attack. The counter <code>sent_packets_count</code> tracks the number of packets sent.</li>
        <li><b>Termination:</b> When the user interrupts the attack (via CTRL+C), the script calls the <code>restore()</code> function to reset the network devices to their normal state.</li>
    </ol>

<h1><b>What is ARP?</b></h1>
ARP (Address Resolution Protocol) is a network protocol used to map an IP address to its corresponding MAC (Media Access Control) address in a local network. ARP operates at the Data Link Layer (Layer 2) and the Network Layer (Layer 3) of the OSI model.

<br></br>

When a device on a network needs to communicate with another device, it uses IP addresses to route the message. However, once the message reaches the local network, it needs to be delivered to the correct device using its MAC address, which is specific to the network interface. This is where ARP comes into play: it enables devices to discover the MAC address of a device that corresponds to a known IP address.

<h1><b>ARP Request:</b></h1>
    <p>This is a message broadcasted to all devices in the local network (Layer 2 broadcast) asking for the MAC address that corresponds to a specific IP address.</p>
    <p>The request contains:</p>
    <ul>
        <li><b>Sender MAC address:</b> The MAC address of the requesting device.</li>
        <li><b>Sender IP address:</b> The IP address of the requesting device.</li>
        <li><b>Target IP address:</b> The IP address for which the MAC address is being requested.</li>
        <li><b>Target MAC address:</b> Set to <code>00:00:00:00:00:00</code> initially (since it's unknown).</li>
    </ul>
    <p>The ARP request is broadcast to all devices in the local subnet, and the device with the matching IP address responds with its MAC address.</p>
    
<h1><b>ARP Reply:</b></h1>
    <p>This is a unicast message sent by the device that owns the IP address being queried. It provides the MAC address that corresponds to the requested IP.</p>
    <p>The reply contains:</p>
    <ul>
        <li><b>Sender MAC address:</b> The MAC address of the device responding to the request.</li>
        <li><b>Sender IP address:</b> The IP address of the responding device.</li>
        <li><b>Target MAC address:</b> The MAC address of the requesting device (i.e., the device that sent the ARP request).</li>
        <li><b>Target IP address:</b> The IP address of the requesting device.</li>
    </ul>

<h2>How ARP Works</h2>

<b>ARP Request:</b>
<ul>
  <li>A device (e.g., a computer) needs to send data to another device within the same local network but only knows its IP address.</li>
  <li>The device broadcasts an ARP request packet, asking, "Who has IP address <code>X.X.X.X</code>? Tell me your MAC address."</li>
</ul>

<b>ARP Reply:</b>
<ul>
  <li>The device with the matching IP address responds with an ARP reply that contains its MAC address.</li>
  <li>The requesting device then caches this IP-to-MAC mapping for future use.</li>
</ul>

<b>Caching:</b>
<ul>
  <li>Both the requester and the responder cache the mapping of IP-to-MAC in an ARP table (or ARP cache) for a certain period. This eliminates the need for repeated ARP requests for the same address.</li>
</ul>

<b>Example:</b>
<p>Suppose Device A (IP: <code>192.168.1.2</code>) wants to communicate with Device B (IP: <code>192.168.1.3</code>) in the same local network. Device A does not know the MAC address of Device B, so it sends an ARP request:</p>

<pre><code>Who has 192.168.1.3? Tell 192.168.1.2</code></pre>

<p>Device B responds with an ARP reply:</p>

<pre><code>192.168.1.3 is at 00:14:22:47:82:90</code></pre>

<p>Now, Device A knows that <code>192.168.1.3</code> corresponds to the MAC address <code>00:14:22:47:82:90</code>, and it can send packets directly to this address.</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
