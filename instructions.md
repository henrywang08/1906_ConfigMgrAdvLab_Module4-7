#WorkshopPLUS - System Center Configuration Manager: Advanced Concepts and Cloud Services (1906)





===

#Module 4, Lab 1, Exercise 1 - Configure Client Settings

##Scenario

In this exercise you will:

	- make sure that the Compliance Settings feature is enabled

	- change a few client settings that will speed up the policy refresh the state messaging cycle.  

  
You will also configure the Powershell execution policy to unrestricted so the powershell script can be executed.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []On **NYCCFG** \(the Primary Server\), start the **Configuration Manager Console**.


1. []Open the **Administration** workspace and click **Client Settings**.


	!IMAGE[Screenshot](screens/1nelmok0.jpg)

	

1. []Open **Default Client Settings** and view the configuration for **Compliance Settings**. Verify that **Enable compliance evaluation on clients** is **Yes**.

	!IMAGE[Screenshot](screens/1bebebb7.jpg)

	

1. []Select **Client Policy**, and change the **Client policy polling interval \(minutes\)** to 5.

	> [!ALERT] It is not recommended to change the policy polling interval in a production environment. The value you have configured for this setting is to expedite processes in the lab environment.

	!IMAGE[Screenshot](screens/4cd15d6b.jpg)



1. []Select **Computer Agent**, and change **PowerShell execution policy** to **Bypass.**

	> [!KNOWLEDGE] You may also open a PowerShell console with administrative rights and run the following command:  
	>   
	> ***Set-ExecutionPolicy unrestricted*** and press **Y** upon confirmation request

	!IMAGE[Screenshot](screens/71b9c768.jpg)



1. []Select **State Messaging**, and change **State message reporting cycle \(minutes\)** to **1**.

	> [!ALERT] It is not recommended to change the state message reporting cycle in a production environment. The value you have configured for this setting is to expedite processes in the lab environment.

	!IMAGE[Screenshot](screens/de5b657b.jpg)



Now that you customized important client settings and verified that Compliance Settings is correctly enabled, you are able to proceed and start creating the configuration items we will use to check the evaluation state.

===

#Module 4, Lab 1, Exercise 2 - Create a Registry configuration item

##Scenario

In this exercise you will create the first configuration item. This configuration item will check for a registry value that determines if Remote Desktop is enabled.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Open the **Assets and Compliance** workspace and in the **Navigation** pane, click **Compliance Settings** &gt;**Configuration Items**.
 


1. []On the ribbon, click **Create Configuration Item**.


1. []In the **Create Configuration Item Wizard**, type +++*Remote Desktop Active*+++ for **Name**.

1. []Type +++*Check the registry for the correct value*+++ for **Description**.

1. []Verify that **Windows Desktops and Servers \(custom\)** is selected under **Settings for devices managed with the Configuration Manager client**.

1. []Verify that **This configuration item contains application settings** is **cleared**.

1. []Click **Categories**.  On the **Manage Administrative Categories** dialog, click **Create**.  Type +++*CMCS-LAB*+++ for **Create Administrative Category.**

1. []Click **OK** twice, and then click **Next**.

	!IMAGE[Screenshot](screens/0pfg1f1d.jpg)

1. []On the **Supported Platforms** page, clear the **Select All** checkbox and select **Windows Server 2019** and **Windows 10** Click **Next**.

	!IMAGE[Screenshot](screens/omro4m5l.jpg)


1. []On the **Settings** page, click **New**.



1. []In the **Create Setting** dialog, type +++*Terminal Server Is Active*+++ for **Name**.



1. []Type +++*Check the Terminal Server active state*+++ for **Description**.



1. []For **Setting type**, select **Registry value**.  Click **Browse**.



1. []On the **Browse Registry** dialog, type +++*NYCDC*+++ in **Computer name** , and click **Connect**.

	!IMAGE[Screenshot](screens/wvxtgtwb.jpg)



1. []In the Registry tree, browse to *NYCDC \\ HKEY\_LOCAL\_MACHINE \\ SYSTEM \\ CurrentControlSet \\ Control \\ Terminal Server*.  In the **Registry Value** pane, select **fDenyTSConnections**.



1. []Verify **Select the rule that defines compliance for the selected registry value** is selected.  Verify **The selected registry value must exist on client devices** is selected.



1. []Select **This registry value must satisfy the following rule if present** \(Operator and Value are automatically selected\).

	!IMAGE[Screenshot](screens/v0ifp2ox.jpg)






1. []Click **OK** to close the **Browse Registry** window.



1. []Click the **Compliance Rules** tab and view the created compliance rules, then click **OK** to close the Properties window.

	!IMAGE[Screenshot](screens/zvekclid.jpg)

	> [!KNOWLEDGE] **Question A:** How many rules have been created?  
	> **Question B:** Which severity has been automatically defined?



1. []On the **Compliance Rules** page, click **Next**. On the **Summary page**, click **Next**. On the **Completion page**, click **Close**.



You have now created the first compliance setting configuration item to check the state of a registry setting.  
  
System Center Configuration Manager has automatically created the compliance rules.

===

#Module 4, Lab 1, Exercise 3 - Create a File System configuration item

##Scenario

In this exercise you will create the second configuration item. This configuration item will check for a file version that determines the Windows Update agent version

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Open the **Assets and Compliance** workspace and in the **Navigation** pane, click **Compliance Settings** &gt;**Configuration Items**.


1. []On the ribbon, click **Create Configuration Item**.



1. []In the **Create Configuration Item Wizard**, type +++*WUA\_Version*+++ for **Name**.



1. []Type +++*Check the version from wuapi.dll*+++ for **Description**.



1. []Verify that **Windows Desktops and Servers \(custom\)** is selected under **Settings for devices managed with the Configuration Manager client**.



1. []Click **Categories**, select the **CMCS-LAB** category, and click **OK**. Click **Next**


	!IMAGE[Screenshot](screens/k0uv5e5u.jpg)



1. []On the **Supported Platforms** page, clear the **Select All** checkbox. Select only **Windows 10** and **Windows Server 2019** Click **Next**.

	!IMAGE[Screenshot](screens/pgc1ckpg.jpg)



1. []On the **Settings** page, click **New**.



1. []In the **Create Setting** dialog, type +++*WUA\_Version\_wuapi.dll*+++ for **Name**.



1. []For **Setting type**, select **File System**.  Click **Browse**.



1. []On the **Browse File System** dialog, ensure that **Computer name is** +++*NYCDC*+++, and click **Connect**.



1. []In the Folders pane, expand **NYCDC**, and navigate to +++**C:\\Windows\\System32**+++ and in the **Files** pane, select the file **wuapi.dll**.

	> [!ALERT] Make sure you scroll down since not all the files will load immediately

	!IMAGE[Screenshot](screens/4jkcgk1g.jpg)



1. []Ensure that **Select the rule that defines compliance for the selected file** is selected.  Ensure that **The selected file must exist on client devices** is selected.



1. []Select **The selected file must be compliant with the following rules**.  Click **Add**.  In **Add File Property**, for **Property**, select **File version**. For **Operator**, select **Greater than or equal to**. Ensure that Value is automatically selected \(for example, **10.0.17763.1**\) and Click **OK.**

	> [!ALERT] The actual version number may be equal to or higher than 10.0.17763.1.


	!IMAGE[Screenshot](screens/5tqmrzjo.jpg)



1. []Click **OK.**

	!IMAGE[Screenshot](screens/aul0hdjy.jpg)


1. []Click **OK** and then click **Next**. Configuration Manager has automatically created the compliance rules.

	
	!IMAGE[Screenshot](screens/1uzyf03l.jpg)



1. []On the **Compliance Rules page**, select the rule **wuapi.dll must exist**, and click **Edit**.

	!IMAGE[Screenshot](screens/23dw2gne.jpg)



1. []For **Noncompliance severity for reports**, select **Critical with event**, and click **OK**.

	!IMAGE[Screenshot](screens/25grsqei.jpg)



1. []Select the rule **wuapi.dll Version Greater than or equal to 10.0.17763.1**, and click **Edit**.

	> [!ALERT] **Note:** The version number in the rule name may be different. It will match the version of the wuapi.dll that you selected.
	

	!IMAGE[Screenshot](screens/wcgk0rha.jpg)



1. []For **Noncompliance severity for reports**, select **Warning**, and click **OK**.

	!IMAGE[Screenshot](screens/ao5ciklh.jpg)



1. []Click **Next**.  On the **Summary page**, click **Next** and then click **Close**.



You have now created the second compliance setting configuration item to check the Windows Update Agent version.  
  
System Center Configuration Manager has automatically created the compliance rules.

===

#Module 4, Lab 1, Exercise 4 - Create a Script configuration item

##Scenario

In this exercise you will create the third configuration item. This configuration item will execute a VBS script to query information from WMI. The configuration item validates the script response and then sets the compliance state.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Open the **Assets and Compliance** workspace and in the **Navigation** pane, click **Compliance Settings** &gt;**Configuration Items**.



1. []On the ribbon, click **Create Configuration Item**.



1. []In the **Create Configuration Item Wizard**, type +++*RemoteRegistry\_Service\_StartType\_State*+++ for **Name**.



1. []Type +++*Check if the Remote Registry Service is running and the start type is automatic*+++ for **Description**.



1. []Verify that **Windows Desktops and Servers \(custom\)** is selected under **Settings for devices managed with the Configuration Manager client**.



1. []Click **Categories**. Select the **CMCS-LAB** category, and click **OK**. Click **Next**.

	
	!IMAGE[Screenshot](screens/qet2mogk.jpg)



1. []On the **Supported Platforms** page, clear the **Select All** checkbox. Select only **Windows 10** and **Windows Server 2019.** Click **Next**.


	!IMAGE[Screenshot](screens/2cvhld3r.jpg)



1. []On the **Settings** page, click **New**.



1. []In the **Create Setting** dialog, type +++*RemoteRegistry\_Service\_State*+++ for **Name**.



1. []Type +++*Check the service state*+++ for **Description**.



1. []For **Setting type**, select **Script**.

	!IMAGE[Screenshot](screens/jfajfkg0.jpg)

1. []For **Data type**, select **String**

	!IMAGE[Screenshot](screens/rpvi4ctf.jpg)



1. []On the **Discovery Script** panel, click **Add Script**.


1. []For **Script language**, select **VBScript**. Type the VBS script included in the *Knowledge session* or, open the script from +++**\\\\NYCDC\\Software\\Lab Files\\Lab 2\\WUA\_Service\_StartType\_State.vbs**+++.

	> [!ALERT] The script queries WMI for the state of the Remote Registry service.  
	>   
	> As a result, the query returns the service startup type \(StartMode\) and state. The two strings are attached and a single echo prints the result. The result will then be verified against Configuration Manager Compliance rules.  
	>   
	> **Note**: When a script is used to verify a setting or state, only one echo will be checked
	
	> [!KNOWLEDGE]On Error Resume Next  
	> strComputer = &quot;.&quot;  
	> Set SWBemlocator = CreateObject\(&quot;WbemScripting.SWbemLocator&quot;\)  
	> Set objWMIService = SWBemlocator.ConnectServer\(strComputer,&quot;root\\CIMV2&quot;\)  
	> Set colItems = objWMIService.ExecQuery\(&quot;Select \* from Win32\_Service where Name ='RemoteRegistry'&quot;,,48\)  
	> For Each objItem in colItems  
	> wscript.Echo Ucase\(objItem.StartMode\) &amp; &quot;\_&quot; &amp; UCase\(objItem.State\)  
	> Next


	!IMAGE[Screenshot](screens/l05su00k.jpg)
	
	


1. []Click **OK** to close **Edit Discovery Script**.

	

1. []Verify in the **Discovery script** panel that the **Script status** reports **VBScript is created**.


	!IMAGE[Screenshot](screens/kmeccb4p.jpg)



1. []Leave all the remaining settings as default and click **OK** and then click **Next**.



1. []On the **Compliance Rules** page, click **New**.



1. []In **Create Rule**, type +++*Check Remote Registry Service state*+++ for **Name**.


1. []Type +++*Startup type must be Auto and state Running*+++ for **Description**.



1. []Click **Browse**. In the **Select Setting** window, select **RemoteRegistry\_Service\_StartType\_State \(current\)** CI Name under **Select configuration items to view available settings** and verify **RemoteRegistry\_Service\_State** setting is automatically selected under **Available settings in the selected configuration items** and then click **Select**.


	!IMAGE[Screenshot](screens/uzh5omni.jpg)



1. []On **Create Rule**, select **Value** for Rule type. For **The value returned by the specified script**, select **Equals**. Type +++**AUTO\_RUNNING**+++ for **the following values**. Verify that the **Report noncompliance if this setting instance is not found** check box is cleared. For **Noncompliance severity for reports**, select **Warning**. Click **OK** and then click **Next**.



	!IMAGE[Screenshot](screens/vgeova1j.jpg)



1. []On the **Summary page**, click **Next** and then click **Close**.



1. []Which types of settings items have you created?  
	Which types of severity can you define for a setting?

You have now created the third compliance setting configuration item to check compliance using a custom script  
  
System Center Configuration Manager has automatically created the compliance rules.  
  
Congratulations! You have now completed this Lab.  
  
In the next lesson you are going to create a baseline to deploy the settings to a collection of computers

