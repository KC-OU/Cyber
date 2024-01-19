## Incident Handling Definition & Scope

Incident handling (IH) has become an important part of an organization's defensive capability against cybercrime. While protective measures are constantly being implemented to prevent or lower the amount of security incidents, an incident handling capability is undeniably a necessity for any organization that cannot afford a compromise of its data confidentiality, integrity, or availability. Some organizations choose to implement this capability in-house, while others rely on third-party providers to support them, continuously or when needed. Before we dive into the world of security incidents, let's define some terms and establish a common understanding of them.

An `event` is an action occurring in a system or network. Examples of events are:

- A user sending an email
- A mouse click
- A firewall allowing a connection request

An `incident` is an event with a negative consequence. One example of an incident is a system crash. Another example is unauthorized access to sensitive data. Incidents can also occur due to natural disasters, power failures, etc.

There is no single definition for what an IT security incident is, and therefore it varies between organizations. We define an IT security incident as an event with a clear intent to cause harm that is performed against a computer system. Examples of incidents are:

- Data theft
- Funds theft
- Unauthorized access to data
- Installation and usage of malware and remote access tools

`Incident handling is a clearly defined set of procedures to manage and respond to security incidents in a computer or network environment.`

It is important to note that incident handling is not limited to intrusion incidents alone.

Other types of incidents, such as those caused by malicious insiders, availability issues, and loss of intellectual property, also fall within the scope of incident handling. A comprehensive incident handling plan should address various types of incidents and provide appropriate measures to identify, contain, eradicate, and recover from them to restore normal business operations as quickly and efficiently as possible.

Bear in mind that it may not be immediately clear that an event is an incident, until an initial investigation is performed. With that being said, there are some suspicious events that should be treated as incidents unless proven otherwise.

---

## Incident Handling's Value & Generic Notes

IT security incidents frequently involve the compromise of personal and business data, and it is therefore crucial to respond quickly and effectively. In some incidents, the impact may be limited to a few devices, while in others a large part of the environment can be compromised. A great benefit of having an incident handling team (often referred to as an incident response team) handle events is that a trained workforce will respond systematically, and therefore appropriate actions will be taken. In fact, the objective of such teams is to minimize the theft of information or the disruption of services that the incident is causing. This is achieved by performing investigations and remediation steps, which we will discuss more in depth shortly. Overall, the decisions that are taken before, during, and after an incident will affect its impact.

Because different incidents will have different impacts on the organization, we need to understand the importance of prioritization. Incidents with greater severity will require immediate attention and resources to be allocated for them, while others rated lower may also require an initial investigation to understand whether it is in fact an IT security incident that we are dealing with.

The incident handling team is led by an incident manager. This role is often assigned to a SOC manager, CISO/CIO, or third-party (trusted) vendor, and this person usually has the ability to direct other business units as well. The incident manager must be able to obtain information or have the mandate to require any employee in the organization to perform an activity in a timely manner, if necessary. The incident manager is the single point of communication who tracks the activities taken during the investigation and their status of completion.

