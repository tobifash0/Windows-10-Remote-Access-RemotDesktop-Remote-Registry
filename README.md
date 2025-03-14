# Overview: Lab 8 Windows 10 Remote Access: Remote Desktop, Remote Registry
This section of my home lab documentation focuses on setting up and using Remote Desktop and Remote Registry for remote access to a Windows 10 machine in a VirtualBox environment. The project covers the steps for enabling, configuring, and troubleshooting remote access services to allow users and administrators to connect to and manage a Windows 10 PC remotely.

## Objectives
1. Windows 10 Remote Management: Configuring and managing remote access to Windows 10 systems.
2. Remote Registry: Exploring the Remote Registry feature to manage registry settings from another computer.
3. Remote Desktop: Setting up and utilizing Remote Desktop for secure remote control of Windows 10 systems.
4. C$ Administrative Share: Understanding and using the hidden C$ administrative share for file and system access.

## Documentation
In this home lab, we will focus on using Windows 10 Remote Management, Remote Registry, Remote Desktop, and accessing C$. Let's begin by enabling Windows 10 Remote Desktop Services on Desktop2 for Bob. On Desktop2, open File Explorer, right-click on "This PC," and select "Advanced System Settings." Next, use your Helpdesk administrative permissions to enable "Allow Remote Connections" and click on "Select Users" to add the necessary users.

<br>