===

#Module 4, Lab 2, Exercise 1 - Create a Compliance Baseline

##Scenario

In this exercise you will create a compliance baseline with the configuration items you created in the previous lab.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Open the **Assets and Compliance** workspace and in the **Navigation** pane, click **Compliance Settings** &gt;**Configuration Baselines**.



1. []On the ribbon, click **Create Configuration Baseline**.



1. []In the **Create Configuration Baseline Wizard**, type +++*LAB\_Baseline*+++ for **Name**.



1. []Type +++*Check RDP, WUA Version and Remote Registry service state*+++ for **Description**.



1. []Click **Add** and then click **Configuration Items**. In **Add Configuration Items**, from **Available configuration items**, select each configuration item created in the previous exercise and click **Add**.

	!IMAGE[Screenshot](screens/ds3cj11y.jpg)


1. []Click **OK** to close the **Add Configuration Items** window.



1. []Click **Categories**, select the *CMCS-LAB* category, and click **OK**.

	!IMAGE[Screenshot](screens/olp4pmyr.jpg)



1. []Click **OK** to close the **Create Configuration Baseline** window.



You have now created a configuration baseline made of three configuration items. In the next exercise you are going to deploy it to a collection of clients.

===

#Module 4, Lab 2, Exercise 2 - Create a Device Collection

##Scenario

To deploy the created baseline you need a collection with the clients that you will check against the configuration baseline.

1. []Open the **Assets and Compliance** workspace and in the **Navigation** pane, click **Device Collections.**



1. []On the ribbon, click **Create** and select **Create Device Collection.**



1. []In the **Create Device Collection** wizard, on the **General** page, type +++*CS\_LAB\_Collection*+++ for **Name**.



1. []Type +++**Check for RDP, Remote Registry and WUA settings**+++ for **Comment**



1. []Click **Browse**. On **Select Collection**, click **All Systems**, and then click **OK**. Click **Next**.


	!IMAGE[Screenshot](screens/e0b4ec0y.jpg)



1. []On the **Membership Rules** page, click **Add Rule** and then click **Include Collections**.



1. []On **Select Collections**, select **All Desktop and Server Clients**, and click **OK**.


	!IMAGE[Screenshot](screens/zgs3qr5q.jpg)



1. []Click **Next**, click **Next** and then click **Close**.





1. []Select the new collection **CS\_LAB\_Collection**. If you see a Member Count of **0** for the collection, click **Update Membership** on the ribbon, and after the collection updates, click **Refresh** or press **F5** to update the result pane.


	!IMAGE[Screenshot](screens/tccnv0hu.jpg)

	!IMAGE[Screenshot](screens/5raxmyj2.jpg)

	!IMAGE[Screenshot](screens/uggzqx2r.jpg)


You have now created a collection. You will deploy the baseline to that collection next.

===

#Module 4, Lab 2, Exercise 3 - Deploy the Configuration Baseline

##Scenario

In this exercise you will deploy the Baseline to the Collection created earlier

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Open the **Assets and Compliance** workspace and in the **Navigation** pane, click **Compliance Settings** &gt;**Configuration Baselines**.



1. []Select the baseline **LAB\_Baseline** and on the ribbon, click **Deploy**



1. []On **Deploy Configuration Baselines**, click **Browse**.  On **Select Collection**, change to **Device Collections**, select **CS\_LAB\_Collection**, and click **OK** and then click **OK**.

	> [!KNOWLEDGE] You can view the successful deployment of the baseline at the bottom of the console.


	!IMAGE[Screenshot](screens/rad11f3e.jpg)



1. []On the **Details** pane at the bottom, click the **Deployments** tab.

	!IMAGE[Screenshot](screens/fwgce4op.jpg)

	> [!ALERT] Wait at least five minutes for clients to start their policy polling cycle and get the newly created policy with the baseline and configuration items or manually update policy on each client from the Configuration Manager Control Panel on each client.

	> [!KNOWLEDGE] **Note**: You can start *Machine Policy Retrieval &amp; Evaluation Cycle* on the client, and click **Evaluate** in the **Configuration** tab to speed up the process. After the client has read the new compliance baseline deployment policy, it will start to evaluate the configuration items. If configuration items are not downloaded, they will be downloaded first, and the client will create a randomized schedule to evaluate the configuration items within 1440 minutes. The agent will create a state message item for each setting. The state messages are sent to the management point every 15 minutes \(default setting\), but in this lab environment, that setting has been changed to every one minute \(not recommended in a production environment\).



	



You have now deployed your baseline. The next step is to evaluate compliance on the clients

===

#Module 4, Lab 2, Exercise 4 - Validate the Compliance of Clients

##Scenario

In this exercise, you will be able to:  

- Assess each computer against the compliance baseline.
  

1. []Click **Start**, Type **Control Panel** and then click **Configuration Manager**. **Note:** If you cannot see the **Configuration Manager** in **Control Panel**, change **View by** to **Large icons**.

	> [!ALERT] To ensure that all machines have received the baseline, connect to each of these machines \( **NYCDC**, **NYCCFG**, **NYCCL1**\) and repeat the following steps on them.

1. []Select the **Configurations** tab.

	> [!ALERT] To ensure that all machines have received the baseline, connect to each of these machines \( **NYCDC,NYCCFG, NYCCL1**\) and repeat the following steps on them.

1. []Select the baseline **LAB\_Baseline** and click **Evaluate**. After a few minutes, on the **Compliance State** column you should be able to see **Compliant** as the compliance state. **Note:** **NYCCL1** will report **Non-Compliant.** We will address that later in the lab.

	!IMAGE[Screenshot](screens/es3odzow.jpg)
	!IMAGE[Screenshot](screens/dk3bdx3i.jpg)

	> [!ALERT] If you cannot see **LAB\_Baseline**, select the **Actions** tab, select **Machine Policy Retrieval and Evaluation Cycle** and click **Run Now**. Navigate back to **Configurations** tab and after a few minutes click **Refresh**.

	> [!ALERT] If NYCDC is showing as Non-Compliant, review **Remote Registry** Service Status, It should be **started.**

	!IMAGE[Screenshot](screens/qzgko0v5.jpg)


You have now completed the evaluation of the Baseline. In the next exercise you will check the compliance result uisng the Configuration Manager console



===

#Module 4, Lab 2, Exercise 5 - Check the Compliance State on the Console

##Scenario

In this exercise you will use the Configuration Manager console to check the Compliance State.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Launch **Configuration Manager Console**.

1. []Open the **Assets and Compliance** workspace and in the **Navigation** pane, click **Compliance Settings** &gt;**Configuration Baselines**.


1. []Select the baseline **LAB\_Baseline**

1. []Click the **Deployments** tab at the bottom. You should be able to see the overall compliance of the baseline expressed as a percentage. In case you don't see it, move on to the next step since you will probably need force a summarization \(which will be covered in a following step\)


	!IMAGE[Screenshot](screens/hfq5sraa.jpg)

1. []Select the deployment **CS\_LAB\_Collection**, and on the ribbon, click **View Status**. The console switches automatically to the Monitoring workspace and selects the LAB\_Baseline\_status to CS\_LAB\_Collection node in the Navigation pane. The Deployment Status pane shows the compliance status details.

	> [!ALERT] **Note**: If you expect a different result, resulting from a change in compliance, click **Run Summarization** and then click the **Refresh** link located on the top-right of Deployment Status pane. The client must send the state messages to the primary site. On the client, the **StateMessage.log** file can show you the information. Look for the line **Successfully forwarded state Message to the MP**.


	!IMAGE[Screenshot](screens/vqr3oayb.jpg)

Congratulations! You just checked the evaluation result using the console.

===

#Module 4, Lab 2, Exercise 6 - Run Compliance Settings Reports

##Scenario

In order to check the state of the compliance of the machines against a baseline, you can leverage the reporting infrastructure of Configuration Manager.  
  
The access to the reports can be accomplished in two ways:  
  

- Through the **Report** node in the console
- Through the **Reporting Service** web page

Now let us examine the compliance settings reports that are available and useful for our scenario:  
  
**Summary compliance by configuration baseline:** The summary compliance for a collection by configuration baseline report is the main report from where DCM troubleshooting usually begins.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Connect to **NYCCFG**. In Configuration Manager console, open the **Monitoring** workspace.



1. []In the Navigation pane, expand **Reporting**, click **Reports** and select the **Compliance and Settings Management** folder.

1. []Select the **Summary compliance by configuration baseline** report, and on the ribbon, click **Run**.


	!IMAGE[Screenshot](screens/uchyq430.jpg)

1. []Click **LAB\_Baseline**. The Summary compliance by configuration items for a configuration baseline report opens. It displays a summary of the compliance by configuration items in a specified configuration baseline. You can scroll to the right to view the Non-Compliant column, which shows the number of systems per configuration item that report compliant, non-compliant, or other states.


	!IMAGE[Screenshot](screens/1dngon5p.jpg)

1. []Click a linked number in the **Compliant** column. A new report opens up, **List of assets by compliance state for a configuration item in a configuration baseline** that lists the devices or users in a specified compliance state following the evaluation of a specified configuration item.

	!IMAGE[Screenshot](screens/w0vpzefv.jpg)

1. []Click the computer name in the **Device Name** column, and a new report opens: **Rules and errors summary of configuration items in a configuration baseline for an asset.** This report displays a summary of the compliance state of rules and any setting errors for a specified configuration item deployed to a specified device or user.

	!IMAGE[Screenshot](screens/tlkxp13j.jpg)

These reports displays a summary of the compliance state and additional details as well

===

#Module 4, Lab 2, Exercise 7 - Check the Compliance State Locally on the Client

##Scenario

To ensure that all machines have received the baseline, connect to the following server machines:  
  

- NYCDC
- NYCCFG
- NYCCL1


> Switch to @lab.VirtualMachine(NYCDC).SelectLink

1. []Connect to **NYCDC**. Click **Start**, select **Control Panel** and then click **Configuration Manager**.

	> [!ALERT] **Note**: If you cannot see the **Configuration Manager** in **Control Panel**, change **View by** to **Large icons**.



1. []Select the **Configurations** tab, select the baseline **LAB\_Baseline.**

1. []To verify the compliance, click **View Report**. A new browser page opens, and you will see the compliance state for each configuration item.


	!IMAGE[Screenshot](screens/jmhq5qud.jpg)

	> [!ALERT] **Note**: If **Remote Registry** Service is Stopped, Start the Service and Evaluate Compliance Again
	!IMAGE[Screenshot](screens/342dq4xa.jpg)
	

1. []Connect to **NYCCFG**, and repeat steps 1 to 3.

> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1. []Repeat steps 1 to 3.

	> RemoteRegistry\_Service\_StartType\_State will report as Non-Compliant.

	!IMAGE[Screenshot](screens/vwbmpak1.jpg)

You have now checked the compliance state locally on each client.

===

#Module 4, Lab 2, Exercise 8 - Review the Compliance after a Change Occurs \(Optional\)

##Scenario

In this exercise you will change settings to verify detection for non-compliant configuration items.

> Switch to @lab.VirtualMachine(NYCDC).SelectLink

1. []Connect to NYCDC. Open Services Console. Click **Start**, type **run** and on run windows type +++*Services.msc*+++


1. []Right-click **Remote Registry** and click **Properties**.



1. []Change Startup type from **Automatic** to **Manual** to and click **OK**.

	!IMAGE[Screenshot](screens/x0fwva35.jpg)

1. []Close **Services Console**

1. []In **Control Panel**, open **Configuration Manager**.

1. []Click the **Configurations** tab. Select the baseline **LAB\_Baseline** and click **Evaluate**. After a minute, in the Compliance State column you should see **Non-Compliant** as the state, and you should also see an updated timestamp in the Last Evaluation State column. 


	!IMAGE[Screenshot](screens/sfxav4fy.jpg)

1. []Click **View Report**. The browser opens a new page and you will be able to see that for one configuration item the compliance state changed to Non-Compliant with severity Warning.

	!IMAGE[Screenshot](screens/hdo3empu.jpg)

1. []Click the configuration item name and you are able to see the details of the rule that reports the non-compliance state. Verify the compliance history change by means of a Configuration Manager report.


	!IMAGE[Screenshot](screens/aic0jrvh.jpg)


> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Connect to **NYCCFG**. In Configuration Manager console, open the **Monitoring** workspace.



1. []In the Navigation pane, expand **Reporting**, expand **Reports**, and select the **Compliance and Settings Management** folder.



1. []Click **Compliance history of a configuration baseline**, and on the ribbon, click **Run**.

!IMAGE[Screenshot](screens/4wfkhukn.jpg)

1. []Set the following parameters:  
	  
	Baseline Name: LAB\_Baseline / Start Date: Today’s date / End Date: Tomorrow’s date / Device Name: NYCDC

1. []Click **View Report**, and after viewing the report, close the report. 

	
	!IMAGE[Screenshot](screens/ool1hmnq.jpg)

1. []In the Compliance and Settings Management report folder, select **Compliance history of a configuration item**, and on the ribbon, click **Run**.

	!IMAGE[Screenshot](screens/ldlq4pvn.jpg)

1. []Set the following parameters:  
	  
	Configuration Item Name: RemoteRegistry\_Service\_StartType\_State / Start Date: Today’s date / End Date: Tomorrow’s date / Device Name: NYCDC

