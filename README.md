# K8S-Cluster-Env
Dockerfile templates configuring deep learning running environments for kubernetes (K8S) cluster usage

## Following illustration based on the user account *pchen6* with *PyTorch-Env*
### Step 1: Prepare Dockerfile
* Use the template Dockfile inside PyTorch (or prepare your prefered Dockerfile)
```
$ git clone https://github.com/idso-fa1-pathology/K8S-Cluster-Env.git
$ cd K8S-Cluster-Env/PyTorch-Env
```
### Step 2. Build docker image
* Build docker image from Dockerfile (choose based on your computer), can take long (10-20 minutes)
```
$ docker build -t pytorchenv:pchen6 .                          # on T6
$ docker build --platform linux/x86_64 -t pytorchenv:pchen6 .  # on Mac
```
### Step 3. Push docker image to HPC-Harbor
* Create a public project, named the same as your user account, on HPC-Harbor first
* Then on your computer, login, tag, and then push to HPC-Harbor
```
$ docker login hpcharbor.mdanderson.edu                                           # login to the Harbor
$ docker tag pytorchenv:pchen6 hpcharbor.mdanderson.edu/pchen6/pytorchenv:pchen6  # tag as hpcharbor version
$ docker push hpcharbor.mdanderson.edu/pchen6/pytorchenv:pchen6                   # push to hpcharbor
```
## Step 4. Start K8S Jupyter for interactive model development
* Visit http://hpcexhaproxy.mdanderson.edu/jupyter
* Go to "Custom Environment", set number of CPUs(32)/GPUs(1)
* Set your own docker image (hpcharbor.mdanderson.edu/pchen6/pytorchenv:pchen6)
* Click the "Start", and wait for 2-3 minutes