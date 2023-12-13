# Configuring Linux File Permissions
<h2>Description</h2>
In this project, I was given a task to improve a fictional company's security posture. I practiced the principle of least privilege by using bash commands on Linux to configure file permissions to a secure state.

# Check file and directory details (examples highlighted in yellow!)</h2>

To start my investigation, I used the `pwd` command to see my current directory.

I used the `ls` command to view the current folders and files, and I discovered the `projects` folder.

After that, I navigated to the `projects`folder by using the `cd` `projects` command. <br>

The `cd` command is used when you want to change the directory. 

Add `cd` and then add your argument, which is the "name" of the directory. </br>

I typed the `ls -l` command to view the files and folder permissions of files and folders in the `projects` folder. <br>

I typed in the `ls -la` command to view the permissions for hidden files and folders, then I discovered a hidden file called `.project_x.txt` <Br>

Having "`.`" in front of the file indicates that the file is hidden.

<img src="https://imgur.com/ERqgvsL.png" height="80%" width="80%"/>

# Change file permissions  (examples highlighted in yellow!)
The `project_k.txt` file was misconfigured for “other” 

`project_k.txt` reads `-rw-rw-rw-` <br>

Here is how to read these 10 string permissions:<Br>
| Letter | Description |
|----------|----------|
|  `r`   | `Read`: This is the ability to read all contents in the directory including both files and subdirectories |
|  `w` | `Write`: This is the ability to make modifications on the file contents; for directories, this is the ability to create new files in the directory |
|  `e` | `Execute`: This is the ability to execute the file if it’s a program; for directories, this is the ability to enter the directory and access its files|

| Owner Type | Description |
|----------|----------|
| `USER` | The owner of the file |
| `GROUP` | A group that the owner is part of |
| `OTHER` | All other users on the system


| Character | Example | Meaning |
|:---|  :--- |  :--- |
| 1st   | `d`rwxrwxrwx   | File Type <br> `d` for directory <br> `-` for a regular file    |
||| **USER (2nd to 4th character)**|
| 2nd    | d`r`wxrwxrwx   | `Read` Permissions for the `user` <br> `r` if the `user` has `Read` permissions <br> `-` if the `user` lacks `Read` permissions|
| 3rd    | dr`w`xrwxrwx    | `Write` Permissions for the `user` <br> `w` if the `user` has `Write` permissions<br> `-` if the `user` lacks `Write` permissions  |
| 4th    | drw`x`rwxrwx    | `Execute` Permissions for the `user` <br> `x` if the `user` has `Execute` permissions <br> `-` if the `user` lacks `Execute` permissions    |
||| **GROUP (5th to 7th character)**|
| 5th    | drwx`r`wxrwx    | `Read` Permissions for the `group` <br> `r`if the `group` has Read permissions <br> `-`if the `group` lacks `Read` permissions    |
| 6th    | drwxr`w`xrwx    | `Write` Permissions for the `group` <br> `w` if the `group` has Write permissions <br> `-` if the `group` lacks `Write` permissions    |
| 7th    | drwxrw`x`rwx    |`Execute` Permissions for the `group` <br> `x` if the `group` has Execute permissions <br> `-` if the `group` lacks `Execute` permissions    |
|||**OTHER (8th to 10th character)**|
| 8th    | drwxrwx`r`wx    | `Read` Permissions for the `other` <br> `r` if the `other` has `Read` permissions <br> `-` if the `other` lacks `Read` permissions    |
| 9th    | drwxrwxr`w`x    | `Write` Permissions for the `other` <br> `w` if the `other` has `Write` permissions <br> `-` if the `other` lacks `Write` permissions    |
| 10th    | drwxrwxrw`x`    | `Execute` Permissions for the `other` <br> `x` if the `other` has `Execute` permissions <br> `-` if the `other` lacks `Execute` permissions    |

<br> From the tables `-rw-rw-rw-` means that `User`, `Group`, and `Other` have `rw-` permissions, this tells us that each group has `read` and `write` with no execute permissions because of the `-` symbol at the end means it lacks `execute` permissions. `Other` should not have `write` permissions.