1. []Click **View Report**, and after viewing the report, close the report.

	!IMAGE[Screenshot](screens/ydjx2gwk.jpg)

Congratulations! You have now completed this lab.

===

#Module 4, Lab 2, Exercise 9 - Create a Collection for Manual Remediation

##Scenario

In this exercise, you will be able to;  
  

- Create a collection based on non-compliance of the compliance items

One of the new features of Configuration Manager is the ability to remediate non-compliant machines. The auto-remediation feature works only with registry, WMI, or script settings.  
  
In this task, you will create a collection of non-compliant machines. If it is not possible to use the automatic remediation feature of Configuration Manager compliance settings, you may be able to target a software or script deployment to a collection of non-compliant computers, or use the collection to identify computers that must be manually remediated.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Connect to **NYCCFG** and open **Configuration Manager Console**.  Switch to the **Assets and Compliance** workspace.



1. []Navigate to **Configuration Baselines** in the Navigation pane. Select the baseline **LAB\_Baseline.** Click the **Deployments** tab at the bottom.


	!IMAGE[Screenshot](screens/cdd0w5dt.jpg)

1. []Select the **CS\_LAB\_Collection** deployment and on the ribbon, click **Create New Collection** and then click **Non-compliant**.

	!IMAGE[Screenshot](screens/qe110nex.jpg)


1. []On **Create Device Collection Wizard**, on the **General** page, click **Next**.

	!IMAGE[Screenshot](screens/s5dolset.jpg)

1. []On the **Membership Rules** page, notice that a query membership rule called **Noncompliant** has been automatically generated.

	!IMAGE[Screenshot](screens/dmeopz2z.jpg)


1. []Click **Next**, click **Next** and then click **Close**.

1. []In the Navigation pane, select **Device Collections**.

1. []Select **LAB\_Baseline\_CS\_LAB\_Collection\_Noncompliant,** and on the ribbon, click **Collection** and select **Update Membership**. Click **Yes**.

1. []Click **Collection,** select **Refresh,** and then click **Show Members**

1. []You should be able to see the non-compliant computers **NYCDC** and **NYCCL1**. If the collection is empty, click **Update Membership** on the ribbon. \(Press **F5** to refresh the console\)

	!IMAGE[Screenshot](screens/kstwztoc.jpg)

Congratulations! You have now created a collection based on non-compliance machines. On the next exercise we will remediate these machines.

===

#Module 4, Lab 2, Exercise 10 - Configure Auto Remediation

##Scenario

Settings for registry, WMI or scripts can be automatically remediated. When the remediation is configured, Configuration Manager will set the desired configuration and will report the wrong evaluated value.  
  
In this task, you will modify the registry and script configuration item to auto-remediate the wrong settings.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Connect to **NYCCFG**. Open the **Assets and Compliance** workspace and in the **Navigation** pane, click **Compliance Settings** &gt;**Configuration Items**.



1. []Select the **Remote Desktop Active** configuration item, and on the ribbon, click **Properties**. Click **Settings**

1. []Click the setting **Terminal Server Is Active** and then click **Edit**.

1. []On **Terminal Server Is Active Properties**, click the **Compliance Rules** tab.

1. []Select the rule **fDenyTSConnections Equals 0** and click **Edit**.

1. []In **Edit Rule**, select **Remediate noncompliant rules when supported**. Click **OK**, click **OK** and then click **OK**.

	!IMAGE[Screenshot](screens/nugqpa3w.jpg)

1. []Select the **RemoteRegistry\_Service\_StartType\_State** configuration item, and on the ribbon, click **Properties**. Click the **Settings** tab.

1. []Select the setting **RemoteRegistry\_Service\_State** and click **Edit**

1. []In **RemoteRegistry\_Service\_State Properties**, on the **Remediation script \(optional\)** panel, click **Add Script**.

1. []In **Create Remediation Script,** for the **Script language**, select **Windows PowerShell**. In the Script box, type the following:  
	+++*cmd /c sc config RemoteRegistry start= auto*+++
	+++*cmd /c sc start RemoteRegistry*+++

	!IMAGE[Screenshot](screens/g1zk4jcl.jpg)

1. []Click **OK** to close the **Create Remediation Script** window

1. []Cick the **Compliance Rules** tab. Select the rule **Check RemoteRegistry Service State** and click **Edit**.

1. []Select **Run the specified remediation script when this setting is noncompliant**. Click **OK**, click **OK** and then click **OK**.

	!IMAGE[Screenshot](screens/jfm2b251.jpg)

1. []Navigate to **Configuration Baselines**. Select the baseline **LAB\_Baseline**. Click **Deployments** tab at the bottom.

1. []Select the deployment **CS\_LAB\_Collection**, and on the ribbon, click **Properties**. In Configuration Baseline Deployment Properties, select **Remediate noncompliant rules when supported**. Click **OK**.

	!IMAGE[Screenshot](screens/o5a4ayz1.jpg)

Congratulations! You have now configured the automatic remediation feature.

===

#Module 4, Lab 2, Exercise 11 - Re-run the Compliance Baseline

##Scenario

In this exercise you will re-evaluate the baseline to trigger the automatic remediation

1. []You will run the steps below on both **NYCDC** and **NYCCL1**

1. []Righ-click **Start**, select **Control Panel**, and then click **Configuration Manager**.

	> [!ALERT] **Note**: If you cannot see the **Configuration Manager** in **Control Panel,** change **View by** to **Large icons**.

1. []Select **Actions**, select **Machine Policy Retrieval &amp; Evaluation Cycle** and click **Run Now**. You may need to wait a couple of minutes before proceeding.

	!IMAGE[Screenshot](screens/yw1pfx5o.jpg)

1. []Select the **Configurations** tab, and click **Refresh**.

1. []Select the baseline **LAB\_Baseline** and click **Evaluate**. In the Compliance State column, you should see **Compliant**.

	!IMAGE[Screenshot](screens/kw0tafrz.jpg)

1. []To open the local report, click **View Report**. Microsoft Internet Explorer starts and you see the compliant state for every compliant setting item.

	!IMAGE[Screenshot](screens/z02fk4gb.jpg)

	> [!ALERT] **Note**: If you get an error as the compliance state, check the Windows PowerShell execution policy with the command *get-executionpolicy* from a Windows PowerShell command shell window. You can modify the Windows PowerShell execution policy with the following command  
	>   
	> *Set-ExecutionPolicy unrestricted*  
	>   
	> Press **Y** at the confirmation request.

	> [!KNOWLEDGE] Every time Configuration Manager evaluates the baseline, the settings with auto-remediation will try to remediate them to a compliant state.  
	>   
	> To see the result in the non-compliant collection you have to update the membership. The client needs some time to forward the client state. You may have to wait for few minutes before you can update the collection membership.


Congratulations! You have now used the remediation features in Configuration Manager

===

#Module 4, Lab 2, Exercise 12 - Troubleshooting Techniques \(Optional\)

##Scenario

In this exercise, you will learn the tools and troubleshooting techniques to use when compliance settings evaluation raises unexpected results.  
  
Your IT manager requests you to verify whether on your machines the following configuration is respected:  
  

- If Adobe Reader is installed on client machines. Only version greater than 10.0 must be present and must be properly configured

You are going to leverage the Configuration Manager compliance settings feature in order to detect the right installation and the right configuration  
  
If a computer drifts from the expected configuration, you can now easily remediate it

Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Connect to **NYCCFG**. Open the **Assets and Compliance** workspace and in the Navigation pane, click **Compliance Settings** and then click **Configuration Items**. On the ribbon, click **Create Configuration Item**.

	
1. []In **Create Configuration Item Wizard**, on the **General** page, type +++**Adobe Reader X**+++ for **Name** and  +++**Check the presence and version of Adobe Reader X**+++ for Description.


1. []Select **This configuration item contains application settings**. Click **Categories**, select **CMCS-LAB** category, and click **OK**. Click **Next**.

	!IMAGE[Screenshot](screens/jpnphuwt.jpg)

1. []On the **Detection Methods** page, select **Use Windows Installer Detection**. Click **Open** and type +++*\\\\NYCDC\\Software\\Adobe Reader X\\AcroRead.msi*+++ under **File name. Product code** and **Version** will be automatically populated. Change **Version** to +++**10.1.0**+++ \(the actual version for this MSI is **10.1.0** and the MSI file incorreclty shows 10.0.0 as the version\). Click **Next.**

	> [!ALERT] Make sure you change the **Version** to **10.1.0** since the .MSI incorrectly shows version **10.0.0**


	!IMAGE[Screenshot](screens/ytjnz43p.jpg)

1. []On the **Settings** page, click **New**. In the **Create Setting** dialog box, type +++**Adobe Reader version**+++ for **Name**. Type +++**Check the version of Adobe Reader**+++ for Description.

1. []For **Setting type**, select **WQL query**. For **Data type**, select **String**. Ensure that **root\\cimv2** is set for **Namespace**. Type +++**Win32\_Products**+++ for **Class**. Type +++**Version**+++ for **Property**. Type +++**Caption LIKE '%Adobe Reader%'**+++ for **WQL query WHERE clause**.

	!IMAGE[Screenshot](screens/jke3cjki.jpg)

1. []Click the **Compliance Rules** tab. Click **New**. In **Create Rule**, type +++**Adobe Reader Version**+++ for **Name**. Type +++**Check the version of Adobe Reader**+++ for Description.

1. []For **Rule Type**, select **Value**. In the bottom pane for **The setting must comply with the following rule**, change the **Operator** to **Begins with**. Type +++**10.1**+++ for **the following values**. For **Noncompliance Severity for reports**, select **Warning**. Click **OK** and then click **OK** to return to the **Settings** page.


	!IMAGE[Screenshot](screens/now5nfyx.jpg)

1. []Click **New**. In the **Create Setting** dialog box, type +++**Installation path of Adobe Reader version**+++ for **Name**. Type +++**Check the installation path of Adobe Reader**+++ for Description.

1. []For **Setting type**, select **WQL query**. For **Data type**, select **String**. Ensure that **root\\cimv2** is set for **Namespace**. Type +++**Win32\_Products**+++ for **Class**. Type +++**InstallLocation**+++ for **Property**. Type +++**Caption LIKE '%Adobe Reader%'**+++ for **WQL query WHERE clause**.

	
	!IMAGE[Screenshot](screens/b2mt134y.jpg)

1. []Click the **Compliance Rules** tab. Click **New**. In **Create Rule**, type +++**Check the right installation path of Adobe Reader**+++ for **Name**. Type +++**Check the installation path of Adobe Reader**+++ for Description.

1. []For **Rule Type**, select **Value**. In the bottom pane for **The setting must comply with the following rule**, change the **Operator** to **Begins with**. Type +++**C:\\Program Files \(x86\)\\Adobe**+++ for **the following values**. For **Noncompliance Severity for reports**, select **Warning**. Click **OK** and then click **OK** to return to the **Settings** page.


	!IMAGE[Screenshot](screens/3qbwaznr.jpg)

1. []Click **Next**. On the **Compliance Rules page**, review the compliance rules just created and click **Next**. 

	!IMAGE[Screenshot](screens/bmniramx.jpg)


1. []On the **Supported Platforms** page, clear the **Select all** checkbox and select only **Windows 10**. Click **Next**, click **Next** and then click **Close**.


	!IMAGE[Screenshot](screens/5jmtwjmb.jpg)

1. []Navigate to **Configuration Baselines** in the navigation pane. Select the baseline **LAB\_Baseline**, and on the ribbon, click **Properties**. In the **Description** box, modify the text to +++*Check RDP, WUA version, Remote Registry service state and Adobe Reader*+++.

	!IMAGE[Screenshot](screens/2aby0ivo.jpg)

1. []Click the **Evaluation Conditions** tab. Click **Add** and then click **Configuration Item**. In **Add Configuration Items**, select **Adobe Reader X**, and click **Add**. Click **OK.**


	!IMAGE[Screenshot](screens/au2th4iu.jpg)

1. []Now you can see the list of configuration items that are part of the baseline **LAB\_Baseline**. Notice all configuration items have **Required** in the column **Purpose.** Select the **Adobe Reader X** configuration item. Click **Change Purpose** and then click **Optional**. Click **OK** to close the **Properties** window.

	> [!ALERT] **Note**: You have changed the purpose of the configuration item top **Optional** as this setting must be evaluated only on machines where **Adobe Reader X** is installed.


	!IMAGE[Screenshot](screens/xcs0nyl3.jpg)

> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1. []Connect to **NYCCL1**. Click **Start**, select **Control Panel** and then click **Configuration Manager**

	> [!ALERT] **Note**: If you cannot see the **Configuration Manager** in **Control Panel**, change **View by** to **Large icons**.


1. []Click the **Configurations** tab. You should see that the **LAB\_Baseline** has a revision that is greater than or equal to **2**. Select the baseline **LAB\_Baseline** and click **Evaluate**. After a while, on the Compliance State column a new compliance state should appear.  
	Click **View Report** to look at the compliance state for each configuration item.

	> [!ALERT] **Note**: If revision is not greater than or equal to **2:**  
	>   
	> 
	> 1. Select the **Actions** tab.
	> 2. Select **Machine Policy Retrieval &amp; Evaluation Cycle**, and click **Run Now**.
	> 3. Navigate back to the **Configurations** tab and after a while click **Refresh**.
	> 
	> 

	> [!KNOWLEDGE] 
	> - Which is the compliance state of the baseline?
	> - Which configuration items and compliance rules are responsible for the error?
	> 
	> 

