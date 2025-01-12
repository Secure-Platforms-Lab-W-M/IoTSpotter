# IoTSpotter Artifact

Understanding IoT Security from a Market-Scale Perspective

## Introduction

IoTSpotter is a tool for automatically identifying mobile-IoT apps, IoT specific library, and potential vulnerabilities (i.e., third-party library vulnerabilities, cryptographic API misuse, and Janus vulnerabilities) in the wild based on natural language processing and deep learning. Based on IoTSpotter, we identify 37,783 mobile-IoT apps from google play and 19,939 IoT Specific third-party library package names, which are available in this repo. Moreover, based on the identification results, we discover 43,172 cryptographic violations that affect over 900 apps with more than a million installs each, 65 vulnerable libraries specific to IoT used by 40 apps containing 79 unique vulnerabilities mapped to CVEs, and 7,887 apps that is affected by the Janus vulnerability.

<p align="center"><img src="figure/iotspotter.PNG" alt="workflow" width="800"></p>

## Table of Contents
- [IoTSpotter Artifact](#iotspotter-artifact)
  - [Introduction](#introduction)
  - [Table of Contents](#table-of-contents)
  - [Citation](#citation)
  - [Data Release](#data-release)
    - [1. 37K mobile-IoT apps](#1-37k-mobile-iot-apps)
    - [2. App manual validation and 5,100 Confirmed IoT apps](#2-app-manual-validation-and-5100-confirmed-iot-apps)
    - [3. 19K IoT specific package names](#3-19k-iot-specific-package-names)
    - [4. IoT specific library vulnerabilities](#4-iot-specific-library-vulnerabilities)
    - [5. Datasets of mobile-IoT app classifiers](#5-datasets-of-mobile-iot-app-classifiers)
    - [6. Mobile-IoT app classifiers](#6-mobile-iot-app-classifiers)
    - [7. IoT products and name entity recognition (NER) model](#7-iot-products-and-name-entity-recognition-ner-model)
  - [Installation](#installation)
  - [Mobile-IoT classifier](#mobile-iot-classifier)
  - [IoT product NER model](#iot-product-ner-model)
  - [Third-party library identification](#third-party-library-identification)
  - [IoT library curation and vulnerability analysis](#iot-library-curation-and-vulnerability-analysis)
    - [1. Identify maven repository links by google search](#1-identify-maven-repository-links-by-google-search)
    - [2. Crawl IoT specific libraries from maven repository](#2-crawl-iot-specific-libraries-from-maven-repository)
    - [3. Collect vulnerable library information](#3-collect-vulnerable-library-information)
  - [Cryptographic-API misuse analysis](#cryptographic-api-misuse-analysis)
  - [APK signature vulnerability analysis](#apk-signature-vulnerability-analysis)
  - [CDF](#cdf)
  - [Bug Report](#bug-report)

## Citation

If you find our data and tools useful, please consider to cite our paper [IoTSpotter](https://xinjin95.github.io/assets/pdf/IoTSpotter_ccs2022_paper.pdf):

```plaintext
@inproceedings{jin2022understanding,
  title={Understanding IoT Security from a Market-Scale Perspective},
  author={Jin, Xin and Manandhar, Sunil and Kafle, Kaushal and Lin, Zhiqiang and Nadkarni, Adwait},
  booktitle={Proceedings of the 2022 ACM SIGSAC Conference on Computer and Communications Security},
  pages={1615--1629},
  year={2022}
}
```

## Data Release

We provide the corpus and IoTSpotter identification results. Please don't distribute them. We will open source them to the public after the paper is published.

### 1. 37K mobile-IoT apps

37K mobile-IoT apps are listed in this [file](data/apk_androzoo_sha256/shared_sha256_androzoo.csv). The metadata of our identified 37K IoT apps is [here](https://drive.google.com/file/d/1Fq4sGUpEuU7EPnZuxMMCZdWlBXjDD8wN/view?usp=sharing). Each line of the metadata file is a json object, e.g.,
```json
{
  "title": "Doodle It - Pictionary for your Chromecast",
  "icon": "https://play-lh.googleusercontent.com/MBMHhCzEFKYmD1kE88NMMj-wFEcCqSJONGoMcayGjRExEjkvVp6wvKh08X828jHaVA",
  "screenshots": [
    "https://play-lh.googleusercontent.com/zyi_NuligVJYZmjHTTGH2nhfjcD6xVbt5zR_tuPqxmmdhhfe7aPiePe1dCCEV7mIB1Vt=w720-h310-rw",

  ],
  "video": "https://www.youtube.com/embed/sbhm4pjWKuU",
  "category": [
    "GAME_WORD"
  ],
  "score": "4.2",
  "histogram": {
    "1": null,
    "2": null,
    "3": null,
    "4": null,
    "5": null
  },
  "reviews": 84,
  "description": "Whit \"Doodle it\" you can challenge your friends and family in a fun and interactive game where everyone participates!\nThe rules are simple:\n• Split in two teams\n• Each turn, one draws a random word, the rest of the team has to guess it\n• The first team to reach 10 wins!\n\"Doodle it\" is like playing charades with pen and paper, using your tablet as the drawing board.\n\"Doodle it\" is the ideal game to add to your set for a fun game night.\n\"Doodle it\" will challenge your artistic skills and fast thinking trying to draw and guess the more than 1000 different words provided by the FULL package!!!\n\"Doodle it\" will provides a special KIDS package so kids can play and have fun!!!\n\"Doodle it\" will cast your drawings live to your TV! You draw on your tablet, the rest guess from the Chromecast!\n--\n• We are still working on improving the game and we will love to hear your feedback",
  "description_html": "Whit \"Doodle it\" you can challenge your friends and family in a fun and interactive game where everyone participates!<br/><br/>The rules are simple:<br/><br/>• Split in two teams<br/>• Each turn, one draws a random word, the rest of the team has to guess it<br/>• The first team to reach 10 wins!<br/><br/>\"Doodle it\" is like playing charades with pen and paper, using your tablet as the drawing board.<br/><br/>\"Doodle it\" is the ideal game to add to your set for a fun game night.<br/><br/>\"Doodle it\" will challenge your artistic skills and fast thinking trying to draw and guess the more than 1000 different words provided by the FULL package!!!<br/><br/>\"Doodle it\" will provides a special KIDS package so kids can play and have fun!!!<br/><br/>\"Doodle it\" will cast your drawings live to your TV! You draw on your tablet, the rest guess from the Chromecast!<br/><br/>--<br/>• We are still working on improving the game and we will love to hear your feedback",
  "recent_changes": null,
  "editors_choice": false,
  "price": "0",
  "free": true,
  "iap": true,
  "developer_id": "Hi%27ona+Studios",
  "updated": "April 3, 2020",
  "size": "3.0M",
  "installs": "10,000+",
  "current_version": "1.8.3",
  "required_android_version": "5.0 and up",
  "content_rating": [
    "Everyone"
  ],
  "iap_range": [
    "Everyone"
  ],
  "interactive_elements": null,
  "developer": "Hi'ona Studios",
  "developer_email": "hiona.studios@gmail.com",
  "developer_url": "https://www.reddit.com/r/doodle_it",
  "developer_address": "Råggatan 8, lght 1004\n18 59 Stockholm\nSweden",
  "app_id": "com.hiona.doodleit",
  "url": "https://play.google.com/store/apps/details?id=com.hiona.doodleit"
}
```
Since the total file size of all APKs of 37 mobile-IoT apps is more than 100GB, we recommend you to directly download them via [Androzoo](https://androzoo.uni.lu/). For the same APKs that we used for analysis, you can download them via Androzoo APIs with the [sha256 signatures](data/apk_androzoo_sha256/shared_sha256_androzoo.csv). 

### 2. App manual validation and 5,100 Confirmed IoT apps

As stated in our paper, we manually validated some apps to give more confident results. 

Specically, we annotated the 917 mobile-IoT apps with > 1M downloads and the validation results are provided in this [file](data/app_validation/917_1M_apps_validation.csv), where the column of `app_id` corresponds to that in the metadata file and `manual_label` is 1 when the app is an IoT app.

Moreover, we also annotated 2250 randomly sampled apps from 37K mobile-IoT apps. And the validation results are in this [file](data/app_validation/2250_apps_validation.csv).

Finally, we combined all the apps that we have manually labeled and validated from our training/validation/test sets, 917 validated apps, and 2250 validated apps. The combined results are in this [file](data/app_validation/all_labeled_apps.csv), in which 5,100 apps are confirmed as IoT apps.

### 3. 19K IoT specific package names

Our differential analysis component identifies 19K 3rd-party library package names, which can be found [here](data/3rd_party_lib/filtered_package_names.txt). Each line of the file corresponds to one unique package name. Here, package names are the name of [JAVA packages](https://docs.oracle.com/javase/tutorial/java/concepts/package.html).

Moreover, we also release the information about the apps using each of the 19K package names. You can find it in [this file](data/3rd_party_lib/iot_lib_map_ranked.txt). Moreover, we also cluster the 19K package names based on their prefixes (length of 3) and identify the iot apps using these package names of each prefix. You can find the results in [this file](data/3rd_party_lib/cluster_app_mapping.txt).

### 4. IoT specific library vulnerabilities

We provide the identified vulnerable libraries and the vulnerabilities (i.e., CVEs) in this [file](data/maven_crawling/vulnerability.txt). If you want to identify more vulnerabilities, you can use our script specified in [this section](#iot-library-curation-and-vulnerability-analysis).

For our identified 27 vulnerable libraries that affecting the 40 top IoT apps (with > 50K downloads), we release the apps and the libraries in [this sheet](https://docs.google.com/spreadsheets/d/1ShkskYD6gteH5rjTO6SSJJ0DaPm36N8DqNZq_k4x6wU/edit?usp=sharing).

### 5. Datasets of mobile-IoT app classifiers

You can find our annotated datasets under [data/dataset](data/dataset), where the `label` is 1 (IoT) and 0 (non-IoT). Part of the IoT app samples are from Wang'2019 USENIX Security paper, we obtained all their apps from this [link](http://seclab.soic.indiana.edu/xw48/iot_companion_appset.tar.gz). Then we removed the apps that were not in GPlay any more and obtained the remaining apps for annotataion. And we provide the remaining app list [here](data/artifacts/app_list.txt).

### 6. Mobile-IoT app classifiers

For the mobile-IoT app classifiers, you can find the BiLSTM classifier under [data/classifiers/](data/classifiers/bilstm.h5) and download the BERT model via this [link](https://drive.google.com/drive/folders/1qzGOPXfE4FLZRfF0GoL1iFdfazwvGGlf?usp=sharing).

### 7. IoT products and name entity recognition (NER) model

You can download the NER dataset, script and model via this [link](https://drive.google.com/file/d/1HxqHFE-VnofdMNHWEyyjLXymRMzrzWfn/view?usp=sharing). After identifying the IoT products, we cluster them with [GSDMM model](https://github.com/rwalk/gsdmm-rust). You can find resulting clusters [here](data/artifacts/iot_product_clustering_results.zip), in which the non-empty files are unique clusters.

## Installation

We recommend `conda` to setup the environment and install the required packages. Conda installation instructions can be found [here](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html). The following setup assumes Conda is installed and is running on Linux system (though Windows should work too).

First, create the conda environment,

`conda create -n iotspotter python=3.6`

and activate the conda enviroment:

`conda activate iotspotter`

Then, install the `pip` package manager and other packages:

`conda install pip`

`pip install -r requirement.txt`

## Mobile-IoT classifier

To train the BiLSTM classfier, you have to first download the pretrained word vectors from [Glove](https://nlp.stanford.edu/data/glove.6B.zip) and put the `glove.6B.300d.txt` file under [data/glove/](data/glove).

Commands to train the model:

`cd classification`

`python bilstm.py`

The resulting model will be `data/classifiers/bilstm_new_training.h5`.

To classify model, run the following commands:

`cd classification`

`python classification.py`

If you want to classify your own apps, you have to first obtain the app's description from app market place. Then you can use our preprocessing script to preprocess the description and feed it to the classifier. The script is under [classification/preprocess.py](classification/preprocess.py), where the processing function is `preprocess_one_description`.

For the BERT model, we provide the script and instructions along with the classifier via this [link](https://drive.google.com/drive/folders/1qzGOPXfE4FLZRfF0GoL1iFdfazwvGGlf?usp=sharing).


## IoT product NER model

For the NER model, we give instructions on how to run it along with our [code](https://drive.google.com/file/d/1HxqHFE-VnofdMNHWEyyjLXymRMzrzWfn/view?usp=sharing).

## Third-party library identification

We provide the executable and code of our third-party library identification module [here](https://github.com/xinjin95/app-third-party-library).

## IoT library curation and vulnerability analysis

### 1. Identify maven repository links by google search

To identify the maven repository links for our interested libraries (e.g., IoT and non-IoT libraries), we use the google search engine. If you seek for fast google search APIs, you may be interested in the [programmable search api](https://developers.google.com/custom-search/v1/overview).

We provide the script to crawl the google search results via this [script](maven_repo/google_search.py). Note that google sets rate limits for our search queries, so you may expect to finish several hundreds of search queries per day.

### 2. Crawl IoT specific libraries from maven repository

To crawl the library file from maven repository, you have to first prepare a lost of starting [links](data/maven_crawling/maven_matched.txt), e.g., 

```json
{
  "package_name": "com.threeplay.android",
  "search_item": "com.threeplay.android maven",
  "links": [
    "https://mvnrepository.com/artifact/com.threeplay.libraries",
    "https://mvnrepository.com/artifact/com.threeplay",
    "https://github.com/Triple-T/gradle-play-publisher",
    "https://www.programmersought.com/article/61136303813/",
    "https://www.fanduel.com/threeplay-giveaway",
    "https://www.py4u.net/discuss/613115",
    "https://thetoymaven.com/product/el-shop-learn-cash-register/",
    "https://maven-music-player-3d-sound.apk.gold/android-9.0",
    "https://workplacemaven.com/dream-meaning-casino/",
    "https://mirrors.huaweicloud.com/repository/maven/com/",
    "https://ideas.walmart.ca/best-tech-gifts/",
    "http://www.mobyware.org/zte-z835-maven-3-lte-device-11321/sport-games-tag/pedal-up-download-333356.html",
    "https://time.com/3418190/best-video-games-of-fall-2014/",
    "https://cdmana.com/2021/07/20210725045305968x.html",
    "https://luxembourgish.english-dictionary.help/english-to-luxembourgish-meaning-connoisseur",
    "https://vault.si.com/vault/2004/06/21/fantasy-world-these-three-play-your-neighbor-plays-your-boss-plays-everybody-plays-once-the-secret-preserve-of-stats-geeks-fantasy-sports-are-now-a-billion-dollar-business"
  ],
  "matched_links": [
    "https://mvnrepository.com/artifact/com.threeplay.libraries",
    "https://mvnrepository.com/artifact/com.threeplay"
  ]
}
```
where `package_name` is the IoT specific package name, `search_item` is the keywords for google search, `links` is the google search top results, and `matched_links` is the maven repo links in google search results.

Commands to run the maven repo crawler:

`python maven_repo/large_scale_maven_crawler.py`

After crawling, a list of library jar files will be downloaded. 

### 3. Collect vulnerable library information

Moreover, as mentioned in the paper, we noticed that the maven repo (mvnrepository.com) annotates vulnerable libraries, e.g.,

<p align="center"><img src="figure/maven_repo_vuln.PNG" alt="workflow" width="800"></p>

We also provide the [script](maven_repo/lib_vuln_crawler.py) for crawling the vulnerable library information. 
If you want to identify the vulnerable libraries, you can run this script with preparing the start urls as above. The vulnerability information of our IoT specific libraries are provided in [this file](data/maven_crawling/vulnerability.txt).

you can identify the vulnerable libraries and related CVEs under [data/maven_crawling/](data/maven_crawling). we then use [LibScout](https://github.com/reddr/LibScout) to detect the vulnerable library usages.

## Cryptographic-API misuse analysis

For crypto-API misuse analysis, we rely on the popular crypto analysis tools, [CryptoGuard](https://dl.acm.org/doi/10.1145/3319535.3345659) and [Cognicrypt](https://doi.org/10.1109/TSE.2019.2948910). You can refer to their repositories for setup instructions.

Moreover, as we described in the paper, the rule set table in CryptoGuard paper doesn't match the output of CryptoGuard tool. To help future research on resolve this problem, we open source the [mapping table](data/cryptoguard_correction/cryptoguard_rules_mapping.csv) to convert the output of CryptoGuard tool to the result table listed in our paper.

## APK signature vulnerability analysis

We rely on Apksigner to identify Janus vulnerabilities. The apksigner tool is available in revision 24.0.3 and higher of the Android SDK Build Tools.

The basic commands for detecting the vulnerabilities are:

```python
import os

apk_path = path_to_target_apk

result_path = path_to_detection_result

cmd = f"apksigner verify --print-certs --verbose  -Werr {apk_path} | tee {result_path}"
os.system(cmd)
```

For more information about `apksigner`, please refer to this [link](https://developer.android.com/studio/command-line/apksigner).

To parse the detection results, we developed a function:

```python
def parse_one_app(result_path):
    """
    parse one app's apksigner result
    :param result_path: path to the apksigner result

    :return: json object of the scheme result
    """
    res = ['', '', '', '']
    with open(result_path, 'r') as f:
        for line in f:
            line = line.strip('\n')
            if "(JAR signing): " in line:
                line = line.split('(JAR signing): ')
                res[0] = line[1]
            elif "(APK Signature Scheme v2): " in line:
                line = line.split("(APK Signature Scheme v2): ")
                res[1] = line[1]
            elif "(APK Signature Scheme v3): " in line:
                line = line.split("(APK Signature Scheme v3): ")
                res[2] = line[1]
            elif "(APK Signature Scheme v4): " in line:
                line = line.split("(APK Signature Scheme v4): ")
                res[3] = line[1]
    result = []
    for r in res:
        if r == 'true':
            result.append(1)
        elif r == 'false':
            result.append(0)
        else:
            result.append(0)

    apk_signing_scheme = {
        "v1": result[0],
        "v2": result[1],
        "v3": result[2],
        "v4": result[3]
    }
    return apk_signing_scheme
```

Refer to this script for more details.

## CDF

To examine if the app install number affects our measurement results, we provide some statistics of the app install number distribtions in this [doc](cdf_stats.md).

## Bug Report

If you find any problems, please consider to file an [issue](https://github.com/xinjin95/IoTSpotter/issues) or contact us via jin.967@osu.edu or xinjin5991@gmail.com.