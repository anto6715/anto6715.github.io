---
layout: single
toc: true
---

# DAS Download Procedures

---
## Introduction

The das account on both **Juno** and **Zeus** is in charge to of all download actions.
This guide will describe how to manage the download from marine data store


[new developments](./new_dev/index.html)
---
## Installation

### Conda Environment

To install **mds** conda env:

```shell
git clone -b mds_switch git@github.com:CMCC-Foundation/DasCrontab.git
cd DasCrontab
conda create -n mds --file mds/env_mds.txt
```

### Update copernicusmarine toolbox

Please keep update the copernicusmarine to the latest version using the command:

```shell
conda activate mds
pip install --upgrade copernicusmarine
```

### mds library and downloader tool

Download the dasDwlSystem which contains the mds library and the python downloading tool:

```shell
git clone -b am_mds_protocols git@github.com:CMCC-Foundation/dasDwlSystem.git <DAS_DOWLOAD_PATH>
```


Then link to the home the dasDwlSystem:

```shell
cd $HOME
ln -s <DAS_DOWLOAD_PATH> dasDwlSystem
```

### DasCrontab

```shell
git clone -b mds_switch git@github.com:CMCC-Foundation/DasCrontab.git <DAS_CRONTAB_PATH>
```

The installation script, will copy all the scripts under ~/script **only if the script is not present or if it's different** respect the previous one.
It means, that if only a file has been updated, running the command `./install.sh ~/script`, only that specific file will be moved under `~/script`


---
## Configuration

### MDS library

Please create a link in $HOME to reach the mds library:

Then link to the home the dasDwlSystem:

```shell
cd $HOME
ln -s <DAS_DOWLOAD_PATH> dasDwlSystem
```

### Download via LSF

Due to the very high nuber started from crontab, it is necessary to use LSF for the download script. The script [submit_task.sh](https://github.com/CMCC-Foundation/DasCrontab/blob/master/submit_task.sh)
has been prepared to solve the follwing problems:

* submit the script to LSF
* avoid to re-submit twice the same script on LSF (check if the same script is on PEND or RUN status)
* Redirect log on a specific directory

### Crontab

In the file [crontab_das.op](JUNO_crontab_das.op) is present the whole crontab installed in JUNO@das account.
The file [crontab.txt](crontab.txt) instead contains the files that have been updated with the migration to mds.

---
## How to test a download

It's mandatory to exec the instructions in [Requirements](#requirements)
To test a script, follow these commands:

```shell
./install.sh ~/script
~/script/utility/submit_task.sh ~/script/download/ocean/model/MedSea/Med_PHY_eas8/PHY_med_eas8_sm_15m_CMEMS_dwn.sh
```

The script `PHY_med_eas8_sm_15m_CMEMS_dwn.sh` can be replaced with any of the script that download from mds
