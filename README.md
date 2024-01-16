# K8S-Cluster-Env
Dockerfile templates configuring running environment for usage of kubernetes (K8S) cluster 

## Following illustration based on user *pchen6* with *DL-Env*, replace *pchen6* to your own user name for experimentation 
### Step 1: Prepare Dockerfile
* Access Dockfile within the DL-Env folder (best to adapt it for your purpose)
```
$ git clone https://github.com/idso-fa1-pathology/K8S-Cluster-Env.git
$ cd K8S-Cluster-Env/DL-Env
```
### Step 2. Build Docker Image
* Build docker image from Dockerfile (choose one from two options below based on your local machine), the building process can take long (5-30 mins)
```
$ docker build -t dlenv:pchen6 .                          # on T6
$ docker build --platform linux/x86_64 -t dlenv:pchen6 .  # on Mac
```
### Step 3. Push Docker Image to HPC-Harbor
* On [HPC-Harbor](https://hpcharbor.mdanderson.edu), create a public project named as your user name, for storing docker images
* On your local machine, first tag the built docker image as hpcharbor version, next login to hpcharbor, and then push the tagged docker image to hpcharbor
```
$ docker tag dlenv:pchen6 hpcharbor.mdanderson.edu/pchen6/dlenv:pchen6  # tag docker imagea as hpcharbor version
$ docker login hpcharbor.mdanderson.edu                                 # login HPC-Harbor
$ docker push hpcharbor.mdanderson.edu/pchen6/dlenv:pchen6              # push image to hpcharbor
```
## Step 4. Launch K8S Instance for DL Model Development
* Visit http://hpcexhaproxy.mdanderson.edu/jupyter
* Go to "Custom Environment", set number of CPUs(32)/GPUs(1)
* Set your own docker image (hpcharbor.mdanderson.edu/pchen6/dlenv:pchen6)
* Click the "Start", and wait 2-3 minutes for environment initiation, retry if encountering Timeout 