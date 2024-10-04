
# Advanced Features and Authentication

1. Understand SOC-as-a-service ( SOCaaS)
2. Understand FortiGuard Forensic Analysis
3. Understand Digital experiemce Monitoring
4. Understand dedicated public IP address Functionality.

## Fortiguard Intergration with SOCaaS

- included with advanced and comprehensive license
- 24*7*365 monitoriing services enabled through global SOC locations.
- Powered by FortiGuard threat intelligence and SOAR platform.
- Investigations and incident triage led by dedicated Fortinet Security Experts
- To enable this service, on FortiSASE portal, click on Analytics > Logs > Settings and enable "Log Forwarding to SOCaaS"

Fortinet SOCaaS is a cloud-based managed security and 24x7x365 monitoring service. The global team of Fortinet experts
provides round-the-clock monitoring of your FortiGate and FortiSASE environments, offering vigilance beyond standard business
hours. Fortinet leverages artificial intelligence, machine language, and human analysis to sift through alerts, distinguishing
real threats from false positives. Upon detecting a threat, the Fortinet SOC team quickly notifies the customer, ensuring rapid
response to minimize attacker dwell times. 

The SOC team guides the customer through resolving these threats, working in
real time. SOCaaS is included with a FortiSASE advanced and comprehensive license. 

Integrating FortiSASE with SOCaaS helps IT and security teams ensure consistent security monitoring for on-premises and remote users. This integration allows for log forwarding to the SOCaaS portal, enabling effective monitoring and rapid response to detected network anomalies, therefore elevating network defense capabilities. You can enable this service on the FortiSASE portal. The cloud-based SOCaaS portal includes intuitive dashboards, on-demand reports, and quarterly Fortinet expert meetings.

## FortiGuard Forensic Analysis

- Included with advanced and Comprehensive Analysis
- Leverage FortiGuard forensics service to investigate potentially compromised endpoints.
- Submit endpoints for analysis directly from FortiSASE portal
- FortiGuard forensice teams will analyse and provide verdict and details report on findings.

Like SOCaaS, FortiGuard forensics analysis is included with FortiSASE advanced and comprehensive licenses. The FortiGuard forensics services helps customers identify and mitigate potential risks to their network. The FortiGuard forensics analysis helps endpoint customers respond to and recover from cyber incidents. For each engagement, FortiGuard forensics analysts remotely assists customer in the collection, examination, and presentation of digital evidence, including a final detailed report. A FortiSASE administrator can request a detailed analysis of the endpoint from the FortiGuard forensics team, if they observe a high-risk applications, malware, intrusion attempts, and so on, on that endpoint. 

FortiSASE subscriptions that include the forensics service, entitle customers to reach out to the forensics experts whenever an event happens. By doing so, they offload the issue from their internal teams, and accelerate the investigation by handing it off to analysts who are deeply familiar with the tools of endpoint security.

## DEM 

- Included with advanced and comprehensive licenses
- Granular visibility into the health and performance of major SaaS applications
- Efficiently troubleshoot user-to-application performance issues
- Monitor their real-time network bandwidth, CPU, memory, and hard disk usage
- DEM agent is packed along with the FortiClient installer and available to download as a single executable file from FortiSASE when users download FortiClient

Remote work presents a challenge when employees are spread out across a large area, use different ISPs, and have different
needs. Getting visibility from monitoring nodes located where employees or customers are physically located makes it easier to maintain service delivery for those workers. DEM serves as a valuable tool for network administrators in diagnosing connectivity and network issues for remote users, along with monitoring their real-time network bandwidth, CPU, memory, and hard disk usage. DEM offers quality and experience monitoring between the FortiClient endpoint, FortiSASE POP, and Software-as-a-Service (SaaS) application by tracing end-to-end network performance.

DEM functionality is included with FortiSASE advanced and comprehensive user licenses. The DEM agent is packaged along with the FortiClient installer and  available to download as a single executable file from FortiSASE when users download. You will learn to run a trace job on an endpoint in a later lesson.

## IP Address Assignment

- FortiSASE uses a shared IP environment if there are no dedicated IP addresses assigned
- Dedicated IP addresses can be purchased as an add-ons with a standard user license
- Four dedicated IP addresses are included with advanced and comprehensive licenses
- Additional IP addresses can be purchased
- Three use cases:
	- Traffic identification and isolation
	- Geolocation rules
	- Source IP anchoring

