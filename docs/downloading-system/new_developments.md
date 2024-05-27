---
layout: default
title: New Development
parent: Downloading System
nav_order: 3
---



# How to start a new development


## Download template

- Use as starting point the [mds_get_template.sh](https://github.com/CMCC-Foundation/DasCrontab/blob/master/mds/mds_get_template.sh).

## Configure mds parameters

```shell
# the bucket can be found here: https://stac.marine.copernicus.eu/mdl-metadata/nativeBuckets.json
bucket=mdl-native-05
# product to download
product=WAVE_GLO_PHY_SWH_L3_NRT_014_001
# dataset to download
dataset=cmems_obs-wave_glo_phy-swh_nrt_swon-l3_PT1S
# the tag can be found with cope
tag=202311
# add the path after /data/inputs/METOCEAN - hereno reference to year/month/day
output_directory="${ADir}/historical/obs/ocean/satellite/CMS/GlobOce/altimetry/L3/sec"
# how much day in the past to download (i.e start_offset=7 start to download from a week ago)
start_offset=7
```

## Dataset specific configuration

```shell
local mds_filter="global_vavh_l3_rt_*_${date_to_download}T??????_????????T??????_????????T??????.nc"
# where to download output files
local dest="${output_directory}/Swon/${year}/${month}"
# how file are stored in mds - to check the specific dataset
local subdir="${year}/${month}"
```

## Prepare the file for the installation

- Copy the file in [obs](https://github.com/CMCC-Foundation/DasCrontab/tree/master/obs) or [model](https://github.com/CMCC-Foundation/DasCrontab/tree/master/model) path        
- `./install.sh ~/script`
- `~/script/utility/submit_task.sh ~/script/download/ocean/your_script.sh`
- check the log in `/work/cmcc/$(whoami)/dwl/log`
