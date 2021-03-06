## Network Security Homework

### Part 1

Before we get started on the lab exercise, complete the following review questions:


#### Security Control Types

With the understanding that Defense in Depth can be broken down into three different security control types, answer the following questions:

1. Walls, bollards, fences, guard dogs, cameras, and lighting are what type of security control?

    Physical

2. Security awareness programs, BYOD policies, and ethical hiring practices are what type of security control?



3. Encryption, biometric fingerprint readers, firewalls, endpoint security, and intrusion detection systems are what type of security control?



#### Intrusion Detection and Attack indicators

What's the difference between an IDS and an IPS?

IDS - Takes no action - just detects

IPS - Mediates the threat - Takes action to stop ip.



What's the difference between an Indicator of Attack and an Indicator of Compromise?

IOA:

IoAs focus more on the WHY and intent of an actor.

IOC:

IoCs are largely reactive, after exposure to a threat event or an actual incident. They do not commonly include earlier stages of an attack, such as reconnaissance against a target. In most cases, they rely heavily upon known historical hostile data to associate maliciousness by reputation or emerging reports in the wild.

Source: https://www.optiv.com/blog/ioc-and-ioa-indicators-intelligence

#### The Cyber Kill Chain

Name each of the seven stages for the Cyber Kill chain and provide a brief example of each.



#### Snort Rule Analysis

Use the Snort rule to answer the following questions:

Snort Rule #1

```
alert tcp $EXTERNAL_NET any -> $HOME_NET 5800:5820 (msg:"ET SCAN Potential VNC Scan 5800-5820"; flags:S,12; threshold: type both, track by_src, count 5, seconds 60; reference:url,doc.emergingthreats.net/2002910; classtype:attempted-recon; sid:2002910; rev:5; metadata:created_at 2010_07_30, updated_at 2010_07_30;)
```

1. Break down the Sort Rule header and explain what is happening.

Someone is scanning for VNC ports.

2. What stage of the Cyber Kill Chain does this alert violate?

Stage 1 - Reconnaissance

3. What kind of attack is indicated?

  ET SCAN Potential VNC Scan 5800-5820

  A VNC port scan

Snort Rule #2

```
alert tcp $EXTERNAL_NET $HTTP_PORTS -> $HOME_NET any (msg:"ET POLICY PE EXE or DLL Windows file download HTTP"; flow:established,to_client; flowbits:isnotset,ET.http.binary; flowbits:isnotset,ET.INFO.WindowsUpdate; file_data; content:"MZ"; within:2; byte_jump:4,58,relative,little; content:"PE|00 00|"; distance:-64; within:4; flowbits:set,ET.http.binary; metadata: former_category POLICY; reference:url,doc.emergingthreats.net/bin/view/Main/2018959; classtype:policy-violation; sid:2018959; rev:4; metadata:created_at 2014_08_19, updated_at 2017_02_01;)
```

1. Break down the Sort Rule header and explain what is happening.

A Widows executable is trying to download trough a browser.  

2. What layer of the Defense in Depth model does this alert violate?

Layer 2 - Intrusion

3. What kind of attack is indicated?

A drive-by download.


Snort Rule #3

Your turn! Write a Snort rule that alerts when traffic is detected inbound on port 4444 to the local network on any port. Be sure to include the `msg` in the Rule Option.



### Lab: "Drop Zone"

In this lab, you will assume the role of a Jr. Security Administrator at an indoor skydiving company called Drop Zone.

- Your company hosts a web server that takes online reservations and credit card payments. As a result, your company must comply with PCI/DSS regulations which requires businesses who take online credit card payments to have a firewall in place to protect PII.

- Your network has been under attack from the following three IPs: `10.208.56.23`, `135.95.103.76`, and `76.34.169.118`. Therefore, you have decided to add these culprits to the drop zone within your firewall.

