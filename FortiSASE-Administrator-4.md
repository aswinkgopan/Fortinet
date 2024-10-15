## Security and Endpoint Profiles

`Configuration > Traffic > Security > Profiles`

You can create security profile groups on the Security page.

Security profile groups allow you to group different security profile settings. You can then configure the profile group as part of a policy. You can customize and enable or disable security profiles within the security group. You can create separate security profile groups for different policies, depending on the requirements your organization. 

FortiSASE has a preconfigured default profile that you can't delete.

The following security profiles are available in a security profile group:
- SSL Inspection
- Antivirus
- Web Filtering With Inline-CASB
- File Filter
- Intrusion Prevention
- Data Loss Prevention
- DNS Filter
- Application Control With Inline-CASB

You will learn about some of the security profiles in this lesson.

### SSL Inspection

When you use certificate inspection, FortiSASE inspects only the header information of the packets. You use certificate inspection to verify the identity of web servers. You can also use it to make sure that the HTTPS protocol isn't used as a workaround to access sites you have blocked using web filtering.

Certificate inspection offers some level of security, but it does not allow FortiSASE to inspect the flow of encrypted data between the outside server and the internal client.

### SSL Deep Inspection

- SSL deep inspection requires that FortiSASE act as certificate authority (CA) to generate an SSL private key and certificate as a proxy web server
- FortiSASE devices that support full SSL inspection can get their CA certificate from a couple of sources:
	- A self-signed Fortinet_CA_ SSL certificate from within FortiSASE
	- A certificate issued by an internal CA (FortiSASE then acts as a subordinate CA)
- The root CA certificate must be imported into the client machines
- Deep inspection is required to decrypt and inspect content in encrypted traffic for these FortiSASE features:
	- Split DNS
	- Antivirus
	- Web filtering with inline CASB
	- File filter
    - Data loss prevention
	- Application control with inline CASB

FortiSASE performs web proxy and must act as a CA in order for it to perform SSL deep inspection. The internal CA must generate an SSL private key and certificate each time an internal user connects to an external SSL server. The key pair and certificate are generated immediately so the user connection with the web server is not delayed.

Although it appears as though the user browser is connected to the web server, the browser is connected to FortiSASE. FortiSASE is acting as a proxy web server. In order for FortiSASE to act in these roles, its CA certificate must have the basic constraints extension set to `cA=True` and the value of the keyUsage extension set to `keyCertSign`.

The `cA=True` value identifies the certificate as a CA certificate. The `keyUsage=keyCertSign` value indicates that the private key corresponding to the certificate is permitted to sign certificates. For more information, see `FC 5280 Section 4.2.1.9 Basic Constraints`.

All FortiSASE devices that support SSL deep inspection can use the self-signed Fortinet CA SSL certificate that is provided with FortiSASE, or an internal CA, to issue FortiSASE a CA certificate. When FortiSASE uses an internal CA. FortiSASE acts as a subordinate CA. Note that your client machines and devices must import the root CA certificate in order to trust FortiSASE and accept an SSL session.

### Configure SSL Inspection

`Security > profiles > SSL Inspection`

You can configure SSL inspection on the Security page by selecting the appropriate security profile group. You can click Customize in the SSL inspection profile and then select Certificate Inspection to enable certificate inspection. To enable deep inspection, select Deep Inspection, and then select the CA certificate to perform SSL deep inspection.

You can upload your own CA certificate to use with SSL deep inspection on the System > Certificates page. FortiSASE can detect certificates that are invalid for the following reasons:

- Expired: The certificate is expired.
- Revoked: The certificate has been revoked based on CRL or OCSP information.
- Validation timeout: The certificate could not be validated because of a communication timeout.
- Validation failed: The certificate could not be validated because of a communication error.

When a certificate fails for any of the reasons above, you can configure any of the following actions:

- Allow: FortiSASE allows the website and takes the certificate as trusted.
- Block: FortiSASE blocks the content of the site.