FortiSASE with a standard user license uses a shared IP environment, meaning remote users from different customers connected to a specific POP use the same public IP address for outgoing traffic. This prevents the identification and isolation of each customer's traffic. Customers can purchase dedicated IP addresses as an add-ons with a standard user license. There are four dedicated IP addresses included with an advanced and comprehensive licenses.

Three common use cases for dedicated public IP address deployments are: Traffic identification and isolation Geolocation rules
Source IP anchoring You must open a support ticket to implement geolocation rules and source IP anchoring use cases. This slide shows an
example of a shared IP environment, where remote users from different customers are connected to the same POP location. All of them use the same public IP address to connect to the internet.

### Traffic Identification and Isolation

- One dedicated IP address for each POP with a maximum of 4 POPs.
- Default geolocation of a POP is used.

If the customer has purchased an add-on license or has dedicated IP addresses as part of their license, they are entitled to one
dedicated IP address per POP, with a maximum of four POPs. The public IP address will be registered to the default geolocation of the POP.

In the example shown on this slide, users of customers A, B, and C are connected to the same FortiSASE POP location. Customer A
has a dedicated IP address in their FortiSASE user license. Customer A will get a dedicated public IP address for their user traffic, allowing for traffic isolation and identification.

### Geolocation Rules

- A public IP addres from a different geolocation is mapped to a POP, while traffic still transits through its actual geolocation.

In the geolocation rules use case, the customer can request the dedicated public IP address of a POP to be mapped to a different geolocation, while traffic still transits through its actual geolocation. In the example shown on this slide, customer A is connected to a POP in Toronto, Canada. The customer can request the dedicated public IP address of the POP to be mapped to New York, USA. This allows for users using a specific security POP to access content that is tailored to or restricted by users' geolocation. Mapping to a different geolocation is considered the best effort because cloud services use different geolocation providers and not all are consistent.

### Source IP anchoring

- Additional dedicated public IP add-on license is required with four additional dedicated IP addresses
- Additional four public IP addresses can all be used on one single POP, or one IP per POP, or a combination of the two
- Source IP anchoring policy can be used to SNAT a specific user, group, or country of incoming remote users

In the source IP anchoring use case, you will need an additional dedicated public IP add-on license with four additional dedicated IP addresses on top of the initial dedicated public IP address license. The additional four public IP addresses can all be used on one single POP, or one IP per POP, or a combination of the two. You can use source network address translation (SNAT) for a specific user, user group, or country of incoming remote users. In the example shown on this slide, users are part of company A and part of different
user groups. Traffic for the engineering group is source-anchored to a different dedicated IP address (2.2.2.2) based on the user group and source country, while the marketing group and finance group are using the same dedicated public IP address (1.1.1.1).

# Create Local Users

1. Understand endpoint MOde
2. Understand SWG mode
3. Configure Local Users
4. Configure the FortiClient agent
5. Configure the agentless proxy client

## Endpoint Mode

- Agent-based mode
- FortiClient connects to FortiSASE using an SSL VPN tunnel
- Firewall-as-a-Service (FWaaS) comes between the endpoint and the internet
- VPN policies on FortiSASE secure all internet traffic
- Per-endpoint (user-based) licensing is required

In endpoint mode, FortiClient connects to FortiSASE using a secure SSL VPN tunnel. Once the connection is established,
FortiSASE acts as a firewall and is placed between the endpoint and the internet. The VPN policy on FortiSASE is configured with the required security components, such as web filter, application control, and so on, to secure the internet traffic. Endpoint mode also supports configuring zero trust network access (ZTNA) for compliance checks.


This slide shows the flow of events that occurs during endpoint mode manual activation.

1.The FortiSASE administrator sends an invitation email to the remote user, as part of user onboarding.
2. The end user downloads FortiClient and connects to the FortiSASE Endpoint Management System (EMS) to activate the license, using the code in the email
3. Once the license is activated, a secure SSL VPN is established from FortiClient to the nearest FortiSASE POP, based on geolocation selection.
4. The FortiSASE administrator can apply security profiles on the VPN policies to secure internet traffic.
5. You can also provision using FortiClient installers that you can download from the FortiSASE portal. Click Configuration, and then, in the ACCESS section, click Users > Onboard Users > Download Installer. 

