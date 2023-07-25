This is a tutorial to use the following system for detecting and classifying polyps.

For detection:
1) Create a safe enviroment to run the code on. Using miniconda3 the command
    conda create -n yolov7_custom python=3.10
    conda activate yolov7_custom
2) Clone the repository to your computer. 
3)In the folder of yolov7 run in the conda prompt the following line
    pip install -r requirements.txt
4) Run 
    pip install -r requirements_gpu.txt
5)Run 
    python train.py --workers 1 --device 0 --batch-size 8 --epochs 25 --img 256 256 --data data/custom_data.yaml --hyp data/hyp.scratch.custom.yaml --cfg cfg/training/yolov7-custom.yaml --name yolov7-custom --weights yolov7.pt
The model is trained in the folder data/images, the labels are in data/labels.
6)After running, from the 'runs/train/yolov7_custom/weights' folder copy the best.pt and paste it in yolov7 folder 
7)Change the name for yolov7_custom.pt. Run the following line
python detect.py --weights yolov7_custom.pt --conf 0.5 --img-size 256 --source C:\Users\juana\Desktop\YOLOV7\yolov7-custom\tests\test --view-img --no-trace
The conf value can be changed according to the desired threshold 
8) A folder named "crop" is created with the polyps segmented pictures, and in "runs/detect/exp" the results of the original pcitures with the segmented boxes marking the polyps detected with the porcentege prediction of it.

For classidication:
For this stage pictures used should be segmented versions of the polyps, as the ones created by yolo in the folder "crop" mentioned before.
    Approach 1: Enter the folder "classification/approach 1", run all the code in GLCM_colorchanNew.ipynb jupyter notebook. The pictures in "train-yolo" is the training set of images and the "test" folder is the test set of images. 
    Approach 2: Enter the folder "classification/approach 2", run all the codes for the jupyter books. Denpending on the model you want to use for the extraction of deep features you can choose between the following CNNs:
        - DenseNet210
        - InceptionV3
        - MobileNetV2
        - ResNet50
        - ResNet152
        - VGG16
        - Xception
    In each code the 4 classifiers are available: SVM, Logistic Regression, Grabient Boosting and Random Forest. 
    The "traintest" is the folder with the image set for training and validating, the "tests" folder has the images set to test the system.