 
# SIA and SSA

In this lesson, you will learn about common use cases of secure internet access ( SIA ) and secure SaaS access ( SSA ) in a FortiSASE deployment.

1. Understand SIA for FortiClient agent-based remote users
2. Understand SIA for agentless remote users.

## SIA

- Allows safe bowsing for anywhere
- Secures traffic goign to the internet
- Redirects remote user internet traffic to closest FortiSASE pop
- FortiSASE acts as a gatekeeper for all internet traffic

FortiSASE SIA extends an organization's security by enforcing a common security policy to remote users for
intrusion prevention systems (IPS), application control, web filtering, antimalware, sandboxing, and so on. FortiSASE acts as a gatekeeper to inspect and secure all internet traffic, which allows safe browsing from anywhere for off-net users.

FortiSASE redirects the internet traffic of remote users to the closest FortiSASE point of presence (POP) using geolocation selection.


### SIA - Agent based Use Case

Agent-based deployment is the most common use case in FortiSASE deployment. 

FortiClient is deployed on endpoints and the endpoints connect back to FortiSASE using a secure SSL VPN tunnel. FortiSASE Firewall-as-a-Service (FWaaS) sits between the FortiClient endpoint and the internet to secure the internet. FortiSASE FWaaS uses its security profile component, which includes web filter, application control, SSL deep inspection, and so on, to inspect the internet traffic. 
FortiClient offers endpoint protection platform (EPP) functionality, which includes features like antivirus, vulnerability scanning, sandbox inspection, and so on. Agent-based deployment also supports zero trust network access (ZTNA) for continuous posture check and enforcement.

### Configure Policies - VPN Users

The VPN Users policy contrls traffic between the FortiClient endpoint and internet for SIA.

When you create a policy, you configure the following parameters:

`Configuration > Traffic > Policies > Internet Access`

- Name: The unique policy name is a mandatory parameter, and it helps in analysis for FortiView and logging.
- Source Scope: You can select VPN Users or Edge Device, based on the endpoint traffic requirement.
	- VPN Users: Policies that have this scope control the traffic that goes through the SSL VPN tunnel that FortiClient establishes.
- Source: You can add ZTNA tags to enforce device posture checks for agent-based (FortiClient) users in an
internet access policy or private access policy.
- User: This parameter is available only when you select VPN Users. It is based on a user identity that can come
from several authentication authonties. It is a single user or group you set up in advance and can select from the
User field.
- Destination: You can define policies to connect to specific addresses on the internet.
- Service: The services you choose represent the TCP/IP suite port numbers that are most commonly used to
transport the named protocols or groups of protocols
- Profile Group: You can create security profile groups, to allow you to group different security profile settings and then apply them to a policy.
- Force Certificate Inspection: When enabled, this policy ignores the SSL inspection mode specified in the profile
group and user certificate inspection.
- Action: If the traffic matches a firewall policy, FortiSASE applies this action. If the Action is set to DENY,
FortiSASE drops the session. If the Action is set to ACCEPT, FortiSASE allows the session and applies other configured settings for packet processing, such as user authentication, source, antivirus scanning, web filtering, and so on.

### SIA Agentless Use Case

- Used for unmanaged endpoints
- PAC file is distributed to Usefs
- SWG service for agentless inline inspection
- Full security stack ( antivirus, web filter, application control, and so on )
- Shared security profiles for consistent protection

The use case for agentless deployment does not require the installation of FortiClient endpoints, and ZTNA tags are not supported. In this use case, FortiSASE acts as a secure web gateway (SWG) and distributes a proxy auto-configuration file (PAC) file to end users for using the FortiSASE SWG service as an explicit web proxy. 

SWG deployment secures only web traffic protocols, such as HTTP and HTTPS. The SWG component on FortiSASE offers a full security stack with antivirus, web filter, application control, and so on. The secunty profiles can be shared between agent and agentless deployment, for consistent protection. 

This use case is usually recommended for unmanaged endpoints like a contractor or temporary employee.

### Configuring Policies

- An SWG policy controls web traffic between the proxy client endpoint and internet for SIA

> Configuration > Traffic > SWG Policies

