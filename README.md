# YOLOv4_Geimer

# Object Detection with YOLO

## Functions
#### I Test (Detection)
- Use our trained YOLOv4 model to detect trucks, excavators, wheel loaders, bulldozers, dumpers, person and cars.
#### II Training
- Train a YOLO model with your own dataset.

## I Test (Detection)
#### Step 1. Clone Darknet to local
```sh
git clone https://github.com/AlexeyAB/darknet.git
cd darknet
```
#### Step 2. Modify the Makefile（since your computer is not suitable for GPU, please do not use this step）
- In the directory **darknet**, there is file called **Makefile**. Before building the darknet, we need to modify some varibles.
- If the NVIDIA driver, CUDA and CuDNN are installed, and the version of CUDA >= 10.2, we can change `GPU=0` to `GPU=1`, `CUDNN=0` to `CUDNN=1`, in order to use GPU acceleration.
- If OpenCV is installed, and the version of OpenCV >= 2.4, we can change `OPENCV=0` to `OPENCV=1`, in order to accelerate the image pre-processing.
- You can mannually change these variables in **Makefile**, or directly run the following commands in Terminal:
```sh
sed -i 's/GPU=0/GPU=1/' Makefile
sed -i 's/CUDNN=0/CUDNN=1/' Makefile
sed -i 's/OPENCV=0/OPENCV=1/' Makefile
```

#### Step 3. Build the Darknet
Run `make` in the Terminal. This step may need more than one minute.
```sh
make
```
#### Step 4. Prepare the configuration files
- Run the following commands in Terminal to make a folder **cfg**, so that configuration files could be neatly organized.
```sh
cd cfg
```
- Run the following commands in Terminal. **yolov4.cfg** contains the network structure and basic training parameters of YOLOv4. **obj.names** contains the class names of our model. **obj.data** contains the custom files we need.
```sh
wget https://raw.githubusercontent.com/XiangYusheng/YOLOv4_Geimer/main/KIT.cfg
wget https://raw.githubusercontent.com/XiangYusheng/YOLOv4_Geimer/main/KIT.names
wget https://raw.githubusercontent.com/XiangYusheng/YOLOv4_Geimer/main/KIT.data
cd ..
```

#### Step 5. Prepare the weight file
- Download our pre-trained weight file from the following URL, so that the YOLOv4 model could be directly used to detect trucks, excavators et al.
```
https://drive.google.com/file/d/1vhK-e2nDTJy3T_u7RyPW0DmJIN2gfMnP/view?usp=sharing
```


#### Step 6. Test your own images with this trained model
Run the following commands to test your own images. `chmod +x darknet/darknet` is used to make the `darknet` executable. `example.jpg` is your own images to be detected. 
```sh
chmod +x darknet
./darknet detector test cfg/KIT.data cfg/KIT.cfg yolov4_CM.weights -ext_output data/000001.jpg
```



