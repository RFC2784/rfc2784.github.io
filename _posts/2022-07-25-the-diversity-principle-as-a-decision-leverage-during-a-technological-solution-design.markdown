---
layout: post
title:  "The diversity principle as a decision leverage during a technological solution design"
date:   2022-07-25 14:00:00 -0400
categories:
  - IT Network
  - Network Design
tags:
  - Network Design
  - Network
  - Design  
---
***Disclaimer:** This post contains mainly high-level concepts and reference information for a better understanding of the largest audience. It does not go into details about the technical topics covered.*

# Why talk about diversity in such context? #
If you live in Canada, or you are aware of IT newsfeeds, you certainly heard about the major outage Rogers Communications faced July 8, 2022.
At the early stages of this event, I was puzzled that such an outage led to service interruption for critical applications such Interac payment platform or a bunch of Canadian government services web portals.

To be honest, I can't imagine that related decision-makers did not apply fully the diversity principle at the stage of solution design.

# What do I mean about the diversity principle? #
Among all lessons learned as a problem solver, then as a network solutions designer, one of the most significant is **not to underestimate the importance to apply diversity as a key factor for redundancy and security on a technological solution design** :

- The bigger the underlying business organization is, the most diverse the solution must be,
- It must prevail in each decision taken to ideate and initiate an integration project.
- It can apply to several use cases, such :
  - Several vendors for the same device type used on different scopes,
  - Several providers for the same kind of service needs to be redundant,
  - Several paths to route a critical application flow,
  - Etc...

# The diversity principle by example: Interac network connectivity #

*As stated earlier, Interac payment platform was impacted by what I will call from now the "Rogers Outage". It's already well known that Interac have chosen Rogers as its main service provider for its operation systems' network connectivity. So let's review together how this company applies the diversity principle onto its network design !*

## Good example : my findings about Interac platform Internet transit connectivity ##

Such an organization runs its proper Internet Autonomous System to manage public IPv4 prefixes (AS399405 held under ARIN). So it's quite easy to retrieve some useful info regarding the corresponding route objects and peering partners :

<img src="/content/images/AS399405_info_20220722.jpg" width=400px alt="bgp.he.net AS399405 infos"></center>
<center><b><i>Source: <a href="https://bgp.he.net/AS399405#_asinfo" target="_blank">https://bgp.he.net/AS399405#_asinfo</a></b></i><center><br><br>

- For sure, we can conclude that <ins>the diversity principle is correctly applied at Internet transit level</ins>, as <ins>BGP peering is established with two different ISPs</ins> :
  - Rogers Communications (AS812),
  - Beanfield Technologies (AS2199).
- Route announcement of the /23 IPv4 prefix owned by Interac captured the day of the Rogers Outage by a Twitter user proves that **everything was fine from Beanfield peering** :

<center><img src="/content/images/bgp-interac-tweet.jpg" width=400px alt="Twitter screenshot"></center>
<center><b><i>Source:  <a href="https://twitter.com/mattools/status/1545440711981645826" target="_blank">https://twitter.com/mattools/status/1545440711981645826</a></b></i><center><br><br>

- *Interesting to note that Interac considered having more than one Internet Transit provider post-COVID19 lockdowns periods :)*

## Bad example: my assumptions about the initial version of Interac platform network interconnectivity design ##

As stated by Rogers in its [response to the Request For Information from the Canadian Radio-television and Telecommunications Commission regarding the Rogers Outage](https://crtc.gc.ca/public/otf/2022/c12_202203868/4215445.docx) :
- "A specific coding was introduced in our Distribution Routers which triggered the failure of the Rogers IP core network" during a planned change.
- "The configuration change deleted a routing filter and allowed for all possible routes to the Internet to pass through the routers. As a result, the routers immediately began propagating abnormally high volumes of routes throughout the core network. <ins>Certain network routing equipment became flooded, <b>exceeded their capacity levels and were then unable to route traffic</b></ins>, causing the common core network to stop processing traffic."
- "Since the outage was to Rogers’ core network, **all of Rogers’ services by all our brands [...] were impacted**."

As mentioned earlier, we know for sure that Internet Transit connectivity setup for Interac operational systems was probably still active through an alternate ISP despite the Rogers Outage.
<ins>So how can it be possible that a global Rogers outage still results in Interac payment unavailability</ins>?

A possible explanation can be that the **private network interconnectivity between the different hosting locations for Interac operational systems was relying solely on Rogers Communication backbone**, as illustrated in the following diagram (based on my assumptions) :

![Interac Network Interconnectivity Logical diagram based on Geoffray REAU's assumptions](/content/images/interac-logical.png)

- Note that a full meshed private network based on Ethernet point-to-point connectivity can rely on a Service Provider's backbone. In such figure, the Service Provider proposes the layer 2 connectivity across layer 3 in the middle, such Ethernet-over-MPLS.
- Among several scenario, a plausible one invovles the Internet-facing component of a business-critical application:
  - it might be hosted at one site, but relies on back-end's private services hosted at another hosting facility.
  - By breaking the inter-sites' private connectivity, the application hence becomes unavailable...
- <ins>This scenario was kind of confirmed on </ins>[Interac Statement on Rogers Outage](https://www.interac.ca/en/content/news/interac-statement-on-rogers-outage/) :

   *"Each of our platforms, both Interac Debit and Interac e-Transfer, have <ins>redundant networks, <b>including circuit diversity</b></ins>. These networks include 24/7 availability commitments from our suppliers, however <ins>the events of July 8th clearly revealed that these commitments could not be fulfilled. <b>These redundant networks with circuit diversity should not have been so vulnerable to the Rogers core maintenance activity</b></ins>."*
   
**Facts and assumptions - Overview**
- Rogers Communications provided the private network connectivity between Interac's operational system sites and committed to providing redundancy by ensuring diversity between some private circuits. This service provider probably met this commitment by providing physical path diversity across two or more Ethernet-Over-MPLS circuits.
- Even if the circuits were not relying on the same Rogers' Points of Presence (PoP), these latter are probably relying on Rogers' common core network to deliver the service.
- We can easily imagine that the PoP routers, by a waterfall effect, were also surged by the massive route announcements that lead to Rogers core network outage, leading to Interac services interruption.

## Remediation plan: apply the principle of diversity for improvements ##
Still according to the official statement mentioned above, Interac indicated that remediation of this weakest link will be made by "adding supplier diversity to strengthen our existing network redundancy", and by continuing "to work with our existing suppliers to strengthen commitments" :
- We have here a confirmation that the principle of diversity must be applied at every layer of a technological solution design, and **can also be applied during its improvement**.
- Based on the connectivity suppliers we identified upper (Rogers and Beanfield), assuming that private network connectivity is relying on point-to-point Ethernet-Over-MPLS circuits fully provided by Rogers, a possible network design evolution is to divert one of those point-to-point circuits from Rogers to Beanfield, as illustrated by the diagram below:

![Interac Network Interconnectivity evolution Logical diagram based on Geoffray REAU's assumptions](/content/images/interac-logical-evolution.png)

# Call to discussion ! #
As you can see, this post reflects my own opinions and assumptions about this topic. I'm open to external points of view to elaborate !

So <b>don’t hesitate to reach me on the social medias (links on footer) and <ins>react to that post with your own thoughs and words</ins> !</b>