Congratulations! You have now troubleshooted and identified several issues in compliance settings.


===

#Module 4, Lab 2, Exercise 13 - Identify the Problem and Troubleshoot \(Optional\)

##Scenario

To identify issue related to Compliance Settings, baseline evaluation is necessary to investigate which CI is raising the exception. To accomplish this task try to analyze the problem from different approaches:  
  
Server-side: from the console and running the compliance reports  
Client-side: running the local report on client machine and analyzing the client logs

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Connect to **NYCCFG** and open **Configuration Manager Console**. Navigate to the **Monitoring** workspace and select the **Deployments** node from the **Navigation** pane.



1. []Select **LAB\_Baseline** from the **Deployments** pane. At the bottom, you will see overall compliance status for the baseline deployment.

	> [!ALERT] **Note**: The Total Asset Count may be different from that shown in the following figure, but one system should show with **error** status. If it does not, on the **ribbon**, click Run Summarization, click **Refresh**.

	!IMAGE[Screenshot](screens/ath0mcff.jpg)

1. []Click **View Status** to display a more detailed view of the compliance state. Click the **Error** tab

	> [!KNOWLEDGE] Which configuration item is raising the issue?  
	> Which settings are responsible for the error?  
	> Which is the common error description?


	!IMAGE[Screenshot](screens/w0rsg5fm.jpg)

1. []In the **Navigation** pane, expand **Reporting**, click **Reports**, and select the **Compliance and Settings Management** folder. Click **Details of errors of configuration items in a configuration baseline for an asset**, and on the ribbon, click **Run**.

1. []Set the following parameters: Configuration Baseline Name: **LAB\_Baseline** / Configuration Item Name: **Adobe Reader X** / Device Name: **NYCCL1** / User Name: **System**

	!IMAGE[Screenshot](screens/3shhfw1k.jpg)

1. []Click **View Report**. As you could previously see in the console, the problem is caused by an **Invalid Class** used in the WMI Query Language \(WQL\) query.

	!IMAGE[Screenshot](screens/i3grbdeg.jpg)

1. []For the purpose of this exercise, you are going to analyze only the significant logs that report the cause of the problem.

	> [!KNOWLEDGE] Troubleshooting of the client reporting the failure during the evaluation of the baseline can be accomplished looking at the Configuration Manager client log files. Here are the logs related to Compliance settings \(in C:\\Windows\\CCM\\Logs\):  
	>   
	> DCMAgent.log  
	> DCMReport.log  
	> DCMWMIProvider.log  
	> CIDownloader.log  
	> CIStateStore.log  
	> CIStore.log

> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1. []Connect to **NYCCL1**. Open **Windows Explorer** and navigate to C:\\windows\\ccm\\logs. Open **DCMWMIProvider.log**. You can see a significant number of error messages related to the invalid class contained into the WQL query.  
	*Failed in discovering instance. Invalid class \(Error: 80041010; Source: WMI\)*  
	*Failed to do HandleExecQueryAsync\(\). Invalid class \(Error: 80041010; Source: WMI\)*

	> [!KNOWLEDGE] How would you proceed to fix the issue?

	!IMAGE[Screenshot](screens/3fv1oemh.jpg)

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Connect to **NYCCFG**. Open the **Assets and Compliance** workspace and in the **Navigation** pane, click **Compliance Settings** and then click **Configuration Items**. Select the **Adobe Reader X** configuration item, and on the ribbon click **Properties**.



1. []Click the **Settings** tab. Select **Adobe Reader Version** and click **Edit**. In the **Class** box, update to +++**Win32\_Product**+++ instead of **Win32\_Products**. Click **OK**.


	!IMAGE[Screenshot](screens/ijyg5jrf.jpg)

1. []Select **Installation path of Adobe Reader** and click **Edit**. In the **Class** box, update to +++**Win32\_Product**+++ instead of **Win32\_Products**. Click **OK** and then click **OK**.

	!IMAGE[Screenshot](screens/z0hnmrqz.jpg)

1. []Select **Configuration Baseline**, open *Lab\_Baseline* properties, modify **Description** to add &quot;+++*ver2*+++&quot; in the end. Click **OK**.


	!IMAGE[Screenshot](screens/pt4mip0g.jpg)

1. []Connect to **NYCCL1**. Right-click **Start**, select **Control Panel** and then click **Configuration Manager**.

	> [!ALERT] **Note**: If you cannot see the**Configuration Manager** in **Control Panel**, change **View by** to **Large icons**.

1. []Select the baseline **LAB\_Baseline** and click **Evaluate**. After a while, on the Compliance State column the baseline should switch back to **Compliant**.

	> [!ALERT] **Note**: If not,  
	>   
	> 
	> 1. Select the **Actions** tab
	> 2. Select **Machine Policy Retrieval &amp; Evaluation Cycle**, and click **Run Now**.
	> 3. Navigate back to **Configurations** tab and after a while click **Refresh**.
	> 
	> 


	!IMAGE[Screenshot](screens/rtavoldr.jpg)

1. []Click **View Report** to look at the compliance state for each configuration item.


	!IMAGE[Screenshot](screens/lfxi1i32.jpg)

Congratulations! You have now successfully fixed the issue and evaluated Adobe Reader compliance.

===

#Module 5, Lab 1, Exercise 1 - Configure Client Agent Settings and Set User Device Affinity

##Scenario

In this exercise you will configure the User Device Affinity to be set automatically and manually set a primary device for the user **Mark**. 

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on to **NYCCFG** and launch the **Configuration Manager Console**

1. []On the **Administration** workspace, select **Client Settings** &gt; **Default Client Settings**. Click **Properties** from the ribbon.

	> [!ALERT] **Note**: This action launches the **Client Settings** configuration page. In this exercise, we will be enabling the client settings for **User and Device Affinity**.



1. []On the **Default Settings** dialog box, select **User and Device Affinity**.



1. []In the **Device Settings** section, set **Automatically configure user device affinity from usage data** to **Yes**.

	> [!ALERT] **Note**: The Automatically configure user device affinity from usage data setting requires the clients to be configured to audit log on events and audit account log on events. If user activity falls below the defined threshold, the user device affinity will be removed. The time period should not be set less than seven days to avoid users being inadvertently removed.



1. []In the **User Settings** section, set **Allow user to define their primary devices** to **Yes**.

	!IMAGE[Screenshot](screens/peg23f0s.jpg)



1. []In the **Computer agent** section, set **Organization name displayed in Software Center**, type +++**Contoso**+++ and Click **OK** to close the default settings.

	!IMAGE[Screenshot](screens/zk3b1vtu.jpg)




1. []In the **Configuration Manager** console, open the **Assets and Compliance** workspace. Click the **Devices** node and select **NYCCL1**.



1. []On the ribbon, select **Device** and click **Edit Primary Users**.

	!IMAGE[Screenshot](screens/zxnvkp2k.jpg)

1. []In **Type a search string to search ALL** **users** of the **Edit Primary Users** dialog box, type +++**CONTOSO\\Mark**+++, then in the search results select **CONTOSO\\Mark** and click **Add** to assign **Mark Steele** as the **Primary User** and Click **OK.**

	> [!ALERT] **Note**: The Edit Primary Users screen will by default display users that have logged onto the system. If the user you wish to assign is not displayed, you can use the search box to locate the correct user. Enter the name of the user you wish to assign to the system. The user name must have already been discovered by ConfigMgr User Discovery.


	!IMAGE[Screenshot](screens/zbmqdd33.jpg)

You have now configured necessary client settings for application deployment and user device affinity. On the next lesson you will be ready to deploy applications

===

#Module 5, Lab 2, Exercise 1 - Create and deploy an application for Lync 2010

##Scenario

The company is currently running the Microsoft Office Communicator 2007 R2 application. A new version of this application needs to be deployed to Windows Workstation and Professional systems. Create a deployment of Microsoft Lync 2010 that replaces Office Communicator 2007 R2.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on to **NYCCFG.** On **NYCCFG**, start the **Configuration Manager Console**

1. []In the **Configuration Manager** console, open the **Software Library** workspace, expand **Application Management** and select **Applications**.



1. []On the ribbon, click **CREATE,** **Create Application**.

	> [!ALERT] **Note**: Applications can be created in two ways, manually or automatically. When using the automatic method, the application information is gathered from the selected MSI and used to create the basic application properties.



1. []Select **Manually specify the application information** and click **Next**.


	!IMAGE[Screenshot](screens/ihcerzu4.jpg)



1. []On the **General** page of the **Create Application Wizard**, type the following settings:  
	- **Name**: +++*Microsoft Lync 2010*+++
	- **Publisher**: +++*Microsoft*+++ 
	- **Software Version**: +++*2010*+++

	!IMAGE[Screenshot](screens/1d1046b4.jpg)



1. []To set **Administative categories**, click **Select**. On **Manage Administrative Categories**, click **Create**. In **Create Administrative Category**, type +++*Communication*+++ and click **OK** &gt; **OK** &gt;**Next**.


	!IMAGE[Screenshot](screens/msdxwwi3.jpg)



1. []On the **Software Center** page of the **Create Application Wizard**, type the following settings:  
	- **Localized application name**: +++*Microsoft Lync 2010*+++
	- **User documentation**: +++*http://intranet/documentation/en-US/Lync2010.html*+++  
	- **Keywords**:+++*Meeting, collaboration, IM, Live Meeting, Instant Messaging, Communication*+++


	!IMAGE[Screenshot](screens/1xl3gqim.jpg)



1. []To set **User categories**, click **Edit**. On **User Categories**, click **Create**. In **Create User Category**, type +++*Communication*+++ and click **OK** &gt; **OK**.

	!IMAGE[Screenshot](screens/0q4gj2bk.jpg)



1. []To set the **Icon**, click **Browse**. On the **Change Icon** dialog box, type +++*\\\\NYCDC\\Software\\Lync 2010\\en\_lync\_2010\_x64\_598490.exe*+++ in the **File Name** field and click **Open**. Ensure that the icon is selected. Click **OK**. Click **Next** to confirm the **Software Center** settings.


	!IMAGE[Screenshot](screens/pq54p3yh.jpg)

1. []Click **Next** to continue without creating a **Deployment Type**.

	> [!ALERT] **Note**: We will create a deployment type for this application in a later step of this lab.


	!IMAGE[Screenshot](screens/fvyhpruj.jpg)

1. []Review the **Summary page**, click **Next** and wait for the **Completion page**. Click **Close** to exit the **Create Application Wizard**.


	!IMAGE[Screenshot](screens/vgdjss0x.jpg)

1. []In the **Configuration Manager** console, under **Application Management,** select **Global Conditions**.

	!IMAGE[Screenshot](screens/f35e53b4.jpg)

1. []On the ribbon, click **Create Global Condition**. Type the following details:  
	**Name**: +++*All Windows 10 x64 Workstations*+++ **Description**: +++*All 64-bit Workstations*+++. **Device type**: *Windows*. **Condition type**: *Expression*.


	!IMAGE[Screenshot](screens/ssd4d5ii.jpg)



1. []Click **Add Clause**, confirm that **Category** is set to **Device**, change **Condition** to **Operating System**.

1. []Configure settings as below, and click **OK** to create the custom **Global Condition**:  
	Expand **Windows 10**, select **All Windows 10 \(64-bit\)** and Click **OK** to create the custom **Global Condition**.

	!IMAGE[Screenshot](screens/ihjv4d2i.jpg)

1. []In the **Configuration Manager** console, under **Application Management**, select **Applications**.

1. []Select **Microsoft Lync 2010** and from the ribbon, click **Application**, and select **Create Deployment Type**. In the **Create Deployment Type** wizard, change the **Type** drop-down list to **Script Installer**. This will automatically select **Manually specify the deployment type information**. Click **Next**.


	!IMAGE[Screenshot](screens/rt3js54n.jpg)

	!IMAGE[Screenshot](screens/5hl3wifn.jpg)

1. []In the **Name** field, type +++*Install Lync 2010 \(silent\)*+++ and click **Next**.


	!IMAGE[Screenshot](screens/ktxfrio0.jpg)

1. []On the **Content page**, enter the following settings, then click **Next**  
	- **Content location**: +++*\\\\NYCDC\\Software\\Lync 2010*+++ 
	- **Installation program**: +++*en\_lync\_2010\_x64\_598490.exe /install /silent*+++ 
	- **Uninstall program**: +++*en\_lync\_2010\_x64\_598490.exe /uninstall*+++ 

	> [!ALERT] **Note**: You can use Browse to view and select the correct file from the previously specified content location.

	!IMAGE[Screenshot](screens/xajrcmax.jpg)

