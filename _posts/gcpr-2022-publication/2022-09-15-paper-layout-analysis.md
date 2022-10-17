---
layout: post
title:  "A Dataset for Analyzing Complex Document Layouts"
date:   2022-10-17 10:00:00 +0200
tags: [publication]
---

**We are planning to release another extra test set for benchmarking - we expect to finish that by end of November.**

In this short article I want to give a summary of [our publication][1] that we presented at the GCPR 2022.

### Dataset [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.6885144.svg)](https://doi.org/10.5281/zenodo.6885144)

<figure>
<img src="/assets/img/img-gcpr-2022/montage.png" alt="Sample 1 image of the TexBiG Dataset">
<figcaption>Fig 1. Sample images of the dataset. Dashed lines marks annotator A and dotted lines signifies annotator B. 
The colors indicate matching (green), missed (blue) or class wise disagreed (red) annotations.</figcaption>
</figure>

The here presented dataset focuses on complex layouts of historical documents. It can be used to train models for
document layout analysis similar to [PubLayNet](https://github.com/ibm-aur-nlp/PubLayNet) or 
[DocBank](https://github.com/doc-analysis/DocBank). As an annotations format we used the 
[COCO-Format](https://cocodataset.org/#format-data) and provide manual annotated polygons and bounding boxes, 
which means the dataset can be used to train Object Detection and Instance Segmentation models. The 52,000 annotated
instances are spread across 19 classes. For more details please refer to [our publication][1].

We trained and tested<sup id="benchmark">[[1]](#benchmark-ref)</sup> the dataset with two different models:

| Task - Model     | bbox - Mask R-CNN | bbox - VSR | mask - Mask R-CNN | mask - VSR |
|------------------|-------------------|------------|-------------------|------------|
| mAP              | 73.18             | 75.90      | 64.43             | 65.80      |
| mAP<sub>50</sub> | 85.12             | 87.80      | 80.31             | 82.60      |

Our code for VSR is available at [github](https://github.com/Madave94/VSR-TexBiG-Dataset). For Mask R-CNN we only
attach the [weights and config](https://doi.org/10.5281/zenodo.6885033) in our auxiliary materials.

##### Notes

<small id="benchmark-ref"><sup>[[1]](#benchmark)</sup> Since these data are evaluated on repeated labels, the model can never achieve perfect results.
That is also why we decided to release another test dataset.</small>


[1]:{{ site.url }}/assets/pdf/a_dataset_for_analysing_complex_layouts.pdf