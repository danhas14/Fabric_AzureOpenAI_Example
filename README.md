# Using Azure OpenAI Endpoints Natively in Fabric

A useful feature in Microsoft Fabric is the ability to use some Azure AI services, like Azure OpenAI, directly in Fabric without having to deploy a separate endpoint. Per the Fabric documentation, "Fabric seamlessly integrates with Azure AI services, allowing you to enrich your data with prebuilt AI models without any prerequisite. We recommend using this option as you can utilize your Fabric authentication to access AI services, and all usage are billed against your Fabric capacity. This option is currently in public preview with limited AI services available.

https://learn.microsoft.com/en-us/fabric/data-science/ai-services/ai-services-overview

This tutorial will walk you through implementing a simple use-case leveraging the Fabric native Azure OpenAI endpoint. 

To start, open up Microsoft Fabric and create a new Lakehouse by selecting 'Create' in the top left hand corner and then selecting 'Lakehouse' as shown in the image

<img width="929" alt="image" src="https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/f3f6cacc-7095-4e53-a978-d4c12911bc54">


For the name of the Lakehouse, type Reviews_Lakehouse as shown below:

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/40f25173-1441-47cb-8db2-f8c4304b2df4)



![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/032b59bd-cf55-42ed-a109-8160986e0af5)

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/5b760906-90c2-4f08-a007-42f037986ddf)


![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/5338857e-3e02-40e9-9944-a0fda6db9c20)


![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/d51831d2-3eff-45b8-a932-c5553a4dcc03)

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/7800b110-9dea-4a47-be08-1c2968ccd78e)

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/51c63f53-d27e-414d-9b25-27e653fbfeaa)

![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/8246548d-1e97-43d8-8d78-24e88079c42c)


![image](https://github.com/danhas14/Fabric_AzureOpenAI_Example/assets/27227060/5fca0ec0-00a0-4416-ad4c-c807a6ed6638)



