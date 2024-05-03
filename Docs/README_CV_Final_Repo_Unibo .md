# Computer Vision Final Repository (UniBo) [[Repo link](https://zenodo.org/records/11091938#:~:text=10.5281/zenodo.10956705.)]

## Repo structure
In the context of the SHEET project, **Unibo worked on computer vision applications** to automate data collection for future applicaiton. The presented repository contains all the computer-vision related datasets and models developped during the project.
Below a brief explaination of the directories of this repository and their content.

### *dataset* directory
In the **dataset** folder are stored the image dataset generated for the project.\
Each dataset contains images and annotations in both [YOLO detection format](https://docs.ultralytics.com/datasets/detect/#supported-dataset-formats) and [Supervsely format](https://docs.supervisely.com/customization-and-integration/00_ann_format_navi) and a ***'dataset_composition.yaml'*** file describing for each dataset the composition, the labelled class numerosity, related trained models and other informations.\
The dataset available are the following:

#### YOLOv5
The choice of implementing YOLOv5 was made because of those models are fast, accurate and simple to be trained, making them suitable to infere in real-time with field conditions.

- ***on_tree_apple_detector*** - dataset used to train YOLOv5 detection models for **apple fruit detection**. 
  
- ***on_tree_grape_detector*** - dataset used to train YOLOv5 detection models for **grape cluster detection**

- ***trunk_detector_apple_rgbd*** - dataset used to train a YOLOv5 detection model to detect **trunks in apple orchards**

#### YOLOv8 
The choice of implementing YOLOv8 was made because of those models are lightweight and optimized to run faster on smartphone applications (**TBD - link the realesed app** . Furthermore, differently from YOLOv5, YOLOv8 also provides models for classification and segmentation tasks.

- ***sb_detector*** - dataset used to train YOLOv8 detection model needed to **detect apple fruit** within images shot with smaprtphones and at close distances. The model was then used to make a first detection of fruits to be fed to the sb_classifier model able to classify the level of sunburn symptoms.

- ***sb_classifier*** - dataset used to train a YOLOv8 classification model needed to  **classify the fruit sunburn symptops**. The dataset is composed of fruit-level images generated from the detection bounding box of the trained model "Detector_sb_apples_Y8s".


### *models* directory
Here are stored the YOLO models trained on the datasets described above. Each model presents its own directory containing the training results, plots, metrics etc. The models are the following:

#### YOLOv5
- '***on_tree_apple_detector_Y5l***' - YOLOv5-large detection models trained to **detect apple fruits when framing the whole tree**. training was done to improve performance in detect fruit using Intel realsense D435 **RGB(-D) images**
- '***on_tree_apple_detector_Y5s***' - YOLOv5-small detection models trained to **detect apple fruits when framing the whole tree**. training was done to improve performance in detect fruit using Intel realsense D435 **RGB(-D) images**; trained for testing real-time application.
- '***on_tree_grape_detector_Y5l***' - YOLOv5-large detection models trained to **detect grape cluster when framing the whole tree**. training was done to improve performance in detect fruit using Intel realsense D435 **RGB(-D) images**
- '***trunk_detector_apple_Y5s***' - - YOLOv5-small detection models trained to **detect apple tree trunks when framing the whole tree**. training was done to improve performance when using Intel realsense D435 **RGB(-D) images**


#### YOLOv8
- '***Detector_sb_apples_Y8s***' - YOLOv8-det detection model used to **detect the foreground apple fruit** of a picture to be later feed in the '*Classifier_sb_apples_Y8s*' for sunburn symptomps classsificaiton; it works with **high quality** smartphone pictures done at **max 1 meter** distance from the fruit
- '***Classifier_sb_apples_Y8s***' - YOLOv8-cls classification model used **to classify apple sunburn damages** on the detection bounding box obtained by the application of '*Detector_sb_apples_Y8s*'.


### *examples* directory
Here are contained the resulting examples obtained by running the "*cascade_classification.py*" algortihm  present in the *src* directory. More details below


### Code Scripts - '*src*' directory
Here are present code scripts use to manage the data or train the models:
- '***cascade_classification.py***' - code to run the **apple detection + sunburn classification** on smatphone images
- '***classification_dataset_balancing***' - code to **balance image numerosity** based on the lowest represented class
-  '***classification_dataset_creator*** - code to **create dataset for classification training** by extracting detected object in the images and saving them in a dedicated folder named with the class for later classification training. 
-  '***dataset_metadata_parser_CLI***' - code to **get dataset infos** from the ' *dataset_composition.yaml* ' file 
-  '***dataset_train_val_test_split_CLI***'  - code to **random split in train_val_test** labelled images
-  '***dataset_train_yolov8_CLI***' - **custom code for trainig YOLOv8-cls classification models**