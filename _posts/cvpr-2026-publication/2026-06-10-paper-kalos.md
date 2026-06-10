---
layout: post
title:  "Measuring label quality (CVPR 2026 paper)"
date:   2026-06-10 12:30:00 +0200
tags: [publication]
---

Label variations exist in all datasets, but they often remain hidden in those containing only
one rater per image. While reducing these variations is a direct way to mitigate the
issues caused by "noisy labels," it is first necessary to identify whether these are structural
disagreements or individual errors.

For my recent [CVPR publication][1], we developed the KαLOS (KaLOS) toolkit to rigorously evaluate dataset
quality. The tool provides granular diagnostics to identify:

- Hard images and difficult classes for annotators.
- Collaboration clusters and "school of thought".
- Annotator vitality and individual rater consistency.

KαLOS is designed for use during both the creation and post-hoc assessment of datasets. It
is versatile enough to evaluate human labels, semi-automated proposals, and fully
automated annotations.

<figure>
    <img src="/assets/img/img-cvpr-2026/collaboration_heatmap_mean.svg"
         alt="Collaboration cluster analysis on the TexBiG.">
    <figcaption>Fig 1. Collaboration cluster analysis on the TexBiG dataset, visualizing agreement levels
between raters. "NaN" values indicate raters who did not share any overlapping tasks.</figcaption>
</figure>

KαLOS code can be found on [GitHub][2] or can be installed via `pip install kalos`.

I presented KαLOS at CVPR 2026 in Denver in June as a main track paper. If you missed it, here is a quick overview video
on [YouTube][3].

```bibtex
@inproceedings{tschirschwitz2026kalos,
  title={KαLOS finds Consensus: A Meta-Algorithm for Evaluating Inter-Annotator Agreement in Complex Vision Tasks},
  shorttitle = {KαLOS},
  author = {Tschirschwitz, David and Rodehorst, Volker},
  booktitle={Proceedings of the IEEE/CVF Computer Vision and Pattern Recognition Conference (CVPR)},
  year = {2026}
}
```


[1]: https://openaccess.thecvf.com/content/CVPR2026/html/Tschirschwitz_KaLOS_finds_Consensus_A_Meta-Algorithm_for_Evaluating_Inter-Annotator_Agreement_in_CVPR_2026_paper.html
[2]: https://github.com/Madave94/kalos
[3]: https://youtu.be/lHC73-y6mvs