One of the most widely used resources on incident handling is [NIST's Computer Security Incident Handling Guide](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf). The document aims to assist organizations in mitigating the risks from computer security incidents by providing practical guidelines on responding to incidents effectively and efficiently


# Cyber Kill Chain

## What Is The Cyber Kill Chain?

Before we start talking about handling incidents, we need to understand the attack lifecycle (a.k.a. the cyber kill chain). This lifecycle describes how attacks manifest themselves. Understanding this lifecycle will provide us with valuable insights on how far in the network an attacker is and what they may have access to during the investigation phase of an incident.

The cyber kill chain consists of seven (7) different stages, as depicted in the image below: 

![Cyber Kill Chain](https://academy.hackthebox.com/storage/modules/148/Cyber_kill_chain.png)

The `recon` stage is the initial stage, and it involves the part where an attacker chooses their target. Additionally, the attacker then performs information gathering to become more familiar with the target and gathers as much useful data as possible, which can be used in not only this stage but also in other stages of this chain. Some attackers prefer to perform passive information gathering from web sources such as LinkedIn and Instagram but also from documentation on the target organization's web pages. Job ads and company partners often reveal information about the technology utilized in the target organization. They can provide extremely specific information about antivirus tools, operating systems, and networking technologies. Other attackers go a step further; they start 'poking' and actively scan external web applications and IP addresses that belong to the target organization.

In the `weaponize` stage, the malware to be used for initial access is developed and embedded into some type of exploit or deliverable payload. This malware is crafted to be extremely lightweight and undetectable by the antivirus and detection tools. It is likely that the attacker has gathered information to identify the present antivirus or EDR technology in the target organization. On a large scale, the sole purpose of this initial stager is to provide remote access to a compromised machine in the target environment, which also has the capability to persist through machine reboots and the ability to deploy additional tools and functionality on demand.

In the `delivery` stage, the exploit or payload is delivered to the victim(s). Traditional approaches are phishing emails that either contain a malicious attachment or a link to a web page. The web page can be twofold: either containing an exploit or hosting the malicious payload to avoid sending it through email scanning tools. In all fairness, the web page can also mimic a legit website used by the target organization in an attempt to trick the victim into entering their credentials and collect them. Some attackers call the victim on the phone with a social engineering pretext in an attempt to convince the victim to run the payload. The payload in these trust-gaining cases is hosted on an attacker-controlled web site that mimics a well-known web site to the victim (e.g., a copy of the target organization's website). It is extremely rare to deliver a payload that requires the victim to do more than double-click an executable file or a script (in Windows environments, this can be .bat, .cmd, .vbs, .js, .hta and other formats). Finally, there are cases where physical interaction is utilized to deliver the payload via USB tokens and similar storage tools, that are purposely left around.

The `exploitation` stage is the moment when an exploit or a delivered payload is triggered. During the exploitation stage of the cyber kill chain, the attacker typically attempts to execute code on the target system in order to gain access or control.

In the `installation` stage, the initial stager is executed and is running on the compromised machine. As already discussed, the installation stage can be carried out in various ways, depending on the attacker's goals and the nature of the compromise. Some common techniques used in the installation stage include:

- **Droppers**: Attackers may use droppers to deliver malware onto the target system. A dropper is a small piece of code that is designed to install malware on the system and execute it. The dropper may be delivered through various means, such as email attachments, malicious websites, or social engineering tactics.
    
- **Backdoors**: A backdoor is a type of malware that is designed to provide the attacker with ongoing access to the compromised system. The backdoor may be installed by the attacker during the exploitation stage or delivered through a dropper. Once installed, the backdoor can be used to execute further attacks or steal data from the compromised system.
    
- **Rootkits**: A rootkit is a type of malware that is designed to hide its presence on a compromised system. Rootkits are often used in the installation stage to evade detection by antivirus software and other security tools. The rootkit may be installed by the attacker during the exploitation stage or delivered through a dropper.
    

In the `command and control` stage, the attacker establishes a remote access capability to the compromised machine. As discussed, it is not uncommon to use a modular initial stager that loads additional scripts 'on-the-fly'. However, advanced groups will utilize separate tools in order to ensure that multiple variants of their malware live in a compromised network, and if one of them gets discovered and contained, they still have the means to return to the environment.

The final stage of the chain is the `action` or objective of the attack. The objective of each attack can vary. Some adversaries may go after exfiltrating confidential data, while others may want to obtain the highest level of access possible within a network to deploy ransomware. Ransomware is a type of malware that will render all data stored on endpoint devices and servers unusable or inaccessible unless a ransom is paid within a limited timeframe (not recommended).

It is important to understand that adversaries won't operate in a linear manner (like the cyber kill chain shows). Some previous cyber kill chain stages will be repeated over and over again. If we take, for example, the `installation` stage of a successful compromise, the logical next step for an adversary going forward is to initiate the `recon` stage again to identify additional targets and find vulnerabilities to exploit, so that he moves deeper into the network and eventually achieves the attack's objective(s).

Our objective is to `stop an attacker from progressing further up the kill chain`, ideally in one of the earliest stages.