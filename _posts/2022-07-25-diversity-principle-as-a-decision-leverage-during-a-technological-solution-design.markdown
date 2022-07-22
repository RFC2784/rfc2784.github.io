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
# Why talking about diversity in such context ? #
If you live in Canada, or aware of IT newsfeeds, you certainly heard about the major outage Rogers Telecommunication faced on early July 2022.
At the early stages of this event, I was puzzle that such outage led to service interruption for critical application such Interac payment platform or a bunch of Canadian government services web portals.

To be honest, I can't imagine that related decision makers did not apply fully the diversity principle at the stage of solution designs.

# What do I mean about diversity principle ? #
Among all lessons learned as a problem solver, then as a network solutions designer, one of the most significant is **not to underestimate the importance to apply diversity as a balance factor between redundancy and security on an technological solution design** :

- The more bigger the underlying business organization is, the most diverse the solution must be,
- It must prevail in each decision taken to ideate and initiate an integration project.


# Diversity principle by the exemple : Interac network connectivity #

*As stated earlier, Interac payment platform was impacted by what I will call from now the "Rogers Outage". It was already well known that Interac have chosen Rogers as its main service provider for its operation systems main hosting facilities and network connectivity supplier. So let's review together how this company applied the diversity principle onto its network design !*

## Good example : my findings about Interac platform Internet transit connectivity ##

Such an organization run its proper Internet Autonomous System to manage public IPv4 prefixes (AS399405 held under ARIN). So it's quite easy to retrieve some useful info regarding the rcorresponding route objects and peering partners.

## Bad example : my assumptions about the remaining items of Interac platform network solution desigm ##
## Possible remediation plan by applying diversity principle on such context ##
