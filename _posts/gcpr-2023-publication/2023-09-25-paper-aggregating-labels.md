---
layout: post
title:  "Coping Noisy Annotations in Object Detection with Repeated Labels"
date:   2023-10-18 9:00:00 +0200
tags: [publication]
---

**The Evaluation Server can be found on [EvalAI](https://eval.ai/web/challenges/challenge-page/2078/)**

This article gives a quick overview of my colleagues and my [publication][1] presented at the GCPR 2023 in Heidelberg.

### Human Label Variation in Computer Vision


When data is labeled or annotated for computer vision tasks, inconsistencies can arise between different labelers. 
These inconsistencies can stem from:
1. Differences in interpretation due to ambiguity.
2. Genuine mistakes or errors.
3. Various other factors.

Specifically, in tasks like object detection and instance segmentation, inconsistencies often manifest in three ways:

1. Mismatched class assignments.
2. Imperfect boundary outlining.
3. Overlooked instances.

These inconsistencies can be thought of as "noise" since the mapping from visual features to labels isn't unique. 
Since humans are the source of this inconsistency, it's termed "human label variation" ([B. Plank, 2022](https://arxiv.org/abs/2211.02570)).

While training deep neural networks with such "noisy" annotations is a challenge in itself, evaluating them using 
standard metrics like [Average Precision](https://cocodataset.org/#detection-eval) is not straightforward. To address this, 
one can either consolidate the annotations (**aggregating**) or sift through and select the most reliable ones (**filtering**). 
The approach discussed in the referenced paper leans towards consolidating or aggregating these annotations.

### Aggregating object detection and instance segmentation annotations

<figure>
<img src="/assets/img/img-gcpr-2023/processing_graphic_aggregation.png" alt="processing graphic for the aggregation process">
<figcaption>Fig 1. Left: Original input image featuring three separate annotations by distinct annotators. 
Center: Application of the LAEM aggregation method to the three annotations, yielding an approximate ground truth. 
Right: Aggregated ground truth utilized during the training process.</figcaption>
</figure>

The aggregation process mentioned earlier is a two-step approach: first, there's a voting mechanism, and based on the 
results of this voting, overlapping regions are merged. This results in a new approximation of the ground truth, which 
can be utilized for both training and testing purposes. For an in-depth look, please refer to [the publication][1].

<figure>
<img src="/assets/img/img-gcpr-2023/aggregation_example_1.png" alt="ground truth aggregation example 1">
<img src="/assets/img/img-gcpr-2023/aggregation_example_2.png" alt="ground truth aggregation example 2">
<figcaption>Fig 2. Comparison between different ground truth aggregation methods, exemplary on the VinDr-CXR dataset Left: 
the original image with the repeated labels indicated by the different line types. Right: the four smaller images from top 
left to bottom right are, MJV+∩, LAEM+µ, LAEM+∪ and WBF.</figcaption>
</figure>

### Annotation budget study

#### Purpose of the Study:

We wanted to delve deep into the world of image annotations to understand the most efficient way to allocate resources. 
The question was straightforward: is it better to have multiple annotations for fewer images or a single annotation 
for many images, given a fixed budget?

#### What We Investigated:

We conducted two studies, examining different 'annotation budgets'. An 'annotation budget' here refers to the total 
amount of images or instances that can be labeled, considering the constraints of the annotators' available time. 
We looked at scenarios where:

1. Only single annotations were available.
2. There was a blend of single and repeated annotations.
3. Annotations were mostly repeated, leading to significantly less training data.

#### Our Findings:

- For the TexBiG dataset: We found a saturation point beyond which adding more data didn't bring much improvement. 
This indicates the potential of multi-annotator learning to make the most out of repeated labels.

- For the VinDr-CXR dataset: The results improved with a larger budget, suggesting that more annotations are beneficial, 
especially when dealing with noisy labels that don't often agree.

- Inclusion of Repeated Labels: Adding moderate repeated labels didn’t hurt performance. In fact, these labels not only 
bolster reliability but also support efficient use of multi-annotator learning methods. The effort to create these 
repeated labels doesn't seem to cost much in terms of performance or resources.

- Annotator Splits: Fragmenting the annotations among more splits might lead to lower performance. The effect becomes 
noticeable especially under tight annotation budgets. This hints at future research directions where determining optimal 
splits even before starting the annotation might be crucial.

#### Conclusion:

While multiple annotations aren’t always the answer, they can be especially useful when the budget is tight. However, 
knowing which scenarios will benefit most from repeated annotations remains a challenge.

For a comprehensive analysis and detailed results, please refer to our [research paper][1].

[1]:{{ site.url }}/assets/pdf/coping_noisy_annotations_in_object_detection_with_repeated_laebls.pdf