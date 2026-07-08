# ActiveDirectoryLab

<h1>Active Directory</h1>


<h2>Description</h2>
Project consists using Azure to gain familiarity with the cloud service. I started by creating a Resource Group. After that a Storage Account was added to it. Once that is done, I created a simple text file and uploaded it to the Storage Account. From Azure, I edited the text file and saved it locally under a new file name. Afterwards I delete the entire Resource group from Azure and check on Cost Analysis.
<br />


<h2>Utilities Used</h2>

- <b>Microsoft Azure</b> 
- <b>Remote Desktop Connection</b>

<h2>Lab walk-through:</h2>

<p align="center">
Create Resource Group and Virtual Network <br/>
<img width="572" height="387" alt="image" src="https://github.com/user-attachments/assets/ad96da6e-f031-4389-a140-de28abdc6331" />

<br />
<br />
Create Domain Controller:<BR>
<img width="647" height="577" alt="image" src="https://github.com/user-attachments/assets/f3dde99b-d014-4b9e-9b7c-3da537d8380b" /><BR><BR>
Create Client VM: <BR>
<img width="647" height="486" alt="image" src="https://github.com/user-attachments/assets/c1a8b974-1cd9-4185-add4-efb669163991" />
<BR><BR>
Set Domain Controller private IP to static.<BR><BR>
To do this in Azure I went to the DC1 VM into Network and Network Settings and clicked the virtual NIC
<img width="846" height="528" alt="image" src="https://github.com/user-attachments/assets/f23f0ee6-8cb7-4c64-bbd8-e4799106480f" />

  
