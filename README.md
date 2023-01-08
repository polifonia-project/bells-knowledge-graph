---
component-id: bells-knowledge-graph
name: BELLS Knowledge Graph
description: The Knowledge Graph about Italian bells, bell towers and bell ringers.
type: Repository
release-date: 30/12/2022
release-number: v0.1
work-package: 
- WP2
- WP4
licence: CC BY
links:
- https://github.com/polifonia-project/bells-knowledge-graph
credits:
- https://github.com/elenamusumeci
- https://github.com/valecarriero
---

# BELLS Knowledge Graph
BELLS Knowledge Graph stores information about Italian bells, bell towers and bell ringers.
[...]

BELLS Knowledge Graph can be queried on the [ArCo SPARQL endpoint](https://dati.cultura.gov.it/sparql).
Moreover, it can be downloaded from this repository in different formats (also, see [here](http://dati.beniculturali.it/resource/datasetCampaneLiguria)).

***License***: [Attribution 4.0 International (CC BY)](https://creativecommons.org/licenses/by/4.0/)

## Knowledge Graph Description

This knowledge graph contains data about Italian bells and bell towers.
Data about bells refer to both measurable, intrinsic aspects such as weight, materials, conservation status, as well as properties deriving from interpretation situations, such as authorship attribution, dating, execution techniques, and their related objects (e.g. bibliography).
The Bells knowledge graph is integrated in the ArCo knowledge graph.

## Competency questions addressed by this knowledge graph
- Where is the building/church/bell tower?
- When (what year) was the building built?
- In which context is the building located (urban, periurban...)?
- Are there bells in the church/bell tower? How many bells are in the church/bell tower?
- Is there a single bell or a poliorganic instrument (a set of bells) in a church/bell tower?
- By whom (by which foundry) were they melted?
- When were they melted?
- Which is the material of the bell?
- Which is the weight of the bell?
- Which are the measures of the bell?

## Examples of SPARQL queries addressed by the module
- By whom (by which foundry) were the bell(s) melted? When where they melted?
```
PREFIX tiapit: <https://w3id.org/italia/onto/TI/>
PREFIX core: <https://w3id.org/arco/ontology/core/>
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/>
PREFIX arco: <https://w3id.org/arco/ontology/arco/>
SELECT DISTINCT ?bell ?desc ?author ?authorLab ?dating ?datingTime
WHERE { ?bell arco:isCulturalPropertyComponentOf ?setofbells ; rdf:type arco:MusicHeritage ;
core:description ?desc ;
a-cd:hasDating ?dating ;
a-cd:hasAuthor ?author ;
dc:subject ?o .
?author rdfs:label ?authorLab .
?dating a-cd:hasDatingEvent ?datingEv .
?datingEv tiapit:atTime ?datingTime
FILTER(str(?o)='campana')
}
```

- Are there bells in the church/bell tower?
```
PREFIX tiapit: <https://w3id.org/italia/onto/TI/>
PREFIX core: <https://w3id.org/arco/ontology/core/>
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/>
PREFIX arco: <https://w3id.org/arco/ontology/arco/>
SELECT DISTINCT ?site ?siteLab ?bell ?desc
WHERE { ?bell arco:isCulturalPropertyComponentOf ?setofbells ; rdf:type arco:MusicHeritage ;
a-loc:hasTimeIndexedTypedLocation ?titl ;
core:description ?desc ;
dc:subject ?o .
?titl a-loc:atSite ?site .
?site rdfs:label ?siteLab
FILTER(str(?o)='campana')
}
```

- Which is the weight of the bell?
```
PREFIX tiapit: <https://w3id.org/italia/onto/TI/>
PREFIX muapit: <https://w3id.org/italia/onto/MU/>
PREFIX core: <https://w3id.org/arco/ontology/core/>
PREFIX a-cd: <https://w3id.org/arco/ontology/context-description/>
PREFIX arco: <https://w3id.org/arco/ontology/arco/>
PREFIX a-dd: <https://w3id.org/arco/ontology/denotative-description/>
SELECT DISTINCT ?bell ?desc ?m ?mLab ?v ?u ?uLab
WHERE { ?bell arco:isCulturalPropertyComponentOf ?setofbells ; rdf:type arco:MusicHeritage ;
a-loc:hasTimeIndexedTypedLocation ?titl ;
core:description ?desc ;
a-dd:hasMeasurementCollection ?mc ;
dc:subject ?o .
?mc a-dd:hasMeasurement ?m .
?m a-dd:hasMeasurementType a-dd:Weight .
?m rdfs:label ?mLab ; a-dd:hasValue ?mVal .
?mVal muapit:value ?v ; muapit:hasMeasurementUnit ?u .
?u rdfs:label ?uLab
FILTER(str(?o)='campana')
}
```


BELLS Knowledge Graph is described in two dedicated MELODY data stories: **[Overview of the bells in Liguria](https://projects.dharc.unibo.it/melody/bells/overview_of_the_bells_in_liguria)** and **[Bells on the map](https://projects.dharc.unibo.it/melody/bells/bells_on_the_map)**.
