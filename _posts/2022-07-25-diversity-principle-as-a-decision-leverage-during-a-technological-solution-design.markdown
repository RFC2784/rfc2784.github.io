---
layout: post
title:  "Diversity principle as a decision leverage during a technological solution design"
date:   2022-07-25 12:00:00 -0500
categories:
  - IT Network
  - Network Design
tags:
  - Network Design
  - Network
  - Design  
---
<i><b>Disclaimer:</b> This post contains mainly high level concepts and reference information for a better understanding of the largest audience. It does not go into detail about the technical topics covered.</i>

# Why talking about diversity in such context ? #
If you live in Canada, or you aare aware of IT newsfeeds, you certainly heard about the major outage Rogers Communications faced July 8, 2022.
At the early stages of this event, I was puzzle that such outage led to service interruption for critical application such Interac payment platform or a bunch of Canadian government services web portals.

To be honest, I can't imagine that related decision makers did not apply fully the diversity principle at the stage of solution designs.

# What do I mean about diversity principle ? #
Among all lessons learned as a problem solver, then as a network solutions designer, one of the most significant is **not to underestimate the importance to apply diversity as a key factor for redundancy and security on an technological solution design** :

- The more bigger the underlying business organization is, the most diverse the solution must be,
- It must prevail in each decision taken to ideate and initiate an integration project.
- It can apply on several use case, such :
  - Several vendors for the same device type used on different scopes,
  - Several providers for the same kind of service that needs to be redundant,
  - Several paths to route a critical application flow,
  - Etc...

# Diversity principle by the exemple : Interac network connectivity #

*As stated earlier, Interac payment platform was impacted by what I will call from now the "Rogers Outage". It was already well known that Interac have chosen Rogers as its main service provider for its operation systems main hosting facilities and network connectivity supplier. So let's review together how this company applies the diversity principle onto its network design !*

## Good example : my findings about Interac platform Internet transit connectivity ##

Such an organization run its proper Internet Autonomous System to manage public IPv4 prefixes (AS399405 held under ARIN). So it's quite easy to retrieve some useful info regarding the corresponding route objects and peering partners :

<center><img src="/content/images/AS399405_info_20220722.jpg" width=400px alt="bgp.he.net AS399405 infos"><b><i>Source : https://bgp.he.net/AS399405#_asinfo</b></i></center><br><br>

- For sure, we can conclude that the diversity principle is correctly applied, as BGP peering is established with two different ISP for Internet transit :
  - Rogers Communications,
  - Beanfield Technologies.
- Route annoucement of the /23 IPv4 prefix owned by Interac captured the day of the Rogers Outage by a Twitter user proves that everything was fine from Beanfield peering :

<center><img src="/content/images/bgp-interac-tweet.jpg" width=400px alt="Twitter screenshot">
<span style="font-size: 8pt; font-weight: bold; font-style: italic;">Source : https://twitter.com/mattools/status/1545440711981645826</span></center><br>

- Interesting to note that Interac consider to have more than one Internet Transit provider post-COVID19 lockdown periods :)

## Bad example : my assumptions about the initial version of Interac platform network interconnectivity design ##

As stated by Rogers in its [response to the Request For Infomation from the Canadian Radio-television and Telecommunications Commission regarding the Rogers Outage](https://crtc.gc.ca/public/otf/2022/c12_202203868/4215445.docx) :
- "A specific coding was introduced in our Distribution Routers which triggered the failure of the Rogers IP core network" during a planned change.
- "The configuration change deleted a routing filter and allowed for all possible routes to the Internet to pass through the routers. As a result, the routers immediately began propagating abnormally high volumes of routes throughout the core network. Certain network routing equipment became flooded, exceeded their capacity levels and were then unable to route traffic, causing the common core network to stop processing traffic."
- "Since the outage was to Rogers’ core network, all of Rogers’ services by all our brands [...] were impacted."

As mentioned earlier, we know for sure that Internet Transit connectivity setup for Interac operational systems was probably still active through an alternate ISP despite the Rogers Outage.
<ins>So how can it be possible that a global Rogers outage still results to Interac payment unavailability</ins> ?

A possible explanation can be that the **private network interconnectivity between the different hosting locations for Interac operational systems was relying solely on Rogers Communication backbone**, as illustrated on the following diagram :

![Interac Network Interconnectivity Logical diagram accroding to assumptions](/content/images/interac-logical.png)

- Note that a full meshed private network based on Ethernet point-to-point connectivity can rely on a Service Provider backbone. In such case, the Service Provider propose the layer 2 connectivity across layer 3 in the middle, such Ethernet-over-MPLS.
- In that case, it could be possible that the Internet-facing part of a critical application is hosted on one site, but depends on back-end private services hosted on another location. By breaking the inter-location private connectivity, the application hence becomes unavailable...
- This scenario was kind of confirmed on [Interac Statement on Rogers Outage](https://www.interac.ca/en/content/news/interac-statement-on-rogers-outage/) :

   *"Each of our platforms, both Interac Debit and Interac e-Transfer, have redundant networks, including circuit diversity. These networks include 24/7 availability commitments from our suppliers, however the events of July 8th clearly revealed that these commitments could not be fulfilled. These redundant networks with circuit diversity should not have been so vulnerable to the Rogers core maintenance activity."*
   
**As a summary**
- Rogers provided the private network connectivity between Interac Operation systems locations, and were committed to provide redundacy by providing diversity between some private circuits. They certainly fullfilled this commitment by the garanty to diverse the physical path of two or more Ethernet-Over-MPLS circuits.
- Even if the circuits were not relying on the same Rogers Point of Presence, these latter are relying to the Rogers common core network to deliver the service.
- We can easily imagine that the PoP routers, by waterfall effect, were also surged by the massive route announcements that lead to Rogers core network outage, hence leading to Interac services interruption.

## Remediation plan : apply diversity principle for improvements ##
Still on the official statement mentionned above, Interac was remmediating this wekest link by "adding supplier diversity to strengthen our existing network redundancy", and by continuing "to work with our existing suppliers to strengthen commitments".
