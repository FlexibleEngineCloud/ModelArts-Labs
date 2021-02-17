# Using a Notebook for Handwritten Digit Recognition

ModelArts provides the notebooks for AI engineers. Engineers can prepare data, train models, and perform prediction in notebooks.

This section describes how to use MoXing to develop a handwritten digit recognition application, helping you quickly learn about AI development with notebook instances on ModelArts.

MNIST is a dataset containing handwritten digits, and is often used as an introductory example of deep learning. In this example, model training and prediction code (provided by ModelArts by default) for the MNIST dataset are compiled using the MoXing interface. You can use this example to complete model training in a notebook and upload images for prediction.

Before you start, carefully complete the preparations described in Preparations. To use a notebook to build a model, perform the following steps:

Step 1: Prepare Data
Step 2: Use a Notebook to Train a Model and Perform Prediction
Step 3: Delete Related Resources to Avoid Unnecessary Billing

Preparations
You have registered with HUAWEI CLOUD and checked the account status before using ModelArts. The account cannot be in arrears or frozen.

You have configured access authorization for the current account. For details, see Configuring Agency Authorization. For users who have been authorized using access keys, you are advised to clear the authorization and configure agency authorization.

You have created a bucket and folders in OBS for storing the sample dataset and model. In this example, create a bucket named test-modelarts and folders listed in Table 1.

For details about how to create OBS buckets and folders, see Creating a Bucket and Creating a Folder. Ensure that the OBS directory you use and ModelArts are in the same region.

Table 1 Folder list
| Folder  | Usage |
| ------------- | ------------- |
| dataset-mnist  | 	Stores the dataset.  |
| mnist-MoXing-code  | Stores the compiled model code file mnist_example.ipynb.  |
| train-log  | Stores images for prediction.  |

In this example, ModelArts provides a compiled model code file mnist_example.ipynb. You need to obtain this file from GitHub. After the model training is complete, you need to upload the file to the specified location.
Go to the ModelArts-Lab project on GitHub, click Clone or download, and then click Download ZIP to download the project.
Figure 1 Downloading ModelArts-Lab

After the project is downloaded, decompress the ModelArts-Lab-master.zip file and obtain sample code file mnist_example.ipynb from the \ModelArts-Lab-master\official_examples\Using_Notebook_to_Create_a_MNIST_Dataset_Recognition_Application\code directory.
Upload the mnist_example.ipynb file to the mnist-MoXing-code folder of the test-modelarts bucket by referring to Uploading a File.
Prepare an image of 28 x 28 pixels with a white handwritten digit on the black background. For example, prepare an image named 7.jpg. The image contains a handwritten digit 7. Upload the prepared image to the train-log folder of the test-modelarts bucket for prediction.

Step 1: Prepare Data
ModelArts provides a sample MNIST dataset named Mnist-Data-Set. This example uses this dataset to build a model. Perform the following operations to upload the dataset to the OBS directory test-modelarts/dataset-mnist created in preparation.

Download the Mnist-Data-Set dataset to the local PC.
Decompress the Mnist-Data-Set.zip file to the Mnist-Data-Set directory on the local PC.
Upload all files in the Mnist-Data-Set folder to the test-modelarts/dataset-mnist directory on OBS in batches. For details about how to upload files, see Uploading a File.
The following provides content of the Mnist-Data-Set dataset. .gz is the compressed package.

t10k-images-idx3-ubyte: validation set, which contains 10,000 samples
t10k-images-idx3-ubyte.gz: compressed package file of the validation set.
t10k-labels-idx1-ubyte: labels of the validation set, which contains the labels of the 10,000 samples
t10k-labels-idx1-ubyte.gz: compressed package file of the validation set label
train-images-idx3-ubyte: training set, which contains 60,000 samples
train-images-idx3-ubyte.gz: compressed package file of the training set
train-labels-idx1-ubyte: labels of the training set, which contains the labels of the 60,000 samples
train-labels-idx1-ubyte.gz: compressed package file of the training set label
Step 2: Use a Notebook to Train a Model and Perform Prediction
After data preparation is completed, use a notebook to compile code for modeling. ModelArts provides a sample code file mnist_example.ipynb for handwritten digit image training and prediction based on MoXing.