SWG policies control the traffic that the user's client software proxies through FortiSASE, such as a web browser. You can configure an SWG policy on the SWG Policies page. The parameters used to configure an SWG policy are similar to the VPN Users policy.

## Site-Based Users

- Understand SIA for edge devices
- Configure FortiExtender as a FortiSASE LAN extension
- Configure FortiAP as an edge device
- Configure FortiGate as a FortiSASE LAN extension

### SIA - Edge Device Use Case

- Usually for microbranch offices
- Requires configuring FortiExtender, or FortiGate as a LAN extension
- FortiExtender, FortiAP, or a FortiGate is responsible for centralizing site connectivity to the FortiSASE FWaaS
- FortiExtender or FortiGate establishes a secure VXLAN-over-IPsec with FortiSASE 
- FortiAP establishes a secure CAPWAP connection with FortiSASE 
- No endpoint configuration needed

LAN extension is a configuration mode on FortiSASE that allows FortiExtender or FortiGate to provide remote thin
edge connectivity back to the FortiSASE over a backhaul connection. A FortiExtender or FortiGate deployed at a
remote location will discover the FortiSASE access controller (AC) and form an IPsec tunnel back to the FortiSASE. 

A virtual eXtensible LAN (VXLAN) is established over the IPsec tunnels to create a layer 2 network between the FortiSASE and the network behind the remote FortiExtender or FortiGate. FortiSASE can manage a FortiAP deployed in a remote location over a backhaul connection to provide SIA to Wi-Fi clients. The FortiAP discovers the FortiSASE AC, and establishes an IPsec VPN tunnel that encrypts the data channel between FortiSASE and FortiAP. The FortiAP
carries Control and Provisioning of Wireless Access Points (CAPWAP) data packets and includes the FortiAP serial
number within this tunnel. 

In this SlA use case, FortiExtender, FortiAP, or FortiGate is responsible for centralizing site connectivity to
the FortiSASE FWaaS . No configuration is required on endpoints. All endpoint traffic is routed from the
FortiExtender, FortiAP, or FortiGate to FortiSASE FWaaS, where security profiles secure it.

### Connecting Edge Devices to FortiSASE Using FortiZTP

FortiZTP is the recommended configuration method of deploying FortiAP and FortiExtender to FortiSASE. To access the FortiZTP portal, on the FortiSASE portal, click Services > FortiZTP. After you register the devices on the Fortinet support portal with proper licenses, you can view them on the UNPROVISIONED tab on the FortiZTP portal.

You can then provision them with the target location FortiSASE. After you provision the FortiAP or FortiExtender
on the FortiZTP portal, it is automatically listed on the FortiSASE portal as an edge device, and you must Authorize it. 

After you successfully authorize the device on FortiSASE as an edge device, it connects to the POP closest to its physical location.

### Alternative Configuration Method

- Obtain FortiSASE domain name from FortiSASE Portal

As an alternative configuration method, you can enter the FortiSASE domain name as an access controller in the
FortiAP and FortiExtender GUI to connect them as an edge device on FortiSASE. To obtain the FortiSASE domain name
from the FortiSASE portal, click Edge Devices > FortiExtenders, and then click Connect FEXTs.

To connect FortiExtender to FortiSASE, on the FortiExtender GUI, click Settings > Management. Select fortigate as the controller type, static as the discovery method, and then type the FortiSASE domain name in the Server section.

Similarly, you can connect FortiAP to FortiSASE using the FortiAP GUI. On the Settings > Local Configuration page
in the WTP Configuration section, select DNS as the AC Discovery Type, and then type the FortiSASE domain name
in the AC Host Name 1 field.

### Access Point Profile

- FortiSASE automatically assigns a default FortiAP profile to newly discovered APs
	- Default profile named is based on the AP model, followed by "Default"
- FortiSASE must authorise the FortiAP device before it pushes any configuration settings to the AP

`Edge Devices > FortiAPs > Managed FortiAPs`

A FortiAP profile defines configuration settings for an access point (AP) including operating band, channels, SSID
networks, and so on. The FortiAP profile specifies the type of hardware that a FortiAP device uses. This information is required for FortiSASE when it pushes configuration
parameters to the managed AP. 

