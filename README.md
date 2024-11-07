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
        <li><b>Graceful Termination:</b> When the user interrupts the attack (via CTRL+C), the script calls the <code>restore()</code> function to reset the network devices to their normal state.</li>
    </ol>

</br>

```commandline


````

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