Within the deep inspection profile, you can also specify which FortiGuard categories or hosts, if any, you want to exempt from SSL inspection. You may need to exempt traffic from SSL inspection if it is causing problems with traffic, or for legal reasons.

### Web Filter - FortiGuard Category Filter

`Security > Profies > Web Filter with Inline-CASB`

- FortiGuard category filter
	- Provides categories from the FortiGuard Web Filter service that you can use to filter web traffic
	- Split into multiple categories and subcategories

You can configure the Web Filter With Inline-CASB profile on the Security page by selecting the appropriate security profile group. Rather than blocking or allowing websites individually, FortiGuard category filtering reviews the category that a website has been rated with. 
Then, FortiSASE takes action based on that category, not based on the URL. In addition, by default, FortiSASE blocks web pages that return a rating error. You can change this behavior by enabling Allow websites when a rating error occurs.

You can enable the FortiGuard category filtering on the web filter. Categories and subcategories are listed, and you can customize the actions to perform individually. The following actions are available:

- Allow: passes the traffic to the remaining web filters, antivirus inspection engine, and DLP inspection engine. If the URL does not appear in the URL list, FortiSASE allows the traffic.
- Monitor: processes the traffic the same way as the allow action. For the monitor action, FortiSASE generates a log message each time it establishes a matching traffic pattern.
- Block: denies or blocks attempts to access any URL that belongs to the category. A replacement message is displayed.
- Warning: displays a message to the user allowing them to continue if they choose.

### Web Filter - URL Filter

Static URL filtering is another web filter feature. FortiSASE checks configured URLs in the URL filter against the visited websites. If FortiSASE finds a match, it takes the configured action. URL filtering has the following pattern matches: simple, regular expressions, and wildcard.

The following actions are available:

- Allow: passes the traffic to the remaining web filters, antivirus inspection engine, and DLP inspection engine. If the URL does not appear in the URL list. FortiSASE allows the traffic.
- Block: denies or blocks attempts to access any URL that matches the URL pattern. A replacement message displays.
- Exempt: allows the traffic to pass through, bypassing other web filters, the antivirus inspection engine, and the LP inspection engine.
- Monitor: processes the traffic the same way as the allow action. For the monitor action, FortiSASE generates a log message each time it establishes a matching traffic pattern.

### Web Filter - Content Filtering

- Requires FortiSASE to use SSL deep inspection
- Controls access to web pages containing specific patterns
- Scans the content of every website accepted by security policies
- Matches content from wildcards or Perl regular expressions Actions:
	- Exempt
	- Block

You can also control web content in the web filter profile by blocking access to websites containing specific words or patterns. This helps to prevent access to sites with questionable material.

You can add words, phrases, patterns, wildcards, and Perl regular expressions to match content on websites. You configure this feature at the web filter level, not at the global level. So, it is possible to add multiple web content filter lists and then select the best list for each web filter profile.


### Web Filter - Custom Category

If you want to make an exception, for example, rather than unblock access to a potentially unwanted category, change the website to an allowed category. You can also do the reverse. You can block a website that belongs to an allowed category.

Remember that changing categories does not automatically result in a different action for the website. This depends on the settings within the web filter profile. In the example shown on this slide, the URL www.lotteryusa.com belongs to the FortiGuard category Gambling. The URL www.lotteryusa.com is added to the custom category Gambling custom to make an exception. The action for the FortiGuard Gambling category in the Web Filter With Inline-CASB profile is Block. When a user browses to www.lotteryusa.com, the custom category action takes precedence over the FortiGuard category, so access to www.lotteryusa.com is allowed.

### Web Filter - Inline CASB Headers

The FortiSASE web filter inline cloud access security broker (CASB) component can be used to customize HTTP headers when agentless (proxy) or agent-based (FortiClient) remote users are accessing Software-as-a-Service(SaaS) applications. Customizing HTTP headers requires SSL deep inspection enabled on the security profile group. FortiSASE can intercept HTTP headers to add or remove header requests/responses, as required by the SaaS application. You must know the format and content of vendor-specific headers supported by a SaaS application to use this feature. 

