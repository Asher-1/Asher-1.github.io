---
permalink: /resource/
title: "Resource"
author_profile: true
redirect_from: 
  - /md/
  - /resource.html
---

## Tips and hints

* Name a file ".md" to have it render in markdown, name it ".html" to render in HTML.
* Go to the [commit list](https://github.com/Asher-1/Asher-1.github.io/commits/main) (on your repo) to find the last version Github built with Jekyll. 
  * Green check: successful build
  * Orange circle: building
  * Red X: error
  * No icon: not built

This repository aims to provide convenient, easy deployable and scalable
REST API for InsightFace face detection and recognition pipeline using
FastAPI for serving and NVIDIA TensorRT for optimized inference.

Code is heavily based on API
[code](https://github.com/deepinsight/insightface/tree/master/python-package)
in official DeepInsight InsightFace
[repository](https://github.com/deepinsight/insightface).

This repository provides source code for building face recognition REST
API and converting models to ONNX and TensorRT using Docker.

![Draw detections example](https://Asher-1.github.io/images/draw_detections.jpg)


## Key features:

- Ready for deployment on NVIDIA GPU enabled systems using Docker and
  nvidia-docker2.
- Fully automatic model bootstrapping, including downloading and
  MXnet->ONNX->TensorRT conversion of official DeepInsight InsightFace
  models.
- Up to 3x performance boost over MXNet inference with help of TensorRT
  optimizations, FP16 inference and batch inference of detected faces
  with ArcFace model.
- Inference on CPU with ONNX-Runtime.

## Contents

[List of supported models](#list-of-supported-models)
- [Detection](#detection)
- [Recognition](#recognition)
- [Other](#other)

[Prerequesites](#prerequesites)

[Running with Docker](#running-with-docker)

[API usage](#api-usage)
- [/extract](#extract-endpoint)

[Work in progress](#work-in-progress)

[Known issues](#known-issues)

[Changelog](#changelog)


## Resources
 * [Liquid syntax guide](https://shopify.github.io/liquid/tags/control-flow/)

## List of supported models:

### Detection:

| Model                 | Auto download | Inference code | Source                      | ONNX File |
|:----------------------|:-------------:|:--------------:|:----------------------------|:---------:|
| retinaface_r50_v1     | Yes           | Yes            | [official package][l1]      |[link][dl1]|
| retinaface_mnet025_v1 | Yes           | Yes            | [official package][l2]      |[link][dl2]|
| retinaface_mnet025_v2 | Yes           | Yes            | [official package][l3]      |[link][dl3]|
| mnet_cov2             | No            | Yes            | [mnet_cov2][2]              |[link][dl4]|
| centerface            | Yes           | Yes            | [Star-Clouds/CenterFace][3] |[link][dl5]|
| scrfd_10g_bnkps       | Yes           | Yes            | [SCRFD][l6]                 |[link][dl6]|
| scrfd_2.5g_bnkps      | No            | Yes            | [SCRFD][4]                  |[link][dl7]|

### Recognition:

| Model                  | Auto download | Inference code | Source                 | ONNX File  |
|:-----------------------|:-------------:|:-------------:|:------------------------|:----------:|
| arcface_r100_v1        | Yes           | Yes            | [official package][l4] |[link][dl8] |
| r100-arcface-msfdrop75 | No            | Yes            | [SubCenter-ArcFace][5] | None       |
| r50-arcface-msfdrop75  | No            | Yes            | [SubCenter-ArcFace][5] | None       |
| glint360k_r100FC_1.0   | No            | Yes            | [Partial-FC][6]        | None       |
| glint360k_r100FC_0.1   | No            | Yes            | [Partial-FC][6]        | None       |
| glintr100              | Yes           | Yes            | [official package][l7] |[link][dl13]|

### Other:

| Model        | Auto download | Inference code | Source                 | ONNX File  |
|:-------------|:-------------:|:--------------:|:-----------------------|:----------:|
| genderage_v1 | No            | Yes            | [official package][l5] |[link][dl14]|
| 2d106det     | No            | No             | [coordinateReg][8]     | None       |


[1]: https://github.com/deepinsight/insightface/tree/master/python-package
[l1]: https://github.com/Asher-1/Asher-1.github.io/blob/main/files/models/retinaface_r50_v1.zip?raw=true
[l2]: https://github.com/Asher-1/Asher-1.github.io/blob/main/files/models/retinaface_mnet025_v1.zip?raw=true
[l3]: https://github.com/Asher-1/Asher-1.github.io/blob/main/files/models/retinaface_mnet025_v2.zip?raw=true
[l4]: https://github.com/Asher-1/Asher-1.github.io/blob/main/files/models/arcface_r100_v1.zip?raw=true
[l5]: https://github.com/Asher-1/Asher-1.github.io/blob/main/files/models/genderage_v1.zip?raw=true
[l6]: https://github.com/Asher-1/Asher-1.github.io/blob/main/files/models/antelope/scrfd_10g_bnkps.onnx?raw=true
[l7]: https://github.com/Asher-1/Asher-1.github.io/blob/main/files/models/antelope/glintr100.onnx?raw=true
[2]: https://github.com/deepinsight/insightface/tree/master/detection/RetinaFaceAntiCov
[3]: https://github.com/Star-Clouds/CenterFace
[4]: https://github.com/deepinsight/insightface/tree/master/detection/scrfd
[5]: https://github.com/deepinsight/insightface/tree/master/recognition/SubCenter-ArcFace
[6]: https://github.com/deepinsight/insightface/tree/master/recognition/partial_fc
[7]: https://github.com/deepinsight/insightface/tree/master/recognition/arcface_torch
[8]: https://github.com/deepinsight/insightface/tree/master/alignment/coordinateReg

[dl1]: https://drive.google.com/file/d/1peUaq0TtNBhoXUbMqsCyQdL7t5JuhHMH/view?usp=sharing
[dl2]: https://drive.google.com/file/d/12H4TXtGlAr1boEGtUukteolpQ9wfUTWe/view?usp=sharing
[dl3]: https://drive.google.com/file/d/1hzgOejAfCAB8WyfF24UkfiHD2FJbaCPi/view?usp=sharing
[dl4]: https://drive.google.com/file/d/1xPc3n_Y0jKyBONRx71UqCfcHjOGOLc2g/view?usp=sharing
[dl5]: https://drive.google.com/file/d/10tXAXhiq06VNdTAdYt5-pjkGn7zOFMk4/view?usp=sharing
[dl6]: https://drive.google.com/file/d/1OAXx8U8SIsBhmYYGKmD-CLXrYz_YIV-3/view?usp=sharing
[dl7]: https://drive.google.com/file/d/1qnKTHMkuoWsCJ6iJeiFExGy5PSi8JKPL/view?usp=sharing
[dl8]: https://drive.google.com/file/d/1sj170K3rbo5iOdjvjHw-hKWvXgH4dld3/view?usp=sharing
[dl13]: https://drive.google.com/file/d/1TR_ImGvuY7Dt22a9BOAUAlHasFfkrJp-/view?usp=sharing
[dl14]: https://drive.google.com/file/d/1MnkqBzQHLlIaI7gEoa9dd6CeknXMCyZH/view?usp=sharing

## Requirements:

1. Docker

2. Nvidia-container-toolkit

3. Nvidia GPU drivers (460.x.x and above)

   
## ErowCloudViewer: A Modern System for 3D Data Processing

![ErowCloudViewer UI](https://Asher-1.github.io/images/ErowCloudViewerMainUI.png)

### version3.9.0 （MacOS support）

| Items            |           Date               |       Version                                                                                |
| --------         | ------ | ------------------------------------------------------------                           |
| [ErowCloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.9.0/ErowCloudViewer-3.9.0-2022-09-04-win-amd64.exe?raw=true)  | 2022-09-04   | Windows 64bits                                                          |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.9.0/CloudViewer-3.9.0-2022-09-04-win-amd64.exe?raw=true)      | 2022-09-04   | Windows 64bits                                                          |
| [ErowCloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.9.0/ErowCloudViewer-3.9.0-2022-04-04-ubuntu1804-amd64.run?raw=true)     | 2022-04-04   | Linux  64bits (Ubuntu18.04)                             |
| [ErowCloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.9.0/ErowCloudViewer-3.9.0-2023-04-02-mac-arm64.dmg?raw=true)     | 2023-04-02   | MacOS  64bits (M1-MX)                                   |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.9.0/CloudViewer-3.9.0-2023-04-02-mac-arm64.dmg?raw=true)      | 2023-04-02  | MacOS  64bits (M1-MX)                                                    |
| [Colmap](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.9.0/colmap-3.9.0-2023-04-02-mac-arm64.dmg?raw=true)      | 2023-04-02  | MacOS  64bits (M1-MX)                                                                         |

### version3.8.0

| Items            |           Date               |       Version                                                                                |
| --------         | ------ | ------------------------------------------------------------                           |
| [ErowCloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.8.0/ErowCloudViewer-3.8.0-2021-11-12-win-amd64.exe?raw=true)  | 2021-11-12   | Windows 64bits                                                          |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.8.0/CloudViewer-3.8.0-2021-11-12-win-amd64.exe?raw=true)      | 2021-11-12   | Windows 64bits                                                          |
| [ErowCloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.8.0/ErowCloudViewer-3.8.0-2021-10.10-ubuntu1804-amd64.run?raw=true)     | 2021-10.10   | Linux  64bits (Ubuntu18.04)                             |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.8.0/CloudViewer-3.8.0-2021-10.10-ubuntu1804-amd64.run?raw=true)      | 2021-10.10  | Linux  64bits     (Ubuntu1804)                          |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.8.0/cloudViewer-0.3.8-cp36-cp36m-win_amd64.whl?raw=true)      | 2021-10.10  |  python3.6    win_arm64                                                  |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.8.0/cloudViewer-0.3.8-cp37-cp37m-win_amd64.whl?raw=true)      | 2021-10.10  |  python3.7    win_arm64                                                  |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.8.0/cloudViewer-0.3.8-cp38-cp38-win_amd64.whl?raw=true)       | 2021-10.10  |  python3.8    win_arm64                                                  |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.8.0/cloudViewer-0.3.8-cp36-cp36m-manylinux1_x86_64.whl?raw=true)     | 2021-10.10  |  python3.6    manylinux1_x86_64                          |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.8.0/cloudViewer-0.3.8-cp37-cp37m-manylinux1_x86_64.whl?raw=true)     | 2021-10.10  |  python3.7    manylinux1_x86_64                          |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.8.0/cloudViewer-0.3.8-cp38-cp38-manylinux1_x86_64.whl?raw=true)     | 2021-10.10  |  python3.8   manylinux1_x86_64                           |


### version3.7.0

| Items            |           Date                                                 |     Version                                                                                |
| --------         | ------ | ------------------------------------------------------------                           |
| [ErowCloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.7.0/ErowCloudViewer-3.7.0-2020-12-07-win-amd64.exe?raw=true)  | 2020-12-07   | Windows 64bits                                                          |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.7.0/CloudViewer-0.3.7-2020-12-07-win-amd64.exe?raw=true)      | 2020-12-07   | Windows 64bits                                                          |
| [ErowCloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.7.0/ErowCloudViewer-3.7.0-2020-12-15-linux-amd64.run?raw=true)     | 2020-12-05   | Linux  64bits (Ubuntu18.04)                             |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.7.0/CloudViewer-x86_64-0.3.7-linux.run?raw=true)              | 2020-12-05  | Linux  64bits (Ubuntu18.04)                                              |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.7.0/cloudViewer-0.3.7-cp36-cp36m-win_amd64.whl?raw=true)      | 2020-12-07  |  python3.6    win_arm64                                                  |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.7.0/cloudViewer-0.3.7-cp37-cp37m-win_amd64.whl?raw=true)      | 2020-12-07  |  python3.7    win_arm64                                                  |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.7.0/cloudViewer-0.3.7-cp38-cp38-win_amd64.whl?raw=true)       | 2020-12-07  |  python3.8    win_arm64                                                  |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.7.0/cloudViewer-0.3.7-cp36-cp36m-manylinux1_x86_64.whl?raw=true)     | 2020-12-07  |  python3.6    manylinux1_x86_64                          |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.7.0/cloudViewer-0.3.7-cp37-cp37m-manylinux1_x86_64.whl?raw=true)     | 2020-12-07  |  python3.7    manylinux1_x86_64                          |
| [CloudViewer](https://github.com/Asher-1/Asher-1.github.io/blob/main/files/ErowCloudViewer/version3.7.0/cloudViewer-0.3.7-cp38-cp38-manylinux1_x86_64.whl?raw=true)     | 2020-12-07  |  python3.8   manylinux1_x86_64                           |


## Locations of key files/directories

* Basic config options: _config.yml
* Top navigation bar config: _data/navigation.yml
* Single pages: _pages/
* Collections of pages are .md or .html files in:
  * _publications/
  * _portfolio/
  * _posts/
  * _documentation/
  * _downloads/
* Footer: _includes/footer.html
* Static files (like PDFs): /files/
* Profile image (can set in _config.yml): images/profile.png


## Definition Lists

Definition List Title
:   Definition list division.

Startup
:   A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.

#dowork
:   Coined by Rob Dyrdek and his personal body guard Christopher "Big Black" Boykins, "Do Work" works as a self motivator, to motivating your friends.

Do It Live
:   I'll let Bill O'Reilly [explain](https://www.youtube.com/watch?v=O_HyZ5aW76c "We'll Do It Live") this one.

## Unordered Lists (Nested)

  * List item one 
      * List item one 
          * List item one
          * List item two
          * List item three
          * List item four
      * List item two
      * List item three
      * List item four
  * List item two
  * List item three
  * List item four

## Ordered List (Nested)

  1. List item one 
      1. List item one 
          1. List item one
          2. List item two
          3. List item three
          4. List item four
      2. List item two
      3. List item three
      4. List item four
  2. List item two
  3. List item three
  4. List item four

## Buttons

Make any link standout more when applying the `.btn` class.

## Notices

**Watch out!** You can also add notices by appending `{: .notice}` to a paragraph.
{: .notice}

## HTML Tags

### Address Tag

<address>
  1 Infinite Loop<br /> Cupertino, CA 95014<br /> United States
</address>

### Anchor Tag (aka. Link)

This is an example of a [link](http://github.com "Github").

### Abbreviation Tag

The abbreviation CSS stands for "Cascading Style Sheets".

*[CSS]: Cascading Style Sheets

### Cite Tag

"Code is poetry." ---<cite>Automattic</cite>

### Code Tag

You will learn later on in these tests that `word-wrap: break-word;` will be your best friend.

### Strike Tag

This tag will let you <strike>strikeout text</strike>.

### Emphasize Tag

The emphasize tag should _italicize_ text.

### Insert Tag

This tag should denote <ins>inserted</ins> text.

### Keyboard Tag

This scarcely known tag emulates <kbd>keyboard text</kbd>, which is usually styled like the `<code>` tag.

### Preformatted Tag

This tag styles large blocks of code.

<pre>
.post-title {
  margin: 0 0 5px;
  font-weight: bold;
  font-size: 38px;
  line-height: 1.2;
  and here's a line of some really, really, really, really long text, just to see how the PRE tag handles it and to find out how it overflows;
}
</pre>

### Quote Tag

<q>Developers, developers, developers&#8230;</q> &#8211;Steve Ballmer

### Strong Tag

This tag shows **bold text**.

### Subscript Tag

Getting our science styling on with H<sub>2</sub>O, which should push the "2" down.

### Superscript Tag

Still sticking with science and Isaac Newton's E = MC<sup>2</sup>, which should lift the 2 up.

### Variable Tag

This allows you to denote <var>variables</var>.
