# ABCD dataset

ABCD (AIST Building Change Detection) dataset is a new labeled dataset, specially geared toward constructing and evaluating damage detection systems to identify whether buildings have been washed-away by tsunami.  

The paper:  
**Aito Fujita, Ken Sakurada, Tomoyuki Imaizumi, Riho Ito, Shuhei Hikosaka and Ryosuke Nakamura, "Damage Detection from Aerial Images
via Convolutional Neural Networks," IAPR International Conference on Machine Vision Applications (MVA), 2017.** ([pdf](http://www.airc.aist.go.jp/gsrt/fujita_final.pdf))

## Synopsis
Each datum in this dataset is a pair of pre- and post-tsunami aerial image patches, and encompasses a target building at the center of the patch.   
The below shows eight samples from the dataset, where four pairs are shown for "washed-away" buildings (left column) and "surviving" buildings (right column), respectively. The class label assigned to each patch pair (i.e. "washed-away" or "surviving") represents whether or not a building at the center of the pre-tsunami patch got wahshed-away by tsunami. 

<p align="center"> 
<img src ="https://user-images.githubusercontent.com/13417696/27384118-b5539e1e-56c8-11e7-9c0c-7d06b899763f.png" />
</p>

These pairs were cropped from a hefty number of RGB aerial images of Tohoku region of Japan. These aerial images were taken before or after the Great East Japan earthquake, with the original pixel resolution of 40 cm for pre-quake images and 12 cm for post-qukae images (actually, resampled to 40 cm).

We prepared the patch pairs for two types of size: **fixed-scale** and **resized**. Fixed-scale patches were cropped from aerial images with the fixed size of 160 x 160 pixels; so they have the same resolution of the original images (40 cm). In contrast, resized patches  were cropped depending on the size of each target building (specifically, three times larger than the target building), and then all resized to 128 x 128 pixels; so the spatial scale of the patches varies from building to building.
The resulting ABCD dataset comprised 8,506 pairs for fixed-scale (4,253 washed-away) and 8,444 pairs for resized (4,223 washed-away). 

As source of class labels, we employed the existing, post-quake survey result (http://fukkou.csis.u-tokyo.ac.jp/). This survey result is the outcome of an exhaustive
field investigation which was carried out under the initiative of MLIT (Ministry of Land, Infrastructure, Transport and Tourism) in the wake of the Great East Japan earthquake on March 11, 2011. As a consequence of this survey, over 220,000 buildings in the ravaged areas were assessed, and each building was assigned a label according to the degree of damage.



## Download
IMPORTANT -- Please read the [Terms of Use](https://github.com/gistairc/ABCDdataset/blob/master/LICENSE.md) before downloading the ABCD dataset.

The dataset can be downloaded from [here](https://data.airc.aist.go.jp/ABCDdataset/ABCDdataset.zip) (2.1GB).   
Or type the following in the terminal:
```
$ wget https://data.airc.aist.go.jp/ABCDdataset/ABCDdataset.zip
$ unzip ABCDdataset.zip
```


Schematic of the directory configuration in the unzipped file is as follows:
```
./ABCDdataset/fixed-scale/
     |
     |- patch-pairs/
     |     |
     |     |- patch-pair_1.tif
     |     |- patch-pair_2.tif
     |          :
     |     |_ patch-pair_8506.tif
     |
     |_ 5fold-list/
           |
           |- cv1-train.csv
           |- cv1-test.csv
                :
           |_ cv5-test.csv

./ABCDdataset/resized/
     |
     |- patch-pairs/
     |     |
     |     |- patch-pair_1.tif
     |     |- patch-pair_2.tif
     |          :
     |     |_ patch-pair_8444.tif
     |
     |_ 5fold-list/
           |
           |- cv1-train.csv
           |- cv1-test.csv
                :
           |_ cv5-test.csv

```
The root directory contains two directories, `fixed-scale/` and `resized/`, each corresponding to fixed-scale and resized patch pairs as mentioned above. Each of the directories has two subdirectories, `patch-pairs/` and `5fold-list/`. In `patch-pairs/`, "washed-away" and "surviving" patch pairs are stored in `.tif` format. Each `.tif` file comprises 6 channels, the first three channels for a pre-tsunami RGB patch and the last three channels for a post-tsunami patch. Also, for traceability of our experiment, in `5fold-list/` we prepared csv files that specify file names we actually used for our 5-fold cross validation. For example, `cv1-train.csv` and `cv1-test.csv` are training and test set for one of 5 folds, and so on. These csv files take the following format:

```
patch-pair_14.tif,1
patch-pair_600.tif,1
:
patch-pair_34.tif,0
```
where each record corresponds to each tiff file, the first field is file name and the second field represents class label of the file in the first field ("1" for "washed-away" and "0" for "surviving").


---

### Contact
If you have any questions, please contact the following:  
Aito Fujita  
National Institute of Advanced Industrial Science and Technology (AIST), Japan  
Email: fujita.713[at]aist.go.jp  

### Acknowledgement
This dataset is based on results obtained from a project commissioned by the New Energy and Industrial Technology Development Organization (NEDO).  
We also appreciate MLIT (Ministry of Land, Infrastructure, Transport and Tourism) and CSiS (Center for Spatial Information Science, The University of Tokyo) for compiling [the archive of the Great East Japan Earthquake Survey](http://fukkou.csis.u-tokyo.ac.jp/), which we employed as source for groundtruths. 
