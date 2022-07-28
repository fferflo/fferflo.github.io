---
layout: page
title: Continuous Self-Localization on Aerial Images Using Visual and Lidar Sensors
description: IROS 2022
img: assets/img/contselfloc22-preview.jpg
# importance: 1
category: publications
---

<a href="https://arxiv.org/abs/2203.03334" class="btn btn-sm z-depth-1" role="button">Paper</a>

*tl;dr Perform metric self-localization by matching a vehicle's lidar and camera readings against aerial imagery.*

<div class="row justify-content-sm-center">
    <div class="col-md-auto">
      <figure>
            <picture>
                <img  src="/assets/img/contselfloc22-demo.gif"  title="demo video" />
            </picture>
            <figcaption class="caption"><font size="1"> Maps data: Google ©2022 GeoBasis-DE/BKG (©2009)</font></figcaption>
        </figure>
    </div>
</div>

### Abstract
---

This paper proposes a novel method for geo-tracking, i.e. continuous metric self-localization in outdoor environments by registering a vehicle's sensor information with aerial imagery of an unseen target region. Geo-tracking methods offer the potential to supplant noisy signals from global navigation satellite systems (GNSS) and expensive and hard to maintain prior maps that are typically used for this purpose. The proposed geo-tracking method aligns data from on-board cameras and lidar sensors with geo-registered orthophotos to continuously localize a vehicle. We train a model in a metric learning setting to extract visual features from ground and aerial images. The ground features are projected into a top-down perspective via the lidar points and are matched with the aerial features to determine the relative pose between vehicle and orthophoto.

Our method is the first to utilize on-board cameras in an end-to-end differentiable model for metric self-localization on unseen orthophotos. It exhibits strong generalization, is robust to changes in the environment and requires only geo-poses as ground truth. We evaluate our approach on the KITTI-360 dataset and achieve a mean absolute position error (APE) of 0.94m. We further compare with previous approaches on the KITTI odometry dataset and achieve state-of-the-art results on the geo-tracking task.

### Citation
---

{% raw %}
```
@misc{fervers2022continuous,
  doi = {10.48550/ARXIV.2203.03334},
  url = {https://arxiv.org/abs/2203.03334},
  author = {Fervers, Florian and Bullinger, Sebastian and Bodensteiner, Christoph and Arens, Michael and Stiefelhagen, Rainer},
  keywords = {Computer Vision and Pattern Recognition (cs.CV), Robotics (cs.RO), FOS: Computer and information sciences, FOS: Computer and information sciences},
  title = {Continuous Self-Localization on Aerial Images Using Visual and Lidar Sensors},
  publisher = {arXiv},
  year = {2022},
  copyright = {arXiv.org perpetual, non-exclusive license},
}
```
{% endraw %}
