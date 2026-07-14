# ActiveDirectoryLab

<h1>Active Directory</h1>


<h2>Description</h2>
Project consists creating a domain controller and a client VM, setting the DC as the DNS server for the client. After that I install and set up Active Directory onto the server. I then populate the server with users, edit a group policy, and simulate different actions that can be done with AD such as unlocking accounts and reseting password, as well as checking logs for failed logins.
<br />


<h2>Utilities Used</h2>

- <b>Microsoft Azure</b> 
- <b>Remote Desktop Connection</b>
- <b>Active Directory</b>

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
To do this in Azure I went to the DC1 VM into Network and Network Settings and clicked the virtual NIC<BR><BR>
<img width="846" height="528" alt="image" src="https://github.com/user-attachments/assets/f23f0ee6-8cb7-4c64-bbd8-e4799106480f" /><BR><BR>
Then I clicked on "ipconfig1" and selected Static under "Private IP address settings" and save my changes.<BR><BR
<img width="443" height="132" alt="image" src="https://github.com/user-attachments/assets/1e12f13e-327e-4db8-baae-c4d39da26421" />
<BR><img width="476" height="197" alt="image" src="https://github.com/user-attachments/assets/1d3fd1fd-fa42-449f-b4ce-383285221663" />
<BR><BR>
For the purpose of this lab, I disable the firewall in DC1.<BR><BR>
I run "wf.msc" <BR>
<img width="460" height="295" alt="image" src="https://github.com/user-attachments/assets/8c7e6659-502d-494f-800b-cd9729f672e1" /><BR><BR>
I go to "Windows Defender Firewall Properties"<BR>
<img width="409" height="149" alt="image" src="https://github.com/user-attachments/assets/473b3bac-4407-4d03-95f1-4ff683047200" /><BR><BR>
I switch the Firewall state to off in Domain, Private, and Public Profile tabs.<BR><BR>
<img width="419" height="87" alt="image" src="https://github.com/user-attachments/assets/6e45f6e0-bdc7-4dcd-9d9c-fd817485827b" /><BR><BR>
Next step is to set Client VM DNS settings to DC1's Private IP Address.<BR><BR>
<img width="312" height="42" alt="image" src="https://github.com/user-attachments/assets/da6d9e56-f94d-4b80-9323-9479eb60c3ab" /><BR><BR>
I ran into an issue where the private ip was considered invalid by Azure. I restarted DC1 and it accepted the ip. After the network changes have been saved, I restarted Client VM.<BR><BR>
<img width="1242" height="492" alt="image" src="https://github.com/user-attachments/assets/12b3b2a3-cf66-424a-b358-079edd51272f" /><BR><BR>
To verify that Client and DC1, I remote into Client and ping the private ip of DC1.<BR><BR>
<img width="681" height="278" alt="image" src="https://github.com/user-attachments/assets/21846a4b-3a18-474f-96cc-28bf0813e996" /><BR><BR>
Next I run ipconfig /all, and see that the DNS Server listed is the private IP of DC1.<BR><BR>
<img width="993" height="703" alt="image" src="https://github.com/user-attachments/assets/24c84555-07a3-4e46-af2f-a33a8f14f519" /><BR><BR>
Now I will be installing and setting up Active Directory. I remote into the domain controller, open Server Manager and click on "Add roles and features"<BR><BR>
<img width="1072" height="158" alt="image" src="https://github.com/user-attachments/assets/d3472542-e2ea-4d78-a4d2-934d351d4813" /><BR><BR>
I go to Server Roles and check Active Directory Domain Services and select Add Feature and install.<BR><BR>
<img width="675" height="238" alt="image" src="https://github.com/user-attachments/assets/72a5adfa-b5d5-48a4-8683-a3276bf63418" /><BR>
<img width="525" height="556" alt="image" src="https://github.com/user-attachments/assets/f0e4cdb4-bfe5-4345-a60c-31eb17d89b12" /><BR>
<img width="966" height="563" alt="image" src="https://github.com/user-attachments/assets/e1f3cb53-787c-4d91-9d86-d81f8a08c565" /><BR><BR>
Next I promote DC1 to a domain controller in Server Manager.<BR><BR>
<img width="430" height="194" alt="image" src="https://github.com/user-attachments/assets/7c360094-33e3-405d-a486-5f5108420e1b" /><BR><BR
I select Add a new forest in the window that pops up. I enter mydomain.com as the root domain name.<BR><BR>
<img width="568" height="207" alt="image" src="https://github.com/user-attachments/assets/84bcda67-c344-4962-bb13-ff493473d3cf" /><BR><BR>
After hitting next I set a Directory Serives Restore Mode password.<BR><BR>
<img width="574" height="151" alt="image" src="https://github.com/user-attachments/assets/9a6fd7d3-198e-4248-bc10-e2f6d5829cd3" /><BR><BR>
Next I click install under the Prerequisites Check and restart DC1.<BR><BR>
<img width="632" height="257" alt="image" src="https://github.com/user-attachments/assets/e3399afc-0b58-45fb-acd3-ba3fbde59fd4" /><BR><BR>
I log back into DC1 with the username mydomain.com\labuser<BR><BR>
<img width="505" height="157" alt="image" src="https://github.com/user-attachments/assets/7e55d5d3-7f55-4441-bf2f-f2db08d479a9" /><BR><BR>
In Active Directory Users and Computers, I am going to be adding a couple OUs. "_EMPLOYEES" "_ADMINS"<br><br>
<img width="747" height="570" alt="image" src="https://github.com/user-attachments/assets/b55b68f3-8415-432d-90d8-23ea6ed492ff" /><br>
<img width="290" height="217" alt="image" src="https://github.com/user-attachments/assets/5b890bf3-6b93-4c5d-b720-afe6ae78397f" />
<br>
<img width="318" height="227" alt="image" src="https://github.com/user-attachments/assets/cbf263c4-c833-47ac-a36c-1b9d3ccafbdc" /><br><br>
Next I will add a user Jane Doe in the _ADMINS OU.<BR><BR>
<img width="490" height="404" alt="image" src="https://github.com/user-attachments/assets/ef6f284f-f801-4e22-9157-cb5ab93f50b0" /><BR>
<img width="368" height="391" alt="image" src="https://github.com/user-attachments/assets/0126729c-a2a7-45ff-9798-4ea9709a4588" /><BR><BR>
Next I add Jane Doe to the Domain Admins security group. I right click Jane Doe and go to Properties. I go to the Member Of tab, click Add, and type Domain Admins.<BR>
<img width="516" height="481" alt="image" src="https://github.com/user-attachments/assets/0781c264-17e4-4ab1-afd7-8960305f0b49" /><BR><BR>
System > About > Domain or workgroup > Change <BR><BR>
<img width="662" height="733" alt="image" src="https://github.com/user-attachments/assets/7d472562-ffdc-4bec-80ee-316f7dbd5c0e" /><BR><BR>
Set the Domain as mydomain.com
<img width="382" height="90" alt="image" src="https://github.com/user-attachments/assets/fe75bd6f-4889-4a72-b04c-86fa9d1c7df3" /><BR><BR>
Admin login. I used jane_admin to confirm the domain changes and restart Client VM<BR><BR>
<img width="363" height="183" alt="image" src="https://github.com/user-attachments/assets/ab6414ea-980a-470a-961f-8236c49d05d0" /><BR><BR
From within DC1 I add a new OU "_CLIENTS" and add Client vm to it by dragging Client from Computers into _CLIENTS and confirm the move.<BR><BR>
<img width="796" height="348" alt="image" src="https://github.com/user-attachments/assets/f65fe373-4ed4-4f89-867a-737b680ac944" /><BR><BR>
I, then, log into the Client VM as Jane using mydomain.com\jane_admin and enable non-administrative users by going to System > About > Remote Desktop > Remote Desktop users > Add and type "domain users" and click Check Names and click Okay.<BR><BR>
<img width="448" height="332" alt="image" src="https://github.com/user-attachments/assets/20f16f0d-6fc2-47b2-8ea3-9623d6b2d927" /><BR>
<img width="292" height="271" alt="image" src="https://github.com/user-attachments/assets/a03e2ce6-3cd6-43bc-b8a7-6bb5f9ec4d5e" /><BR>
<img width="586" height="253" alt="image" src="https://github.com/user-attachments/assets/13e286d2-9f8e-4958-858b-3de94ef2ced7" /><BR>
<img width="208" height="115" alt="image" src="https://github.com/user-attachments/assets/70994fce-235a-4c79-a51f-1e0a9827f23b" /><BR><BR>
Withing DC1, I use a [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) created and provided by [Josh Madakor](https://github.com/joshmadakor1) to generate users for the directory using powershell.<BR><BR>
<img width="998" height="1068" alt="image" src="https://github.com/user-attachments/assets/de847ad4-a493-4f71-8ef8-5c7726577d60" />
<BR><img width="296" height="340" alt="image" src="https://github.com/user-attachments/assets/b50be491-dff7-4edf-aa29-cae79a985731" />
<BR>
<img width="575" height="363" alt="image" src="https://github.com/user-attachments/assets/0ee1e489-7ce5-4434-a90a-d4c9514662ff" /><BR><BR>
Now I will attempt to log in with one of the users generated.<BR><BR>
<img width="805" height="322" alt="image" src="https://github.com/user-attachments/assets/2c7f4bc7-4a81-4131-8ecd-b12af044cf7f" /><BR>
<img width="247" height="487" alt="image" src="https://github.com/user-attachments/assets/341aa31d-0397-4e70-8849-c6d69f4b8aed" /><BR><BR>
Set up a Group Policy Lockout rule<BR><BR>
<img width="446" height="178" alt="image" src="https://github.com/user-attachments/assets/ef97f0a9-ef86-4235-afcf-f0f7696ac72e" /><BR><BR>
From Group Policy Management go to Default Domain Policy, right click and select Edit.<BR><BR
<img width="515" height="303" alt="image" src="https://github.com/user-attachments/assets/fb08eb39-1f04-4223-83ae-bac7477d0f65" /><BR><Br>
This will take you to Group Policy Management Editor. From there go Computer Configuration > Policies > Windows Settings > Security Settings > Account Lockout Policies. Right click Account lockout threshold and select Propeties. From there I changed the lockout policy to 10 failed attempts.<BR><BR>
<img width="922" height="398" alt="image" src="https://github.com/user-attachments/assets/4d86b521-187f-4769-a1da-a0e0c0426644" /><BR><BR>
I then log into Client and jane_admin and force a gp update<BR><BR>
<img width="503" height="256" alt="image" src="https://github.com/user-attachments/assets/9921e96d-140e-462c-b90f-4e0c90512596" /><BR><BR>

Testing the Account Lockout rule by failing 10 logins with a user from the list randomly generated names.<BR><BR>
<img width="472" height="157" alt="image" src="https://github.com/user-attachments/assets/f9fcf836-90c0-4b74-a7ff-a6d1ba62c28e" />
<BR>
<img width="677" height="188" alt="image" src="https://github.com/user-attachments/assets/343d7259-0337-49f4-9dc2-980b1ef0f86e" /><BR><BR>
Now that the account is locked out, I will use Active Directory to unlock the account and log into Client with the user account.<BR><BR>
<img width="487" height="345" alt="image" src="https://github.com/user-attachments/assets/1df45a44-525a-4e5b-b358-3fd3d6c9bb25" /><BR>
<img width="370" height="463" alt="image" src="https://github.com/user-attachments/assets/5077e122-6138-4cf2-b4c0-50b73fc6c70e" /><BR>
I also reset the password for the user by finding his name in ADUC, right click his name and click Reset Password. I then enter a new password for him.<BR><BR>
<img width="471" height="320" alt="image" src="https://github.com/user-attachments/assets/6012731d-6f98-4ec5-ad9d-0c86e3bbee9d" /><BR><BR>
Enabling/disabling an account.<BR><BR>
<img width="351" height="114" alt="image" src="https://github.com/user-attachments/assets/333f31f5-23e7-491d-abc4-60af346253e7" /><BR>
<img width="333" height="118" alt="image" src="https://github.com/user-attachments/assets/ae5dcd9d-2e25-45aa-933e-fa830ebb0f55" /><BR>
Next I view the logs from the user's failed logins.<BR><BR>
In my domain controller I open Event Viewer and go Windows Logs > Security. I right click Security and select Find. I search for the user.<BR><BR>
<img width="250" height="225" alt="image" src="https://github.com/user-attachments/assets/58317e55-c080-4c7e-ab30-e543eae8c0da" /><BR>
<img width="789" height="371" alt="image" src="https://github.com/user-attachments/assets/746784f4-2829-46b8-9db0-f68a784ace37" /><BR><BR>
Here is the log of the user failing their login.<BR><BR>
<img width="767" height="610" alt="image" src="https://github.com/user-attachments/assets/20eef9c6-a0f2-4836-81f4-0aea6ceec1e7" />










































  