By default, when a FortiAP device is connected to FortiSASE, FortiSASE tries to discover the FortiAP device. Upon discovery of the FortiAP device, FortiSASE automatically assigns it a default profile, based on the FortiAP hardware model.

### Custom FortiAP Profile

`Edge Devices > FortiAPs > FortiAP Profiles`

FortiSASE allows you to configure a custom AP profile that controls all the settings that it pushes to an AP. You must select the correct model to tell FortiSASE what type of hardware the AP uses.

The Country/Region field provides radio frequency (RF) channels available in your area. By default, the country is set to United States. Each country has different radio regulations and, to comply with these regulations, you should select the correct Country/Region.

Client Load Balancing can assist with distributing the load across APs, using either Frequency Handoff or AP
Handoff. FortiAP can act as an 802.1X supplicant to authenticate against the RADIUS server using EAP-FAST, EAP-TLS, or EAP-PEAP. This setting is for FortiAP devices connected to a switch port with 802.1X authentication enabled.

### SSID

- Only traffic mode tunnel is supported
- Traffic is tunneled back to wireless controller using CAPWAP data channel
- FortiSASE uses IPAM to automatically configure IP address/netmask settings for an SSID
- FortiSASE wireless controller supports the following security modes:
	- WPA2 Personal
		- Pre-shared keys
	- WPA2 Enterprise and WPA3 Enterprise Only
		- RADIUS-based security modes
			- User group
			- Remote RADIUS server

By default, tunnel mode SSID is created when you define an SSID on FortiSASE. In tunnel mode, all the traffic is tunneled back to the FortiSASE wireless controller using a CAPWAP data channel. FortiSASE uses IP address management (IPAM) to automatically configure IP address/netmask
settings for an SSID.

WPA2 security with a pre-shared key for authentication is called WPA2 Personal. This mode can work well for one
person or a small group of trusted people. But, as the number of users increases, it is difficult to distribute new
keys securely and there is increased risk that the key could fall into the wrong hands.

`WPA2 Enterprise` and `WPA3 Enterprise Only` are `RADIUS-based security modes`. These are the standards any enterprise class network should be using. If you have a database of users with a RADIUS front end, this is what to use. Encryption and authentication are strongest in an enterprise network. FortiSASE supports two types of RADIUS deployment: user groups and remote RADIUS server.

### Steps to Configure FortiGate as a FortiSASE LAN Extension

To configure FortiGate as FortiSASE `LAN extension`, follow these general steps:

1. On the secure edge FortiGate, enable multi-VDOM.

2. Create a new VDOM with type LAN extension on the `SYSTEM > VDOM` page.

3. Move a minimum of two interfaces from the root VDOM to the newly created LAN extension VDOM. Configure one with the role WAN and the other with the role LAN. Configure the WAN interface with routing to reach the internet. The interface with the role LAN is where the client PCs connect to for SIA through FortiSASE. To obtain the FortiSASE domain name from the FortiSASE portal, click `Edge Devices > FortiGates`, then click Connect FortiGates, and then copy the domain name.  On the secure edge FortiGate in the newly created LAN extension VDOM, click Network > LAN Extension, paste the FortiSASE domain name, and then click `Test connectivity`.

5. To authorize the secure edge FortiGate, in the `FortiSASE portal, click Edge Devices > FortiGates`, select the FortiGate, and then click Authorize.

6. To verify the Connection Summary on the secure edge `FortiGate, click Network > LAN Extension`. When you configure the LAN extension VDOM on the secure edge FortiGate, FortiOS automatically configures a VDOM link (VLINK) between a traffic VDOM, which is by default the root VDOM, and the LAN extension VDOM.

### Secure Edge FortiGate Topologies

When you deploy an edge FortiGate as a FortiSASE LAN extension, FortiSASE can inspect traffic for users connected
to the LAN extension VDOM. Edge FortiGate inspects traffic for users connected to the default root VDOM. This can help offload some of the security inspection tasks from the edge FortiGate.

You can also use the SD-WAN functionality on the edge FortiGate to apply application steering to FortiSASE. You
can add the local internet interface on the root VDOM and the VLINK interface between the root VDOM and LAN
extension VDOM along with the specific applications to the SD-WAN rule.