You can then provision your endpoints by doing one of the following:
- Use a mobile device management (MDM) software suite using this installer. 
- Distribute this installer to end users and have them install it on their endpoints

## SWG Mode

- Proxy-based mode
- Remote users set up a web browser or a PAC file to use the FortiSASE SWG service as an explicit web proxy
- Only HTTP and HTTPS traffic is redirected and inspected by the FortiSASE SWG policy
- All other non-web traffic bypasses FortiSASE and is forwarded directly to the internet

Secure web gateway mode is an agentless deployment for remote users. Remote users configure FortiSASE as an explicit web proxy through their web browser or by using a proxy autoconfiguration (PAC) file. IT administrators can push a PAC file to the end user by using a group policy object (GPO). 

FortiSASE supports a Google Chrome extension that allows you to enforce SWG connectivity for selected endpoints with the Google Chrome browser installed, including Chromebooks, based on the endpoint OS and the corresponding extension policy that the Google Workspace administrator configured. The web browser redirects HTTP and HTTPS traffic to FortiSASE, which secures user web traffic by implementing SWG security policies. All other non-web traffic bypasses FortiSASE andis forwarded directly to the internet.

## Configure Local Users

- User authenticates with FortiSASE directly
- FortiSASE sends instructions and invitation code to the configured email address
- User uses this invitation code to connect FortiClient to FortiSASE
- FortiSASE can import users from a CSV file

You can configure local users on FortiSASE. These users will directly authenticate with FortiSASE. To do this, click Configuration and then, in the ACCESS section, click Users & Groups. First, type an email address for FortiClient to send the invitation code to. The email address is also the username. The user uses the invitation code to connect FortiClient to FortiSASE. FortiSASE can also import users in bulk from a CSV file. Click Configuration, and then in the ACCESS section, click Users > Import/Export > Import Users.

As part of onboarding, FortiSASE sends the user an email instructing the user to activate their account. The user clicks Activate and then sets a password. The activation email also contains links to download FortiClient installers and an invitation code for FortiClient to connect to FortiSASE.

## Agent Configuration

To connect FortiClient to FortiSASE, the user types the invitation code from the activation email, in the ZERO TRUST TELEMETRY> Register with Zero Trust Fabric field, and click Connect.

After FortiClient has registered successfully, the VPN Name field displays Secure Internet Access. Now
the FortiSASE EMS manages the endpoint. The user can connect to the Secure Internet Access VPN tunnel by using the credentials set up during user activation or remote authentication, if configured. All user internet traffic is routed using FortiSASE VPN policies.

## Agentless Configuration

You can enable SWG on the SWG Configuration page.

When you enable SWG, users can configure their browser to proxy all HTTP and HTTPS web traffic for
the FortiSASE SWG policies to inspect. While the web traffic is being proxied, FortiSASE replaces and
signs the certificates of secure protocols like HTTPS. 

You should provide users with the required certificate
authority (CA) certificate and PAC file to connect to the FortiSASE gateway. You can download the SWG certificate and the PAC file from the SWG Configuration page.

The user can configure the SWG settings at the OS level or in a browser by using a PAC file or by
specifying the URL of the hosted PAC file, which is provided by FortiSASE. When the user starts a new web browser session, they are prompted to log in. The user can log in using the credentials that they set up during activation or any remote authentication, if configured.

# Configure Remote Authentication Servers

1. Describe Remote authentication with LDAP and RADIUS
2. Describe importing remote users
3. Describe SAML SSO.

FortiSASE provides support for many remote authentication servers, including RADIUS, LDAP, and
SAML for SSO. Unlike local user accounts, where FortiSASE knows the credentials, remote authentication servers verily user credentials and provide group membership information to FortiSASE on demand.

## Remote Authentication Server - LDAP

You can configure FortiSASE to connect to a remote LDAP server on the LDAP page. You must enter all required information about the remote LDAP server. such as the IP address (or FQDN) as well as the connecting port.

The Access Type setting is how the LDAP server can be accessed from FortiSASE.

- Public means the LDAP server is directly accessible on the internet.
- Private means the LDAP server is accessible through secure private access.

The Common Name Identifier setting is the attribute name you use to find the username.

The Distinguished Name setting identifies the top of the tree where the users are located, which is generally the domain controller (DC) value; however, it can be a specific container or organizational unit(OU).

