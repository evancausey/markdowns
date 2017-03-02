# The TortoiseGit Experience with GitLab
This work instruction shows our experience loading and configuring ***“Git for Windows,”*** ***“TortoiseGit”*** and the network GitLab site.

It describes how to perform standard tasks using TortoiseGit.

It describes how to use Git from the Linux command line.

## Getting Started - Loading the Programs
--------------------------
Google ***“Git for Windows.”*** Go to the site, download and install the program.  No problems.


When writing this document we navigated to the website https://git-scm.com/download/win and downloaded Git **2.2.0.0**.

Search ***“TortoiseGit”*** on Google.  Go to the site, download and install the program.  No problems.

When writing this document we navigated to the website https://tortoisegit.org and downloaded TortoiseGit **2.9.2.windows.1**.

You can view the version numbers for Git and TortoiseGit by right clicking on ***"TortoiseGit > About."***

## Generating an SSH Key 
----------------------
The following steps describe how to generate an SSH key.
1. Navigate to the folder in which you would like to create an SSH key.
Note that our folder of choice was ***h:/.ssh.*** We chose this folder after observing that Git Gui was searching for an SSH key at this location.
2. Once you are inside of the designated .ssh folder, type ***ssh-keygen -t rsa -C "[first].[last]@ga-asi.com"***, but with your name explicitly listed.
3. Hit enter and ssh-keygen will prompt you to name the files it is about to create containing the keys.
For example, we chose the name ***“id_rsa.”*** 
4. Hit enter and ssh-keygen will prompt you for a password.
Note that we left the password blank. This will allow you to push and pull to and from the remote repository without needing to type in a password every time.
5. Enter your ***“password”*** twice and ssh-keygen will respond with either success or fail.
Note that if the process was successful you can type ***“ls -l”*** and see the newly created files along with a timestamp for the files.


## Creating a RSA Key when Using TortoiseGit (Alternative Method)
--------------------------
This approach only works if you have no other id_rsa.pub files located in any .ssh folders on your windows machine.

Using the Windows File Explorer, right click on any directory name, then click ***“Git GUI Here.”***  

Click on ***“Help.”*** Click the ***“Generate Key”*** button and the “Copy to Clipboard” button, then close the dialog box. 
![guiHelp](Images/GitGuiHelpRSAKey_gitInstruction.png)
This automatically enters the key in TortoiseGit.


## Signing into GitLab on the Network
--------------------------
Browse to http://ms-gitlab.ga.com/users/sign_in to sign in to GitLab.  

If you are still signed in, it will tell you so.  Otherwise, a box pops up as shown on the following figure.
 ![gitlabSignIn](Images/Signon_gitInstruction.png)
Enter your standard user ID and your password that you use every time you log into your windows computer. 

If desired, click ***“Remember me”*** to potentially skip this step next time.



## Properly Copying the SSH Key from Git Gui to GitLab
--------------------------
The following steps describe how to properly copy an SSH key located on Git Gui to the 
GitLab website.
1. Right click on any folder and navigate to ***“Git Gui Here.”***
2. Click on Git Gui here and a window will appear on your screen.
3. Located on the top of the form is a tab labeled ***“help.”***
4. Left click on help and navigate to ***“Show SSH key.”***
5. Click on show SSH key and a window will appear on your screen.
![guiSSHHelp](Images/gitGuiHelpSSH_gitInstruction.PNG)
6. This form will display the current SSH key Git is using to pull and push from the remote repository.
Note that if this is not the key you created, the form also displays the path of where it is locating the SSH key. Follow this path and set your SSH key accordingly.
7. Located at the bottom of the form is a button labeled ***“Copy to Clipboard.”*** 
Note that during the creation of this document we observed that if you skip this step and copy the key directly from the ***.ssh/yourfile,*** 
the key will create a fingerprint when you attempt to add the key to GitLab.
8. Log onto your GitLab account. 
9. Locate and click the ***"Profile Settings”*** tab located inside the menu tab on the upper left corner of the browser window.
In the upper left corner of the browser window, click on the menu icon that looks like this. ![gitlabMenuIcon](Images/MenuIcon_gitInstruction.png) 
It will open up as follows.
![gitlabMenu](Images/MainMenu_gitInstruction.png)
10. Then click on ***“SSH Keys”*** at the top of the new page.
11. In the textbox labeled ***“key”*** paste the key you just copied into your clipboard from the Git Gui.
Note that after you complete this step the textbox labeled ***“Title”*** will be automatically filled with the email address at the end of your SSH key. If it doesn’t automatically fill you can enter the name by hand.
12. After making sure all required fields are filled in, click ***“Add Key”*** and the browser will respond with either success or fail. 
![sshKeygen](Images/SSHKeyGen_gitInstruction.png)   
13. After making sure all required fields are filled in click ***“Add Key”*** and the browser will respond with either success or fail. 
Note that if the key was added successfully you will receive an email informing you that a key was added to your account.

