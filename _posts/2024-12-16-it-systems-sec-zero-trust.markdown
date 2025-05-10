---
layout: post
title: "IT Systems Security: The Rise of Zero Trust"
ref: itsecztrust
lang: en
date: 2024-12-16 11:45:00 -0400
categories:
  - IT Network
  - Network Design
  - IT Security
tags:
  - Network Design
  - IT Security
  - Network
  - Security
  - Design  
---
🔒*As cyber threats evolve and challenge traditional security zone approaches, discover how the Zero Trust model can transform your infrastructure and protect your sensitive data, even against the craftiest hackers.*<br/><br/>🕵️‍♂️*Also learn how the Zero Trust approach could have prevented Kevin's worst Honda Civic nightmare😅*

---
***Foreword**: This article, enhanced with AI-generated improvements ([Napkin](https://www.napkin.ia), [Microsoft Copilot](https://copilot.microsoft.com/)), is made available under the* <span xmlns:cc="http://creativecommons.org/ns#"><i><a href="https://creativecommons.org/licenses/by-nd/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-ND 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nd.svg?ref=chooser-v1" alt=""></a></i></span>

---
# Trust Levels and IT Risk Management
Inspired by military domains, the first iterations of security zone management rely on a clear and structured organization of flows. There are mainly three types of zones:

![Network security zones](/content/images/sec_zones_en.jpg){: style="display: block; margin: 0 auto;"}

## Trust Zones
These zones group everything with known and controlled origins, such as private user networks or internal servers.

## Untrust Zones
This category includes everything not under control, like the Internet, where risks are unpredictable.

## Demilitarized Zones (DMZ)
These zones host services that, although managed from a trust zone, must be accessible from untrust zones.

# Traffic Rules Between Trust Zones
Traffic flowing within the same zone encounters no restrictions. However, to ensure system security, communication between zones goes through strict controls, following these basic principles:

![Traffic rules between trust zones](/content/images/sec_zones_2_en.jpg){: style="display: block; margin: 0 auto;"}
- Traffic initiated from a trust zone to DMZs and untrust zones is allowed. However, traffic initiated outside the trust zone is systematically blocked to prevent compromise.
- The DMZ is by definition more exposed to risk, and therefore is accessible from both trust and untrust zones.

# Evolution of Cyber Threats

In a world where human and business interactions greatly depend on the digital realm, the robustness of network security controls is constantly challenged, undermining basic traffic flow principles.
In less than half a century, malicious individuals have armed themselves with various tools to elevate their threats to a higher level.

## Malware
Designed to infiltrate, damage, or disrupt computer systems. There are several types including:
- **Trojans**, malicious programs distributed as legitimate software to deceive users,
- **Viruses**, which attach to files and spread when the host file is opened/executed,
- **Worms**, which execute and propagate without user intervention,
- **Ransomware**, which once infiltrated into systems, encrypts all data to allow attackers to demand a ransom for decryption.

![Types of malware](/content/images/malware_types_en.jpg){: style="display: block; margin: 0 auto;"}

## Phishing
This technique involves deceiving users into disclosing sensitive information, such as passwords or credit card numbers, by impersonating trusted entities. The most common variants are:
- **Phishing**, via email, aimed at tricking users into clicking fraudulent links (fake websites, malware downloads, etc.)
- **Smishing**, the SMS variant of phishing,
- **Vishing**, by phone, aimed at tricking people into verbally revealing sensitive information.

![Common techniques leading to information disclosure](/content/images/phish_techs_en.jpg){: style="display: block; margin: 0 auto;"}

## Security Vulnerability Exploitation
Although brute force attacks are still present, they are becoming less effective as security systems evolve.

Instead, cybercriminals are turning to more sophisticated techniques to exploit system vulnerabilities. Security flaws can exist in software, operating systems, or even network configurations. Once a vulnerability is discovered, it can be exploited to execute malicious code, access sensitive data, or disrupt normal system operations. Targeted attacks, such as zero-day exploits, are particularly dangerous because they exploit vulnerabilities unknown to developers and users, leaving little time to react and patch the flaws.

![Understanding system vulnerabilities and cyber threats](/content/images/understand_vuln_en.jpg){: style="display: block; margin: 0 auto;"}

## Denial of Service Attacks
You know when the e-commerce site you're browsing shows a 503 error during Black Friday? That's a denial of service caused by traffic overload, because you're not alone in trying to get those deals ;-)

This undesirable side effect has inspired cyber villains, who have found ways to coordinate high-amplitude attacks to make entire services and networks inoperable by overwhelming them with useless requests.

![Denial of service attacks](/content/images/DDoS_en.jpg){: style="display: block; margin: 0 auto;"}

# Zero Trust Model: "You can't trust jack squat these days, for real..."
By examining the main attack vectors, it's become obvious that cyber threats seek to disrupt normal data flow patterns in a system. In other words, attackers try to manipulate or hijack normal data flows to access confidential information and compromise the security of the targeted system.

The concept of **Zero Trust Network Access** has emerged as an effective remedy to this de facto decompartmentalization.

## What's This Zero Trust Thing?

Unlike traditional security models based on trust perimeters, the Zero Trust model assumes that no entity, whether inside or outside the network, should automatically be trusted.

![Zero Trust Security Framework](/content/images/0trust_framework_en.jpg){: style="display: block; margin: 0 auto;"}

Zero Trust is based on several key principles:
- **Continuous verification**: Every attempt to access resources must be authenticated and authorized, regardless of the request's origin.
- **Least privilege**: Users and systems receive only the permissions necessary to perform their tasks, minimizing risks in case of compromise.
- **Micro-segmentation**: The network is divided into smaller, secure segments, limiting threat propagation in case of a breach.
- **Monitoring and analysis**: Constant monitoring and behavior analysis enable quick detection and response to suspicious activities.

## What Does It Take to Implement Zero Trust?
![Implementing a Zero Trust Strategy](/content/images/0trust_strat_en.jpg){: style="display: block; margin: 0 auto;"}

Implementing a Zero Trust strategy requires a comprehensive and integrated approach. Here are some essential steps to adopt this model:
1. **Asset and risk assessment**: Identify critical assets and evaluate risks associated with their access and use.
2. **Authentication enhancement**: Implement multi-factor authentication (MFA) mechanisms to strengthen identity verification.
3. **Access control**: Use attribute-based access control (ABAC) or role-based access control (RBAC) policies to manage permissions dynamically and contextually.
4. **Network segmentation**: Implement micro-segmentation to isolate different network parts and limit attackers' lateral movement.
5. **Continuous monitoring**: Deploy monitoring and analysis tools to detect anomalies and respond quickly to security incidents.

## Sounds Good, But What Are the Benefits?
![Benefits of implementing the Zero Trust model](/content/images/0trust_perks_en.jpg){: style="display: block; margin: 0 auto;"}

Well, yes :) It mainly provides the following advantages:
- **Reduced attack surface**: By limiting access and segmenting the network, there are fewer opportunities for hackers to find a breach.
- **Improved resilience**: Systems become more robust against attacks because potential breaches are contained and isolated.
- **Regulatory compliance**: Zero Trust helps comply with data protection and security laws and regulations.
- **Flexibility and adaptability**: The model adapts to new work environments, such as remote work or cloud infrastructures.

## Yeah, But Modernizing Is Expensive... What If I Keep Things As They Are?
Despite significant progress in mindsets over the past decade, I still sometimes hear "nothing has ever happened with the current system, and you're proposing top-notch stuff that's going to cost so much... Why should I transform anything?"

It's a bit like Kevin's story who, after saving for several years, just bought his dream car, but has no covered parking or garage to park it, and no budget for comprehensive insurance. He doesn't care, he lives in an uneventful suburb, nothing has ever happened. And there's the family dog, Spot, who's been watching over the house since Kevin learned to walk, it's chill!

Of course, as you might guess, quite a story unfolds:
- Thieves broke into the yard, took advantage while Spot was sleeping to loot and wreck the precious vehicle, leaving only a wreck good for scrap.
- Even worse, they stole Kevin's backpack that was inside, containing what Kevin cherished even more than his car: his Pokémon card collection!
- The very next day, the thieves contact our young friend to extort such an indecent ransom that he'll end up missing his only chance to ever see his mint condition shiny MewTwo again...

# Conclusion
*Kevin's story perfectly illustrates why modernizing IT system security is crucial, even if it might seem costly and unnecessary at first glance. Here's what we can learn from it.*

Kevin thought his quiet neighborhood and faithful dog were enough to protect his precious car and Pokémon card collection. But when thieves struck, he lost much more than what he had saved for years. Only after this painful experience did he understand the importance of investing in robust security measures, like a secure garage and surveillance system.

Similarly, companies might think their current systems are sufficient because they've never been attacked. But cyber threats constantly evolve, and what was safe yesterday isn't safe today. **Waiting for an attack to happen before acting can cost much more than modernizing security now**. By investing in advanced security solutions like Zero Trust, companies can prevent catastrophic losses and protect their most precious assets, just as Kevin finally protected his new car and Pokémon card collection.

![Investing in security prevents losses](/content/images/0trust_invest_en.jpg){: style="display: block; margin: 0 auto;"}