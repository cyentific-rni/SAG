### Summary
This repository provides enhanced [STIX 2.1](https://oasis-open.github.io/cti-documentation/stix/intro.html) representations of the [MITRE ATT&CK Groups](https://attack.mitre.org/groups/) knowledge base, structurally extending the ones provided in the [Official MITRE GitHub Repository](https://github.com/mitre/cti/tree/master/enterprise-attack/intrusion-set). In particular, this project makes existing semi-structured information in the ATT&CK Groups knowledge base fully structured and programmatically accessible, allowing it to be queried upon and correlated with other sources and knowledge bases more easily. 

Additional information that is now structured includes:
* **the suspected country of origin of a group,**
* **targeted sectors and countries,** 
* **and their motivations.** 

---

### This project currently enhances the following versions:

| Version | Description |
| :--- | :--- |
| [Version 11.1](https://github.com/fovea-research/SAG/tree/ATT%26CKv11.1) | The version/commit that has been processed is [1c96a78cb5d7fc53ab18d0cd3686e8f690115943](https://github.com/mitre/cti/tree/1c96a78cb5d7fc53ab18d0cd3686e8f690115943/enterprise-attack/intrusion-set).|
| [Version 9.0](https://github.com/fovea-research/SAG/tree/ATT%26CKv9.0) | The version/commit that has been processed is [eb1b9385d44340ce867a77358c5f5aaed666e54c](https://github.com/mitre/cti/tree/eb1b9385d44340ce867a77358c5f5aaed666e54c/enterprise-attack/intrusion-set).|


---

**The following information has been fully structured and made available in the following way:**

* STIX relationship objects and domain objects indicating **the location (country) the groups/intrusion-sets appear to originate from.**

`
sdo:intrusion-set -> sro:originates-from -> sdo:location
`

* STIX relationship objects and domain objects indicating **the locations (countries and regions) the groups/intrusion-sets have been observed targeting.**

`
sdo:intrusion-set -> sro:targets -> sdo:location
`

* STIX relationship objects and domain objects indicating **the sectors (industries) the groups/intrusion-sets have been observed targeting** (using the `sectors` property in the `identity` object).

`
sdo:intrusion-set -> sro:targets -> sdo:identity
`

* new `intrusion-set` objects that additionally represent **the motivation factor of a group** (using the `primary_motivation` property in the `intrusion-set` object).

`
sdo:intrusion-set
`

---


The newly enriched intrusion-set (group) objects with the `primary_motivation` property populated relate to the existing MITRE-created `intrusion-set` objects via the `derived-from` relationship object.

<p align="center">
  <img src="/images/figure1.png" width="40%">
</p>

<br/>

The entity that created a STIX Object is an inherent, factual part of that object, and therefore that information is captured in an embedded relationship contained in the `created_by_ref` property.

---

### How do I operationalize this work and access the ATT&CK STIX representation?

The STIX objects available in the branches of this repository **complement** the ones found in the Official MITRE GitHub Repository; thus, the objects from both repositories should be utilized/imported. Check the correct versions and commits to operationalize as referenced in the table above.

In addition, to avoid duplicating objects, we utilized the [STIX location objects](https://github.com/oasis-open/cti-stix-common-objects/tree/main/objects/location) from the OASIS CTI TC [common objects repository](https://github.com/oasis-open/cti-stix-common-objects) to connect the intrusion sets/ATT&CK Groups with their possible origin and targeted countries/regions. Thus, those objects should be utilized/imported too. The location objects have been populated based on the ISO 3166-1 and the United Nations M49 standards.

**To make use of this project, the following objects need to be utilized/imported:**

1. The STIX Objects available in the branches of this repository (e.g., ATT&CKv11.1), and in particular, the objects from the folders' intrusion-set', 'relationship', 'identity', and 'location', or the file 'enterprise-attack-enrich.json' that unifies all the objects together.
2. The MITRE-generated STIX Objects available in their official repository, and in particular, the objects from the folder 'intrusion-set' within the 'enterprise-attack' folder, other object types available in the rest of the folders, or the MITRE-generated' enterprise-attack.json' file that unifies all the objects together.
3. The STIX Objects available in the folders [location](https://github.com/oasis-open/cti-stix-common-objects/tree/main/objects/location) of the OASIS CTI TC, or our generated 'oasis-cti-stix-common-objects-location.json' file available under each branch that unifies all the objects together.

The ATT&CK STIX representation is easily manipulated in Python using the stix2 library. However, because STIX 2.1 is represented in JSON, other programming languages can easily interact with the raw content [3]. Also, dedicated efforts that work with STIX can be used (e.g., the OpenCTI platform).

---

### The lists/taxonomies that have been used to enrich the STIX representation of ATT&CK Groups and can be used to perform queries and conduct analysis are:

* Countries based on ISO 3166-1:
  * ALPHA-2 Codes. Can be queried using the `country` property of the `location` object.
  * Country names. Can be queried using the `name` property of the `location` object.


* Geographic regions based on the United Nations M49 Standard and two additional, namely, `middle-east` and `south-china-sea`:
  *  Can be queried using the `region` property of the `location` object. The region list can also be found in the [STIX Specification Version 2.1 Committee Specification 02 - Region Vocabulary](https://docs.oasis-open.org/cti/stix/v2.1/cs02/stix-v2.1-cs02.html#_i1sw27qw1v0s).

* Motivations as presented in the [STIX Specification Version 2.1 Committee Specification 02 - Attack Motivation Vocabulary](https://docs.oasis-open.org/cti/stix/v2.1/cs02/stix-v2.1-cs02.html#_dmb1khqsn650).

* A sector/industry taxonomy as presented right below. **Note that the sector/industry taxonomy for cyber threat intelligence is a work in progress from the [OASIS Threat Actor Context Technical Committee (TAC)](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=tac)**. The specification perse will be referenced when it reaches OASIS's Committee Specification status/level.

  * aerospace
    * aviation
  * agriculture
  * automotive
  * biotechnology
  * chemical
  * commercial
    * retail
  * consulting
  * construction
  * cosmetics
  * critical-infrastructure
  * dams
  * defense
  * education
  * emergency-services
  * energy
    * non-renewable-energy
    * renewable-energy
  * media
  * financial
    * banking
  * food
  * gambling
  * government
    * local-government
    * national-government
    * regional-government
    * public-services
  * healthcare
    * hospital
  * information-communications-technology
    * electronics-hardware
    * software
    * telecommunications
  * legal-services
  * lodging
  * manufacturing
  * maritime
  * metals
  * mining
  * non-profit
    * humanitarian-aid
    * human-rights
  * nuclear
  * petroleum
  * pharmaceuticals
  * research
  * transportation
    * logistics-shipping
  * utilities
  * video-game
  * water


---

### Confidence level

The additional structured information provided in the feeds of this repository has been extracted from the descriptions of the MITRE ATT&CK Groups and should not be immediately considered of high confidence. The extraction has been performed programmatically using Natural Language Processing (NLP).

---

### Glossary

STIX: Structured Threat Information eXpression

ATT&CK: Adversarial Tactics, Techniques, and Common Knowledge

sdo: STIX Domain Object

sro: STIX Relationship Object

---

### References

[1] Slide deck regarding the idea/concept, presented at the 6th EU MITRE ATT&CK Workshop (October 23, 2020). [Presentation 9](https://web.tresorit.com/l/FDl4u#NHx11i1KRZQQjHFGg01Jsg&viewer=o0IL9EDvNwpAxQ54TpClIFyBxFRaTFbq)

[2] "Adversarial Tactics, Techniques & Common Knowledge (ATT&CK)," MITRE, 2021. [Online]. Available: https://attack.mitre.org/groups/

[3] "Accessing ATT&CK Data," MITRE, 2021. [Online]. Available: https://attack.mitre.org/resources/working-with-attack/

[4] MITRE Github - STIX Interface for ATT&CK, MITRE, 2021. Accessed: May 1, 2021. [Online]. Available: https://github.com/mitre/cti/tree/master/enterprise-attack/intrusion-set.
(Note: commit eb1b9385d44340ce867a77358c5f5aaed666e54c)

[5] STIX™ Version 2.1. Edited by Bret Jordan, Rich Piazza, and Trey Darley. 25 January 2021. OASIS Committee Specification 02. https://docs.oasis-open.org/cti/stix/v2.1/cs02/stix-v2.1-cs02.html. Latest stage: https://docs.oasis-open.org/cti/stix/v2.1/stix-v2.1.html. (Note: commit for location objects 942af96041439aa3fda01c85133701cc1b27abdf)

[6] OASIS Open GitHub - CTI STIX Common Objects, OASIS, 2021. Accessed: May 13, 2021. [Online]. Available: https://github.com/oasis-open/cti-stix-common-objects

[7] OASIS Threat Actor Context (TAC) Technical Committee. [Online]. Available: https://www.oasis-open.org/committees/tac

---

### Research Team

* [Vasileios Mavroeidis](https://www.linkedin.com/in/vasileiosmavroeidis/)
* [Mateusz Zych](https://www.linkedin.com/in/mateuszzych/)