## Problems Creating a RSA Key for SSH Encoding in Windows (Using the "Generate It" Link Displayed Above)
--------------------------

Click on the ***“generate it”*** link shown in the figure above to display instructions for generating a RSA key.
In my case, the instructions had some problems.  For Windows, it says to type the following.
```sh
type %userprofile%\.ssh\id_rsa.pub
```
##### Did that work?  No.
```sh
C:\Windows\system32Ftype %userprofile%
Access is denied.

C:\>echo %USERPROFILE%
C:\Users\[MyId]

C:\>set userprofile
USERPROFILE=C:\Users\[MyId]

C:\Users>type %userprofile%\.ssh\id_rsa.pub
```

The system cannot find the path specified.


The instructions displayed in GitLab say to type the following
```sh
ssh-keygen -t rsa -C "[first].[last]@ga-asi.com",but with your name explicitly listed.
```
>>This worked in my case, but the files did not show up under the ***“C:\Users”*** directory.  Instead, the files were found in ***“c:\cygwin\home\[MyID]\.ssh”*** .  I guess it’s lucky I had Cygwin installed.  When I renamed the Cygwin directory to CygWin1, the ssh generation did not work, i.e. the ssh-keygen program would not run – there was no direct windows program of that name.  When the ssh-keygen program ran, it printed out a bunch of hex digits, but it turned out they could not be used in the GitLab box which then displayed an error.  Instead, the actual contents of the file named id_rsa.pub in the directory ***“c:\cygwin\home\[MyID]\.ssh”*** contained the public RSA key and that is what was required and accepted by GitLab.  I used my favorite editor to copy it to the clipboard.  There is another file in there named id_rsa, which contains the corresponding private key – keep it private.


## Configuring TortoiseGit Credentials for HTTP
--------------------------
1. Right click on any folder on your PC and navigate to ***“TortoiseGit > Settings.”***
2. Click on settings and a window will appear on your screen.
3. Located on the left side of the form is a list of options.
4. Navigate to ***“Git > Credential.”***
5. Click on credential and a window will appear on your screen.
6. Located at the top of the form is a picklist labeled ***“Credential Header.”*** Set this field to ***“Advanced.”***
7. The field ***“Config Type”*** should be set to system.
8. In the ***"URL"*** textbox, paste the HTTP URL of the desired remote repository that you can acquire from the GitLab webpage.
9. In the ***"helper"*** textbox type or select ***“wincred.”***
10. In the username textbox type your personal GitLab username.
Note that this username is the same as your GitLab website username.
11. Click the ***“Add New/Save”*** button.
12. At this point, continue to the Git Instruction document section labeled ***“Cloning a Repository for the First Time Using HTTP.”*** 
13. Complete all the steps described in that section and TortoiseGit will be configured properly.
Note that the first time you clone a repository you will have to provide your password. 
By completing these steps your PC will save your username and password in the ***“Credential Manager.”***
You can see your helper by navigating to ***Control Panel > User Accounts > Credential Manager.***

## Configuring TortoiseGit Username and Email
--------------------------
In order to perform a commit, the TortoiseGit user information must be configured to a specific git login name and email.
1. Right click on any folder on your PC and navigate to ***“TortoiseGit > Settings.”*** 
2. Click on settings and a window will appear on your screen.
3. Located on the left side of the form is a list of options.
4. Navigate to ***“Git”***
5. Click on git and a configuration screen will appear on your screen.
Note that the first section ***“Config Source”*** defaults to ***“Global”***. For this document we left this checked. 
6. In the ***“User Information”*** section fill in the textboxes labeled ***“Name”*** and ***“Email.”***
7. Once you have selected all parameters of interest, hit apply.
This form will permit additional alterations to be made to the user’s profile. For this document we elected to leave all other sections as their default settings.

