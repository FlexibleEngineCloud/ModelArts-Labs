#  1.Preparations

## 1.1 Obtaining the Access Key and configuring ModelArts

When using the Training Jobs, Model Management, and Notebooks functions of ModelArts, you need to use Object Storage Service (OBS) to store data. Therefore, before using ModelArts to develop AI models, obtain access keys and add them on the ModelArts management console.

### 1.1.1 Obtaining an Access Key

1. On the ModelArts management console, hover over the username in the upper right corner and choose My Credentials from the drop-down list.
<p align="center">
 <img align="left" width="100" height="100" src="Images/credentials.JPG">
</p>
3. On the My Credentials page, choose Access Keys > Create Access Key.
![](Images/Picture2.png)
5. In the Create Access Key dialog box that is displayed, enter the verification code received by SMS or email.
6. Click OK and save the access key file as prompted. The access key file is saved in the default download folder of the browser. Open the credentials.csv file to view the access key (Access Key Id and Secret Access Key).

### 1.1.2 Adding an Access Key

1. Log in to the ModelArts management console. In the left navigation pane, click Settings. The Settings page is displayed.
2. Click Create Access Key and enter the obtained access key.
  – AK: Enter the value of the Access Key Id file in the key file
  – SK: Enter the value of the Secret Access Key file in the key file
3. Click OK. The access key is added.
![](Images/Picture3.png)
