# Google Street View To Detect Wildfire Risks
This is the first part of the senior capstone. This project uses Google Street View to collect the images for the dataset. In conjuction with labellbox the images uses object detection to train a DeTr HuggingFace model to label SDG&E equipment such as poles and transformers. First we needed to collect images and our section leader helped us out with this [jupyter notebook](https://github.com/pdashk/streetwatch/tree/master). The following information, until the "Part 1" title, were important to the project but it does not need to be repilcated to see the final model.

# Object Detection Model for Grading
Upload the [finetune_detr notebook](https://github.com/mjignacio/dsc180a-streetview/blob/main/notebooks/finetune_detr.ipynb) in a [Google Colab](https://colab.research.google.com) or use an environment with a NVIDIA gpu as it requires cuda cores to run. Then run through it and observe the results. This is the final form of the model but there is so much more information that it took to get here which is why there are so many extra files and info on this readme.

## Data Sources
Data for this project is collected from [Google Street View Static API](https://developers.google.com/maps/documentation/streetview/overview).

## Setup

### Conda Environment
After cloning repo, navigating to root level and run:
```
conda env create -f environment.yml
```

### Credentials
Store credentials in `.env` file and load using [python-dotenv](https://pypi.org/project/python-dotenv/).

### Training Data (DISCLAIMER since I've already collected the data you do not need to run this)
Create training data by running the following after setup is complete:
```
python scripts/collect_images.py
```
You do not need to run this I just included this to show that it was necessary for the 

# Project Structure

```
├── data/               <- Local data files only 
│
├── notebooks/          <- Jupyter notebooks
│
├── scripts/            <- Python scripts to run in command line
│
├── .env                <- Environment variables for the project
│
├── .gitignore          <- Git ignore file
│
├── environment.yml     <- Conda environment file
│
└── README.md           <- The top-level README for repo
```

# Part 1 Collection and Labelling

## Image Collection and Labeling
Using the Google Street View api I acquired imgages of 5 transformers and 5 poles from around San Diego at 3 different zooms and 5 angles totaling in 150 images. Then wrote a script in a Jupyter Notebook that uses the api to collect, name, and save images. Including supplementary functions that allow the image to be properly attained using a digital signature. After collecting the images I used [Labelbox](https://labelbox.com) to classify the fixtures for detection as poles or underground structures.

The image collection python files and COCOjson annotations were compiled on our domain website and I used some of them to train my models. They are included just for show because they were important but are not necessary to recreate the finetune_detr notebook. 

# Part 2 Fine tuning A DeTr Model and Collaboration
With a detection transformer model, based on Woctezuma's repository, I used multiple image collection scripts to finetune the model. I adjusted the code of Woctezuma's original notebook to pull the files from my repository and use the Google Street View Images as the dataset with their accompanying COCOjson annotations. To combine the json files into one file for the model, I found [this](https://github.com/mohamadmansourX/Merge_COCO_FILES) repository. 

The train2017.zip and custom_train.json files uses kelly.py and kelly.json made by Kelly Park and the val2017.zip and custom_val.json files use alex.py and alex.json made by Alex Denny. The train2017_large.zip file was made from the image collection scripts of Kelly Park, Sunny Kim, Alex Denny, and Phi Nguyen and the cooinciding "large" annotation file were also made with their work, while slightly modified. Additionaly the val2017_large.zip file was made with Noel Molina and Joshua Chuang's work with the matching annotation json file as well. I did not use my own files because there was a difference in my json annotation file that made it incompatible with the other files so I could not combine them. As I ran out of time I decided it was ok to just use my peer's data.

# Object Detection Model Restated
Upload the [finetune_detr notebook](https://github.com/mjignacio/dsc180a-streetview/blob/main/notebooks/finetune_detr.ipynb) in a [Google Colab](https://colab.research.google.com) or use an environment with a NVIDIA gpu as it requires cuda cores to run. Then run through it and observe the results.
## 
