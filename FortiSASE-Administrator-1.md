# Fortinet SASE Administrator - Module 1

1. Understand Remote Access VPN Architecture
2. Understand the challenges of Working from anywhere.

## Remote Access VPNs

In a Traditional VPN architecture and Next Generation Firewall NGFW is deployed on the edge of the organisational network. Remote access VPNs are intended to extend corporate network to remote users in a secure way using a software client or agent. Remote Access VPNs rely on IPSEC or SSL based VPN implementation. 

Remote Access VPNs are deployed with "Full Tunelling Mode" or "Split Tunneling Mode".

In Full Tunelling Mode 
	- Traffic destined for the organisation's internal network and internet is sent through the VPN tunnel to the NGFW for threat detection and mitigation.
	- Network congestion at NGFW WAN links
	- Latency and packet loss while acessing cloud services

In Split tunelling MOde 
	- Traffic destined for the internal network is sent through the VPN tunnel and the internet traffic is sent out through the ISP Link.
	- Internet traffic without any network security protection

Unmanaged off-net devices
	- Outdated software leading to potential vulnerabilities
	- Lack of visibility


## SASE Architecture and Components

1. Define SASE
2. Understand SASE Architecture
3. Identify SASE components
4. Understand the Fortinet SASE solution

### Define SASE

Secure Access Service Edge ( SASE ) delivers converged network and Security-as-a-Service (SECaaS) capability, including SD-WAN, secure web gateway (SWG), cloud access security broker (CASB), NGFW, and zero trust network access (ZTNA).

SASE supports branch offices, remote workers, and on-premises secure access use cases. SASE is primarily delivered as a service and enables zero-trust access based on the identity of the device or entity, combined with real-time context and security and compliance policies.

The SASE architecture focuses on using a cloud-delivered service that enforces secure access at the farthest edge of the network-namely, at the service edge or user endpoints. The goal of SASE is to offer a secure connection to the user connecting from anywhere.

### Understand Components

A "cloud-hosted security solution" frees devices from the need to rely on protection that is hosted at a physical corporate data center. Cloud-hosted security includes components like Firewall-as-a-Service (FWaaS), SWG, and CASB. FWaaS provides the same security features as a standard hardware firewall, but using software in the cloud. SWG blocks unauthorized traffic from getting into your organization's network with web filtering, antivirus, file filtering, data loss prevention (DLP), and more for both managed and unmanaged devices. CASB is positioned between the user accessing the cloud and the cloud-based application they are trying to access. It is used to monitor activity and enforce an organization's security policies.

In the context of a SASE architecture, "network service components" are used for optimized path selection and application-based routing. An SD-WAN solution can decide the best path for network traffic, and application-based routing provides access to the user to perform their jobs regardless of their location.

"ZTNA components" (Authentication, Authorisation and Control Monitoring) is built on the zero-trust access core principle of "never trust, always verify." All users, devices, and applications are assumed to be threats and, until they prove otherwise, they are not allowed to connect.

### SASE Objectives

1. Secure access for remote users
2. Reduce latency for remote users
3. Reduce network congestion
4. Scalability to meet endpoint traffic demands
5. Enforce ZTNA

When remote users connect through VPN and their internet traffic is redirected through the corporate NGFW, they experience high latency. SASE reduces this latency by allowing remote users to connect directly to the closest geographical point of presence (POP) for a cloud-delivered FWaaS, where the internet traffic is subject to advanced threat measures. Also, each POP can scale to meet user demand and reduce the
possibility that a single WAN link becomes a congestion point for these remote users. 

ZTNA allows you to apply zero-trust principles to control which users will access which application over the network. Applications are accessed when needed, directly through an access proxy or broker. With ZTNA, a user can more seamlessly work from the office or remotely, which creates a smoother user experience.

### Fortinet SASE solution 

- FortiSASE
	- Single-Vendor Approach
	- Support FWaaS
		- Same features as FortiGate NGFW
	- Supports SWG
		- Utilize FortiOS explicit web proxy, captive portal, and authentication features
	- Uses FortiGuard AI-powered security services.

FortiSASE, Fortinet's single-vendor SASE approach, empowers organizations to consistently apply enterprise-grade security and superior user experience across all edges, converging networking and security across a unified OS and agent. The cloud-delivered security service is located between the remote endpoints and any networks those endpoints access, regardless of the location of the remote endpoints. FortiSASE extends
FortiGuard security services across thin edge, secure edge, and remote users, enabling secure access to users both on and off the network. You will learn more about the different deployment methods in another
lesson.

FortiSASE supports FWaaS and SWG functionality, both of which rely on threat intelligence that FortiGuard labs provides. The FortiSASE FWaaS has all the same features, security, and reliability that customers depend on the Fortinet FortiGate NGFW physical and virtual appliances. Likewise, FortiSASE SWG relies on FortiOS explicit web proxy, captive portal, and authentication features to secure customers' web traffic. SSO integration through SAML is supported for SWG and VPN deployments.

