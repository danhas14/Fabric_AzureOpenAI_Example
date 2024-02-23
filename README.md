# Using Azure OpenAI Endpoints Natively in Microsoft Fabric

A useful feature in Microsoft Fabric is the ability to use some Azure AI services, like Azure OpenAI, directly in Fabric without having to deploy a separate endpoint. Per the Fabric documentation, "Fabric seamlessly integrates with Azure AI services, allowing you to enrich your data with prebuilt AI models without any prerequisite. We recommend using this option as you can utilize your Fabric authentication to access AI services, and all usage are billed against your Fabric capacity. This option is currently in public preview with limited AI services available.

https://learn.microsoft.com/en-us/fabric/data-science/ai-services/ai-services-overview

This tutorial will walk you through implementing a simple use-case leveraging the Fabric native Azure OpenAI endpoint. 

To start, open up Microsoft Fabric and create a new Lakehouse by selecting 'Create' in the top left hand corner and then selecting 'Lakehouse' as shown in the image

<img width="929" alt="image" src="https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/f3f6cacc-7095-4e53-a978-d4c12911bc54">


For the name of the Lakehouse, type Reviews_Lakehouse as shown below and then hit Create:

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/40f25173-1441-47cb-8db2-f8c4304b2df4)

Now lets upload some data we can use in the lakehouse. See the attached CSV file McDonalds Reviews and download it to your desktop. Once you do that, go back to your new Fabric Lakehouse and upload the data as shown in the following picture by selecting 'Upload Files':

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/032b59bd-cf55-42ed-a109-8160986e0af5)

Select the file you just downloaded to upload:

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/5b760906-90c2-4f08-a007-42f037986ddf)

You should see the file show up in the Files section of the Lakehouse if the upload was successful:
![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/5338857e-3e02-40e9-9944-a0fda6db9c20)

Now right click on the file and select 'Load to Tables' to load the data into a Fabric lakehouse table.

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/d51831d2-3eff-45b8-a932-c5553a4dcc03)

Select 'Load'

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/7800b110-9dea-4a47-be08-1c2968ccd78e)

Now select the Tables folder in the lakehouse and right click and select 'Refresh'. There should be a new mcdonalds_reviews table created from the CSV. 

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/51c63f53-d27e-414d-9b25-27e653fbfeaa)

Note the table will have blanks in the review_topic column and review_sentiment columns. We will have OpenAI populate the data for those columns in just a minute.

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/8246548d-1e97-43d8-8d78-24e88079c42c)

Now download the attached file 'Fabric OpenAI Restaurant Reviews.ipynb'. 

Next, select the icon on the bottom left side of the Fabric UI and select 'Data Engineering'. Once in the Data Engineering area of Fabric, select the 'Import Notebook' icon. Select the 'Upload' icon to select the Fabric OpenAI Restaurant Reviews.ipynb file you just downloaded. 

<img width="623" alt="image" src="https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/f6395566-faf0-4648-92f7-abcd45294e2d">


Now select and open the notebook you just imported. 


![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/a4f23d37-c29f-401e-bd14-7e4cdc2281e9)


On the left hand side, select 'Lakehouses' to associate our Reviews_Lakehouse with the notebook. At the prompt, select 'Existing Lakehouse', then 'Reviews_Lakehouse'. You should see something like below:


![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/f901e8e7-73cc-4163-a2cc-fe73798585c6)

Now run the first 3 cells in the notebook one at a time. Note it may take a minute for the Fabric Spark engine to initialize the first time you run it. The first cell will import the OpenAI library used in the notebook and the second cell will specify some categories we want Azure OpenAI to use to categorize the reviews. The 3rd cell will load the data from our lakehouse table into a Spark dataframe.

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/b1e7f7b2-74c6-4167-a6da-c299689676eb)

Now run the fourth cell. This cell will loop through each row in the table and then ask Azure OpenAI to provide any topics relevant to the review along with an over sentiment. You can see the prompt, or instructions, provided to Azure OpenAI on line 25-31 of the cell. Note we didn't have to provide an Azure OpenAI to call or a key since Fabric takes care of all of that for us. We just provide the Azure OpenAI model we want to use, which is gpt-35-turbo in this case. Lines 78-84 of the notebook do a Delta 'merge' command to merge the topics and sentiment returned by Azure OpenAI back into the table based using the unique _unit_id column as a key.

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/17933fcf-f909-4d31-8f3a-697a598ff9ad)

The fifth cell does a select from the table again, which now shows our updated rows based on the updates from Azure OpenAI.

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/f9ec18f9-3349-42ad-b086-14d594f37301)

Now select our Reviews_Lakehouse icon on the left hand side of the screen to return to the lakehouse view. 


<img width="344" alt="image" src="https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/4f2bb16a-e6f4-4f87-b9bb-8fc2dca29431">


On the top right side there is a drop-down where it says 'Lakehouse'. From the drop-down, select 'SQL Analytics Endpoint'


![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/ccbdad5b-cb90-4561-8f86-8ade7ff7752c)