## Configuring TortoiseGit with Beyond Compare 3

The Beyond Compare download can be found at the following link, http://www.scootersoftware.com/download.php?zz=dl3_en.

Note that the path to the Beyond Compare executable will be needed for the configuration step.
Perform the following steps in order to configure TortoiseGit to use the Beyond Compare difference tool.
1. Right click on any folder on your PC and navigate to ***“TortoiseGit > Settings.”***
2. Click on settings and a window will appear on your screen.
3. Located on the left side of the form is a list of options.
4. Navigate to ***“Diff Viewer.”***
5. Click on diff viewer and a window will appear on your screen.
![guiBeyond](Images/beyondCompare_gitInstruction.PNG)
6. Locate the Diff Viewer TortoiseGitMerge section and switch ***“TortoiseGitMerge”*** to ***“External.”***
7. Locate the textbox directly below the external radio button and type the path to your local Beyond Compare executable.
For example, the path could be, ***“C:\Program Files (x86)\Beyond Compare 3\BCompare.exe."***
8. Once the changes have been made, click apply.

## Cloning a Repository 
--------------------------
### Cloning a Repository for the First Time Using HTTP

Perform the following steps in order to clone a repository for the first time using HTTP.
1. Locate the URL of the repository on the GitLab website. Note that you can find the URL by logging onto the GitLab website and locating the project of interest.
2. Click on the project and GitLab will open the project's main page. Look directly below the project's name and locate a text field labeled SSH. Note that SSH is a header for the URL section.
3. Left click on SSH and select the tab ***HTTP***.
4. Locate the button to the right of the URL labeled ***“Copy to Clipboard.”***
5. Click this button and follow instructions 1, 2, 3 and 5 in the section below labeled ***Recloning a Repository.*** 

Note that after you click ***”Git Clone”*** the new URL will be automatically filled into the URL textbox.


### Cloning a Repository for the First Time Using SSH.

Perform the following steps in order to clone a repository for the first time using SSH
1. Locate the URL of the repository on the GitLab website.
Note that you can find the URL by logging onto the GitLab website and locating the project of interest.
2. Click on the project and GitLab will open the project's main page.
Look directly below the project's name and locate a text field labeled SSH.
Note that SSH is a header for the URL section.
2. Locate the button to the right of the URL labeled ***“Copy to Clipboard.”***
3. Click this button and follow instructions 1, 2, 3 and 5 in the section below labeled **Recloning a Repository.**

Note that after you click ***”Git Clone”*** the new URL will be automatically filled into the URL textbox.

 ![guiClone](Images/TortoiseContextMenuGitClone_gitInstruction.png)  
 
## Recloning a Repository
--------------------------
Perform the following steps in order to reclone a repository.
1. Locate the folder of interest in which you wish to clone the repository.
For example, the folder can be ***"update-synthetic-video."***
2. Right click on the folder and navigate to ***“Git Clone…”***
3. Click on git clone and a clone window will appear on your screen.
4. Locate the textbox labeled ***“URL”*** and click on the picklist located to its right.
Note that this list will display all previously used repositories and it will allow you to select one.
Also note that if you wish to clone from a particular branch; locate the textbox labeled ***”Branch”***. Place a check in the checkbox to its left and type the name of the desired branch in the textbox.
5.  Once you have selected all parameters of interest, hit okay. Git will respond with either success or fail.

Note that depending on your setup, Git may ask you for a password during the cloning process.

![guiCloneBox](Images/GitCloneBox_gitInstruction.png)  

## The file names are decorated with colorful icons to display the checking status of the files.

![gitFilemanger](Images/FileManagerIcons_gitInstruction.png)

## Creating a Branch
--------------------------
**This section and following sections have been tested with the update-synthetic-video project in GitLab with the branch lat-lon-alt-tracker.**
**They describe typical actions that are part of code development using TortoiseGit.**

In order to create a branch, perform the following steps.

