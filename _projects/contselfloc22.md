---
layout: page
title: Continuous Self-Localization on Aerial Images Using Visual and Lidar Sensors
description: Florian Fervers, Sebastian Bullinger, Christoph Bodensteiner, Michael Arens, Rainer Stiefelhagen<br>IROS22
img: assets/img/contselfloc22-preview.jpg
# importance: 1
category: publications
---

<a href="https://arxiv.org/abs/2203.03334" class="btn btn-sm z-depth-1" role="button">Paper</a>
<a href="https://www.youtube.com/watch?v=4H-d2gHNcm0" class="btn btn-sm z-depth-1" role="button">Video</a>


*tl;dr Perform metric self-localization by matching a vehicle's lidar and camera readings against aerial imagery.*

<div class="row justify-content-sm-center">
    <div class="col-md-auto">
        <figure>
            <picture>
                <img  src="/assets/img/contselfloc22-demo.gif"  title="demo video" />
            </picture>
            <figcaption class="caption"><font size="1"> Maps data: Google ©2022 Stadt Karlsruhe VLW, GeoBasis-DE/BKG (©2009)</font></figcaption>
        </figure>
    </div>
</div>

### Abstract
---

This paper proposes a novel method for geo-tracking, i.e. continuous metric self-localization in outdoor environments by registering a vehicle's sensor information with aerial imagery of an unseen target region. Geo-tracking methods offer the potential to supplant noisy signals from global navigation satellite systems (GNSS) and expensive and hard to maintain prior maps that are typically used for this purpose. The proposed geo-tracking method aligns data from on-board cameras and lidar sensors with geo-registered orthophotos to continuously localize a vehicle. We train a model in a metric learning setting to extract visual features from ground and aerial images. The ground features are projected into a top-down perspective via the lidar points and are matched with the aerial features to determine the relative pose between vehicle and orthophoto.

Our method is the first to utilize on-board cameras in an end-to-end differentiable model for metric self-localization on unseen orthophotos. It exhibits strong generalization, is robust to changes in the environment and requires only geo-poses as ground truth. We evaluate our approach on the KITTI-360 dataset and achieve a mean absolute position error (APE) of 0.94m. We further compare with previous approaches on the KITTI odometry dataset and achieve state-of-the-art results on the geo-tracking task.

### Method
---

##### 1. Alignment

<div class="row justify-content-sm-center">
    {% include figure.html path="assets/img/contselfloc22-summary.jpg" title="Summary" class="img-fluid" %}
</div>

##### 2. Tracking

We choose a simple tracking method based on an Extended Kalman Filter (EKF) with the constant turn-rate and acceleration (CTRA) motion model that continuously integrates measurements of an inertial measurement unit (IMU). The EKF keeps track of the current vehicle state and corresponding state uncertainty. To demonstrate the effectiveness of our registration, we use only the turn-rate and acceleration of the IMU which on its own results in large long-term drift. The acceleration term is integrated twice to produce position values, such that small acceleration noise leads to large translational noise over time. We use our registration method to continuously align the trajectory with aerial images such that the drift is reduced to within the registration error of the method.

### Results
---

We achieve state-of-the-art results on both the KITTI and KITTI-360 datasets. The KITTI dataset contains only a single front-facing camera and can thus not leverage the full potential of our method. We still evaluate on KITTI since it is the dataset that most related works reported on. We achieve better results than other approaches, but our method fails to track two scenes due to the limited field-of-view. KITTI-360 includes a front-facing camera and two side-facing cameras and is captured over different trajectories than KITTI. Here, we successfully track all scenes and achieve sub-meter accuracy.

<div class="row justify-content-sm-center">
    {% include figure.html path="assets/img/contselfloc22-results-quantitative.jpg" title="Results" class="img-fluid" %}
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.html path="assets/img/contselfloc22-results-qualitative.jpg" title="Results" class="img-fluid" %}
    </div>
</div>

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