1. []On the **Detection Method** page, click **Add Clause**. Change the **Setting Type** to **Windows Installer** and type +++*\{B31017AA-FBF8-4003-8785-EC789C2AE0C2\}*+++ as the **Product code** and click **OK**. Click **Next**.

	> [!ALERT] **Note**: When creating a **Windows Installer Deployment Type**, the product code is automatically discovered. In this case, the MSI is wrapped with an EXE and as such, the product code cannot automatically be imported.  
	>   
	> To obtain the Product code of such an application, install the EXE on a test system and run a WMIC command to get the PackageCode. An example query is:  
	>   
	> *wmic product where\(name like &quot;%lync%&quot;\) get name,IdentifyingNumber*  
	>   
	> Detection rules can be combined using AND/OR conditions. Rules can be created from **Windows Installer** product codes, items on the file system, or items in the registry.

	!IMAGE[Screenshot](screens/dq1jecjc.jpg)

1. []Set the **Installation behavior** to **Install for system** and click **Next**.


	!IMAGE[Screenshot](screens/vpfd0ope.jpg)

1. []Set the following settings for the **Create Requirement** dialog and click **OK**:  
	- **Category**: *Custom*
	- **Condition**: *All Windows 10 x64 Workstations* (Select from drop down menu)
	- **Operator**: *Equals*
	- **Value**: *True*

	!IMAGE[Screenshot](screens/jdss22sm.jpg)
	
1. []Click **Next** on the **Requirements** page.

	!IMAGE[Screenshot](screens/c1tk1io2.jpg)


1. []On the **Dependencies** page, click **Next**. Review the **Summary**, click **Next** and Click **Close**.

	!IMAGE[Screenshot](screens/rmzbtlzk.jpg)

1. []Locate the **Microsoft Lync 2010** application and select **Properties** from the ribbon.

1. []Select the **Supersedence** tab and click **Add**. On the **Specify Supersedence Relationship** window, click **Browse** and locate the **Microsoft Office Communicator 2007** application, select it, and click **OK**.


	!IMAGE[Screenshot](screens/3bgzfu3p.jpg)


1. []Locate the entry with **Microsoft Office Communicator 2007** in the **Old Deployment Type** column. Change the **New Deployment Type** drop-down list to **Install Lync 2010 \(silent\)**. Select **Uninstall** and click **OK**.


	!IMAGE[Screenshot](screens/5xh5s5dj.jpg)

1. []Confirm that the supersedence was created correctly by visually reviewing the entry on the **Supersedence** tab and click OK.

	!IMAGE[Screenshot](screens/tbw2qvq2.jpg)

	> [!ALERT] **Note**: Configuration Manager has a feature that displays a graphical representation of Application relationships. To view the relationship created:  
	>   
	> 
	> 1. []Return to **Software Library** &gt; **Applications**.
	> 2. Locate and select **Microsoft Lync 2010** application.
	> 3. On the ribbon, select **View Relationships** icon and click **Supersedence**.
	> 
	> 

	!IMAGE[Screenshot](screens/4lolrvf0.jpg)

1. []Select the **Microsoft Lync 2010** application, click **Deployment** and then click **Deploy** from the ribbon.

1. []On the **Deploy Software Wizard**, locate the **Collection** line and select **Browse**. In this scenario, we are going to deploy this software to the **All Desktop and Server Clients** collection. To locate this collection, change the drop-down list from **User Collections** to **Device Collections** and select **Root** in the left navigation pane. Select **All Desktop and Server Clients**. Click **OK** and click **Next**.


	!IMAGE[Screenshot](screens/kgqhqaum.jpg)

1. []On the **Content screen**, click **Add** and select **Distribution Point**. Select **NYCCFG.CONTOSO.COM**. Click **OK** &gt; **Next**.


	!IMAGE[Screenshot](screens/hhy3tc1e.jpg)

1. []On the **Deployment Settings** screen, configure the following settings and click **Next**:  
	- **Action**: *Install*. 
	- **Purpose**: *Required*. 
	
	Select **Pre-deploy software to the user’s primary device**.


	!IMAGE[Screenshot](screens/w5s5eh5d.jpg)

1. []Accept the defaults on the **Scheduling** page and click **Next**.

	> [!ALERT] **Note**: In a real world scenario, the scheduling settings will be commonly used to control when clients become aware of a policy \(Schedule the application to be available at\) and when the installation will take place \(Installation deadline\).


	!IMAGE[Screenshot](screens/tqfglzhn.jpg)

1. []The **User Experience** page controls how the deployment will interact with users. In this case, accept the defaults and click **Next**. Accept the defaults on the **Alerts** page and click **Next**. Review the **Summary** and click **Next** &gt; **Close**.

	> [!ALERT] The status of the deployment can be monitored by accessing the **Monitoring** workspace, selecting **Deployments**, and locating the deployment to be monitored. It may take several minutes. You can proceed with the following exercise and check the status later.


	!IMAGE[Screenshot](screens/kugw3mfv.jpg)

	!IMAGE[Screenshot](screens/ligrpwtd.jpg)

Congratulations! You have now created and deployed your first application.

===

#Module 5, Lab 2, Exercise 2 - User-targeted Application Deployment

##Scenario

The helpdesk staff is requesting a local installation of the Configuration Manager console on their computers. As they log into multiple computers, the application should be installed only on their primary device. You are tasked with creating an application to install the console on the helpdesk staff’s primary devices only.  
  
In this exercise, you will:  
  

- Install the Configuration Manager console
- Create a script-based application
- Create a dependency
- Create a Requirements rule
- Deploy an application



1. []Log on to **NYCCFG** and on the **Configuration Manager** console, Click **Software Library** node, select **Applications** and click **Create,** **Create Application**.

	!IMAGE[Screenshot](screens/gjsiecsn.jpg)

1. []Select **Manually specify the application information** and click **Next**.


	!IMAGE[Screenshot](screens/kxgbpdsy.jpg)

1. []On the **General** **Information** page of the **Create Application Wizard**, type the following settings and click **Next**:  
	- **Name**: +++*Microsoft System Center Configuration Manager Console*+++
	- **Publisher**: +++*Microsoft*+++
	- **Software Version**: +++*Current Branch*+++


	!IMAGE[Screenshot](screens/xxicb10w.jpg)

1. []Accept the defaults on the **Software Center** page and click **Next**.


	!IMAGE[Screenshot](screens/n0n4fz4i.jpg)


1. []On the **Deployment Type** page, click **Add**. Set **Type** to **Script Installer** and click **Next**.


	!IMAGE[Screenshot](screens/wns40abb.jpg)

1. []Enter **Name** as +++**ConfigMgr Console \(silent\)**+++ and click **Next**.


1. []On the **Content** page, enter the following settings and click **Next**:  
	- **Content location**: +++\\\\NYCCFG\\SMS\_NYC\\tools\\ConsoleSetup+++  
	- **Installation program**: +++&quot;ConsoleSetup.exe&quot; /q TargetDir=&quot;%ProgramFiles%\\Microsoft Configuration Manager&quot;  DefaultSiteServerName=NYCCFG.CONTOSO.COM+++ 
	- **Uninstall program**: +++*msiexec.exe /x \{CEC93134-0862-481E-842F-A19417FD5E12\} /q*+++

	> [!ALERT] **Note**: For Installation Program, you can use **Browse** to view and select the correct file from the previously specified content location. For Uninstall program, you can use the next step to copy the correct MSI Product code, click Previous button, and paste the correct product code into Uninstall program.  

	!IMAGE[Screenshot](screens/kultes20.jpg)

1. []On the **Detection Method** page, click **Add Clause**. Change the **Setting Type** to **Windows Installer**. Click **Browse...** button,  select **AdminConsole**, and click **Open**.  Verify the Product code, select **OK**. Click **Next**.


	!IMAGE[Screenshot](screens/yiwd5j2p.jpg)

	!IMAGE[Screenshot](screens/hb12mwp2.jpg)



1. []Set the following settings for **User Experience** and click **Next**.  
	- **Installation behavior**:  *Install for system.*  
	- **Logon requirement**: *Whether or not a user is logged on*.


	!IMAGE[Screenshot](screens/zoevqzpf.jpg)

1. []On the **Requirements** page, click **Add**. In the **Create Requirement** dialog box, set the following settings and click **OK**:  
	- **Category**: User 
	- **Condition**: Primary Device 
	- **Operator**: Equals 
	- **Value**: *True*.


	!IMAGE[Screenshot](screens/gfr0z5rd.jpg)

1. []Click **Add**. In the **Create Requirement** dialog box, set the following settings and click **OK**:  
	- **Category**: Custom 
	- **Condition**:  All Windows 10 x64 Workstations
	- **Operator**: Equals 
	- **Value**: True
	
	Click **Next**.


	!IMAGE[Screenshot](screens/nhpukqnb.jpg)

1. []On the **Dependencies** page, keep default and click **Next**.

	> [!ALERT] **Note**: Microsoft .NET Framework dependency for this Application is already Installed on the Machines.


1. []Click **OK** &gt; **Next** to proceed to the **Summary**. 

	!IMAGE[Screenshot](screens/qj0z0o5y.jpg)


1. []Click **Next** &gt; **Close** to close the wizard. Click **Next** &gt; **Close** to complete the. **Create Application Wizard**.


	!IMAGE[Screenshot](screens/yhr2mhjj.jpg)

	!IMAGE[Screenshot](screens/izkqana4.jpg)

1. []Locate the **Microsoft System Center Configuration Manager Console** application and select **Deployment, Deploy** from the Home tab on the ribbon.

	!IMAGE[Screenshot](screens/pwtxwjhg.jpg)

1. []On the **Deploy Software Wizard**, locate the **Collection** line and click **Browse**. In this scenario, we are going to deploy this software to the **IT Admins** collection. To locate this collection, confirm that the drop-down list is set to **User Collections** and select **Root** in the left navigation pane. Find the collection **IT Admins** and click **OK**.

	!IMAGE[Screenshot](screens/dvwminxy.jpg)

1. []Make sure **Automatically distribute content for dependencies** is selected and click **Next**.

	> [!ALERT] **Note**: In a production environment, you might distribute content for required dependencies. In this lab environment, all computers have .NET Framework 4.0 installed already.

	!IMAGE[Screenshot](screens/z3sda2kh.jpg)

1. []On the **Content** screen, click **Add** and select **Distribution Point**.  Select **NYCCFG.CONTOSO.COM** and click **OK** &gt; **Next**.


	!IMAGE[Screenshot](screens/olrf0d2j.jpg)

1. []On the **Deployment Settings** screen, confirm the following settings and click **Next**:  
	- **Action** as *Install*  
	- **Purpose** as *Available*


	!IMAGE[Screenshot](screens/rd4hpngq.jpg)

1. []Accept the defaults on the **Scheduling** page and click **Next**.


	!IMAGE[Screenshot](screens/lhqp3c2a.jpg)

1. []The **User Experience** page controls how the deployment will interact with users. In this case, accept the defaults and click **Next**.


	!IMAGE[Screenshot](screens/xgifrvtl.jpg)

1. []Accept the defaults on the **Alerts** page and click **Next**.

	!IMAGE[Screenshot](screens/ud251xtp.jpg)


1. []Review the **Summary** and click **Next** &gt; **Close** to complete the creation of the Deployment.


	!IMAGE[Screenshot](screens/js40sdyf.jpg)

1. []Log on to **NYCDC** with the following credentials:  
	- **Username**: +++*Mark*+++
	- **Password**: +++*Pa$$w0rd*+++
	- **Domain**: +++*CONTOSO*+++


1. []To launch the **Software Center**, Click on **start** , select **Microsoft System Center** and click on **Software Center**

	!IMAGE[Screenshot](screens/ufwzeppb.jpg)


1. []On the **Software Center**, under **Applications** select **Microsoft System Center Configuration Manager Console.**  and Click **INSTALL**.


	!IMAGE[Screenshot](screens/wczpyvjw.jpg)

	!IMAGE[Screenshot](screens/wl3neht0.jpg)

1. []Did the application install?

	!IMAGE[Screenshot](screens/x3nuzdca.jpg)

1. []Log on to **NYCCL1** with the following credentials:  
	- **Username**: +++*Mark*+++
	- **Password**: +++*Pa$$w0rd*+++
	- **Domain**: +++*CONTOSO*+++  
	
1. []Launch **Software Center** and Install **Microsoft System Center Configuration Manager Console.**

	!IMAGE[Screenshot](screens/wktj0emf.jpg)

	> [!ALERT] **Note**: Configuration Manager Console is Installed on Client Machine and **NOT** on DC, due to the ***Requirements** configurations.
	

Congratulations! You have now sucessfully deployed the Configuration MAnager console

===

#Module 5, Lab 2, Exercise 3 - Application Deployment and Maintenance Windows

##Scenario

In this exercise, you will:  
  

- Create an application and MSI Deployment Type
- Create a deployment for a computer in a maintenance window
- Modify maintenance windows to allow install while suppressing reboot ensuring that if the application needs to reboot, that reboot will occur during the maintenance window

Maintenance windows are in place currently to control the behavior of installation and reboots. A new application needs to be installed, but there is a requirement that the application be installed as soon as possible and to ignore the maintenance windows. However, management has communicated that if a restart is required, it should only be performed naturally by the end user or during the defined maintenance window.

1. []Log on to **NYCCFG** and on the **Configuration Manager** console, select **Assets and Compliance**.  Expand **Overview**. Select **Devices**.

1. []Right-click **NYCCL1** and select **Add Selected Items** &gt; **Add Selected Items to Existing Collection**. In the **Select Collection** dialog box, locate **Maintenance Window Collection** and click **OK**.

	> [!ALERT] **Important**: Wait one minute before proceeding to the next task.

	!IMAGE[Screenshot](screens/mb1bth2p.jpg)