1. First locate the branch master folder in which you would like to create a new branch. For example, the project folder can be update-synthetic-video. 
2. Right click the folder and navigate to ***TortoiseGit > Create Branch.***
3. Once you click on ***create branch*** a window will appear. 
![guiBranch](Images/creatingBranch_gitInstruction.PNG) 
4. This window will allow you to name your branch, choose the base of your branch, add your branch onto another branch, add it to a specific tag, or commit. 
5. Finally, it will ask you for a description of your branch. 

Once you finish, hit okay. TortoiseGit will respond with either success or fail.

## Checking Out a Branch
--------------------------
**The following steps describe how to check out a branch or get a list of available branches.**

1. First locate the branch master folder. 
For example, the folder can be ***update-synthetic-video.*** 
2. Right click the folder and navigate to ***TortoiseGit > Switch/Checkout.***
3. Once you select ***switch/checkout*** a window will appear.
![guiCheckOutBranch](Images/checkingOutBranch_gitInstruction.PNG) 
4. Located on this window is a radio button labeled ***"Branch."*** 
5. Once you select this button a picklist will appear with all available branches for the current project. 
    This form will also give you the option to check out a branch. 
6. You can perform this action by selecting the branch of interest and hitting okay.
    Note that TortoiseGit will have options to either force or merge a branch. 
    In our example, we did not select those buttons.
7. Once you finish, hit okay. 
    TortoiseGit will respond with either success or fail.

## Creating Changes to a Pending Commit
--------------------------
**TortoiseGit allows modifying, adding, deleting, or renaming files for a pending commit.**
### Modifying a file
Perform the following steps in order to modify a file.

1. In order to modify a file, open the file in your editor of choice and make the appropriate modification.
2. Perform the steps described in the section ***"Committing Changes to your Local Repository."***

### Adding a File
Perform the following steps in order to add a file.

1. In order to add a file to your local repository, right click on the folder containing the added file. 
For example, the folder can be ***update-synthetic-video.***
2. Navigate to ***TortoiseGit > Add.***
3. Click on add and an add window will appear on your screen.
![guiAdd](Images/addingFile_gitInstruction.PNG) 
4. This form will show all ***"Not Versioned Files"*** and will allow you to choose which files you may add.
5. Select the files of interest.
6. Click okay and the files will be added.

### Deleting a File
Perform the following steps in order to delete a file.

1. To delete a file in your local repository, right click on the file that you wish to delete.
For example, the file can be ***"jerk_test5.txt."***
2. Navigate to ***TortoiseGit > Delete.***
3. Click on delete and a delete window will appear on your screen.
4. This form will display two options, either ***"submit"*** or ***"abort."***
5. Click submit and the file will be deleted.

### Renaming a File
Perform the following steps in order to rename a file.

1. To rename a file in your local repository, right click on the file that you wish to rename.
For example, the file can be ***"jerk_test5.txt."***
2. Navigate to ***TortoiseGit > Rename.***
3. Click on rename and a rename window will appear on your screen.
![guiRename](Images/rename_gitInstruction.PNG) 
4. This form will display the current name of the file and contain a textbox for entering a new name.
5. Once a new name has been entered click okay and the file will be renamed.

## Reverting a Change before a Commit
--------------------------
In order to revert a change on a file, perform the following steps.

1. First locate the folder containing the file. 
2. Right click the folder and navigate to ***TortoiseGit > Revert.***
3. Once you click revert a window will appear. 
![guiRevert](Images/revertAdd_gitInstruction.PNG) 
4. This window will allow you to choose which files you wish to revert to the previous state.
5.  Once you select all the files of interest, hit okay. 
TortoiseGit will respond with either success or fail. 

## Deleting All Untracked Files.
--------------------------
#### Suppose that a folder contains a number of untracked files. In order to clean up the folder and make it match the local repository, perform the following steps.

1. First locate the folder containing the files to be cleaned up or removed. 
2. Right click the folder and navigate to ***TortoiseGit > Clean up.***
3. Once you click clean up a window will appear. 
4. This window will allow you to choose where you want the deleted files to go.
Note that this option will delete all untracked files.  

Once you select all the files of interest, hit okay. 
TortoiseGit will respond with either success or fail.

## Committing Changes to your Local Repository
--------------------------
**You may wish to perform a commit after modifying, adding, deleting, or renaming files.**

Perform the following steps in order to commit changes to your local repository.