FortiSASE intercepts HTTP headers and can modify them for outgoing traffic as follows:

- Add to request
- Add to response
- Remove from request
- Remove from response

The example on this slide shows how to restrict access to personal accounts using the login.live.com domain. You can restrict access to personal accounts by adding a request to the HTTP header with the vendor header name and header content. You can find the format and content of vendor-specific headers on the vendor's website. You can locate the headers used this in example, at https:// learn.microsoft.com/en-us/azure/active-directory/manage-apps/tenant-restrictions. You will also need to apply SSL deep inspection to the security profile group, and then apply the security profile group to the applicable policy. When the end user tries to access login.live.com, their access will be blocked with a Microsoft error page.


## DNS Filter

The filter includes various configuration settings. You can enable or disable the FortiGuard category-based filter and the static domain filter. You also have the option to:

- Redirect botnet command-and-control requests to block portal
- Allow DNS requests when a rating error occurs from the FortiGuard service
- Redirect blocked requests to FortiGuard portal

Using the DNS Translation feature, you can translate a DNS-resolved IP address to another IP address you specify. 

DNS filtering supports the following actions:

- Allow
- Monitor
- Redirect to block portal

DNS filtering is not supported in SWG deployments.

### Configure Application Control With Inline-CASB

FortiSASE can recognize network traffic generated by a large number of applications. Network traffic is analyzed to detect application traffic, even if the traffic uses nonstandard ports or protocols.

You can configure the Application Control With Inline-CASB profile on the Security page, by selecting the appropriate security group. You can configure actions based on categories and application overrides. The Unknown Applications setting matches traffic that can't be matched to any application control signature and identifies the traffic as unknown application in the logs. The number listed beside the cloud symbol indicates the number of cloud applications in the category.

FortiSASE scans packets for matches, in this order, for the application control profile:

- Application overrides: If you have configured any application, the application control profile considers those first. It looks for a matching override starting at the top of the list.

- Categories: Finally, the application control profile applies the action that you've configured for applications in your selected categories.

### Configure AntiVirus

FortiSASE antivirus delivers automated updates that protect against the latest polymorphic attacks, viruses, spyware, and other content-level threats. Based on the patented content pattern recognition language (CPRL), the anti-malware engine is designed to prevent known and previously unknown malware variants. You can customize which protocol needs to be inspected using antivirus for secure internet access. You can configure an antivirus profile on the Security page, by selecting the appropriate security profile group. For antivirus scanning, the block replacement page is displayed immediately when a virus is detected.

Some of the inspected protocols are - HTTP, SMTP, POP3, IMAP, FTP, CIFS

### DLP

The FortiSASE LP system allows you to prevent sensitive data from leaving your network. When you define sensitive data patterns, data matching these patterns will be blocked, or logged and allowed, when passing through the FortiSASE. You configure the DLP system by creating individual filters based on file type, file size, a regular expression, an advanced rule, or a compound rule in a DLP sensor.

The DLP system is configured based on the following components:

- Data Source Type: LP supports predefined types such as sensors, Microsoft Purview Information Protection (MPIP) label, or none.

	- Sensors: A DLP sensor is a package of filters. Each DLP sensor has one or more filters configured within it. Filters can examine traffic for known files using DLP fingerprints, for files of a particular type or name, for files larger than a specified size, for data matching specified regular expressions, and so on.
	- MPIP Label: You can employ labels as markers for sensitive information. Microsoft provides sensitivity labels, which act as identifiers emphasizing the importance of the data that they are associated with, thereby enhancing the secunty measures in place. 
	- None: LP matches using only file or message type and protocol as criteria.

- Allow: FortiSASE takes no action, even if the patterns specified in the filter are matched.

