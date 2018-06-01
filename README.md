# nvidia-docker based tensorflow-gpu object detection using transfer learning on Google Cloud Platform / Locally


## Quick
https://hub.docker.com/r/tfgpu/od/
```
nvidia-docker run -it -p 6006:6006 -p 8888:8888 -d tfgpu/od:1
```

## Detailed

a. Make sure that You have nvidia-docker https://github.com/NVIDIA/nvidia-docker
  installed as per the latest version on github

b. Make sure you are running Ubuntu natively on hardware and not in a VM, else enable
  GPU pass through
  
    i. Either install in a USB and make persistent and use Nvidia-docker to create a docker container
    
    ii. or install Ubuntu in a HDD and add an entry to the windows boot manager after you disable the secure boot in bios
    
c. make sure the the command shows your GPU’s
```
  docker run --runtime=nvidia --rm nvidia/cuda nvidia-smi
```  
d. Follow the steps
```
  i. docker login
  ii. docker pull tfgpu/od:1
  iii. nvidia-docker run -it -p 6006:6006 -p 8888:8888 -d tfgpu/od:1
  iv. docker
  v. docker ps ( and copy the docke id from the output)
  vi. docker exec -it _image_id_ bash
  vii. python train.py --logtostderr --train_dir=./models/model/train --pipeline_config_file=./models/model/faster_rcnn_resnet101_pets.config
  viii. in another terminal, docker exec -it _image_id_ bash
  ix. python eval.py --logtostderr --pipeline_config_path=./models/model/faster_rcnn_resnet101_pets.config --checkpoint_dir=./models/model/train --eval_dir=./models/model/eval
  x. in yet another terminal, 
    docker exec -it _image_id_ bash
  xi. tensorboard --logdir ./models/model/
  xii. when you want to save the changes, exit
  xiii. docker tag _image_id_ username/repo:tag
  xiv. docker commit _image_id_ -p username/repo:tag
```
