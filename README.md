<h1 align="center">
  K8S Cluster Running Environment Configuration
</h1>

<h3 align="left">
  &mdash; Dockerfile boilerplates for configuring kubernetes (K8S) cluster running environment <br>
  &mdash; Following instructions are based on the user name <strong><i>pchen6</i></strong> with the boilerplate <strong><i>PIP-DL-Env</i></strong>, please replace all <strong><i>pchen6</i></strong> to your own user name for experimentation 
</h3>


## Configuration Procedures
### Step 1: Prepare Dockerfile
* Access Dockerfile within the PIP-DL-Env folder (further adapt it for your purpose)
```
$ git clone https://github.com/idso-fa1-pathology/k8s-cluster-env.git
$ cd k8s-cluster-env/PIP-DL-Env
```

### Step 2. Build Docker Image
* Build docker image from Dockerfile, the first-time building process can take long (5-30 mins)
```
$ docker build --platform linux/x86_64 -t pipdlenv:pchen6 . 
```

### Step 3. Push Docker Image to HPC-Harbor
* On [HPC-Harbor](https://hpcharbor.mdanderson.edu), create a public project named as your user name (e.g., pchen6), for storing docker images
* On your local machine, first login to hpcharbor, next tag the built docker image as hpcharbor format, and then push the tagged docker image to hpcharbor
```
$ docker login hpcharbor.mdanderson.edu                                       # login HPC-Harbor
$ docker tag pipdlenv:pchen6 hpcharbor.mdanderson.edu/pchen6/pipdlenv:pchen6  # tag docker image as hpcharbor format
$ docker push hpcharbor.mdanderson.edu/pchen6/pipdlenv:pchen6                 # push image to hpcharbor
```

## Step 4. Launch K8S Instance for DL Model Development
* Visit http://hpcexhaproxy.mdanderson.edu/jupyter
* Scroll to the bottom, and toggle on "Custom Environment", and set configurations
    - _CPUs_: default **32**, range from 1 to 256
    - _DGX Type_: default **A100**, options are: A100 and H100
    - _GPUs_: default **1**, range from 1 to 4
    - _Image_: no default, the format is **hpcharbor.mdanderson.edu/<project_name>/<image_name>:<image_tag>** (e.g., hpcharbor.mdanderson.edu/pchen6/pipdlenv:pchen6)
* Click the yellow "Start", and wait 1-2 minutes for environment initiation, retry if encountering Timeout 
