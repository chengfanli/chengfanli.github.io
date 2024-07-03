---
title: GLKB
summary: Developed the Genomic Literature Knowledge Base using ontologies and adapted models for PubMed event extraction.
tags:
  - other
date: 2022-05-01
---

In recent years, there has been a concerted effort to enhance the accessibility and utility of genomic research materials. Nonetheless, there remains a clear need for a resource that seamlessly integrates information from both genomic literature and databases, facilitating effortless access and comparison.

In this project, we have introduced the Genomic Literature Knowledge Base (GLKB). The GLKB effectively brings together genomic knowledge derived from a vast pool of more than 33 million PubMed abstracts and meticulously curated databases, all organized according to a rigorous schema. Users have the capability to select and compare results with varying confidence levels, thanks to the Python API and a user-friendly web interface.

By amalgamating insights from both literature and databases into a single, unified resource, the GLKB empowers researchers with a potent tool to expedite the pace of genomic research and discovery.

<img src="https://lllllcf.github.io/project/src/glkb1.png" style="width: 62%;" />

Under the supervision of Dr. Jie Liu, I worked with four peers to build the Genomic Literature Knowledge Base (GLKB), which incorporates multiple ontologies and captures the informative functional relations in the human genome. I extract entities, relationships, and events from the medical literature in the 34 million citations for biomedical literature from MEDLINE, life science journals, and online books in the PubMed database. I review and reproduce existing end-to-end NER and joint extraction models. Reproduce the DeepEventMine model and apply it to the Pubmed biomedical literature database to extract events.