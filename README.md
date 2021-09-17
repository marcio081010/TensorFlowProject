# Tensor Flow Project

## To use tensorflow it is necessary to follow the following steps

#### 1.Set up and install TensorFlow and OpenCV on your Raspberry Pi by following this great guide by Evan https://github.com/EdjeElectronics/TensorFlow-Object-Detection-on-the-Raspberry-Pi/blob/master/Object_detection_picamera.py The guide walks through the following steps:

##### Update the Raspberry Pi

##### Install TensorFlow

##### Install OpenCV

##### Compile and install Protobuf

##### Set up TensorFlow directory structure and the PYTHONPATH variable

#### 2. Make sure your camera is configured by following these instructions https://www.raspberrypi.org/documentation/configuration/camera.md
#### 3. Download or clone this Repo and put the open_cv_group_detection.py in your /object_detection directory
#### 4. (optional) Customisation

- Select a custom model and number of objects (as described in the repo referenced in step 1).

#### For this example I used the same coco model as the boilerplate code but depending on what you want to detect and how accurate you need the model to be, other models can be easily referenced in the code instead. Check out https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md for more resources or have a go at training your own model if you have the necessary hardware https://github.com/EdjeElectronics/TensorFlow-Object-Detection-API-Tutorial-Train-Multiple-Objects-Windows-10.

- Select which objects to include in the log file
 # pulling raw output from object detection. Creates a list of dicts 
 
        # with details of each of the objects meeting the threshold in a given frame.
        Validobj = [category_index.get(value) for index, value in enumerate (classes[0]) if scores [0,index]>0.5]
        
        # Choose your object
        to_detect = 'person' 
        
- Select which criteria to apply for logging in the evidence stamp

        # Creates a log if the chosen object has been detected.
        if Validobj:
            data = [i["name"] for i in Validobj]
            # If in the given frame the number of a given object detected meets the condition then a log is made   
            if data.count(to_detect)>2:
                # Writes a line with how many of the object was detected along with a timestamp
                Summary = ["There is a group of " + str(data.count(to_detect)) + " people" ,time.ctime()]
                print(Summary)
                
                evidence_stamp = [data.count(to_detect),to_detect,time.ctime()]
                output.append(evidence_stamp)
                
- Specify the save location for the log file and image captures (by default this is the working directory). The log file includes a column for number of objects, object type and timestamp. See evidence.bmp for a sample image capture and output.png for a sample log file.

#### 5. Run the open_cv_group_detection.py from your /object_detection directory. To safely stop the process and save outputs press 'q' on the object viewer or Ctrl + C in the command line to exit.

