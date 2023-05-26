---
layout: page
title: IR ADAS
date: MAR 2023 - Present
description: Infrared Driver Assistance Technology for use in Emergency Tow Trucks and Snowplows
img: assets/img/projects/ir-adas-project/main_thumbnail.jpg
importance: 1
category: work
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ir-adas-project/main.jpg" title="ir object detection" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Sun glare or fog can create dangerous driving conditions. (source: Teledyne FLIR Dataset)
</div>

This is a project of developing Advanced Driver Assistance Systems (ADAS) that will improve the safety and efficiency of emergency tow truck and snowplow operations under low-visibility conditions, by providing providing operators with warning systems and the
ability to observe and avoid obstacles.

The project involves finding a model that would inference with a decent FPS (25fps~) on Jetson Nano, training the model with publicly available thermal datasets (FLIR, KAIST etc), and developing a reliable software with Graphical User Interface (GUI) for use in driving. 

Recently, I have been supplied with the new Jetson Orin Nano for this project.

{% include repository/repo.html repository='andrewcwlee/yolov7-flir'%}
{% include repository/repo.html repository='soltanilara/IR-ADAS-FLIR-Jetson'%}