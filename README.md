<h1>Overview: Lab 9 RSOP, Group Policy, Task Manager, and Disable Logoff</h1>

This section of my home lab documentation focuses on configuring **Group Policy**, using **RSOP (Resultant Set of Policy)**, managing **Task Manager** settings, and implementing a configuration to **disable logoff** in a Windows environment. The project demonstrates how to enforce specific policies across machines in a domain, monitor the effective policies using RSOP reports, and control system settings like logoff behavior and Task Manager access. 

<h2>Objectives</h2>

1. **RSOP (Resultant Set of Policy):** Use RSOP to generate reports on the effective policies applied to computers and users.
2. **Group Policy Configuration:** Create and configure Group Policies to enforce specific settings across domain-joined computers, including logoff policies and Task Manager access.
3. **Task Manager Management:** Customize Task Manager settings to control access, visibility, and processes for users in the domain.
4. **Disable Logoff:** Configure policies to disable logoff on domain-joined machines, ensuring users remain logged in for administrative purposes.
5. **Policy Troubleshooting:** Troubleshoot and resolve policy application issues using RSOP and Group Policy tools.


<h2>Documentation</h2>

In this home lab, we will use RSOP commands, Group Policy Management, Task Manager, and disable logoff functionality. First, let's start by disabling Task Manager.

To do this, open **Server Manager** on your Windows Server 2022 account. Then, select **Tools** and click on **Group Policy Management**. In the Group Policy Management console, select **Group Policy Objects** under the **SimoTech.com** domain. From here, we can configure the Group Policy to disable Task Manager.



1. <p align="center">
   <img src="https://i.imgur.com/W6nbrCt.png" height="80%" width="80%" alt="Disk Sanitization Steps 1"/>
   <br />
   <br />
</p>

Next, right-click on Group Policy Objects and select New. Name the new policy "Task Manager". After creating it, select the Task Manager policy under Group Policy Objects. Then, go to the Delegations tab and select Add. Add Bob to grant him the necessary permissions for this policy.

2. <p align="center">
   <img src="https://i.imgur.com/qMjgLMS.png" height="80%" width="80%" alt="Disk Sanitization Steps 2"/>
   <br />
   <br />
</p>



3. <p align="center">
   <img src="https://i.imgur.com/yZmNdkU.png" height="80%" width="80%" alt="Disk Sanitization Steps 3"/>
   <br />
   <br />
</p>

Right-click on Task Manager, select Edit, then go to User Configuration → Administrative Templates → System. Next, select Ctrl+Alt+Del Options.

4. <p align="center">
   <img src="https://i.imgur.com/Eoi0hOz.png" height="80%" width="80%" alt="Disk Sanitization Steps 4"/>
   <br />
   <br />
</p>

Here we will enable “Remove Change Password” and “Remove Task Manager”

5. <p align="center">
   <img src="https://i.imgur.com/v6DOzqO.png" height="80%" width="80%" alt="Disk Sanitization Steps 5"/>
   <br />
   <br />
</p>

Then back on the Group Policy Management, grab the “Task Manager” and move it to “HR”. Select “Yes”

6. <p align="center">
   <img src="https://i.imgur.com/NHQua5s.png" height="80%" width="80%" alt="Disk Sanitization Steps 6"/>
   <br />
   <br />
</p>

Select “Enforced” by right-clicking on it.

7. <p align="center">
   <img src="https://i.imgur.com/LY4lfG5.png" height="80%" width="80%" alt="Disk Sanitization Steps 7"/>
   <br />
   <br />
</p>

Now, on Bob's account on Desktop2, open CMD and type the command gpupdate /force. This will immediately refresh the Group Policy settings for both the computer and user accounts.

8. <p align="center">
   <img src="https://i.imgur.com/KdzHJWS.png" height="80%" width="80%" alt="Disk Sanitization Steps 8"/>
   <br />
   <br />
</p>

After updating the Group Policy on Bob's computer, right-click on the taskbar, and you'll see that Task Manager is now greyed out, indicating that access has been successfully disabled.

9. <p align="center">
   <img src="https://i.imgur.com/EUt5ho4.png" height="80%" width="80%" alt="Disk Sanitization Steps 9"/>
   <br />
   <br />
</p>

If we press Ctrl+Alt+Del on the virtual machine, we will see that the Change Password option has been removed, reflecting the changes made through Group Policy.

10. <p align="center">
    <img src="https://i.imgur.com/JAaezxV.png" height="80%" width="80%" alt="Disk Sanitization Steps 10"/>
    <br />
    <br />
</p>

To check which group policies have been applied to Bob's computer, open the command line and type gpresult /r. This will display the results of the Group Policy settings for both the computer and user accounts.


11. <p align="center">
    <img src="https://i.imgur.com/n07rduH.png" height="80%" width="80%" alt="Disk Sanitization Steps 11"/>
    <br />
    <br />
</p>

If you type taskmgr in the command line, a prompt will appear stating that Task Manager is disabled, confirming that the Group Policy to disable Task Manager has been successfully applied.

12. <p align="center">
    <img src="https://i.imgur.com/9wXbpsb.png" height="80%" width="80%" alt="Disk Sanitization Steps 12"/>
    <br />
    <br />
</p>

If you run Command Prompt as Administrator and then type taskmgr, Task Manager should open, as administrative privileges can bypass the policy restrictions applied to regular users.


13. <p align="center">
    <img src="https://i.imgur.com/0pdK2Jm.png" height="80%" width="80%" alt="Disk Sanitization Steps 13"/>
    <br />
    <br />
</p>

To generate a Group Policy report, go to Group Policy Management, right-click on Group Policy Results, and select Group Policy Results Wizard.... This will guide you through the process of generating a detailed report on the applied Group Policy settings.

14. <p align="center">
    <img src="https://i.imgur.com/JBuW7LW.png" height="80%" width="80%" alt="Disk Sanitization Steps 14"/>
    <br />
    <br />
</p>

Click Next, then select Another Computer and click Browse. Type in Desktop2 and select it, then click Next to proceed with generating the Group Policy report for that computer.

15. <p align="center">
    <img src="https://i.imgur.com/LK5Pk2b.png" height="80%" width="80%" alt="Disk Sanitization Steps 15"/>
    <br />
    <br />
</p>

Select SimoTech\Bob, click Next, and then click Finish. This will generate a report for Bob's Group Policy settings.

16. <p align="center">
    <img src="https://i.imgur.com/tHJS9KG.png" height="80%" width="80%" alt="Disk Sanitization Steps 16"/>
    <br />
    <br />
</p>

If you select the Details tab at the top of the report, it will display all of the policies that have been applied to Bob's account, giving you a detailed view of the Group Policy settings.

17. <p align="center">
    <img src="https://i.imgur.com/eRBXpJd.png" height="80%" width="80%" alt="Disk Sanitization Steps 17"/>
    <br />
    <br />
</p>


Congratulations! We have successfully leveraged RSOP commands, explored Group Policy settings, utilized Task Manager, disabled logoff functionality, removed the ability to change passwords, and restricted access to Task Manager.

 👉 [Next Lab 10 : Installing and Deploying Software with PDQ](https://github.com/melvinensahsl/Installing-and-Deploying-Software-with-PDQ/tree/main)
