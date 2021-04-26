# Vehicle-Traffic-Analysis
This repository contains all source codes relevant for 
- **Training Vehicle Detection Model**
- **Vehicle Detection and Counting**
- **Calculating Flow of Vehicles**
- **Converting pixel velocity of vehicles to real Velocity**  

## DataSet
The data gathered was of 2 busy roads of Lahore. All Videos were created on pedestrian bridge with the view of the road. One video was created on Main Boulevard Gulberg, Lahore opposite Hafeez Center. The other video was created on Main Boulevard New Garden Town, Lahore opposite Mughleazam Fort. For each location we made 2 videos one at day time and one at night. 

The dataset created can be found at:

The dataset is in the video (.avi) format. 

## Training
For annotating the data, [Yolo Annotation tool](https://github.com/ManivannanMurugavel/YOLO-Annotation-Tool) is used. This is the link to the images used for training and their ground truth values [Training Data](). 

Training data contains: 
1. labels 
2. images(resized to 500 * 400)
3. process.py 
4. darknet folder. 

Open Train.ipynb, copy Training data into google colab runtime. 

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

train.ipynb is self explanatory with sections and comments in it. You just need to change the paths to the folders in the top cell of the notebook.
This will create .weights file which will be used in the testing process. Copy .weights file in the google drive so that it can be used in Vehicle Detection notebook.

## Vehicle Detection and Counting
Yolo_Vehicle_Detection.ipynb is self explanatory and contains sections, headings and comments.

There are Four Sections in this notebook:
- Converting video to frames
- Resize images
- Vehicle Detection
- Vehicle Count

You only need to run the first section if you have the data in shape of a video. If data is in format of frames you need to start from section 2. For the vehicle detection section, you need to copy model i.e. .weights file which was created during training. You only need to change path to directories in top cell of the notebook and run the rest of the cells as it is in the Vehicle Detection section.


## Calculating Flow of Vehicles:

This is the Google Colab Notebook implementation of NVIDIA-FlowNet2-pytorch at: [FlowNet2](https://github.com/NVIDIA/flownet2-pytorch)

### How to run:
 
1. Open the notebook in Google Colab
2. Ensure you are running on GPU from 'Runtime'
3. Run the first cell and check which GPU is running. Tesla P100-PCIE or Tesla T4 work currently. Tesla T4 may give an error THCudaCheckError, however it will work. Tesla K80 will not work.
4. If those are not the GPU being used, then go to 'Runtime' > 'Factory Reset Runtime'. Repeat until you get either of the GPU.
5. Carefully change the path to directories.