1. []Log on to **NYCCL1** with the following credentials:  
	- **Username**: *Mark*
	- **Password**: +++*Pa$$w0rd*+++
	- **Domain**: *CONTOSO*

1. []Right-click **Start** &gt; **Control Panel** &gt; **System and Security** and select **Configuration Manager**. On the **Actions** tab, select **Machine Policy Retrieval &amp; Evaluation Cycle** and click **Run Now**.

	> [!ALERT] **Note**: You will evaluate machine policy on NYCCL1 so that the client applies the maintenance window.

	!IMAGE[Screenshot](screens/3lu4332b.jpg)

1. []Log on to **NYCCFG** and on the **Configuration** **Manager** console, open the **Software** **Library** workspace, expand **Application** **Management** and select **Applications**.  From the ribbon, click **Create** **Application**.

1. []On the **General** page of the **CreateApplication** **Wizard**, leave the **Type** as **Windows Installer \(\*.msi file\)** and type the **Location**: as +++*\\\\NYCDC\\Software\\ConfigMgr 2012 R2 Toolkit\\ConfigMgrTools.msi.*+++ Click **Next**.

	> [!ALERT] Note: You may also click the **Browse** button and point to *\\\\NYCDC\\Software\\ConfigMgr 2012 R2 Toolkit\\ConfigMgrTools.msi*

	!IMAGE[Screenshot](screens/dxjcjimd.jpg)

1. []On the **Import Information page**, the wizard has read the properties of the MSI and automatically filled in various pieces of information. Click **Next** to proceed.


	!IMAGE[Screenshot](screens/jnjk0wag.jpg)

1. []Update the **Installation** **program** to include +++**REBOOT=REALLYSUPPRESS**+++ and click **Next**. Click **Next** &gt; **Close** to complete the wizard.

	!IMAGE[Screenshot](screens/ey3tr5gz.jpg)

	!IMAGE[Screenshot](screens/ai14veys.jpg)


1. []Click **ConfigMgr 2012 Toolkit R2** &gt; **Deployment, Deploy** on the ribbon.

1. []In the **Deploy Software Wizard**, locate the **Collection** line and select **Browse**. Change the drop-down list from **User Collections** to **Device Collections** and select **Root**. Select **Maintenance Window Collection**.  Click **OK** &gt; **Next**.

	!IMAGE[Screenshot](screens/c1farzyv.jpg)

	> [!ALERT] **Important**: Although **Maintenance Windows** are applied at a collection level, they become a property of the computer object. A client with a maintenance window applied will evaluate all deployments against that maintenance window no matter what collection the deployment is targeted against.

1. []On the **Content** screen, click **Add** and select **Distribution Point**. Select **NYCCFG.CONTOSO.COM**. Click **OK** &gt; **Next**.


	!IMAGE[Screenshot](screens/phnbmagt.jpg)

1. []On the **Deployment Settings** screen, configure the following settings and click **Next**:  
	- **Action**: *Install*  
	- **Purpose**: *Required*

	!IMAGE[Screenshot](screens/vmmu5n2f.jpg)

1. []Accept the defaults on the **Scheduling** page and click **Next**.


1. []The **User Experience** page controls how the deployment will interact with the users.  In this case, accept the defaults and click **Next**.


	!IMAGE[Screenshot](screens/wgt0vord.jpg)

1. []Accept the defaults on the **Alerts** page and click **Next**.


	!IMAGE[Screenshot](screens/rhvtlqrf.jpg)

1. []Review the **Summary** and click **Next** &gt; **Close** to complete the creation of the **Deployment**.


	!IMAGE[Screenshot](screens/entapguo.jpg)

1. []Log on to **NYCCL1** with the following credentials:  
	- **Username**: *Mark*
	- **Password**: +++*Pa$$w0rd*+++
	- **Domain**: *CONTOSO*

1. []If the **Configuration Manager** Control Panel applet is not already open, right-click **Start** &gt; **Control** **Panel** &gt; **System and Security** and select **Configuration Manager**. On the **Actions** tab, select **Machine Policy Retrieval &amp; Evaluation Cycle** and click **Run Now**.

	!IMAGE[Screenshot](screens/1nsdowg4.jpg)

1. []Click **Start.** On the programs list, expand **Microsoft System Center**. Click **Software Center** to view the progress of the installation. What message is displayed for the status of the application **ConfigMgr 2012 Toolkit R2**?

1. []Log on to **NYCCFG** and on the **Configuration Manager** console, click the **Software Library** workspace, expand **Application Management** and select **Applications**. Locate and select the **ConfigMgr 2012 Toolkit R2** application.  In the bottom navigation window, locate and select the **Deployments** tab.

	!IMAGE[Screenshot](screens/pmvsebfl.jpg)

1. []Select the **Maintenance Window Collection deployment** and select **Properties** from the ribbon.


	!IMAGE[Screenshot](screens/mcjxzkw0.jpg)

1. []Select the **User Experience** tab and select **Software Installation** to allow the application to install outside of the defined maintenance windows.  Click **OK** to update the **Deployment**.

	!IMAGE[Screenshot](screens/2gbvwie4.jpg)

	> [!ALERT] **Important**: This can be a little misleading. This suggests allowing our Deployment Type to run the installation program outside of a maintenance window. If the installation program forcibly restarts the computer, the maintenance windows will not prevent this from occurring.  
	>   
	> Applications that run outside of defined maintenance windows that may restart the computer should leverage command-line arguments to suppress the reboots to prevent unexpected behavior.  
	>   
	


1. []Log on back to **NYCCL1**. If the **Configuration Manager** Control Panel applet is not already open, right-click **Start** &gt; **Control Panel** &gt; **System and Security** and select **Configuration Manager**. On the **Actions** tab, select **Machine Policy Retrieval &amp; Evaluation Cycle** and click **Run Now**.

	> [!ALERT] Wait for the installation to complete. If the installation is not started in five minutes, on the Actions tab, select Application Deployment Evaluation Cycle and click Run Now.

1. []Validate Application Installation Status from Software Center

	!IMAGE[Screenshot](screens/a1dfi1uc.jpg)

1. []Switch back to **NYCCFG**. In the **Configuration Manager** console, select **Assets and Compliance**. Expand **Overview**, select **Device Collections**, select **Maintenance Window Collection**. Right-click and select **Show Members**. Right-click **NYCCL1** and select **Remove from Collection**. Click **OK** to confirm the removal.

	> [!ALERT] To allow the other sections of this lab to function without issue, remove the client **NYCCL1** from the **Maintenance Window Collection**.

Congratulations! You have now deployed applications using maintenance windows



===

#Module 5, Lab 3, Exercise 1 - Evaluate results and troubleshooting

##Scenario

In this exercise, you will:  
  

- Manually Evaluate Machine Policy on the Client
- Evaluate the Client Logs to Determine Compliance Results
- Validate Findings in the Monitoring Workspace
- Modify Application Requirement Rule
- Validate Updated Status in the Monitoring Workspace



1. []Log on to **NYCCL1** with the following credentials:  
	- **Username**: +++*CONTOSO\Administrator*+++
	- **Password**: +++*Pa$$w0rd*+++
	- **Domain**: *CONTOSO*

1. []Right-click **Start** &gt; **Control Panel** &gt; **System and Security** and select **Configuration Manager**. On the **Actions** tab, select **Machine Policy Retrieval &amp; Evaluation Cycle** and click **Run Now**.

	> [!ALERT] **Note**: If the policy is not received, it may be necessary to wait a few minutes before initiating another Machine Policy Retrieval &amp; Evaluation Cycle.

1. []Right-click **Start** &gt; **Run** and type +++*C:\\Windows\\CCM\\logs*+++. Click **OK.**

1. []Open **PolicyAgent.log** and look for **Received Machine delta policy update**, followed by **Compiling policy ‘\{…\}’ version**. Note the unique assignment ID contained within \{\}. The **Policy Agent** requests the assigned machine or user policies using the **Data Transfer Service**.

	!IMAGE[Screenshot](screens/2g41gfwh.jpg)

	> [!ALERT] **Note**:**Some useful SQL Queries**

	>
	Retrieve requirement rules, global conditions and supported platforms
	>
	+++SELECT * FROM vCI_ConfigurationItems WHERE CIType_ID IN (11,13,14) AND isLatest = 1+++

	>
	Retrieve all Application Configuration Items
	>
	+++SELECT * FROM fn_ListApplicationCIs(1033)+++

	>
	Retrieve all Deployment Type Configuration Items
	>
	+++SELECT * FROM fn_ListDeploymentTypeCIs(1033)+++

	>
	Retrieve the requirement rules
	>
	+++SELECT * FROM fn_ListApplicationConditions(1033)+++

	>
	Retrieve Application assignments
	>
	+++SELECT * FROM v_ApplicationsAssignment+++





1. []Open **DCMAgent.log** and look for the Application CI unique ID  that you noted in the previous step. In DCMAgent.log, a DCM agent starts a CI Agent job to download and install the application.

	> [!ALERT] **Note**: You can filter the lines by clicking **Tools** &gt; **Filter**. Select **Filter when Entry Text**. Change **is equal to** and select **contains** and type the first few characters of the unique Application ID.

	!IMAGE[Screenshot](screens/afgy4m1c.jpg)

1. 	[]The CI Agent job starts downloading content. If needed search with **DeploymentType** Id in the CIAgent.log

1.	[]In CAS.log, Cache Manager looks for the content in local cache.
	>a)Content Transfer Manager creates the location request.

	>b)The location request is then sent to the management point.

	>c)CcmMessaging.log records the sending request to the management point.

	>d)CAS.log records the reply.

	>e)Content Transfer Manager (CTM) creates a DTS job to download content in ContentTransferManager.log


1. []Open **AppDiscovery.Log** and review the logs. AppDiscovery.Log records details about the **discovery or detection** of applications on client computers.


	!IMAGE[Screenshot](screens/g05l4xgw.jpg)


1. []Open **AppIntentEval.log** and look for the CI Unique ID which can be retrieved from the **Configuration Manager Console**. AppIntentEval.log records details about the **current and intended state of applications**, their applicability, whether requirements were met, deployment types, and dependencies.

	!IMAGE[Screenshot](screens/yc2qmdwe.jpg)

	!IMAGE[Screenshot](screens/jdw0b2ny.jpg)


1. []Open **AppEnforce.Log** and review the logs. AppEnforce.log records details about **enforcement actions (install and uninstall)** taken for applications on the client.

	!IMAGE[Screenshot](screens/lbohdm4n.jpg)


1. []Log on to **NYCCFG**. In the **Configuration Manager** console, open the **Monitoring** workspace and select **Deployments**, and  review Compliance from Console.

	!IMAGE[Screenshot](screens/ubo2unzj.jpg)




1.	[]Log on to **NYCCFG**. In the **Configuration Manager** console, open the **Monitoring** workspace, select **Reporting** and select **Software Distribution -Application Monitoring** and run **Reports**.

	!IMAGE[Screenshot](screens/kgasnqld.jpg)

Congratulations! You have now completed this lab.


===

#Module 6, Lab 1, Excercise 1 - Check Client Connectivity

##Scenario

In this exercise you will:  
  

- Verify that the client is able to communicate with the management point

**Scenario:**  
  
Checking for client connectivity to the Configuration Manager servers should be the first thing to check when a client is not functioning as expected

> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1. []Log on to **NYCCL1**. 
	  
1. []In the search bar type Control to open **Control Panel**. From the Control Panel go to **System and Security** and click **Configuration Manager**. Confirm the following settings: 
	  
	
	  
	
	  
	- Client certificate is PKI
	  
	- Assigned management point is NYCCFG.contoso.com
	  
	- Site code is SMS:NYC
	  
	
	  
	
	  
1. []On the **Actions** tab, select **Discovery Data Collection Cycle** and click **Run Now** &gt; **OK**
	  
	
	

	> [!KNOWLEDGE] If the client is healthy, a data discovery record \(DDR\) will be generated with Heartbeat Discovery information that will be sent to the assigned management point.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on to **NYCCFG**
	  
1.	[]  Right-click **Start** &gt; **Run**. Type +++E:\\Program Files\\SMS\_CCM\\Logs+++ and click **OK**
	  
1.	[] Open MP\_DDR.log
	  
	
	

	> [!KNOWLEDGE] MP\_DDR.log will contain a message similar to the following message, indicating that a DDR was successfully received by the management point. The DDR file has the .DDR file extension, but is randomly named. The DDR file name will not be identical to the example as shown in the following code:  
	>   
	> Full report from client, action description = Discovery Ddr Task: Translate report attachment to file &quot;E:\\Program Files\\Microsoft Configuration Manager\\inboxes\\auth\\ddm.box\\6SJ4OREK.DDR&quot; returned 0





1. []Click **Start** &gt; **Run**. Type +++E:\\Program Files\\Microsoft Configuration Manager\\Logs+++ and click OK
	  
1.	[] Open DDM.log
	  
	
	

	> [!KNOWLEDGE] The log will contain a message that indicates that the DDR was processed successfully and updated information is added to the database.  
	>   
	> Processing file 6SJ4OREK.DDR ..




