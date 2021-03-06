# Vehicle-Traffic-Analysis
This repository contains all source codes relevant for 
- **Training Vehicle Detection Model**
- **Vehicle Detection and Counting**
- **Calculating Flow of Vehicles**
- **Converting pixel velocity of vehicles to real Velocity**  

Open **Traffic_Analysis.ipynb** to begin.
There are four main sections in this notebook:
1. Yolo Training
2. Yolo Vehicle Detection
3. Vehicles Counting
4. Vehicle Velocity


## DataSet
The data gathered was of 2 busy roads of Lahore. All Videos were created on pedestrian bridge with the view of the road. One video was created on Main Boulevard Gulberg, Lahore opposite Hafeez Center. The other video was created on Main Boulevard New Garden Town, Lahore opposite Mughleazam Fort. For each location we made 2 videos one at day time and one at night. 

![Sample Image](/images/102.jpg)

The dataset created can be found at: [Dataset](https://drive.google.com/drive/folders/1VanRHJXye_qZtC-NbMLV-C7PLa92bSyh)

The dataset is in the video (.avi) format. 

## Training
For annotating the data, [Yolo Annotation tool](https://github.com/ManivannanMurugavel/YOLO-Annotation-Tool) is used.

For training, go to the Yolo training section of this notebook, and copy [Training data](https://drive.google.com/drive/folders/1N14gy_stPiMX-A_lehIp8zbw7ovR2zmH?usp=sharing) into google colab runtime. 

Training data contains: 
1. Labels 
2. Images(resized to 500 * 400)
3. process.py 
4. darknet folder. 



Darknet Folder Tree is below:  
  
  
  ```
    -- Darknet
        |-- Images
        |   |-- 0.jpg
        |   |-- 0.txt
        |   |-- 1.jpg
        |   |-- 1.txt
        |   |-- ...
        |   |-- 150.jpg
        |   |-- 150.txt
        |-- Labels
        |   |-- 0.txt
        |   |-- 1.txt
        |   |-- ...
        |   |-- 150.txt
        |-- Backup
        |-- Cfg
        |-- ...
        |-- process.py
        |-- darknet53.conv.74
  ```
    
Once folder looks like this, run process.py. It will split the train and test data and create train.txt and test.txt. These files will contain the paths to each image.

To run the process.py run the following command:
``` !python process.py -a Images -p 10 ```

This 10 here represents the number of images to be added in test data. You can modify this number.

This section is self explanatory with subsections and comments in it. You just need to change the paths to the folders in the top cell of this section.
This will create .weights file which will be used in the testing process. 

## Vehicle Detection
Go to YOLO Vehicle Detection of the notebook, this section is self explanatory and contains subsections, headings and comments.
### Requirements:
- Frames/Video
- Model (.weights file)

There are Three Subsections in this notebook:
- Converting video to frames
- Resize images
- Vehicle Detection

You only need to run the first section if you have the data in shape of a video. If data is in format of frames you need to start from subsection 2. For the vehicle detection section, you need to copy model i.e. .weights file which was created during training. 

You can also download the [PreTrained Model](https://drive.google.com/drive/folders/1cSdMmaqEOPNbFAFb2kRGXTNqbGW3d0bi?usp=sharing)

You only need to change path to directories in top cell of this section and run the rest of the cells as it is in the Vehicle Detection section.

This will create 2 text files. 
1. Text file containing center cordinates of vehicles (will be used in vehicle velocity section)
2. Text file containing bounding box cordinates with their respective classes (will be used in vehicle counting section)

Sample output of yoloV3:

![Sample Image](/images/Yolo_result.jpg)


## Vehicle Counting

In the Vehicle Count Section, set the path to the directories in the top cell of this section. Run all the cells in the section, it will create a folder containing frames displaying vehicle count wrt to their classes.

### Requirements
- Text file containing bounding box cordinates, generated through Yolo Vehicle Detection
- Text file containing pixel cordinates of counter lines ([Sample](https://drive.google.com/drive/folders/1DHIZhIU-C_vw_knp2xmp5R08RUZ6kA9G?usp=sharing))
- Frames


## Calculating Flow of Vehicles:

This is the Google Colab Notebook implementation of NVIDIA-FlowNet2-pytorch at: [FlowNet2](https://github.com/NVIDIA/flownet2-pytorch)

### How to run:
 
1. Open the notebook in Google Colab
2. Ensure you are running on GPU from 'Runtime'
3. Run the first cell and check which GPU is running. Tesla P100-PCIE or Tesla T4 work currently. Tesla T4 may give an error THCudaCheckError, however it will work. Tesla K80 will not work.
4. If those are not the GPU being used, then go to 'Runtime' > 'Factory Reset Runtime'. Repeat until you get either of the GPU.
5. Carefully change the path to directories.

This will generate .flo files for all the frames which will be further used in vehicle velocity part

### Important:
Before moving to Vehicle Velocity section you need to run lin_inter.py on your system. This will not work on google colab as it does not suppost the click event on immages. You need to manually mark the two lines on the road representing same actual length in meters, and 4 corners representing the road. This will generate text file which will be further used in Vehicle Velocity.

Or go to this [link](https://drive.google.com/file/d/14HI2BT2Q2a-czhwybB3A-5RFnq4uLay2/view?usp=sharing), this text file is generated for gulberg dataset and can be used in vehicle velocity part directly.  

## Vehicle Velocity
Go to Vehicle Velocity Section, you need to set the path to the directories in the top cell of this section.

### Requirements
- Text file containing center pixel cordinates of vehicles
- Text file generated by lin_inter.py
- Flo files for all frames
- Frames

It will generate images with vehicle velocities.

Sample output:
![Sample Image](/images/216.jpg)







