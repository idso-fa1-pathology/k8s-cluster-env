<h1 align="center">
  <a href="https://reactnative.dev/">
    K8S Cluster Running Environment Configuration
  </a>
</h1>

- Dockerfile boilerplates for configuring kubernetes (K8S) cluster running environment
- Following instructions are based on the user name **pchen6** with the boilerplate **DL-Env**, please replace all **pchen6** to your own user name for experimentation 

## Configuration Procedures
### Step 1: Prepare Dockerfile
* Access Dockerfile within the DL-Env folder (best to adapt it for your purpose)
```
$ git clone https://github.com/idso-fa1-pathology/k8s-cluster-env.git
$ cd k8s-cluster-env/DL-Env
```
### Step 2. Build Docker Image
* Build docker image from Dockerfile (choose one from two options below based on your machine), the first-time building process can take long (5-30 mins)
```
$ docker build -t dlenv:pchen6 .                          # on Linux
$ docker build --platform linux/x86_64 -t dlenv:pchen6 .  # on Mac
```
### Step 3. Push Docker Image to HPC-Harbor
* On [HPC-Harbor](https://hpcharbor.mdanderson.edu), create a public project named as your user name (e.g., pchen6), for storing docker images
* On your local machine, first login to hpcharbor, next tag the built docker image as hpcharbor format, and then push the tagged docker image to hpcharbor
```
$ docker login hpcharbor.mdanderson.edu                                 # login HPC-Harbor
$ docker tag dlenv:pchen6 hpcharbor.mdanderson.edu/pchen6/dlenv:pchen6  # tag docker image as hpcharbor format
$ docker push hpcharbor.mdanderson.edu/pchen6/dlenv:pchen6              # push image to hpcharbor
```
## Step 4. Launch K8S Instance for DL Model Development
* Visit http://hpcexhaproxy.mdanderson.edu/jupyter
* Scroll to the bottom, and toggle on "Custom Environment", and set configurations
    - _CPUs_: default **32**, range from 1 to 256
    - _Cuda Version_: default **11**, options are: 11 (NVIDIA A100) and 12 (NVIDIA H100)
    - _GPUs_: default **1**, range from 1 to 4
    - _Image_: no default, the format is **hpcharbor.mdanderson.edu/<project_name>/<image_name>:<image_tag>** (e.g., hpcharbor.mdanderson.edu/pchen6/dlenv:pchen6)
* Click the yellow "Start", and wait 1-2 minutes for environment initiation, retry if encountering Timeout 