1. []Open the **Configuration Manager Console**
	  
1.	[] In the Configuration Manager console, open the **Assets and Compliance** workspace, and select **Device Collection**
	  
1.	[] Right-click **All Systems** &gt; **Show Members**
	  
1.	[] Click **NYCCL1**, right-click and select **Properties**
	  
1.	[] Compare the values in arrays Agent Name and Agent Time
	  
1.	[] Click **OK** to close the Properties dialog box
	  
	
	

	> [!ALERT] For checking the time of the last Heartbeat Discovery, you may need to expand columns to see this information.  
	> The time is *not* UTC, if it does not match your current time you could change the Time Zone of NYCCFG and run another Discovery Data Collection on NYCCL1 again to confirm the results.



1. []Open the Monitoring workspace and select **Client Status** &gt; **Home**
	  
1.	[] Click **Refresh Client Status**
	  
1.	[] Select **Client Status Settings**
	  
1.	[] Note the default settings and click **Cancel**
	  
1.	[] Expand Client Status and select **Client Check**
	  
1.	[] Click the green portion of the Client check results for all devices pie chart
	  
1.	[] On Clients that passed client check from “**All Desktop and Server Clients**” select a device
	  
1.	[] Click the **Client Activity Detail** tab on the results pane.
	  
	
	

	> [!KNOWLEDGE] Client activity information is accessible per client, showing the last time information was sent to the management point. To see updated information, you may need to return to the Client Check node and in the ribbon, click Refresh Client Status.



**Congratulations!  **
  
You have successfully:  
  

- Checked Client Connectivity



===

#Module 6, Lab 1, Excercise 2 - Understanding CCMEval

##Scenario

In this exercise you will:  
  

- See how CCMEVAL is configured through the task scheduler and XML files

**Scenario:**  
  
The IT administrator of Contoso.com is keen to learn more about the process that performs the client health monitoring - CCMEval

> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1. [] Log on to **NYCCL1**
	  
1.	[] In the search bar type Control to open **Control Panel**
	  
1.	[] From the Control Panel go to **System and Security** and in the **Administrative Tools** area double-click **Task Scheduler**
	  
1.	[] Expand **Task Scheduler Library** &gt; **Microsoft**, and select **Configuration Manager**
	  
1.	[] Note the Next Run Time, Last Run Time and Last Run Result for the task **Configuration Manager Health Evaluation**
	  
1.	[] Look through the following tabs in turn
	  
	
	  
	
	  
	- General
	  
	- Actions
	  
	- Settings
	  
	
	

	> [!KNOWLEDGE] By default, CCMEval is run at some random time between 12 AM and 1 AM, and if a scheduled start is missed is set to run as soon as possible.



1. []Right-click **Start** &gt; **Run**, and type +++C:\\Windows\\CCM+++
	  
1.	[] Copy **CCMEval.xml** to the Desktop
	  
1.	[] From your Desktop, open CCMEval.xml with Internet Explorer
	  
1.	[] Go through all the items and review what health checks the ccmeval performs
	  
	
	

	> [!KNOWLEDGE] CCMEval.xml is the configuration file that defines the checks and remediation actions against the client. It is unsupported to edit or alter this file.

> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1. []Log on to **NYCCL1**
	  
1.	[] Right-click **Start** &gt; **Windows PowerShell \(Admin\)**
	  
1.	[] Type services.msc and press Enter
	  
1.	[] Right-click **SMS Agent Host** and select **Properties**
	  
1.	[] Change Startup type to **Disabled**
	  
1.	[] Click Stop and then **OK**
	  
	
	

	> [!KNOWLEDGE] SMS Agent Host \(CCMExec.exe\) is the service that runs the ConfigMgr client, it should be always set to Automatic.





1. []Right-click **Start** &gt; **Windows PowerShell \(Admin\)**. Type wbemtest and press Enter
	  
1. 	[] Click **Connect…**
	  
1.	[] Replace root\\cimv2 with **root** in the Namespace field and click **Connect**
	  
1.	[] Click **Enum Classes**, select **Recursive**, and click **OK**
	  
1. 	[] Double-click **\_\_NAMESPACE** and click **Instances**
	  
1.	[] Select **\_\_NAMESPACE Name=”ccm”** and then click **Delete**
	  
1.	[] Select **Close** for all the dialog boxes and click **Exit**
	  
1.	[] In the search bar type **Control** to open Control Panel
	  
1.	[] From the **Control Panel** go to **System and Security** and click **Configuration Manager**
	  
1.	[] Confirm that no data is shown in the General tab
	  
	
	

	!IMAGE[Screenshot](screens/2fe0f7ac.jpg)



1. []Right-click **Start** &gt; **Windows PowerShell \(Admin\)**
	  
1.	[] Type **C:\\Windows\\Ccm\\Ccmeval.exe** and press Enter
	  
1.	[] Right-click **Start** &gt; **Run**. Type C:\\Windows\\Ccm\\Logs\\ and click **OK**
	  
1.	[] Open CCMEval.log and watch the progress
	  
	
	

	> [!ALERT] Wait for the CCMEval process to complete before proceeding to the next task. You can tell that the CCMEval has completed by looking at the CCMEval.log and looking for the word &quot;ccmeval finished&quot;. It will take approx. 5 minutes.

	> [!KNOWLEDGE] Check in the logs for the message that the remediation attempt has started



1. []Right-click **Start** &gt; **Windows PowerShell \(Admin\)**
	  
1.	[] Type services.msc and press Enter
	  
1.	[] Right-click **SMS Agent Host** and select **Properties**
	  
1.	[] Confirm that the **Startup type** is **Automatic \(Delayed Start\)**
	  
1.	[] In the search bar type **Control** to open Control Panel
	  
1.	[] From the **Control Panel** go to **System and Security** and click **Configuration Manager**
	  
1.	[] Confirm that the *General* tab is once again populated with information
	  
	
	


> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Go to **NYCCFG** and open the **Configuration Manager Console**
	  
1.	[] In the Configuration Manager Console, open the **Monitoring** workspace and select **Client Status**
	  
1.	[] On the ribbon, click **Schedule Client Status Update** and change Recur every to 1 hour and click **OK**
	  
1.	[] Click **Refresh Client Status** from the ribbon
	  
	
	


1. []In the **Monitoring** workspace, expand **Reporting** &gt; **Reports** and select the **Client Status** folder
	  
1.	[] Select **Client status summary** and right-click **Run**
	  
1.	[] Click **Values**
	  
1.	[] In the **Collection** value dialog box, select All Systems, and click OK
	  
1.	[] In the **Client Version** value dialog box, select All Configuration Manager client version, and click OK
	  
1.	[] Click **View Report**
	  
1.	[] Review and close the report
	  
	


1. []Select **Client remediation summary** report and right-click **Run**
	  
1.	[] Next to Collection, click Values
	  
1.	[] On the Parameter Value dialog box, select **All Systems**
	  
1.	[] Click **OK**
	  
1.	[] Next to Remediation Result, click Values
	  
1.	[] On the Parameter Value dialog box, select **Remediation Succeeded \(this option display only remediation succeeded clients\)** and click **OK**
	  
1.	[] Click **View Report**
	  
1.	[] Scroll right and click **1**
	  
	
	

	> [!KNOWLEDGE] The Client Remediation Details window appears displaying the one computer that reported a successful remediation for Windows Management Instrumentation \(WMI\) repository integrity test. Notice that the report also displays the date and time of when the client remediated.



**Congratulations!  **
  
You have successfully:  
  

- Saw how CCMEVAL is configured through the task scheduler and XML files



===

#Module 7, Lab 1, Excercise 1 - Verify and Troubleshoot Management Point  \(MP\) Availability

##Scenario

In this exercise, you will be able to:  
  

- Use logs and status components to verify management point availability 
- Leverage HTTP checks from the client to check management point status

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on to **NYCCFG**
	  
1.	[] Go to **Services** \(run services.msc\)
	  
1.	[] Select **SMS\_Site\_Component\_Manager**
	  
1.	[] Right-click **Properties** and change it to **Disabled**
	  
1.	[] Click **Apply** and then stop the service, click **OK**
	  
1.	[] Select **SMS Agent Host**
	  
1.	[] Right-click **Properties** and change it to **Disabled**
	  
1.	[] Click Apply and then stop the service, click OK
	  
1.	[] Right-click Start and run, type **inetmgr**
	  
1.	[] Expand NYCFGCFG and select Application Pools
	  
1.	[]Right click the SMS Management Point Pool application pool and select Stop
	  
	
	

	!IMAGE[Screenshot](screens/718dac6b.png)


> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1. []Log on to **NYCCL1**
	  
1.	[] In the search bar type Control to open **Control Panel**
	  
1.	[] From the Control Panel go to **System and Security** and click **Configuration Manager**
	  
1.	[] Go to **Actions** tab and select **Hardware Inventory Cycle**
	  
1.	[] Select **Run Now** and then **OK**
	  
	
	

	> [!KNOWLEDGE] You can also force a Policy Refresh action from the Configuration Manager Console, but only when the communication with the Management Point is healthy.



1. []Open the log C:\\Windows\\CCM\\Logs\\Ccmmessaging.log
	  
1.	[] Lok for error 0x8000000a
	  
	
	

	> [!ALERT] Wait approx. 1 minute

	> [!KNOWLEDGE] Error 8000000a means &quot;The data necessary to complete this operation is not yet available.&quot; which is a little bit confusing.  
	>   
	> In reality this is a first sign of communication problems with the Management Point



1. []Open Internet Exporer
	  
1.	[] In the address bar type http://nyccfg.contoso.com and then Enter
	  
1.	[] Confirm that IIS on the Server side is up and running by loading the IIS welcome page
	  
	
	

	> [!KNOWLEDGE] You can find the name of the server to connect by looking at the ccmmessaging.log


1.  []Still in Internet Explorer type http://nyccfg.contoso.com/sms\_mp/.sms\_aut?mplist
	  
1.	[] The message in Internet Explorer will show Error 503
	  
	
	

	> [!KNOWLEDGE] Error 50x usually indicates a problem on the server side, like a service is not available or an issue with the back end \(SQL\)  
	>   
	> For more information on troubleshooting HTTP errors check http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html


> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on to **NYCCFG**
	  
1.	[] Open File Explorer, navigate to *E:\\Program Files\\Microsoft Configuration Manager\\Logs*
	  
1.	[] Open *MPControl.log*, look for &quot;**Http test request**&quot; and confirms it is failing with the same error code 503 as the one showed when running the mplist url test
	  
	
	

	> [!KNOWLEDGE] The MPControl.log logs the activity of the MS\_MP\_CONTROL\_MANAGER, which is responsible for verifying management point availability.



> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Right-click Start and run services.msc
	  
1.	[] Select the **SMS Agent Host** service, right click and select *Properties*, change the startup type to *Automatic*. Click **Apply** and Start the service
	  
	
	

	> [!KNOWLEDGE] The Management Point service is the SMS Agent Host and needs to be running to process incoming requests from clients and processing inventory, state and status message information.  
	> The SMS Site Component Manager was also stopped because it tries to fix any component issues every 60 minutes, including reinstalling component that are unresponsive.


> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1.  []Go to NYCCL1
	  
1.	[] Open Internet Explorer and type http://nyccfg.contoso.com/sms\_mp/.sms\_aut?mplist
	  
1.	[] The message in Internet Explorer still shows an Error 503
	  
	
	

	> [!KNOWLEDGE] The MP relies on 2 components IIS and SMS Agent Host services, so they are all up and running, why is it still not working? It is a good test to check first that IIS is operational, but the MP also relies on the Application Pool to be started.


> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Go to NYCCFG
	  
1.	[] Right-click start and run **inetmgr**
	  
1.	[] Expand **NYCFGCFG** and select **Application Pools**
	  
1.	[] Right click the **SMS Management Point** **Pool** application pool and select **Start**
	  
1.	[] Go back to the **mpcontrol.log** and confirms that that you can see &quot;**Call to HttpSendRequestSync succeeded for port 80 with status code 200**&quot; which means that the MP is now healthy again.
	  
	
	

	> [!KNOWLEDGE] To speed up the process at step 5 you can restart the SMS Executive service

	!IMAGE[Screenshot](screens/423fa563.png)



1. []Go to Services
	  
1. []Select SMS\_Site\_Component\_Manager, 5ight-click Properties and change it to Automatic. Click **Apply** and then Start the service
	  
	
	

	> [!KNOWLEDGE] The Site Component Manager service is also responsible to keep all the components up and running. If a component or a service crashes the Site Component Manager will try to repair it - the check is repeated every 60 minutes. For testing purposes, we have disabled this service to avoid that it will restart the SMS Agent Host.  
	>   
	> The Site Component Manager is not able though to fix any Application Pool related issues, so you must start the SMS Management Application Pool if it fails.


> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1.  []Go to NYCCL1
	  
1.	[] Open Internet Explorer and type http://nyccfg.contoso.com/sms\_mp/.sms\_aut?mplist
	  
1.	[] Confirm that you can see the same information like in the ScreenShot \(click on the camera in the bottom left corner\)
	  
	
	

	!IMAGE[Screenshot](screens/a07dc163.PNG)



1. []Open the log C:\\Windows\\CCM\\Logs\\Ccmmessaging.log
	  
