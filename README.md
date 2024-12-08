# Cloud-Assignment
Wine Quality Prediction Using PySpark on AWS EMR
This project involves building a Python application that leverages PySpark on an AWS Elastic MapReduce (EMR) cluster to train a machine learning model for predicting wine quality using public datasets. The model is then deployed using Docker containers for scalability and ease of deployment.
Project Overview
The main Python script (WineQualityTrainingAndPrediction.py) is designed to:
    - Read the training dataset from Amazon S3.
    - Train machine learning models (Logistic Regression and Decision Tree Classifier) on an AWS EMR Spark cluster.
    - Select the best model based on the F1 score.
    - Make predictions on the test data stored in S3.
    - Print the F1 score to evaluate the model's accuracy.
AWS Configuration
Amazon S3
1. Create a Bucket:
    - Create a new S3 bucket and upload the training and validation datasets.
    
 2. Upload the Training Script:
    - Upload WineQualityTrainingAndPrediction.py to the bucket.
    
  3. Store the Best Model:
    - Create a folder named bestmodel within the bucket to store the best model after training.
Amazon EMR
1. Set up the Cluster:
    - Use an EMR cluster with EC2 instances for distributed processing.
    
    2. Configure EC2:
    - Choose the Master EC2 instance from your cluster.
    - Add an inbound rule to the security group to allow SSH access from your IP.
    
    3. SSH Access:
    - Log in to the Master EC2 instance using PowerShell with the Public DNS and authenticate using the EC2 Key pair.
    
    4. Configure AWS Credentials:
    - Set up AWS credentials and session token.
    
    5. Run Setup Commands:
    - Execute the following commands on the EC2 instance:
      ```bash
      aws s3api get-object --bucket winequalityapp26 --key init.sh /home/hadoop/init.sh
      export ACCESSKey=access-key
      export SECRETKey=secret-key
      sh init.sh
      ```
Code Implementation
Training the Model
To train the model using the Wine Quality dataset, run the following command:
    bash - spark-submit WineQualityTrainingAndPrediction.py --train

Making Predictions
Once the model is trained, use the following command to make predictions:

    bash-python WineQualityTrainingAndPrediction.py --predict

Docker Implementation
Steps to Create and Manage Docker Images
1. Create the Dockerfile:
    - Prepare the Dockerfile with the necessary configurations and dependencies for the Python application.
    
    2. Create a Docker Repository:
    - Go to your Docker profile and create a new repository 
    
    3. Build the Docker Image:
    - Run the following command to build the Docker image:

      docker build -t winequalityapp26
     
    
    4. Tag the Docker Image:
    - After building the image, tag it for pushing to Docker Hub:
      bash
      docker tag winequalityapplication adesh26/ccpg2:V2

    
    5. Push the Docker Image to Docker Hub:
    - Push the tagged image to your Docker Hub repository:
  bash
      docker push adesh26/ccpg2:V2

    
    6. Pull the Docker Image:
    - When you need to pull the image from Docker Hub, use:
    bash
      docker pull adesh26/ccpg2:V2
      
    
    7. Run the Docker Image:
    - To run the Docker container, use the following command:
      ```bash
      docker run -v localfilepath:dockerfilepath -ti adesh26/ccpg2:V2 ValidationDataset.csv --predict
Conclusion
This project demonstrates how to train a machine learning model for predicting wine quality using distributed computing on AWS EMR and Docker for easy deployment. By leveraging AWS services, PySpark, and Docker, this solution scales efficiently and can be easily reproduced across various environments.