Obtain the mnist_example.ipynb file and upload it to OBS, for example, test-modelarts/mnist-MoXing-code. For details, see Preparations.
On the ModelArts management console, choose DevEnviron > Notebooks and click Create in the upper left corner.
On the Create Notebook page, set required parameters by referring to Table 2, and click Next.
Table 2 Parameters in this example
| Parameter  | Description |
| ------------- | ------------- |
| Name  | 	Notebook instance name, which can be customized  |
| Auto Stop  | To avoid resource waste, enable auto stop and select 1 hour later.  |
| Work Environment  | Select Multi-Engine 1.0 (Python 3, Recommended).  |
| Resource Pool  | 	Select Public resource pools.  |
| Type  | Select GPU.  |
| Instance Flavor  | Select GPU: 1 x v100NV32 CPU: 8 vCPUs | 64 GiB. If you select Limited-time free, you may have to queue up for resources.  |
| Storage  | Select OBS and set Storage Path to the OBS path for storing sample files, for example, test-modelarts/mnist-MoXing-code.  |

On the Confirm tab page, check the configurations and click Submit to create a notebook instance.
On the Notebook management page, when the status of the created notebook changes to Running, the notebook is successfully created. In the Operation column, click Open. The Jupyter page is displayed.
On the Files tab page of the Jupyter page, you can see the sample code file uploaded in 1. Click the file name. The notebook details page is displayed.
On the notebook details page, select the kernel environment that matches the code environment as prompted, for example, TensorFlow-1.8, and click Set Kernel. If the following prompt is not displayed, skip the kernel environment configuration, and go to the next step.
Figure 2 Setting the kernel
On the notebook details page, the detailed description of the sample code file is provided, including data preparation, training model, and prediction.
Data preparation: Data has been prepared according to Step 1: Prepare Data. The dataset file is stored in test-modelarts/dataset-mnist/. The sample code provides the description of the dataset.
Model training
In the model training area, change data_url to the OBS path where the dataset is located in Step 1: Prepare Data. You can copy the OBS path from OBS Console, and change the OBS path to a path starting with obs://. The following gives an example:

---

data_url = 'obs://test-modelarts/dataset-mnist/'

---

After the code is modified, click Run from the first cell to run all the cells in the model training area. The run log is displayed at the end of the model training area. If information similar to the following is displayed, the model training is successful. The following log information indicates that the model training is successful and the model file is successfully generated:

---

INFO:tensorflow:No assets to write. 

INFO:tensorflow:Restoring parameters from ./cache/log/model.ckpt-1000 

INFO:tensorflow:SavedModel written to: b'./cache/log/model/saved_model.pb' 

An exception has occurred, use %tb to see the full traceback.

---

Prediction

After the model training is complete, upload an image and use the generated model for prediction. As described in Preparations, upload the 7.jpg file to the test-modelarts/train-log path for prediction.

On the notebook, change the value of src_path in the prediction area to the actual OBS path of the image. Use the OBS path starting with obs://.

---

src_path = 'obs://test-modelarts/train-log/7.jpg'

---

After the code is modified, click  Run from the first cell to run all the cells in the prediction area. The run log is displayed at the end of the prediction area. If information similar to the following is displayed, the prediction result is displayed. For example, the predicted handwritten digit in this example is 7. Compare the digits in the image and prediction result to check whether the prediction result is correct.

---

INFO:tensorflow:Running local_init_op. 
INFO:tensorflow:Done running local_init_op. 
INFO:tensorflow:Done running local_init_op. 
The result: [7] 
INFO:tensorflow:[1 examples] 
INFO:tensorflow:	[1 examples] 
An exception has occurred, use %tb to see the full traceback.

---
