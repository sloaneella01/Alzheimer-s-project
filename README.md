# Alzheimer's Detection

  This project employs image detection using the ResNet-18 framework to recognize various levels of Alzheimer's impairments. It categorizes the impairments into three classifications: No Impairment, Mild Impairment, and Moderate Impairment. 
  Neural networks learn to accomplish their tasks by processing data and adjusting themselves to improve the accuracy of their predictions. By providing our neural network with a set of images from Kaggle, we were able to train it to accurately classify different levels of Alzheimer's impairment

## The Algorithm

The algorithm throughout this project is based on neural networks. These networks learn to perform their tasks by processing data and adjusting themselves to improve prediction accuracy. As the network processes more data, it adjusts itself to minimize prediction error, thereby enhancing the model's performance. In this project, we focused on training our neural network with a set of images sourced from Kaggle. These images were processed and labeled to reflect different levels of Alzheimer's impairment. By leveraging this labeled dataset, our neural network was able to learn the distinguishing features associated with each level of impairment. To facilitate this process, we employed the NVIDIA Jetson Nano device, a powerful yet compact computing platform designed for AI and machine learning applications. The Jetson Nano's advanced processing capabilities enabled us to efficiently train our neural network, even with the complex and high-dimensional data presented by medical images. Through training and validation, we fine-tuned our model to achieve high prediction accuracy. 

![SS1](https://github.com/user-attachments/assets/594c7a29-9727-42ca-a059-8cf778147a8f)

## Running this project

1. First step is to have VS Code dowloanded and then make sure to connect to your remote window to do SSH (connect your nano).
2. The second step is to download this dataset from Kaggle "https://www.kaggle.com/datasets/lukechugh/best-alzheimer-mri-dataset-99-accuracy" and add it to a folder called "alzheimer"
3. Inside this folder add another folder and name it "val" then copy and paste everything from your train folder into the val folder.
4. Then inside the alzheimer folder add a text document called "labels.txt" and put all the levels of the three levels of imparments and save it.

![SS2](https://github.com/user-attachments/assets/889944d1-c716-4e66-a0dc-3313b79f5efd)

6. Go back into VS code and make sure you have your jetson inference folder downloaded.
7. Open a new terminal and do `cd jetson-inference` and once inside then run `./docker/run.sh` to run the docker container. You may have to re-enter your nvidia password at this step
8. From inside the Docker container, change directories so type `cd python/training/classification`
9. Now its time to run the script by typing `python3 train.py --model-dir=models/alzheimer data/alzheimer`
10. When running the model you can also specify the value of how many epochs and batch sizes you want to run. For example at the end of that code you can add: `--batch-size=NumberOfBatchFiles --workers=NumberOfWorkers --epochs=NumberOfEpochs`
11. Once it has trained you can now test the images. Exit the docker container by pressing Ctl + D.
12. On your nano, navigate to the jetson-inference/python/training/classification directory. Use `ls models/alzheimer/` to make sure that the model is on the nano. You should see a file called resnet18.onnx.
13. Set the NET and DATASET variables
NET=models/alzheimer
DATASET=data/alzheimer
14. Run this command to see how it operates on an image from the cat folder.
`imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/alzheimer/imagename.jpg outputname.jpg`

[View a video explanation here](video link)
