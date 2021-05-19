## AzureDataShare
below are instruction on how to use Azure Data Share between two different Azure Tenants.

**at data "provider" subscription / tenant:**
  
1. register microsoft.datashare resource provider
2. create storage account for data provider
3. create a container
4. create a data share resource
	- it will be created a managed identity automatically

5. configure the data that will be shared in "data share" resource
	- select your storage account/container

6. configure RBAC for specific user/group that will manage this storage account
7. configure RBAC for storage account - it need to select a special role "storage blob data reader" and provide access to the managed identity created during data share resource creation
	- NOTE: if that step is not completed succesfully, you will have issues to send snapshot to consumer data store.

8. send a bunch of files from your laptop (on-prems) to Azure blob by using azcopy
	- install azcopy: 
		(https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)
	- send data with an azcopy command:
		(https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10#transfer-data)
		

**at data "consumer" subscription / tenant**

1. register microsoft.datashare resource provider
2. create a storage account that will consume (receive data from provider)
3. create a container at this storage account
4. create a data share resource
5. configure user/group that will work with data on this storage account (consumer) and data share and a resource group
6. configure RBAC for the managed identity created by Data share resource to the storage account
7. log in at azure portal with the user that are the owner/contributor of the storage account (consumer)
a. the same one that was "invited" at data share resource at provider subscription
8. access "data share invitation" resource (look for it at search field at azure portal) *** you don't need an account with email configured ***
9. look for the invitation received from provider and accept it
10. go to your data share (consumer) and configure "received shares" by mapping the provider data with consumer data blob
11. trigger a full snapshot to be sent from provider to consumer
12. install "cloudberry drive" from here : (https://www.msp360.com/drive.aspx?__hstc=41219965.f4eb6e85c68b2b45a6312b83219cdd30.1616002618653.1617876663464.1617900790554.27&__hssc=41219965.26.1617900790554&__hsfp=3952834721) and configure in one laptop as a test
	- you will need to have the storage account name and key
13. test azure blob access through windows file explorer as a network mapped drive
  
