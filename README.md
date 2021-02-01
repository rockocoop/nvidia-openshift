# nvidia-openshift


``Procedure for running Nvidia GPU Operator 1.3.1 in a disconnected environment``

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



 


 
