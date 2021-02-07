# nvidia-openshift


##Procedure for running Nvidia GPU Operator 1.3.1 in a disconnected environment##

1. Setup a RHEL 8.2 machine to work on

2. Clone https://github.com/dmc5179/nvidia-driver repo and follow README instructions for 468
   note: if the instructions arent there then they were not merged and please check my fork https://github.com/rockocoop/nvidia-driver
3. Collect Images using Skopeo

   3a. If using the data directories in this git then you can mount data into a local registry for mirroring
    It includes a precompiled driver for kernel .29 (OCP 4.6.4+)

   3b. If not using this then mirror using the txt files in this repo

   3c. Another option is creating your own pruned index image of certified operators https://docs.openshift.com/container-platform/4.6/operators/admin/olm-restricted-networks.html and runnig the manifests-only option.  Then you can use the mapping.txt and skopeo to mirror the images

4. Mirror to internal registry and deploy/update imagecontentsourcepolicy.yaml (look at included example)

5. Deploy index image as a new catalogsource under the openshift-marketplace project


## Test GPU Setup ##
You can use caffe2ai to test the install as follows:

Prerequisites:
- this repo
- download dataset https://download.caffe2.ai/databases/resnet_trainer.zip
- download the image docker.io/caffe2ai/caffe2 and make it available in your local registry

Run Test:

1) Deploy in a new namespace the caffe2 yaml in this repo

2) Expose the service 

3) Connect to Route

4) Check Pod log for token

5) Login and go to the following path:

```
http://<route on openshift router>/notebooks/caffe2/caffe2/python/tutorials/Multi-GPU_Training.ipynb
```

6) Scroll down to the solution  

7) Update the value in the first section from https://download.caffe2.ai/databases/resnet_trainer.zip to the location
   you have placed this data in your local disconnected network


Once you have run them all you can connect into the driver pod and run nvidia-smi to see that
the GPU is working

 


 