### Fortinet SASE solution - ZTNA

- Supports ZTNA
	- FortiGate configured as Forticlient cloud and fabric connector
	- FortiGate configured as ZTNA access proxy
	- ZTNA tags can be used to device posture checks in secure internet policy and secure private access policy

- Access to CASB portal
- Existing Fortigate SD-WAN integration
- FortiSASE provides secure access to remote users for following use-cases
	- Secure Internet Access (SIA)
	- Secure Private Access (SPA)
	- Secure SaaS access (SSA)

FortiSASE supports ZTNA. In the configuration, the corporate FortiGate device is configured as a FortiClient cloud fabric connector and it acts as a ZTNA access proxy to process ZTNA traffic. FortiSASE synchronizes the ZTNA tags with the corporate FortiGate device. The ZTNA tags are used by FortiGate to allow or deny access to corporate resources. FortiSASE also uses the ZTNA tags to check for device postures in SIA policy and SPA policy.

FortiCASB provides cloud-based and API-based features to enable deep inspection of Software-as-a-Service (SaaS) applications to enable detailed monitoring, analysis, and reporting features. FortiSASE
also provides inline-CASB functionality with a web filter and application control security features. Organizations can integrate FortiSASE with existing FortiGate SD-WAN deployments in order to provide
remote users access to private resources. In this configuration, FortiSASE communicates with the FortiGate SD-WAN hub. After completing this configuration, the FortiSASE security POPs act as
spokes to this hub. 

FortiSASE provides secure access to remote users for the following use cases:

1. Secure Internet Access (SIA) - when remote users access internet adn web-based applications.
2. Secure Private Access (SPA) - when remote users access private company-hosted applications protected by FortiGate.
3. Secure SaaS access (SSA) - when remote users access SaaS applications.

## FortiSASE Provisioning

1. Understand how to provision FortiSASE
2. Understand how MSSP works
3. Understand the FortiFlex offering

To provision FortiSASE, you must register the FortiSASE contract on https://support.fortinet.com using your FortiCloud account. You can use this FortiCloud account for only one FortiSASE instance and cannot
register a FortiClient EMS cloud to this account. To access the FortiSASE portal, visit https://support.fortinet.com, and then click Services CLOUD SERVICES > FortiSASE.

- FortiSASE POPs
	- Remote users are routed to POPs goegraphically closest to them.
	- Additions POPs can be purchased
- Logging
	- Selected data center to host the logging service
- FortiClient endpoint management
	- Endpoints connect to this location to retrieve configuration and validate licenses.

When you access the FortiSASE portal for the first time, you need to select the location of the data centers that suit the requirements of your organization. The FortiSASE POP location is used to route remote users to the POP that is geographically closest to them. 

The logging data center hosts the logging service. The FortiClient endpoint management retrieves configuration information and validates FortiClient endpoint licenses. You can purchase additional POPs as part of the network add-on licenses. 

During initial provisioning, you can select fewer security sites than the maximum you are entitled to. In this case, upon each login, the FortiSASE portal prompts you to select up to the maximum number of security sites. For more details about POP locations, see the FortiSASE Administration Guide.

## IAM User

IAM is a service to help you control access to FortiCloud portals and assets. You can use the portal to manage users, authentication credentials, and asset permissions. You can create permission profiles to assign users permissions to specific features, instead off assigning access to the entire portal. To access the IAM portal, visithttps://support.fortinet. com, and then click Services > ASSETS & ACCOUNTS > IAM. IAM users can access FortiSASE through https://portal.prod.fortisase. com, click SSO Login, and then click AM Login.

### MSSP Workflow

So, the first question is, why multi-tenancy? The primary use case is to manage multiple organizations from a single management console. For example, using multi-
tenancy, a managed security service provider (MSSP) requires logins to only one console to manage multiple organizations efficiently and effectively. The MSSP portal requires configuring an lAM user
corresponding to the root account and a FortiCloud premium subscription. A FortiCloud premium subscription to the root account allows the portal to establish an organization and invite other FortiCare
accounts to join that organization. FortiSASE includes an MSSP portal that supports centralized management and configuration capabilities, enabling the MSSP to deploy and manage SASE services across their client base This slide shows the flow of events to activate the

FortiSASE MSSP portal:
1. Enable organizations on FortiCloud using the root account with a FortiCloud premium subscription.
2. Invite FortiCloud accounts to join organizational units (OUs).
3. Use the FortiCloud IAM portal to create and assign role-based access control (RBAC) to IAM users.
4. Deploy a FortiSASE instance.
5. Log in to the FortiSASE portal after validating the lAM user correspondina to the root account. After logging-in, the IAM user can monitor and manage a tenants FortiSASE instance.

### MSSP Portal