1. To commit changes to your local repository you must first right click on the folder containing your changed files. 
For example, the folder can be ***lat-lon-alt-tracker.***
2. Navigate to ***TortoiseGit > Commit lat-lon-alt-tracker.***
![guiCommit](Images/commit_gitInstruction.PNG) 
3. Click on commit and a commit window will appear on your screen.
4. This form will allow you to pick individual files you wish to commit to your local repository.
5. Once you select the files of interest, you must then add a comment to the commit.
6. At the bottom of the form is a picklist that provides options that you can take.

The options include ***commit***, ***commit and push***, or ***recommit.***

Once you finish, hit okay. TortoiseGit will respond with either success or fail.

## Pushing a File
--------------------------
**TortoiseGit supports pushing changes in the local repository to the remote repository.** 

In order to do so, perform the following steps.

1.  First right click on the folder containing your changes.
2. Navigate to ***TortoiseGit > Push.***
3. Click on push and a push window will appear on your screen.
![guiPush](Images/push_gitInstruction.PNG) 
4. This form will show your local repository name, remote repository name, and allow you to modify other attributes of your push.
5. In the destination section make sure remote is filled in with ***"origin."***
6. Note that ***"push all branches"*** is not checked by default.
In the Ref section verify local is filled in with the desired branch.

For example, it can be ***"lat-lon-alt-tracker."***

In the Ref section verify remote is filled in with the desired branch.

For example, it can be ***"lat-lon-alt-tracker."*** 

Select the okay button to submit. If the push was successful TortoiseGit will respond with a ***"success”*** (amount of data transferred) and a time stamp.

## Pull the Remote Repository 
--------------------------
**Suppose a team member makes changes to the remote repository and you wish to update your local repository to include these changes.**

Perform the following steps in order to pull the remote repository.

1. To pull the remote repository to your local repository, right click on the folder that you wish to pull into.
For example, the folder can be ***"update-synthetic-video."***
2. Navigate to ***TortoiseGit > Pull.***
3. Click on pull and a pull window will appear on your screen.
![guiPull](Images/pull_gitInstruction.PNG) 
4. This form will display information about what type of pull you are about to perform. 
5. In this form you can change the location of your pull. By default the system is set to origin.

Below the Arbitrary URL textbox you will find the ***"remote branch"*** field. This field is where you will select what branch you wish to pull. 

For example, the branch can be ***"lat-lon-alt-tracker."***
There are other options you can modify. In our example we chose to leave all the radio buttons unselected except for ***"tags"*** and ***"prune."***

Note that those two radio buttons are selected by default.

Once you finish, hit okay. TortoiseGit will respond with either success or fail.

## Creating a Tag
--------------------------

1. First locate the branch master folder in which you would like to create a new tag. 
For example, the folder can be ***update-synthetic-video.*** 
2. Right click the folder and navigate to ***TortoiseGit > Create Tag.***
3. Once you click on create tag a tag window will appear.
![guiTag](Images/tag_gitInstruction.PNG) 
4. This window will allow you to name your tag, choose the base of your tag, and choose other options.
Note that TortoiseGit's default for base is ***"head"*** and that branch will be automatically filled with your current branch.
5. It will ask you for a comment describing your tag.

Once you finish, hit okay. TortoiseGit will respond with either success or fail.

## Viewing and Checking Out Tags
--------------------------
The following steps describe how to check out or get a list of available tags.

1. First locate the branch master folder. 
For example, the folder can be ***update-synthetic-video.*** 
2. Right click the folder and navigate to ***TortoiseGit > Switch/Checkout.*** 
3. Once you click switch/checkout a window will appear. 
![guiCheckOutTag](Images/checkingOutTags_gitInstruction.PNG)

4. Located on this window is a radio button labeled ***"tags."***
5. Once you select this button a picklist will appear with all available tags for the current project.  
This form will also give you the option to check out a tag. 
6. You can perform this action by selecting the tag of interest and hitting okay.

Note that by default TortoiseGit will have selected the button ***"Create New Branch."***
In our example we unselected this button. 

Once you finish, hit okay. TortoiseGit will respond with either success or fail.


## Reviewing the Log History of a Project 
--------------------------
**Git associates each check-in with a unique hash number.**

