# Configuring Linux File Permissions
<h2>Description</h2>
In this project, I practiced the principle of least privilege by using bash commands on Linux to change file permissions. I investigated the directory to identify misconfigured permissions.  

<h2>Check file and directory details (examples highlighted in yellow!)</h2>
To start my investigation, I used the “pwd” command to see my current directory.

<br>I used the “ls” command to view the current folders and files discovered “projects”

After that, I navigated to the “projects” folder by using the “cd projects” command. <br>The "cd" command is used when you wantto change directory. Add "cd" and then the "name" of the folder you want to navigate to.

I typed the” ls -l” command to view the files and folder permissions of files and folders in the "projects folder. <br>

I typed in the “ls -la” command to view the permissions for hidden files and folders, then I discovered a hidden file called “.project_x.txt” 

<img src="https://imgur.com/ERqgvsL.png" height="80%" width="80%"/>

<h2>Change file permissions  (examples highlighted in yellow!)</h2>
The project_k.txt file was misconfigured for “other” 

project_k.txt reads “-rw-rw-rw-” <br>

Here is how to read these characters:

| Character | Example | Meaning |
|----------|----------|----------|
| 1st   | **d**rwxrwxrwx   | **File Type** <br> **d** for directory <br> **-** for a regular file    |
||||
| 2nd    | d**r**wxrwxrwx   | **Read Permissions for the user** <br> **r** if the user has Read permissions <br> **-** if the user lacks Read permissions|
| 3rd    | dr**w**xrwxrwx    | **Write Permissions for the user** <br> **w** if the user has Write permissions<br> **-** if the user lacks Write permissions  |
| 4th    | drw**x**rwxrwx    | **Execute Permissions for the user** <br> **r** if the user has Execute permissions <br> **-** if the user lacks Execute permissions    |
||||
| 5th    | drwx**r**wxrwx    | **Read Permissions for the group** <br> **r** if the group has Read permissions <br> **-** if the group lacks Read permissions    |
| 6th    | drwxr**w**xrwx    | **Write Permissions for the group** <br> **r** if the group has Write permissions <br> **-** if the group lacks Write permissions    |
| 7th    | drwxrw**x**rwx    | **Execute Permissions for the group** <br> **r** if the group has Execute permissions <br> **-** if the group lacks Execute permissions    |
||||
| 8th    | drwxrwx**r**wx    | **Read Permissions for the other** <br> **r** if the other has Read permissions <br> **-** if the other lacks Read permissions    |
| 8th    | drwxrwxr**w**x    | **Write Permissions for the other** <br> **r** if the other has Write permissions <br> **-** if the other Write permissions    |
| 10th    | drwxrwxrw**x**    | **Execute Permissions for the other** <br> **r** if the other has Execute permissions <br> **-** if the other lacks Execute permissions    |

“Other”  had permission to write and should only have read permissions.

<img src="https://imgur.com/9Rbi2DX.png" height="80%" width="80%"/>

I typed ”chmod o-w project_k.txt” to remove write permissions from “other”. 
<br>It now reads” -rw-rw-r- -” and is configured to read only.

<img src="https://imgur.com/uYSFSho.png" height="80%" width="80%"/>

project_m.txt file permission for the research_team group had read permissions. 

<img src="https://imgur.com/OABjUW3.png" height="80%" width="80%"/>

I typed “chmod g-r project_m.txt” to remove read permissions from the research_team group. 
<br>It now reads “-rw- - - - - -” so the group "research_team" has no access at all.

<img src="https://imgur.com/erY1xu1.png" height="80%" width="80%"/>

<h2>Change file permissions on a hidden file  (examples highlighted in yellow!)</h2>
The user “researcher2” and group “research_team” have incorrect permissions. 
<br>They both have the write permissions and the research_team is not able to read the hidden file “.project_x.txt” 
<br>The permission reads “-rw- - w - - - - -”  
<img src="https://imgur.com/DuRIUBr.png" height="80%" width="80%"/>

To change to  the correct permissions I typed “chmod u-w, g-w, g+r .project_x.txt” 
<br>It now reads “-r- r - - - - -” Only the user and group can read this hidden file now

<img src="https://imgur.com/uAtCW4R.png" height="80%" width="80%"/>

<h2>Change directory permissions  (examples highlighted in yellow!)</h2>
The group “research_team” has access to the “drafts’” folder when they shouldn't have.
</br>“ Drwx- - x - - -” means research_team has executable permissions, therefore they have access.

<img src="https://imgur.com/FEGsjbv.png" height="80%" width="80%"/>

I typed” chmod g-x drafts” to remove access to drafts from the group “research_team” 
</br>It now reads “drwx - - - - - -” research_team has no permissions or access to the folder now.
<img src="https://imgur.com/7FE73do.png" height="80%" width="80%"/>


<h2>Summary</h2>
In conclusion, I identified regular files and hidden files that had misconfigured permissions and was able to change these permissions back to a secure configuration, therefore increasing this fictional company's security posture.