1.	[] Confirm that there are no more errors indicating that the comunication is back up
	  
	
	
> Switch to @lab.VirtualMachine(NYCCL1).SelectLink

1. []Log on to **NYCCL1**
	  
1.	[] In the search bar type Control to open **Control Panel**
	  
1.	[] From the Control Panel go to System and Security and click Configuration Manager
	  
1.	[] Go to Actions tab and select Hardware Inventory
	  
1.	[] Select **Run Now** and then **OK**
	  
1.	[] Wait approx. 2 minutes
	  
1.	[] Go to **NYCCFG**
	  
1.	[] Open the **Configuration Manager Console**
	  
1.	[] Navigate to Asset and Compliance &gt; Overview &gt; Devices &gt; Device Collections &gt; All Desktop and Server Client \(Show Members\)
	  
1.	[] Select **NYCCL1**
	  
1.	 []Right-click Start &gt; Resource Explorer
	  
1.	[] Navigate to Hardware &gt; Workstation Status
	  
1.	[] The date should be today's date
	  
	
	

	> [!KNOWLEDGE] You can check when the Inventory has finished by lookig at the InventoryAgent.log



Congratulations!  
  
You have successfully:  
Verified and Troubleshooted Management Point \(MP\) Availability

===

#Module 7, Lab 2, Excercise 1 - Backup and Verify

##Scenario

In this exercise you will:  
  

- Check the backup task configuration
- Initiate the backup task manually
- View backup results, log, and status messages

**Scenario:**  
The backup task must be enabled and configured. The installation of a site server does not automatically provide a means for this configuration.

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on to **NYCCFG**
	  
1.	[] Create the folder E:\\BackupSMS
	  
1.	[] Open the Configuration Manager Console
	  
1.	[] In the Configuration Manager console, open the Administration workspace and expand Site Configuration
	  
	1. Select Sites
	  
	1. Right-click CAS – Contoso CAS and select Site Maintenance
	  
	1. On the Site Maintenance dialog box, select Backup Site Server and click Edit
	  
	8. Verify that Enable this task is selected and click Set Paths
	  
	9. On the Set Backup Paths dialog box, verify the following configuration:  
	 Local drive on server for site data and database is selected  
	 Backup destination: **E:\\BackupSMS**
	  
	10. Click OK
	  
	11. Verify Enable alerts for backup task failures is selected and click OK
	  
	12. Click OK to close the Site Maintenance dialog box
	  
	
	




1. []Right-click Start &gt; Run. Type +++E:\\Program Files\\Microsoft Configuration Manager\\inboxes\\smsbkup.box+++ and click OK
	  
1.	[] Open smsbkup.ctl using the notepad and examine its content \(but do not make any changes\)
	  
1.	[] Right-click Start &gt; Run services.msc
	  
1.	[] Start the service SMS\_SITE\_BACKUP
	  
	
	

	> [!KNOWLEDGE] It's a common mistake to think that the service SMS\_SITE\_BACKUP should be set to automatic. This is a service that is triggered by the Site Maintennce task in Configuration Manager and it needs to be Manual.



1. []Open the log +++E:\\Program Files\\Microsoft Configuration Manager\\Logs\\smsbkup.log+++
	  
1.	[] Wait until the process completes with the text &quot;Backup Completed&quot;
	  
1.	[] In the Configuration Manager console, open the Monitoring workspace, expand System Status and select Component Status
	  
1.	[] Right-click SMS\_SITE\_BACKUP from Component column for the Site System NYCAS.CONTOSO.COM \(Site Code is CAS\), expand Show Messages, and select All \(careful not to select NYC site\)
	  
	
	

	> [!ALERT] It takes approx. 5 minutes to complete the backup  
	> Only proceed to the next exercise if your backup has completed successfully

	> [!KNOWLEDGE] Only proceed to the next exercise if your backup has completed successfully

	!IMAGE[Screenshot](screens/95ea70e0.png)



**Congratulations!  **
  
You have successfully:  
  

- Backup the CAS DB and Verified that is successfull.



===

#Module 7, Lab 2, Excercise 2 - Create Post-backup Objects

##Scenario

In this exercise you will:  
  

- Create objects on the CAS pot backup

**Scenario:**  
Backup completed successfully, but administration tasks have occurred since that time. We want to later verify recovery of those objects not contained in the backup from a reference primary

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on to NYCCFG
	  
1.	[] Open the Configuration Manager Console
	  
1.	[] Click Assets and Compliance workspace, right-click Device Collections, and select Create Device Collection
	  
1.	[] On the General page of the Create Device Collection Wizard, type: +++*Test Recovery*+++ as Name. Click Browse and select All Systems. Click OK &gt; Next
	  
1. 	[] Click Next. Click OK to accept the following warning message: This collection has no membership rules. It will not contain any members until at least one membership rule is defined
	  
1.	[] On the Summary page, click Next
	  
1.	[] On the Completion page, click Close
	  
1.	[] In the Configuration Manager console, open the Software Library workspace, expand Operating Systems, and select Task Sequences
	  
	1. Click Create Task Sequence on the ribbon
	  
	1. Select Create a new custom task sequence and click Next
	  
	1. Name the sequence Test Recovery and click Next &gt; Next &gt; Close
	  
	
> Switch to @lab.VirtualMachine(NYCCFG).SelectLink


1. []Log on to NYCCFG

1.  [] Open the Configuration Manager console

1.	[] Open the Assets and Compliance workspace, click Device Collections and verify that Test Recovery has replicated from the CAS
	  
1.	[] In the Configuration Manager console, open the Software Library workspace. Expand Operating Systems and select Task Sequences
	  
1.	[] Verify that Test Recovery has replicated from the CAS
	  
	
	

	> [!ALERT] Wait 5 minutes for the replication to complete


Congratulations!  
  
You have successfully:  
  

- Created 2 items after the backup, that will be used to check if the post recovery task works.



===

#Module 7, Lab 2, Excercise 3 - Simulate Catastrophic CAS failure

##Scenario

**Scenario:**  
The Central Administration server has been lost due to an irrecoverable corruption of the virtual server’s single virtual hard disk during a major power surge. This exercise simulates the creation of a replacement virtual server that has been loaded with the same server name and Microsoft SQL Server installation.


> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on NYCCFG
	  
1.	[] Right-click Start &gt; Run services.msc
	  
1.	[] Stop the SMS\_EXECUTIVE and the SMS\_SITE\_COMPONENT\_MANAGER
	  
1.	[] Right-click Start &gt; Command Prompt \(Admin\)
	  
1.	[] Type  
	+++sc delete SMS\_EXECUTIVE &amp;&amp; sc delete SMS\_SITE\_COMPONENT\_MANAGER+++
	  
	
	

	> [!ALERT] Triple check you are connected to NYCCFG!




1. []Open SQL Server Management Studio 
	  
1.	[] In the Connect to Server dialog box, type NYCCFG for Server name and click Connect
	  
1.	[] Expand Databases
	  
1.	[] Right-click CM\_CAS and click Delete. Select Close existing connections. Click OK.
	  
	
	

	> [!ALERT] Wait 5 minute before continuing with the next exercise.

	!IMAGE[Screenshot](screens/28db6c8c.png)



**Congratulations!  **
  
You have successfully:  
  

- Simulated a Catastrophic CAS failure



===

#Module 7, Lab 2, Excercise 4 - Recover CAS from Backup

##Scenario

In this exercise you will:  
  

- Use the backup set to recover the CAS
- Verify object recovery from NYCCFG site

**Scenario:**  
The replacement server is now available for recovery. Backups were enabled, and it has been less than five days since the backup. Recovery should proceed with a reinitialization of replication

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on NYCCFG
	  
1.	[] Open the Configuration Manager console
	  
1.	[] Click Monitoring workspace and select Database Replication. Click Refresh on the ribbon.
	  
1.	[] Select Replication Link Analyzer from the ribbon.
	  
1.	[] When prompted click Cancel twice to exit Replication Link Analyzer.
	  
	
	

	> [!ALERT] Wait until the link status shows as degraded before proceeding


> Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Log on NYCCFG
	  
1. [] Right-click Start &gt; Command Prompt \(Admin\)
	  
1. []Type regedit and click Enter
	  
1. []Go to HKEY_LOCAL_MACHI\\SOFTWARE\\Microsoft
	  
1. []Rename SMS with SMS.old and exit regedit
	  
1. []Go to E:\\BackupSMS\\CASBackup\\CD.Latest
	  
1. []Double-click splash\(.hta\)
	  
1. []Click Install
	  
1. []On the Before You Begin screen, click Next
	  
1. []Select Recover a site and click Next
	  
	
	

	> [!ALERT] We need to rename the SMS registry key to simulate a new site installation, if the Recovery Wizard detects an existing installation it will prevent the installation of the new binaries.

	> [!KNOWLEDGE] In a true recovery scenario, additional prerequisite items such as Windows Assessment and Deployment Kit \(ADK\) would need to be installed. We are avoiding many of these steps in this simulated failure scenario to reduce the overall time to complete this lab.






	  
1. []Under Recover this site server using an existing backup and Recover the site database using the backup set at the following location type E:\\BackupSMS\\CASBackup\\, and click Next
	  
1. []Type NYCCFG.CONTOSO.COM as the Reference Primary Site \(FQDN\). Click Next
	  
	
	

	> [!KNOWLEDGE] Many new options exist, including the ability to Reinstall this site server without a backup set. An SQL Server backup alone is sufficient, and that database may be restored manually through other processes as well



1. []Select Install the evaluation edition. Click Next
	  
	
	

	> [!KNOWLEDGE] We are using Evaluation for lab purposes only. In a real recovery scenario, you will need the product key. If that is not available during recovery, it must be entered before the evaluation period of 180 days expires. Failure to do so will result in the inability to manage the site until it is entered. To enter a product key, run Configuration Manager Setup from the start menu on the site server, as it will not be an option when running from DVD media




	  
1. []Accept all 3 licenses terms and click Next
	  
1. []On the Prerequisite Downloads page, select Use previously downloaded files and specify E:\\BackupSMS\\CASBackup\\CD.Latest\\redist\\ as the location and click Next
	  
1. []At **Site and Installation folder**
	- Select as Installation folder  
	+++E:\\Program Files\\Microsoft Configuration Manager\\+++  
	
	and click Next
	  
	
	

	> [!ALERT] If you get an error that you do not have permission to create registry key  
	> Open regedit  
	> Go to hklm\\software\\microsoft  
	> Select SMS and right-click Permissions…  
	> Add Full Control to the Administrators group  
	> Restart the machine NYCCFG and redo the steps in this exercise 
	> 

	!IMAGE[Screenshot](screens/4ad908ed.png)



1. []Click Next to confirm Database Information
	  
1. []On Database Information change both paths to E:\\ConfigMgrDB \(in a production environment it is recommended to use different drives for database and logs to achieve optimal performance\)

1. []Click Next at Diagnostic and Usage Data
	  
1. []Click Next At Settings Summary
	  
1.	[] On the Prerequisite Check page, wait for the prerequisite check to finish, and then click Begin Install
	  
1. [] Click View Log to examine the recovery progress in detail
	  
	
	

	> [!ALERT] This task will take approximately 20 minutes to complete

	> [!KNOWLEDGE] The log file can be found at C:\\ConfigMgrSetup.log



1.  []Go to E:\\Program Files\\Microsoft Configuration Manager\\Logs and open **sitecomp.log** and **rcmctrl.log**.
	  
1.	[] Confirm all the steps in the Install Wizard has the green check mark before continuing with the next task
	  
1. []Click Next on the Setup wizard. The Post-Recovery Actions screen is displayed
	  
1. []Click Close once you understand the actions required \(if any\)
	  
	
	

	> [!KNOWLEDGE] Rcmctrl.log displays the logging database replication processes

	!IMAGE[Screenshot](screens/6753dc2d.png)

> Switch to @lab.VirtualMachine(NYCCFG).SelectLink


1. []Open the Configuration Manager console on NYCCFG
	  
1.	[] Go to Monitoring &gt;Database Replication
	  
1.	[] Run the Replication Link Analyzer to confirm the replication is working again
	  
	
	  
	
	  
	- If you are prompted to take any action by the Replication Link Analyzer, exit with Cancel.
	  
	
	  
	
	  
1. []Go to the Initialization tabs and confirm all is at 100%
	  
1.	[] Go to the Replication Detail and confirm all Replication Groups are replicating with a time a few minutes from now

	 > Switch to @lab.VirtualMachine(NYCCFG).SelectLink
 
1.	[] Repeat steps 1-5 on NYCCFG
	  
	
	

	> [!ALERT] If you see that the replication is stuck in recovering deltas, restart NYCCFG

	> [!KNOWLEDGE] The replication state will stay on degraded for a few more minutes, if the result of the Replication Link Analyzer has all green checks, you can be sure it went OK.

	!IMAGE[Screenshot](screens/6ca3ba25.png)


	Switch to @lab.VirtualMachine(NYCCFG).SelectLink

1. []Go to NYCCFG
	  
1.	[] Confirm that the collection *Test Recovery* exists
	  
1.	[] Confirm that the task sequence Test Recovery exists
	  
	
	



**Congratulations!  **
  
You have successfully:  
  

- Recovered a CAS from Backup

Click Continue to close and finalize this lab.
