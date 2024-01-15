# K8S-Cluster-Env
Dockerfile templates configuring running environment for kubernetes (K8S) cluster usage

## Following illustration based on the user account *pchen6* with *DL-Env*
### Step 1: Prepare Dockerfile
* Use the template Dockfile inside the DL-Env folder (or prepare your prefered Dockerfile)
```
$ git clone https://github.com/idso-fa1-pathology/K8S-Cluster-Env.git
$ cd K8S-Cluster-Env/DL-Env
```
### Step 2. Build docker image
* Build docker image from Dockerfile (choose from below based on your local machine), can take long (10-20 minutes)
```
$ docker build -t dlenv:pchen6 .                          # on T6
$ docker build --platform linux/x86_64 -t dlenv:pchen6 .  # on Mac
```
### Step 3. Push docker image to HPC-Harbor
* First create a public project (named the same as your user account) on [HPC-Harbor](https://hpcharbor.mdanderson.edu)
* Then on your local machine, tag docker image, login to HPC-Harbor, and then push docker image 
```
$ docker tag dlenv:pchen6 hpcharbor.mdanderson.edu/pchen6/dlenv:pchen6  # tag docker image as HPC-Harbor version
$ docker login hpcharbor.mdanderson.edu                                 # login HPC-Harbor
$ docker push hpcharbor.mdanderson.edu/pchen6/dlenv:pchen6              # push image to HPC-Harbor
```
## Step 4. Start K8S Jupyter for interactive DL model development
* Visit http://hpcexhaproxy.mdanderson.edu/jupyter
* Go to "Custom Environment", set number of CPUs(32)/GPUs(1)
* Set your own docker image (hpcharbor.mdanderson.edu/pchen6/dlenv:pchen6)
* Click the "Start", and wait for 2-3 minutes, retry if encountering Timeout 