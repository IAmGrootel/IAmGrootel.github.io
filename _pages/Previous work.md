---
title: ""
excerpt: ""
permalink: /selected_work
layout: single
sidebar:
  - title: "Selected Work"
    text: "Have a look at some of the recent projects that I have worked on.  
          
    For further detail check out my [resume](/assets/pdf/AlexvanGrootel_Resume.pdf)."
author_profile: false
gallery2:
  - url: /assets/images/deep_nn2.png
    image_path: /assets/images/deep_nn2.png
    alt: Deep NN architecture
#   - url: /assets/images/precision_recall.png
#     image_path: /assets/images/precision_recall.png
#     alt: precision recall of deep NN model, showing significantly improved permance over baselines.
gallery1:
  - url: /assets/images/extraction_schematic.png
    image_path: /assets/images/extraction_schematic.png
    alt: "NN Architecture"
  - url: /assets/images/PCA_thesis.png
    image_path: /assets/images/PCA_thesis.png
    alt: "PCA map of extracted metal compositions"
---
### Named Entity Recognition for Experiment Disambiguation
<p font-size=1px><i><font color = 'grey' > Tags: NLP, Named Entity Recognition, Recurrent Neural Networks, Deep Neural Networks, Word Embeddings, TF-IDF</font></i></p>
Many groups around the world are looking to automatically extract information from academic articles (see my other work [below](/selected_work#automatic-text-extraction-from-materials-and-manufacturing-journal-articles)). One issue that this field faces is experiment disambiguation; one article often talks about multiple, sometimes dozens, of experiments. It becomes diffcult to seperate them.

Leveraging a capability of the data pipeline we built (table parsing), I was able to identify a cheap way to get tens of thousands of labeled example in text, and was able to use this dataset to design and build a deep, recurrent neural network to predict whether a set of tokens were sample names or not. 

*Paper currently in review.*

{%include gallery id="gallery2" %}

<hr>

### Automatic Text Extraction from Materials and Manufacturing Journal Articles

<p font-size=1px><i><font color = 'grey' > Tags: NLP, unstructured data, text classification, sequence-to-sequence models, Named Entity Recognition, data engineering pipelines</font></i></p>

In the [Olivetti Group](https://olivetti.mit.edu/) at MIT, my [thesis](https://dspace.mit.edu/handle/1721.1/122216?show=full) was on the extraction of information on manufacturing and materials articles using NLP. 

By extracting and structuring this unstructured data from hundreds of thousands of papers, you can do analysis that even a large team of researchers could not hope to do manually. This can be a powerful approach. For instance we created a map of alloys which have been studied in the context of traditional manufacturing processes (casting, rolling, etc), but haven't yet been studied by Additive Manufacturing. This can then be used to identify promising compositions for Additive Manufacturing researchers to try to achieve specific mechanical properties. 

{% include gallery id="gallery1" %}

