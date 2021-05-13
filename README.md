## Summary
This repository provides an elevated [STIX](https://oasis-open.github.io/cti-documentation/stix/intro.html) representation of the [MITRE ATT&CK Groups knowledge base](https://attack.mitre.org/groups/), structurally extending the one provided in the [Official MITRE GitHub Repository](https://github.com/mitre/cti/tree/master/enterprise-attack/intrusion-set).

The version/commit that has been used for this project is [eb1b9385d44340ce867a77358c5f5aaed666e54c](https://github.com/mitre/cti/tree/eb1b9385d44340ce867a77358c5f5aaed666e54c/enterprise-attack/intrusion-set).

In particular, this project aimed to make the existing information in the ATT&CK Groups knowledge base programmatically more accessible, allowing it to more easily being queried upon and correlated with other sources and knowledge bases. The information used to extend and enrich the ATT&CK Groups STIX representation has been derived from the available prose descriptions.

---

**This repository includes:**

* STIX relationship objects and domain objects indicating the location (country) the groups/intrusion-sets appear to originate from.

`
sdo:intrusion-set -> sro:originates-from -> sdo:location
`

* STIX relationship objects and domain objects indicating the locations (countries and regions) the groups/intrusion-sets have been observed targeting.

`
sdo:intrusion-set -> sro:targets -> sdo:location
`

* STIX relationship objects and domain objects indicating the sectors (industries) the groups/intrusion-sets have been observed targeting (using the `sectors` property in the `identity` object).

`
sdo:intrusion-set -> sro:targets -> sdo:identity
`

* new `intrusion-set` objects that additionally represent the motivation factor of a group (using the `primary_motivation` property in the `intrusion-set` object).

`
sdo:intrusion-set
`

---


The new enriched intrusion-set (group) objects with the `primary_motivation` property populated relate to the existing MITRE-created `intrusion-set` objects via the `derived-from` relationship object.

<p align="center">
  <img src="/images/figure1.png" width="40%">
</p>

<br/>

The entity that created a STIX Object is an inherent, factual part of that object and therefore that information is captured in an embedded relationship contained in the `created_by_ref` property.

## How do i operationalize this work and access the ATT&CK STIX representation?

The STIX objects available in this repository **complement** the ones found in the [Official MITRE GitHub Repository](https://github.com/mitre/cti/tree/eb1b9385d44340ce867a77358c5f5aaed666e54c/enterprise-attack); thus, the objects from both repositories should be utilized/imported.

In addition, to avoid duplicating objects, we utilized the [STIX location objects](https://github.com/oasis-open/cti-stix-common-objects/tree/main/objects/location) from the OASIS CTI TC [common objects repository](https://github.com/oasis-open/cti-stix-common-objects) to connect the intrusion sets/ATT&CK Groups with their possible origin and targeted countries/regions, and thus, those objects should be utilized/imported too. The location objects have been populated based on the ISO 3166-1 and the United Nations M49 standards.

**Overall to make use of this project, the following objects need to be utilized/imported:**

1. The STIX Objects available in the folders [intrusion-set](), [relationship](), [identity](), and [location]() of this repository (required), **or the [enterprise-attack-enrich.json]() file that unifies all the objects together**.
2. The MITRE-generated STIX Objects available in the folder [intrusion-set](https://github.com/mitre/cti/tree/master/enterprise-attack/intrusion-set) (required) within the [enterprise-attack](https://github.com/mitre/cti/tree/master/enterprise-attack) folder in GitHub, and optionally the rest of the object folders, **or the MITRE-generated [enterprise-attack.json]() file that unifies all the objects together**.
3. The STIX Objects available in the folders [location](https://github.com/oasis-open/cti-stix-common-objects/tree/main/objects/location) of the OASIS CTI TC (required), **or our generated [oasis-cti-stix-common-objects-location.json]() file that unifies all the objects together**.

The ATT&CK STIX representation is most easily manipulated in Python using the stix2 library. However, because STIX 2.0 is represented in JSON, other programming languages can easily interact with the raw content [3]. Also, dedicated efforts that work with STIX can be used (e.g., the OpenCTI platform).

## Confidence level

The additional structured information provided in the feeds of this repository have been extracted from the descriptions of the MITRE ATT&CK Groups and should not be immediately considered of high confidence. The extraction has been performed programmatically using Natural Language Processing (NLP).

## Glossary

sdo: STIX Domain Object

sro: STIX Relationship Object

## References

[1] Slide deck regarding the idea/concept, presented at the 6th EU MITRE ATT&CK Workshop (October 23, 2020): [Presentation 9](https://web.tresorit.com/l/FDl4u#NHx11i1KRZQQjHFGg01Jsg&viewer=o0IL9EDvNwpAxQ54TpClIFyBxFRaTFbq)

[2] “Adversarial Tactics, Techniques & Common Knowledge (ATT&CK),” MITRE, 2021. [Online]. Available: https://attack.mitre.org/groups/

[3] “Accessing ATT&CK Data,” MITRE, 2021. [Online]. Available: https://attack.mitre.org/resources/working-with-attack/

[4] MITRE Github - STIX interface for ATT&CK, MITRE, 2021. Accessed: May 1, 2021. [Online]. Available: https://github.com/mitre/cti/tree/master/enterprise-attack/intrusion-set.
(Note: commit eb1b9385d44340ce867a77358c5f5aaed666e54c)


## Research Team

* [Vasileios Mavroeidis](https://www.linkedin.com/in/vasileiosmavroeidis/)
* [Mateusz Zych](https://www.linkedin.com/in/mateuszzych/)
