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
The conf value can be changes according to the desired threshold 
8) A folder named "crop" is created with the polyps segmented pictures, and in "runs/detect/exp" the results of the boxs segmentes over the original picture with the prediction made of the polyp is written on the original picture.