Once logged into the FortiSASE MSSP portal, the MSSP administrator can monitor the tenant data including user licenses, security POPs, and so on. You can manage the FortiSASE instance in two ways to get access to the primary dashboard of the desired tenant:

1. Select the tenant, and then, in the Active Licenses
window, click Manage.

2. In the upper-right corner, in the context switch field,
select the organization or suborganization.

## FortiFlex Offering

- FortiFlex Offering
	- Consumption model that offers on-demand user and pay-per-usage charging through BYOL licensing.
- FortiSASE can be deployed the following ways
	- Enterprise subscription: prepaid service
	- MSSP subscription: postpaid service

The FortiFlex program enable organizations to avoid procurement delays, eliminate legacy license management constraints, and benefit from a predictable OpEx model. It is a new consumption model that brings
on-demand use and pay-per-usage charging through bring your own license (BYOL) licensing for virtual security instances, security services, and cloud-based management services.

FortiSASE can now also be deployed using the FortiFlex enterprise subscription, a prepaid service using FortiFlex enterprise points or FortiFlex MSSP subscription, a postpaid subscription service that requires monthly payment for usage in consumption credits. A FortiFlex VM sizing calculator is available on https ://fndn.fortinet.net/index.php?/tools/fortiflex/. This slide shows an example of points
consumed while deploying a FortiSASE instance with a standard service package and 100 users using the FortiFlex enterprise subscription.

For more information about the FortiFlex program refer, to the FortiFlex Ordering Guide.

## Licensing
- Understand FortiSASE license types
- Review Zero-Touvh provisioning using FortiZTP.

### User Based

FortiSASE offers user-based licenses and add-on licenses for edge devices, bandwidth add-on, dedicated public IP addresses, and SPA deployments. You can mix and match license types to suit the needs of your
organization. User-based licenses allow users to connect with multiple devices concurrently. You can use user-based licenses in agent-based or proxy-based mode. In proxy-based mode, FortiSASE provides FWaaS and acts as a SWG.

The features in proxy-based mode include URL filtering, anti-malware, DNS filtering, layer 3 to 7 firewalling, and an in-line CASB. To use agent-based mode, you must install FortiClient on the endpoint. Agent-based mode offers the same features as proxy-based mode, with the addition of endpoint protection with ZTNA. Each user can use up to three devices and a combination of agent-based and proxy-based modes.

- A minumum of 50 users is required
- License Tiers
	- Standard
	- Advanced
	- Comprehensive

FortiSASE offers three different license tiers. Standard license includes SIA, SSA, SPA, endpoint protection, SASE cloud management, REST API, SASE cloud logging, and Fortinet cloud hosted POPs. The advanced
license offers the same features as the standard license, as well as DEM, SOC-as-a-Service (SOCaaS) integration, dedicated IP addresses, and FortiGuard forensics service. The comprehensive license offers the
same features as the advanced license, but the POPs can be hosted on Fortinet cloud or public cloud locations. All license types have add-on features as well. For more details, contact the Fortinet sales team.

### SPA Users
- SPA service connection required for each member of FortiGate HA cluster.
- Enables connectivity to private applications for remote users and branch locations.
- License is required for FortiSASE to establish a dedicated tunnel to SD-WAN hub.

An SPA license allows remote users and branch locations to connect to private applications. If FortiGate is in a high availability (HA) cluster, you will need a separate license for each HA member. To establish a dedicated tunnel to FortiSASE, the FortiGate SD-WAN hub requires an SPA license. Remote users connected to FortiSASE can access private applications behind the FortiGate using this secure dedicated tunnel.

### Edge Devices

An edge device license enables customers to connect branch offices to FortiSASE. Edge device licenses are currently supported only on FortiExtender 200F, FortiAP 231F, FortiAP 431F, and all FortiGate F-series and G-series desktop platforms. Edge devices and FortiSASE should be registered under the same FortiCloud account. You can provision a FortiExtender or FortiAP to FortiSASE using FortiZTP.

## Provisioning FortiAP and FortiExtender Using FortiZTP

FortiZTP enables the deployment of Fortinet security, network, and wireless devices at remote locations where on-site provisioning technical expertise is limited. Remote devices can be assigned to a specific Fortinet management device or service. FortiZTP automatically loads devices that are registered to asset management with the same FortiCloud account on https://support.fortinet.com.

This slide shows the flow of events to deploy a

FortiExtender and FortiAP to your FortiSASE network using FortiZTP:
1.Connect the FortiAP and FortiExtender to your network provider.
2.Register the FortiExtender and FortiAP with FortiCloud asset management using your FortiCloud account. Apply the FortiSASE license to the devices.
3.Provision the devices using the FortiZTP portal.
4.Authorize the devices on the FortiSASE portal as edge devices.
You will learn about the configuration of connecting FortiExtender and FortiAP to FortiSASE in another lesson.

# Module 1 Completed.