### Configure Policies - Edge Devices

- An edge device policy controls the traffic between the edge LAN and internet for SIA

Policies with edge scope control the traffic that goes through edge devices, such as FortiExtender, FortiAP, and FortiGate.

No FortiClient installation is required in this deployment, therefore it doesn't support ZTNA tags.

## Secure SAAS Access

- Understand SSA using inline CASB
- Understand SSA using FortiCASB

### What is Secure SaaS ?

FortiSASE secures SaaS access and enables:
- Cloud application visibility Data security
- Risk assessment
- FortiSASE uses the following components to secure SaaS access:


- Inline CASB
	- Placed directly in the traffic path between the device and cloud application 
	- Detects data in motion

- Out-of-Band CASB
	- FortiCASB (included with FortiSASE standard, advanced, and comprehensive licenses)
	- Uses API to connect to the cloud application
	- Detects data at rest

Given the rapid increase in SaaS adoption, organizations continue to struggle with shadow IT challenges and stopping data exfiltration. FortiSASE is a superior SASE offering that includes SSA with next-generation, dual-mode cloud access security broker (CASB), using both inline and out-of-band support. It provides comprehensive visibility by identifying key SaaS applications and reporting risky applications to
overcome shadow IT challenges.

FortiSASE secures SaaS access and enables:

1. Cloud application visibility: Discover the usage of cloud applications across all sanctioned and unsanctioned
(shadow IT) cloud applications to help enforce policy-based controls.

2. Data security: Protect data in motion and at rest within cloud applications. Control productivity, privacy, compliance, and security of corporate and non-corporate tenants.

3. Assess risk: Evaluate application usage spikes to determine risk and ensure corporate data is handled safely.

FortiSASE includes an inline CASB component to detect data in motion, meaning it scans the data as it passes
through to the cloud application from the endpoint device. Out-of-band CASB utilizes API to connect to the cloud
application. Out-of-band CAB scans the data at rest.

meaning the data has already been uploaded to the SaaS application. FortiCASB is included with per-user and per-
endpoint FortiSASE licensing.

### Inline CASB Use Case

- FortiSASE uses its application control and SSL deep inspection to control SaaS cloud application traffic
- FortiSASE uses web filter and SSL inspection with an inline security component to customize HTTP headers
- FortiSASE uses DLP to keep sensitive data safe from leaking to untrusted networks or people 
- Shadow IT report
	- Usage of SaaS applications
	- Sanctioned and unsanctioned applications

Inline CASB recognizes network traffic that many applications generate. Application control with inline CASB
using IPS protocol decoders can analyze network traffic to detect application traffic, even if the traffic uses nonstandard ports or protocols. Application control with inline CASB supports traffic detection using HTTP (versions 1.0, 1.1, and 2.0). FortiSASE uses web filter and SSL deep inspection to intercept HTTP headers and can modify them for outgoing traffic. 

By customizing HTTP headers for FortiSASE outgoing traffic destined for SaaS applications, the web filter with inline CAB can control SaaS application behavior by restricting tenant access. FortiSASE also uses data leak prevention (DLP) to prevent sensitive data from leaving or entering your network by defining various sensitive data patterns, scanning for the patterns while inspecting traffic, and allowing, blocking, or logging only when traffic matches the patterns. 

You will learn to configure these features in a later lesson.

### FortiCASB Use Case

- Agentless deployment
- Integration with applications using API connector
- Visibility for bring-your-own-device (BYOD) and unmanaged locations and devices
- Data at rest scanned with the CASB engine
- Relies on the network administrator to review and act on insights after they have already occurred

FortiCASB provides visibility, compliance, data security, and threat protection for cloud applications. Using direct API access, it enables deep inspection and policy management for data stored in SaaS and Infrastructure-as-a-Service (laS) applications. 

It also provides advanced tools that provide detailed user analytics and centralized management to ensure policies are enforced and your organization's data isn't getting into the wrong hands. It relies on the network administrator to review and act upon these insights after they have already occurred. Mitigation actions include making configuration changes on FortiSASE to block future suspicious activity, denying or restricting a user's access on the SaaS application itself for the specific user generating the suspicious activity.