1. In order to review the log history of a project, first locate the branch master folder. 
For example, the folder can be ***update-synthetic-video.*** 
2. Right click the folder and navigate to ***TortoiseGit > Show log.***
3. Once you click show log a window will appear.
![guiLog](Images/log_gitInstruction.PNG) 

This window will display the history of the entire local repository. 

Note that you can select individual files and review changes made line by line.

Note that in this window you can also view the ***hash number*** for a specific commit. 

Once you finish, hit okay.

## Placing a Single File on the Ignore List
--------------------------
**TortoiseGit supports creating an ignore list for version control so that a set of files such as object files can be explicitly untracked files.**

1.  First locate the file you wish to place on the ignore list. Right click the folder and navigate to ***TortoiseGit > Add to ignore list.***
2.  Once you click on add to ignore list a window will appear. 
![guiIgnore](Images/ignore_gitInstruction.PNG) 
3. This window will allow you to choose specific options about the file you are planning to ignore or keep as an untracked file. 

Some of these options include ignore item only in this folder, ignore item recursively, and .gitIgnore in repository root.

Once you finish, hit okay. TortoiseGit will respond with either success or fail. 

Note that after you add a file to the ignore list you will see a file appear in your local repository named ***".gitIgnore."***

If you open this file you will see a file or a list of files that are currently being ignored. 

If you wish to revert the ignore action, simply go into .gitIgnore and delete the line containing the name of the file you wish to no longer ignore.


## Adding an SSH Key for a Linux Machine
--------------------------
* On a Linux machine generate an ssh key with the command "***ssh-keygen***"

* Copy the text of the generated key to the console with the command "***cat ~/.ssh/id_rsa.pub***".

* Copy the text of the key to GitLab in the profile -> settings -> SSH keys textbox.

* After successful update of the SSH key on GitLab, you will receive an e-mail from GitLab informing you that the key with its accompanying name has been added to GitLab.

* In order to verify that the key is working properly, log-in to the Linux machine.

* Create a test folder.

* For example, the folder can be ***"sandbox"***.

* Change directory to the test folder.

* On GitLab, navigate to the desired project and copy its URL to the clipboard.

* Issue the command "***git clone URL***" where URL is pasted from the clipboard.

* For example, issue the command "***git clone git@ms-gitlab.ga.com:swprocessing/process.git***".

* Git creates a folder in the current working directory with the appropriate name for the project.

* For example, the previous command creates a subfolder with the name process.

* In that folder is a subfolder with the name ***.git***. This indicates that the folder is the root folder for the project.

## How to Create a New Project using the GitLab Webpage.
--------------------------
* After logging onto your GitLab account locate and click the "***Your Projects***" tab near the top of the page.

* Locate and click a green "***New Project***" button on the top right hand side of the page. This will bring you to the **"create new projects"** page.

* Once there you have the option to either make yourself the owner of the project or to make another member of your team the owner.

* Next, you will have to name your project, leave an optional description, and select a visibility level. Note that a common practice
is to make the visibility level "***Internal***" so that all users can access the project.

* Once you are satisfied with the parameters of your project, click the green "***Create Project***" button on the bottom of the page.

* You are now located inside your project.

* You should see a window with the following information. "The repository for this project is empty
If you already have files you can push them using the command line instructions below.
Otherwise you can start with adding a **README**, a **LICENSE**, or a **.gitignore** to this project."

* Create a **README** for the project.

* Note that after you create a **README** file gitLab will move you into a newly created master branch.

## Using Some Typical Git Commands from the Command Line Assuming a Branch is not Already Made
--------------------------
* In order to make a local repository of a project issue the command "***git clone URL***" where URL is pasted from the clipboard.

* For example, issue the command "***git clone git@ms-gitlab.ga.com:millej/update-synthetic-video.git***."

* In order to create a new branch cd into your newly created project folder and type "***git branch <branchName>***."

* For example, issue the command "***git branch lat-lon-alt-tracker***."

* Create all of the files and subfolders of interest.

* In order to add these files and folders to the local repository, issue the command "***git add .***."

* In order to review the status of the files, issue the command"***git status***."

* Git will indicate new file, modified, deleted, or some other descriptor for each file.

* In order to commit your newly created files to the local repository, issue the command "***git commit –am "comment"***."

* For example, issue the command, "***git commit -am "Kalman Filter and Test Scritps"***."

