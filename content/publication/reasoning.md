+++
title = "Reasoning with Latent Structure Refinement for Document-Level Relation Extraction (to appear in ACL 2020)"
date = 2020-04-10
draft = false
selected = true

authors = ["Guoshun Nan", "Zhijiang Guo", "**Ivan Sekulić**", "Wei Lu"]

abstract = "Document-level relation extraction requires integrating information within and across multiple sentences of a document and capturing complex interactions between inter-sentence entities. However, effective synthesis of relevant information in the document remains a challenging research question. Existing approaches construct static document-level graphs based on syntactic trees, co-references or heuristics from the unstructured text to model the dependencies. Unlike previous methods that may not be able to capture rich non-local interactions for inference, we propose a novel model that empowers the relational reasoning across sentences by automatically inducing the latent document-level graph. We further develop a refinement strategy, which enables the model to incrementally aggregate relevant information for multi-hop reasoning. Specifically, our model achieves $F1$ score of 59.05 on the large-scale document-level dataset (DocRED), significantly improving over the previous results. Furthermore, extensive analysis shows that the model is able to discover more accurate inter-sentence relations. "

publication = "*Proceedings of ACL 2020*"

# url_pdf = "https://arxiv.org/pdf/1811.04655.pdf"
#url_pdf = "files/adapting2019.pdf"

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["document-level", "relation extraction", "ACL2020", "NLP"]
categories = []

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++