![image](https://github.com/user-attachments/assets/1353b7b0-4da0-4838-851b-147347ed0bca)

<br>

1. Select “Add” then add Helpdesk then select “OK” then “Apply”.

<br>

![Screenshot 2025-03-14 at 12 10 35 AM](https://github.com/user-attachments/assets/8337f3a5-da81-4a35-8912-dadd08177dfe)

<br>
2. Now that Remote Desktop is enabled, let's switch to the Helpdesk account. Search for "Remote Desktop Connection" in the Windows search bar and open the application. In the "Computer" field, type "Desktop2" and log in using your Helpdesk credentials. Once the remote session is active, you can select "Yes" to disconnect Bob's session, allowing you to log in to Desktop2 under the Helpdesk account.

<br>

![image](https://github.com/user-attachments/assets/12ea27e0-3aff-46b6-ab35-c5a9717be027)

<br>

3. Now that we're remotely accessing Bob's computer from the Helpdesk account, we can perform various tasks. For example, we can create a new folder for Bob by navigating to his folder, then opening the "Desktop" directory and creating a folder there.

<br>

![image](https://github.com/user-attachments/assets/dbc523c9-c4f4-45d3-8768-b4ac4edc56fe)

<br>

4. We can also delete things in Bob’s download’s folder if Bob wants to.

<br> 

![image](https://github.com/user-attachments/assets/ce73a29d-2c48-4f5d-9a32-fbb12f28e66e)

<br>

5. We can also access Bob’s AppData folder by navigating to User → Bob and typing \appdata in the File Explorer search bar. This will allow us to view and manage the contents of Bob’s AppData directory.

<br>

![image](https://github.com/user-attachments/assets/c9d79f23-9189-4aa9-87f8-6bf4b8b7502c)

<br>

6. Let's disconnect from the Remote Desktop Connection and log back in as Bob on Desktop2. Once logged in, we should see the "Test" folder on Bob's desktop.

<br>

![image](https://github.com/user-attachments/assets/da9886b3-d641-48ed-972e-320479a662a4)

<br>

7. Next, let's show how to determine shared drives. On Desktop2, open Command Prompt (CMD) and type net use. This will display a list of all the network drives currently mapped to the system.

<br>

![image](https://github.com/user-attachments/assets/3347e42b-b8e4-4555-8a7d-219839068f01)

<br>

8. Another way to determine shared drives is to search for "Services" in the Windows search bar and run it as Administrator. Use Helpdesk credentials to bypass. In the Services window, search for "Remote Registry," right-click on it, and select "Properties." Change the "Startup type" from "Disabled" to "Automatic," then click "Apply" and "OK." After that, click "Start" to enable the Remote Registry service. This will allow access to registry information, including shared drives.

<br> 

![image](https://github.com/user-attachments/assets/996d1c85-750f-4f6a-bdd8-e7fd666b230a)

<br> 
9. Now lets go to our Helpdesk account, search up “Registry Editor”

<br> 

![image](https://github.com/user-attachments/assets/67ded443-ba8d-4402-9d90-df9c30ca3f37)

<br> 

10. Select File on the top left → Connect Network Registry → then search “Desktop2” then “OK”.

<br> 

![image](https://github.com/user-attachments/assets/40dd711c-ba0b-4f88-9c85-8ebb106958a4)

<br> 

11. Under HKEY_USERS, we need to browse through the folders to find the one associated with the "Z" drive under the "Network" section. This will show the shared drives that are mapped to the system. The drive letter "Z" will be listed within the registry key associated with the network shares, which helps to identify the shared drives connected to the machine.

<br> 

![image](https://github.com/user-attachments/assets/2347323c-371f-4910-8217-7eebd35e6f8e)

<br>

12. Now, let's use the C$ command with our Helpdesk account, which allows administrators to remotely access the root of the C: drive on the local user account. To do this, open File Explorer on Helpdesk and type \Desktop2\c$ in the search bar, then press Enter. This will grant access to the C: drive of Desktop2 remotely.

<br> 

![image](https://github.com/user-attachments/assets/e0a6cc6d-3494-4f7c-9c03-2eb4eff757f5)

<br>

13. From here, we can delete the "Test" folder we created remotely. Navigate to Users → Bob → Desktop, and then locate the "Test" folder. Once found, simply delete the folder to remove it from Bob's desktop.

<br> 

![image](https://github.com/user-attachments/assets/1bb0551e-1a11-4012-96c7-b57e3478b437)

<br>

14. Now if we check back on Bob’s computer we see that the “Test” folder is no longer in Bob’s desktop.

<br> 

![image](https://github.com/user-attachments/assets/c954d057-3cc6-401b-8839-7146cbcd91ea)

<br>

15. Another way to remote into a users is using Windows Remote Assistance by typing “Windows Remote Assistance” in the Windows search on Desktop2 → then select “Invite someone you trust to help you”.

<br>

![image](https://github.com/user-attachments/assets/4dc0fe20-8756-4fa3-8e30-96fffbcd2afb)

<br> 

16. Select “Save this invitation as file” on desktop.

<br> 

![image](https://github.com/user-attachments/assets/08c4de3e-94fc-4085-abe5-bca67bf65c84)

<br> 

17. Now, back on the Helpdesk account, open Windows Remote Assistance and select Help Someone Who Has Invited You. In the prompt, type \Desktop2\C$ to access the invitation file. Once connected, navigate to Users → Bob → Desktop and locate the invitation file there. Afterward, you can enter the password provided in the invitation to establish the remote session.

<br> 

![image](https://github.com/user-attachments/assets/34bedf44-aded-4610-baae-64bd62054bb5)

<br> 

18. A prompt will ask if we want to allow Helpdesk to remote access, select “Yes”.

<br> 

![image](https://github.com/user-attachments/assets/28500fd8-1be0-4465-8cce-a7e7bc2fbcd0)

<br> 

19. Now we have remote control of Bob’s computer on Helpdesk.

<br> 

![image](https://github.com/user-attachments/assets/3e60b18c-bcf1-4410-828c-31cf273a9e8b)

<br> 

20. Now we can send chats to Bob, request control access on the top left.

<br> 

![image](https://github.com/user-attachments/assets/756a0931-fd58-4fb1-a2ff-fc14f70244b6)

<br>

21.Congratulations! we have successfully access Windows 10 Remote Management exploring the Remote Registry feature, setting up and utilizing Remote Desktop for secure remote control of Windows 10 system and using C$.

<br> 

👉 [Next Lab 9 : RSOP, Group Policy, Task Manager, Disable Logoff](https://github.com/tobifash0/RSOP-Group-Policy-Task-Manager-Disable-Logoff)