* To push your commit to the remote repository, issue the command, "***git push origin <branchName>***."

* For example, issue the command, "***git push origin lat-lon-alt-tracker***."

* To remove a file from the local repository issue the command "***git rm <filename>***."

* For example, issue the command "***git rm jerk_test1.csv***."

* In order to make this change to the local repository issue a git commit command.

* Suppose that when reviewing the status of files prior to a commit the user decides to not go forward with the commit.

* For those familiar with TFS, issue the TFS command "***Undo Pending Changes***". With Git, issue the command
"***git reset –hard***."

* After executing this command, using "***git status***" will show that files have the appropriate setting.

* In order to get the history of the current project with the status associated with each revision, issue the command 
"***git log --name-status***."

## Configuring a Linux Account
--------------------------
* In order to generate a tag the Linux account must be configured to a specific git login name and email.

* In order to add a username on Linux issue the following command "***git config --global user.name <userName>***."

* In order to verify that the username is correct, issue the command "***git config --global user.name***." 

* In order to add a user email on Linux issue the following command "***git config --global user.email <userEmail>***." 

* In order to verify that the email is correct, issue the command "***git config --global user.email***."

## Making and Checking Out Tags
--------------------------
* Git uses a tag or label typically for marking a specific point in history.

* A common tag is a revision number.

* A tag is included as part of the log information.

* Git uses lightweight and annotated tags.

* A lightweight tag does not include a comment whereas an annotated tag does.

* In order to create a lightweight tag issue the command "***git tag -a <versionNum>-lw***."

* For example, issue the command "***git tag –a v1.0–lw***."

* In order to create an annotated tag, issue the command "***git tag -a <versionNum> -m “<note about tag>”***."

* For example, issue the command "***git tag -a v1.0 -m "my version 1.0"***."

* In order to place a tag into the remote repository, issue the command "***git push origin <tagName>***."

* For example, issue the command "***git push origin v1.0***."
* In order to place multiple tags into the remote repository, issue the command "***git push origin --tags***."

* In order to list the available tags in the remote repository, issue the command "***git tag***."

## Git log contains a hash associated with each checkin.
--------------------------
In order to checkout a revision, issue the command "***git checkout <hash>***."

* Git responds with "You are in 'detached HEAD' state. You can look around, make experimental changes and commit them, and 
you can discard any commits you make in this state without impacting any branches by performing another checkout."
* In order to return to the head of the branch issue the command  "***git checkout <branchName>***" where branch name is the desired head of the branch.

* In order to switch to a specific tag located on a branch, issue the command "***git checkout -b <branchName> <tagname>***."
 
* For example, issue the command "***git checkout -b lat-lon-alt-tracker v1.0***."

* In order to switch to a specific tag when the branch is already the current context, issue the command "***git checkout <tagName>***."

* For example, issue the command "***git checkout v1.0***."

## Using Some Typical Git Commands from the Command Line Assuming a Branch is Made
--------------------------
* A helpful reference is Reference 1.

* In order to create a local branch cd in to the main folder of the project.

* For example, "***cd process***."

* Issue the command "***git checkout -b <branchName>***" where branch name is the desired name of the branch.

* For example, issue the command "***git checkout -b mytest***."

* In order to add a file fileName.c to the desired branch, create the file at the desired location.

* Issue the command "***git add fileName.c***."

* Issue the command "***git commit -am "add fileName.c"***."

* In order to commit the branch to the repository issue the command "***git push origin <branchName>***" where branch name is the name of the newly created branch.

* For example, issue the command "***git push origin mytest***."

* In order to get the latest version of the project in the remote repository issue the command "***git pull***."

* In order to switch to a specified branch issue the command "***git checkout <branchName>***" where branch name is the desired name of the branch.

* Note that the default branch name is "***master***."

* For example, switch to the branch mytest with the command "git checkout mytest" and switch to the default branch with the command "***git checkout master***."

## GitLab Flow
--------------------------
* A helpful URL that explains GitLab Flow can be found in Reference 2.


**REFERENCES**
--------------------------

Reference 1: github-git-cheat-sheet.pdf

Reference 2: http://docs.gitlab.com/ee/workflow/gitlab_flow.html

Reference 3: https://tortoisegit.org/docs/tortoisegit/tgit-dug.html