- The first requirement of the PCI DSS is to protect your system with firewalls. "Properly configured firewalls protect your card data environment. Firewalls restrict incoming and outgoing network traffic through rules and criteria configured by your organization." [PCI DSS Quick Reference Guide](https://www.pcisecuritystandards.org/documents/PCI%20SSC%20Quick%20Reference%20Guide.pdf)

#### Instructions:

For this lab you will use the Network Security Lab located in Azure.

- Once logged in, launch an instance of machine `firewalld` from the HyperV Manager and login with the following credentials:
    - Username: `sysadmin`
    - Password: `cybersecurity`


The Senior Security Manager has drafted configuration requirements for your organization with the following specifications:

We will need to configure `zones` that will segment each network according to service type.

- **Public Zone**
    - Services: HTTP, HTTPS, POP3, SMTP
    - Interface: ETH0
- **Web Zone**
    - Source IP: 201.45.34.126
    - Services: HTTP
    - Interface: ETH1
- **Sales Zone**
    - Source IP: 201.45.15.48
    - Services: HTTPS
    - Interface: ETH2
- **Mail Zone**
    - Source IP: 201.45.105.12
    - Services: SMTP, POP3
    - Interface: ETH3

Lastly, you will need to create a Zone that drops all traffic from the following blacklisted IPs:
- `10.208.56.23`
- `135.95.103.76`
- `76.34.169.118`


#### Uninstall `ufw`

Before you get started, it's generally best practice to ensure that you do not have any instances of `ufw` running in order to avoid conflicts with your `firewalld` service. Additionally, this ensures that `firewalld` will be your default firewall.

- Run the command that uninstalls any running instance of `ufw`.

    sudo apt-get remove ufgw

#### Enable and start `firewalld`

By default, these service should be running. If not, then run the following commands:

- Run the commands that enables and starts `firewalld` upon boots and reboots.

  Note: This will ensure that `firewalld` service remains active after each reboot.

#### Confirm that the service is running.

- Run the command that checks whether or not the `firewalld` service is up and running.


    systemctl status firewalld



#### Start `firewalld`

- In your terminal window, run the command that starts `firewalld`.

    systemctl start firewalld


#### List all firewall rules currently configured.

Next, lists all currently configured firewall rules. This will give you a good idea of what's currently configured and save you time in the long run by not doing double work.

- Run the command that lists all currently configured firewall rules:

    - Take note of what Zones and settings are configured. You many need to remove unneeded services and settings.

#### List all supported service types that can be enabled.

- Run the command that lists all currently supported services to see if the service you need is available


#### Enable `http`, `https`, `pop3, and `smtp` service:

- Run the command that enables the services required for your setup:

 Note that we can see that the `Home` and `Drop` Zones are created by default.

#### Zone Views

- Run the command that lists all currently configured zones.

- We can see that the `Public` and `Drop` Zones are created by default. Therefore, we will need to create Zones for `Web`, `Sales`, and `Mail`.

#### Create Zones for `Web`, `Sales` and `Mail`.

- Run the command that creates Web, Sales and Mail zones.

#### Set the zones to their designated interfaces:

- Run the command that sets your `eth0` interface to your zones.

#### Add services to the active zones:

- Run the commands that add services to the **public** zone, the **Web** zone, the **sales** zone,and the **mail** zone.

- What is the status of `http`, `https`, `smtp` and `pop3`?

#### Add you adversaries to the Drop Zone.

- Run the command that will add all current and any future blacklisted IPs to the Drop Zone.

#### Make rules permanent then reload them:

Its good practice to ensure that your `firewalld` installation remains nailed up and services across reboots. This ensure that the network remains secured after unplanned outages such as, power failures.

- Run the command that reloads the `firewalld` configurations and writes it to memory

#### View active Zones

Now we'll want to provide truncated listings of all currently active zones. This a good point to verify your zone settings.

- Run the command that displays all zone services.

#### Verify the Zones are set to the correct interfaces:

- Run the command that verifies the zone setting.

- What is the status of `http`, `https`, `smtp` and `pop3`?

#### Block an IP address

- Use a rich-rule that blocks the IP address `138.138.0.3`.


  sudo firewall-cmd --add-rich-rule='rule family=ipv4 source address=138.138.0.3 reject' --permanent


#### Block Ping/ICMP Requests

You've decided to harden your network against `ping` scans by blocking `icmp ehco` replies.

- Run the command that blocks `pings` and `icmp` requests in your `public` zone.

#### Rule Check

Now that you've set up your brand new `firewalld` installation, it's time to verify that all of the settings have taken effect.

- Run the command that lists all  of the rule settings. Do one command at a time for each zone.

- Are all of our rules are in place? If not, then go back and make the necessary modification before checking again.

Congratulations! You have successfully configured and deployed a fully comprehensive `firewalld` installation.

---

### Part 2

Now, we will work on another lab. Before you start, complete the following review questions.

#### IDS vs. IPS Systems

1. Name and define two ways an IDS connects to a network.

2. Describe how an IPS connects to a network.

3. What type of IDS compares patterns of traffic to predefined signatures and is unable to detect Zero-Day attacks?

4. Which type of IDS is beneficial for detecting all suspicious traffic that deviates from the well-known baseline and is excellent at detecting when an attacker probes or sweeps a network?

#### Defense in Depth

- For each of the following scenarios, provide the layer of Defense in Depth that applies:

    1.  A criminal hacker tailgates an employee through an exterior door into a secured facility, explaining that they forgot their badge at home.

    2. A zero-day goes undetected by antivirus software.

    3. A criminal successfully gains access to HR’s database.

    4. A criminal hacker exploits a vulnerability within an operating system.

    5. A hacktivist organization successfully performs a DDoS attack, taking down a government website.

    6. Data is classified at the wrong classification level.

    7. A state sponsored hacker group successfully firewalked an organization to produce a list of active services on an email server.

- Name one method of protecting data-at-rest from being readable on hard drive.

- Name one method to protect data-in-transit.

- What technology could provide law enforcement with the ability to track and recover a stolen laptop.

- How could you prevent an attacker from booting a stolen laptop using an external hard drive?

### Lab: "Green Eggs & SPAM"

In this activity, you will target spam, discover its whereabouts, and uncover the malicious deeds that the sender is intending.

- You will assume the role of a Jr. Security administrator working for the Department of Technology for the State of California.

- As a junior administrator, your primary role is to perform the initial triage of alert data: the initial investigation and analysis followed by an escalation of high priority alerts to senior incident handlers for further review.

- You will work as part of a Computer and Incident Response Team (CIRT), responsible for producing a **Threat Intelligence Card** as part of your incident report.

#### Threat Intelligence Card

- **Indicator of Attack**

   - **Source IP/Port** 188.124.9.56/80
   - **Destination Address/Port** 192.168.3.35/1035
   - **Event Message** ET TROJAN JS/Nemucod.M.gen downloading EXE payload
   - **Infection Type** (ex. `Trojan, Virus, Worm, etc..`)
   - **Malware Type** (ex. `ransomware, Zombie "DDoS", RAT, etc..`)  

- Description of adversary:

- Adversarial motivation (Purpose of attack):

- Recommended Mitigation Strategies:

**Note:** Use the table below to guide your investigation.

| TTP | Findings |
| --- | --- |
| **Reconnaissance** |  |
| **Weaponization** | |
| **Delivery** | |
| **Exploitation** | |
| **Installation** | |
| **Command & Control (C2)** | |
| **Actions on Objectives** | |

___

For the final part of the homework, complete a set of review questions about firewall architecture and methodologies:

### Firewall Architectures and Methodologies

1. Which type of firewall verifies the three-way TCP handshake? TCP handshake checks are designed to ensure that session packets are from legitimate sources.

2. Which type of firewall considers the connection as a whole? Meaning, instead of looking at only individual packets, these firewalls look at whole streams of packets at one time.

3. Which type of firewall intercepts all traffic prior to being forwarded to its final destination. In a sense, these firewalls act on behalf of the recipient by ensuring the traffic is safe prior to forwarding it?

4. Which type of firewall examines data within a packet as it progresses through a network interface by examining source and destination IP address, port number, and packet type- all without opening the packet to inspect its contents?

5. Which type of firewall filters based solely on source and destination MAC address?

  A layer-2 Firewall

---

### Important:

Please make sure that you are set up on your personal Azure accounts prior to the first day of the Cloud Security unit. Use the following set up guide for detailed instructions: [Set-up Guide](https://docs.google.com/document/d/1gs_09b7eotl7hzTL82xlqPt-OwOd0aWA78qcQxtMr6Y/edit).

___

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