The Bind Type setting depends on the security settings of the LDAP server. When selecting a bind type, which determines how the authentication  information is sent to the server, you can select:

1. Simple, to bind using the user's password, which is sent to the server in plaintext without a search.
2. Regular, to bind using the user's distinguished name (DN) and password and then perform a search. Regular bind is required, if searching for a user across multiple domains.
3. Anonymous, to bind using an anonymous user and search starting from the DN and recurse over the subtrees. Many LDAP servers do not allow this by default.

If you want to have a secure connection between FortiSASE and the remote LDAP server, enable Secure Connection and include the LDAP over SSL (LDAPS), as well as any trusted CA certificates.

### Importing Remote LDAP Users

You can import remote LDAP users on the Users page. You can either import users or import users by group membership. When you are configuring the user group on FortiSASE, select the LDAP server as the remote authentication server and select specific LDAP groups to add to your user group, as defined on the LDAP server. To enter the email addresses of the LDAP users to send the invitation emails to, click Configuration, and then in the ACCESS section, click Users > Onboard Users.


## Remote Authentication Server - RADIUS

You can configure FortiSASE to connect to a remote RADIUS server on the RADIUS page. You must enter all required information about the remote RADIUS server, such as the IP address, port, and shared secret. You also have the option to set up a secondary server for redundancy. You cannot import RADIUS users individually, but you can configure a user group on FortiSASE with RADIUS as the remote authentication server and add user groups based on
RADIUS attributes for group membership.

The Primary Server Secret setting is the secret that is set up on the RADIUS server in order to allow remote queries from this client. Note that FortiSASE must be listed on the RADIUS server as a client of that RADIUS server, or the server will not reply to FortiSASE queries. 

The Authentication Type setting refers to the authentication protocol that the RADIUS server supports. Options include Common-Handshake Authentication Protocol (CHAP), Password Authentication Protocol (PAP), Microsoft CHAP (MS-CHAP), and MSCHAP2.

The Include All Users option adds the RADIUS server and all users that can authenticate against it,
to every user group created on FortiSASE.

This slide shows an example of FortiAuthenticator as the RADIUS server and FortiSASE as the RADIUS client.

## SAML Roles

SAML defines a framework for exchanging security assertions between SAML entities. It uses an XML-
based framework and browser cookies to exchange security assertions between entities to achieve SSO.
One of the main SAML use cases is a multiple- domain web SSO. Online business partners can
exchange SAML assertions, to provide user access to multiple web services, without asking the user to
log in to each domain. At a minimum, you need the following SAML entities
to perform SSO:

Principal: requests access to a service that usually requires authentication and authorization
using the SAML model. A principal can be a user, group, or machine.

IdP: responsible for creating, maintaining, and managing identity information for principals. It is responsible for responding to requests for SAML assertions within a federation.

SP: provides a service to a principal. It relies on an IP for authentication and authorization information that it can use to provide access to a principal.

### Configuring SSO

You can enable SO authentication for FortiSASE endpoint users by configuring SAML. SSO authentication is supported for both SWG and VPN modes. When configuring FortiSASE as a SAML SP, you do not need to host the user database locally.

User authentication is performed by an IdP, and FortiSASE directs principals to the IP portal for authentication.

You can configure SO authentication on the VPN User SSO page for VPN users or SWG User SSO page for SWG users. The service provider fields are preconfigured and should be added to your IdP server. You must enter the IP configuration into FortiSASE to complete the SO configuration.

You can upload a certificate for use with SAML SSO authentication on the Certificates page under System.

Enabling SO authentication overrides any other previously created authentication methods (local database, LDAP, or RADIUS). Fortinet products, like FortiAuthenticator or FortiTrust Identity, can act as an Id for this configuration.

### Testing SSO Configuration

From FortiSASE, you can test the SSO configuration settings end-to-end by logging in to a user account
confiqured on your SSO server. This feature allows you to open a test window that points to the SSO
login page. This test provides SO configuration test results and raw log output of SAML debugs from the
security POP. 

This data can help you troubleshoot issues caused by any misconfigured SSO configuration settings. To perform this test, click Start Test on the VPN User SO page. The Start Test option is available only after you submit the SSO configuration.

### Configure User Groups

You can configure user groups on the Users page. You can add local users to the user group, or you
can add preconfigured remote servers to the group. User groups simplify your configuration, if you want
to treat specific users in the same way.