- Monitor: FortiSASE takes no action on network traffic matching a rule with this action. The filter match is logged. 

- Block: Traffic matching a filter with the block action will not be delivered. The matching message or download is replaced with the data leak prevention replacement message.

### IPS

You can configure IPS sensors on the Security > Profiles page. FortiSASE uses signature-based detection and the FortiGuard extended IPS database to identify malicious activity.

You can select one of the predefined profiles while configuring the IPS sensors: 

- Recommended: scans traffic for all known threats and applies the recommended action.
- Critical: scans traffic for critical threats and blocks them.
- Monitor: scans traffic for threats but does not apply any action. Primarily used for logging.	

For more information on the IPS profiles refer to the FortiSASE Administration Guide. You can create a signature that identifies a certain packet
type, and then add the signature to an IPS sensor. All signatures include a type header (F-SBID) and a series of option/value pairs. You use the option/value pairs to uniquely identify a packet. 

The following options are supported in custom IPS signatures:

- Protocol: options to inspect IP/ICMP/UDP/TCP protocol headers for the value paired with the option.
- Payload: options to inspect the packet payload for the value paired with the option.
- Special: options to inspect other aspects (such as application control) of the packet for the value paired with the option.
- Application options: options to inspect other aspects unique to application control for the value paired with the option.


## Endpoint Profiles

- Understand Endpoint Profiles
- Provision and maintain endpoint profiles

### Endpoint Profiles

- You can configure FortiClient software using endpoint profiles
- Endpoint profiles have the following features
	- Connection
	- Protection
	- Sandboxa
	- ZTNA
	- Settings
- Endpoint profiles do not apply to security web gateway(SWG) mode deployment

You can configure the endpoint profile on the Profile page. Endpoint profiles define the configuration of FortiClient software on endpoints. You can enable features like antivirus, anti-ransomware, vulnerability scans, sandbox detection, ZTNA connection rules, and so on using this profile. When you provision FortiSASE, a default endpoint profile is created. 

By default, this profile is applied to the endpoints if there are no additional custom profiles created. The default profile of the feature is designed to provide effective levels of protection. Endpoint profiles have different features, as this slide shows. SWG mode is an agentless solution and endpoint profiles do not apply to SWG deployment.

### On-Fabric Rule Sets

`Configure > Endpoints > On-Fabric Rule Sets`

- FortiSASE uses rules to determine is on-fabric or off-fabric based on the telemetry data recieved.
- FortiSASE connection can be bypased on FortiClient fabric status
- Allows greated control and visibility of endpoints

You can configure on-fabric detection rules for endpoints.

FortiSASE uses the rules to determine if the endpoint is on fabric or off fabric. A rule set is available for on-fabric detection. If you configure rules of multiple detection types for a rule set, the endpoint must satisfy all configured rules to satisfy the entire rule set.

### Connection

In the endpoint profile, you can configure FortiClient to automatically connect to the FortiSASE SSL VPN when the user logs in to the endpoint, or give the user the ability to connect manually. You can also bypass the FortiSASE autoconnect on FortiClient based on the on-fabric rule set configured. If the endpoint is detected to be on-fabric based on the rule set, then FortiSASE can be bypassed for security inspection because an on-premises firewall like FortiGate
protects the internet access.

You can also configure split tunneling, where you can specify which traffic to exclude from the VPN tunnel and redirect to the endpoint physical interface bypassing FortiSASE.

- Connect to FortiSASE
	- On-device login
	- Automatically connect to FortiSASE SSL
- VPN when user logs in to the endpoint
	- Manually
	- Manually connect to the FortiSASE SSL VPN

### Connection ( Contd )

- Not available in default profile
- Custom VPN tunnels
	- IPsec tunnel
	- SSL VPN tunnel

You can configure a custom IPsec or SSL VPN configuration. These configurations are typically useful for use cases that require endpoints to connect to an on-premises FortiGate through a VPN.