<img src="https://imgur.com/9Rbi2DX.png" height="80%" width="80%"/>

| Command | Description | Argument 1 | Argument 2 |
|:---|  :--- | :--- |:--- |
| `chmod` | Used to modify or change permissions with 2 Arguments | Indicates what permission you want to change, `U` for `User`, `G` for `Group`, `O` for `Other`. <br> You use the `+` or `-` symbols to add or delete read `r`, write `w`, or execute `x`permissions | Indicates which file or folder you want to change permissions for |

<br>I typed `chmod` `o-w` `project_k.txt` to remove `write` permissions from `other`.

| Command | Argument 1 | Argument 2 |
|:---|  :--- | :--- |
| `chmod` | `o-w` (remove `write` permissions of `other`) | `project_k.txt` (the file modified for the command) |


<br>After I typed this command. It now reads `-rw-rw-r--`. `Write` permissions are now removed from `other`.
<img src="https://imgur.com/uYSFSho.png" height="80%" width="80%"/>

`project_m.txt` file permission for the `research_team` `group` had `read` permissions when they shouldn't have.

<img src="https://imgur.com/OABjUW3.png" height="80%" width="80%"/>

I typed `chmod` `g-r` `project_m.txt` to remove `read` permissions from the `research_team` `group`. 
| Command | Argument 1 | Argument 2 |
|:---|  :--- | :--- |
| `chmod` | `g-r`(remove `read` permission for `group`) | `project_m.txt` (the file modified for the command) |

<br>It now reads `-rw------` so the `research_team` `group` has no access at all.

<img src="https://imgur.com/erY1xu1.png" height="80%" width="80%"/>

# Change file permissions on a hidden file  (examples highlighted in yellow!)
Remember hidden files have "." in front of file names.
The `user` `researcher2` and `group` `research_team` have incorrect permissions for the hidden file `.project_x.txt`

The current permission reads`-rw--w-----` This indicates that the `user` has `read` and `write` permissions while the group has `write` permissions.

Both the `user` and the `group` should only have `read` permissions and no `write` permissions. 

So now I need to remove the `write` permissions for both the `user` and the `group` while adding `read` permissions to the `group`. 
<img src="https://imgur.com/DuRIUBr.png" height="80%" width="80%"/>

To change to  the correct permissions I typed `chmod` `u-w`, `g-w`, `g+r` `.project_x.txt` 
| Command | Argument 1 | Argument 2 |
|:---|  :--- | :--- |
| `chmod` | `u-w`(remove `write` permissions for "user"),`g-w`(remove `write` permissions for `group`),`g+r`(add `read` permissions for `group`) | `project_x.txt` (the file modified for the command) |

<br>It now reads `-r--r-----` Only the `user` and `group` can `read` this hidden file now.

<img src="https://imgur.com/uAtCW4R.png" height="80%" width="80%"/>

# Change directory permissions  (examples highlighted in yellow!)
The `research_team` `group` has access to the `drafts` folder when they shouldn't have.

`Drwx--x---` means `research`_team has `execute` permissions, therefore they have access. 

Remember the first character that has `d` means directory. If it is `-` it means file.

<img src="https://imgur.com/FEGsjbv.png" height="80%" width="80%"/>

I typed `chmod` `g-x` `drafts` to remove access to `drafts` from the `group` `research_team` 
| Command | Argument 1 | Argument 2 |
|:---|  :--- | :--- |
| `chmod` | `g-x`(remove execute permission for `group`) | `drafts` (the folder modified for the command) |

It now reads `drwx------` `research_team` has no permissions or access to the folder now.

Only the `user` has `read`, `write`, and `execute` permissions.
<img src="https://imgur.com/7FE73do.png" height="80%" width="80%"/>


# Summary
In conclusion, I identified regular files and hidden files that had misconfigured permissions and was able to change these permissions back to a secure configuration, therefore increasing this fictional company's security posture. My key takeaway from this project is that reducing the amount of people who have access to sensitive data will decrease the likelihood of a data breach due to fewer insider threats. Configuring permissions to only people who need such access to data is crucial in keeping private data safe. 


