---
layout: page
title: Uncertainty-aware Vision-based Metric Cross-view Geolocalization
description: Florian Fervers, Sebastian Bullinger, Christoph Bodensteiner, Michael Arens, Rainer Stiefelhagen<br>CVPR 2023
img: assets/img/vismetcvgl23-preview.jpg
# importance: 1
category: publications
---

<a href="https://arxiv.org/abs/2211.12145" class="btn btn-sm z-depth-0" role="button">arXiv</a> <a href="https://www.youtube.com/watch?v=1vHFiA0prL0" class="btn btn-sm z-depth-0" role="button">Video</a> <a href="/projects/vismetcvgl23/#code" class="btn btn-sm z-depth-0" role="button">Code</a>


*tl;dr Perform metric self-localization by matching a vehicle's camera readings against aerial imagery.*

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.html path="assets/img/vismetcvgl23-title.jpg" title="title image" class="img-fluid" %}
        <figcaption class="caption">Probability distributions for the vehicle position predicted by our model which matches the vehicle's surround camera images with an aerial image. The first and second rows show the front and back cameras in the Ford AV dataset. The last row shows the aerial image with the search region in the center and driving direction pointing upwards. Blue and red color refer to low and high probability predicted by our model. Map data: Bing Maps © 2022 TomTom, © Vexcel Imaging.</figcaption>
    </div>
</div>

### Abstract
---

This paper proposes a novel method for vision-based metric cross-view geolocalization (CVGL) that matches the camera images captured from a ground-based vehicle with an aerial image to determine the vehicle's geo-pose. Since aerial images are globally available at low cost, they represent a potential compromise between two established paradigms of autonomous driving, i.e. using expensive high-definition prior maps or relying entirely on the sensor data captured at runtime.

We present an end-to-end differentiable model that uses the ground and aerial images to predict a probability distribution over possible vehicle poses. We combine multiple vehicle datasets with aerial images from orthophoto providers on which we demonstrate the feasibility of our method. Since the ground truth poses are often inaccurate w.r.t. the aerial images, we implement a pseudo-label approach to produce more accurate ground truth poses and make them publicly available.

While previous works require training data from the target region to achieve reasonable localization accuracy (i.e. same-area evaluation), our approach overcomes this limitation and outperforms previous results even in the strictly more challenging cross-area case. We improve the previous state-of-the-art by a large margin even without ground or aerial data from the test region, which highlights the model's potential for global-scale application. We further integrate the uncertainty-aware predictions in a tracking framework to determine the vehicle's trajectory over time resulting in a mean position error on KITTI-360 of 0.78m.

### Code
---

We publish our code as separate packages:

- [tiledwebmaps](https://github.com/fferflo/tiledwebmaps): Package for fetching aerial images from tiled web maps.
- [cvgl_data](https://github.com/fferflo/cvgl_data): Common interface to all datasets used in the paper. Includes pseudo-labelled ground-truth.
- Training code: Coming soon...

### Method
---

<div class="row justify-content-sm-center">
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.html path="assets/img/vismetcvgl23-summary.png" title="Summary" class="img-fluid" %}
    </div>
</div>

### Dataset
---

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.html path="assets/img/vismetcvgl23-datasets.png" title="Summary" class="img-fluid" %}
        <figcaption class="caption">SD: Average scene duration. Data-frames are divided into disjoint cells with size 100m x 100m to measure aerial coverage.</figcaption>
    </div>
</div>

We collect data from seven different datasets over nine regions to train and test our method. The large amount of data allows evaluating in a cross-area setting, i.e. with disjoint train and test regions. Ford AV and KITTI-360 contain scenes that are significantly longer than the other datasets and are therefore most suited for evaluating tracking frameworks.

In addition to aerial images from DCGIS, MassGIS and Stratmap (which are taken between 2017 and 2021) we collect aerial images from Google Maps and Bing Maps during 2022. These images might be several years old since the recording date is not provided.

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.html path="assets/img/vismetcvgl23-datapreprocessing.png" title="Summary" class="img-fluid" %}
    </div>
</div>

Since the vehicle's geo-locations do not always accurately match the corresponding aerial images, we compute new geo-registered ground truth poses for all datasets used in the work (Fig. 4) and filter out invalid samples via an automated data-pruning approach (Fig. 5).

### Results
---

Our model outperforms previous approaches on the Ford AV dataset following the evaluation protocol of Shi et al. (CVPR2022), even under the strictly more challenging cross-area and cross-vehicle settings - which highlights the potential for global-scale application without fine-tuning on a new region or a new vehicle setup.

<div class="row justify-content-sm-center">
    {% include figure.html path="assets/img/vismetcvgl23-results-fordav.png" title="Results" class="img-fluid" %}
</div>

We additionally train our model without using information from the vehicle cameras, i.e. by setting all RGB values to zero. In this setting, the model learns a prior distribution of vehicle poses w.r.t. the aerial image since the BEV map is constant over different inputs. The model shows a performance similar to the previous state-of-the-art HighlyAccurate [35] for longitudinal recall indicating that their model might rely mainly on prior poses w.r.t. the aerial image rather than on cross-view matching. Fig. 6 shows a visualization of the features learned by the model in this setting.

<div class="row justify-content-sm-center">
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.html path="assets/img/vismetcvgl23-results-featurevis.png" title="Aerial-only feature visualization" class="img-fluid" %}
    </div>
</div>

We use a Kalman tracking framework to filter the uncertainty-aware predictions of the model and inertial measurements over time. In this setting, we outperform a recent lidar-visual metric CVGL method on KITTI-360 and achieve sub-meter accurate poses. We include two videos of the tracking framework applied to scenes in the Ford AV and KITTI-360 datasets below.

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        <iframe width="384" height="582" src="https://www.youtube.com/embed/JAo3Dh8wLcE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        <iframe width="384" height="486" src="https://www.youtube.com/embed/yTR3Wlu6Hdc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
</div>

<br>

### Citation
---

{% raw %}
```
@InProceedings{Fervers_2023_CVPR,
    author    = {Fervers, Florian and Bullinger, Sebastian and Bodensteiner, Christoph and Arens, Michael and Stiefelhagen, Rainer},
    title     = {Uncertainty-Aware Vision-Based Metric Cross-View Geolocalization},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
    month     = {June},
    year      = {2023},
    pages     = {21621-21631}
}
```
{% endraw %}
