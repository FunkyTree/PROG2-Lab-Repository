PROG2 Lab - Git & GitHub
========================

## Introduction
This lab is designed to help you become familiar with the Git Source Control system and GitHub collaboration tools that you will be using to manage the source code of your projects.

## Objectives
In this excercise you will:
- Setup set up your Git and GitHub environment
- Learn to master the basic Git workflows
- Practice cooperation models involving Git and GitHub

## Requirements

**Hardware:** none

**Software:**
- An up to date web-browser
- Your preferred text editor
- Basic Git installation for your platform (see installation section)
- optional: Git GUI client or IDE with Git support

**Resources:**
- User Account on [ZHAW SoE GitHub Enterprise server][zhaw-gh]

## Expected results
Complete the tasks given below. Look up the required commands in the available documentation (see [References](#References). To complete the assignment you will send a Pull-Request containing all your commits to the initial "blessed" Repository.

<!--
## Grading
- none
--> 

## References
Following some references which my help you to complete the tasks:
- [Git interactive cheetsheet][gitcheet]
- [Git Reference][gitref]
- [Pro Git Book][gitpro]
- [Getting Git right tutorial][gitright]
- [Git-Flow branching model][gitflow]
- [GitHub Help][ghhelp]
- [GitHub Guides][ghguides]
- [Markdown on GitHub][markdown]
- [Add SSH key to GitHub][githubssh]

[gitcheet]: http://ndpsoftware.com/git-cheatsheet.html "Git interactive cheetsheet"
[gitref]:   https://www.atlassian.com/git/tutorials "Git Reference"
[gitpro]:   http://git-scm.com/book/en/v2 "Pro Git Book"
[gitright]: https://www.atlassian.com/git/tutorials "Getting Git right tutorial"
[gitflow]: http://nvie.com/posts/a-successful-git-branching-model/ "Git Flow branching model"
[ghhelp]:   https://help.github.com "GitHub Help"
[ghguides]: https://guides.github.com "GitHub Guides"
[markdown]: https://guides.github.com/features/mastering-markdown/ "Markdown on Github"
[zhaw-gh]:  https://github.engineering.zhaw.ch/ "ZHAW SoE GitHub Enterprise"
[install]:  http://git-scm.com/book/en/v2/Getting-Started-Installing-Git
[githubssh]: https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/
<!--
##Preparation Work before the Lab
- none
-->
## General Notes
### Markdown
All the pages in this tutorial will be written in Markdown. Markdown is a simple and clean markup language, which will be converted to HTML on demand by the supported online systems (CMS, blogs, ...). GitHub has very good support for Markdown, therefore it is very often used in GitHub projects. To get help check the [GitHub Markdown Guide][markdown].

### Git Tips 
#### Use the command line tools
Try to use the Git command line tools in this lab whenever possible. GUI clients use often their own abstractions, which may be different from Git. 
To learn how it works it is best to use the *native* tools. The git command line is very expressive and gives a lot of hints.
If you still need some help check the [interactive cheetsheet][gitcheet], lookup the [Git Reference][gitref] or use the extensive git help pages.

- `git help` lists the basic commands (*porclain*)
- `git help <command>` shows all the details for the specific command 

Sometimes it helps to use a GUI tool to get a better overview. For this you can also use the simple clients comming with git (gitk or git gui).

#### Check your git status often
Before you use modifying Git operations (commit, push, pull, ...) always verify with `git status` that the status of all your files is correct. E.g. before you commit, check that only the required files for this commit are in the *staging area*. This is especially important before you push to a remote repository, because distributed changes are tricky to undo or fix.

#### Stashing
If you started to edit and are not ready to commit, but have to do something unrelated in your repository, use `git stash save` to temporary store the changes. As soon you have finished the urgent task, replay the changes back in the current branch using `git stash pop` (replays latest change). To get a list of all stashes use `git stash list`.

#### Ask for help
If you are stuck and have a problem you can not solve using the documentation, ask your colleques, the lecturer or lab assistant for help.


## Tasks

This lab consists of three parts:

1. [Setting up Git](#part1-settingupgit)
2. [Master the basic Git workflows](#part2-masterthebasicgitworkflows)
3. [Practice Git(Hub) collaboration models](#part3-practicegithubcollaborationmodels)

### Part 1 - Setting up Git
#### Installation
Ensure that the command line version of Git is installed on your computer and that you know how to access it via the command line / terminal interface.

You'll find some basic info for all Systems in the [install instructions][install].

##### Windows

Get the installer from <http://git-scm.com/download/win> and run it using the standard options.

> If you are are using an older version than Windows 10, are an advanced user and want to use the command line often, it may make sense to select option 3 "Run Git and Included Unix tools from the Windows Command Prompt" in the PATH environment dialog. The nice extra is, that you also get a good ssh client which can be used on the Windows command prompt. No need for putty anymore.

##### Linux

In Linux you can use the standard packet manager of your distribution to install Git.

Debian/Ubuntu: 
`$ apt-get install git-core`
Fedora/CentOS/RedHat: 
`$ yum install git-core`

##### OS X

You can use the installer from <http://git-scm.com/download/mac>.

As an alternative you can also install Git using a packet manager for OS X like Homebrew or MacPorts. Because the packages are usually compiled during installation you need to install Xcode beforehand. This is recommended especially, if you already have Xcode installed or you would like to install also other common unix packages. 

Homebrew (<http://brew.sh>): 
`$ brew install git`


MacPorts (<http://www.macports.org/install.php>):
`$ port install git-core`


#### Configuration
##### Basic Git configuration
Before using Git you should configure some basic settings in your user specific (*\-\-global* ) configuration (will be stored in `~/.gitconfig` or in newer git versions optionally in `~/.config/git/config`).

Define identity
```
$ git config --global user.name  "John Doe"
$ git config --global user.email "jdoe@example.com"
```

Enable color support
```
$ git config --global color.ui true
```

Set default editor
```
$ git config --global core.editor vi
```

For Windows this might be a little tricky. The following example is setting Notepad++ as default editor
```
$ git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
```

##### Configure your GitHub account
For this lab we are using the GitHub Enterprise server of ZHAW School of Engineering. It would also work on the public GitHub.

> Please do only create public repositories for this lab. It makes the collaboration workflow much easier, because you do not have to give each user access rights to your repository.

- Login to the [ZHAW SoE GitHub server][zhaw-gh]

- Go to your profile page : "Edit profile"

- Add your Information (at least set the Name)

- Add an Avatar image for your account. A good avatar makes reading the commit history much easier.


If you are using ssh to push your changes to your repositories, you must upload your public ssh key.

- In the Profile page go to the 'SSH keys' menu press 'Add SSH key' and paste your public key into the text field.
- On the client side you have to configure the matching private key for this configuration. How to do this depends on you client. 

Please check the instructions on GitHub about [adding a public SSH key to your account][githubssh]

> This concludes part 1 of the lab. You should now have a working Git installation.



### Part 2 - Master the basic Git workflows

Until now you do not have a git repository to work with on your local computer. There are two options to create Git repositories.

1. initializing an empty repository using `git init` (as shown in the lecture).
2. cloning an existing repository using `git clone` 

In our case we will use option two, to get some prepared content, and because we will use it in part 3 for collaboration.

#### Fork your copy on GitHub
First you __must create your own copy oft this repository__ into your personal GitHub space by **forking** the original copy from the @PROG2 organization.

- Make sure you are on the original repository page in the @PROG2 organization
- In the right upper corner click on 'fork' 
- If you are a member of multiple organizations you will be asked for the 
organization to fork to. Select your own space @<username> (e.g. @jdoe). It is not possible to fork within the same organization.
- As soon the operation finishes, the browser shows your newly copied repository.
- Go to the repository 'Settings' on the right side and ensure, that it is 'public'

Now your personal public project repository is ready. This will be the repository, where you will publish (push) all your changes.

#### Create your local clone

Next you need to create a local clone of YOUR public repository, where you will do all the work.
Check the documentation on how to clone a remote repository to your local computer. GitHub supports multiple protocols (SSH and HTTPS) to connect. You can copy the repository address from the URL field on the right side.

- Check the contents of the repository. Explore also the content of the .git directory. 
- Try to find out, what the meaning of the entries in the (*\-\-local* ) configuration file (.git/config) is.
- What is the active (checked out) branch?

Do not change or edit files yet.


#### Create a feature branch to work on your personal info page

All your edits will be done in a feature branch. To make it unique your should use your login name as the branch name. In this document we will be using 'jdoe' as a placeholder for your branch name.

- Check the documentation to create your feature branch.
- Make sure, that you switch to the new feature branch (e.g. check with `git status` or `git branch`)

#### Create and commit your info page

Next you will create your personal info page in the subdirectory 'participants'.

- Copy the template page 'participants/template.md' to 'participants/jdoe.md'
- Edit the page to set your Name, Shortname and Class.
- Commit your first edit. 
  - Remember to always check the status, before commiting if everyting is correct.
  - use meaningfull commit messages "fixed typo" is NOT a good example.
- Add some intrests/hobbies to the info page.  
- Check the differences between the current and the commited version of the file (git diff)
- Add and commit, if everyting is ok.
- Check the current history of your repository
  - How many commits are already there?
- If you discover, that you made a mistake in the commit message and you would like to update it. This is easy for the last commit, somewhat more difficult for earlier commits and very dangerous as soon you already pushed the repository.
- Try it and change your last commit message
- Show the history again and compare it to the one before
  - What do you discover regarding the last commit id? Is it the same as before? Why?
- Now it is time to push your changes upstream
  - Make sure everything is commited
  - Before pushing, check the status on GitHub. What branches exist?
  - To push your *new branch* to your default remote (upstream = origin) you need to explicitly declare the name of the branch to create  `git push -u origin <jdoe>`. By default only the current branch is pushed. So verify, that you are on the jdoe branch.
  - Check the status on GitHub. Do you see the changes?

#### Create and switch branches

Next we want to add your image to the info page. We will do this in a separate feature branch called 'image'.

- Create a new local feature branch 'image' and switch to it.
- Copy your picture to the `images` directory (name it <username>.jpg) and add it to the repository.
- Add your picture to your info page.
- Commit the changes.

#### Merge Branches

The 'image' feature is done. We need to merge it back to the 'jdoe' branch.

- Switch back to the 'jdoe' branch
- Check that everyting is clean
- Merge the 'image' branch.
  - The merge creates a new commit. The commit message is usually already predefined "Merging..."
  - You can edit and extend this message
- Because the merge is done, we do not need the 'image' branch anymore and you can delete it.

#### Resolve a conflict
The above merge should have worked flawless. To test conflict resolving, we will enforce a conflict.

- Create and switch to a new branch called 'conflict'.
- Change your name in your info file.
- Commit the change on the 'conflict' branch.
- Switch to branch 'jdoe'
- Also change your name in the info page, but to a different value.
- Commit your change on the 'jdoe' branch.
- Merge the 'conflict' branch to the 'jdoe' branch. It should give a conflict.
- Check status and edit the file to resolve the conflict manually.
- Mark the conflict as resolved and try to complete the merge.
- After the merge completed successfull, you can delete the 'conflict' branch.
- Make sure everyting is clean and push the 'jdoe' branch upstream

#### Inspect history

You already used `git log` to show the history. As soon you did branching and merging it is not linear anymore. It is possible to show a very nice commit graph in the console using some options.

Example:
```
$ git log --oneline --graph --decorate –all 
```

or even better
```
$ git log --graph --full-history --all --color \
    --pretty=format:'%x1b[33m%h%x09%C(blue)(%ar)%C(reset)%x09%x1b[32m%d%x1b[0m%x20%s%x20%C(dim white)-%x20%an%C(reset)'
```

This is impossible to type each time. So it makes sense to add it as an alias to the configuration
```
$ git config --global alias.graphlog log --graph --full-history --all --color \  
  --pretty=format:'%x1b[33m%h%x09%C(blue)(%ar)%C(reset)%x09%x1b[32m%d%x1b[0m%x20%s%x20%C(dim white)-%x20%an%C(reset)'
```

Now you can invoke this command using `git graphlog`

> This concludes part 2 of the lab. You should now master the basic Git workflows.


### Part 3 - Practice Git(Hub) collaboration models

In part 3 we will practice a typical GitHub collaboration workflow, which is an  'Integration Manager' workflow, adapted to be used with GitHub.  
The following picture shows the workflow:
![GitHub Workflow](./instructions/images/GitHub-Workflow.png "GitHub Information Manager Workflow")

To do this we will work in groups. If there exists no groups please create groups of about 2-3 people.
Each group member has one of the following two roles:

- **Integration Manager (Maintainer)**
  The first user finishing part 2 will take the role of the Maintainer
- **Developer (Contributor)**
  All other students will have the developer/contributor role.

If your were following the above instructions, all the repositories required do already exist. For each developer the public repository on GitHub and the private on his local computer. Similar for the maintainer, but the role of his public repository will change to the shared (blessed) repository.

In this part you will jointly develop an overview page for your project in a shared branche named after your project. In this lab instructions we will be using 'project-x' as a placeholder. 

__Please substitute 'project-x' with your chosen project name in all steps below.__

#### Setup the Integration Manager workflow

**Maintainer** 

- Make sure your repository is in a consistent state.
- Create a new branch 'project-x' and switch to this branch.
- Copy the template file from 'projects/template.md' to 'projects/project-x.md'
- Update the title, description and add links for backlog and documentation.
- Commit the changes in branch 'project-x'
- Push the commit to the public (now blessed) repository

**Contributors**

- All contributors will have to add the new (blessed) public repository as a remote
- Check the documentation on how to add a new remote (Hint: git remote add ....)
    - use 'integrate' as the remote nickname
    - ask the Maintainer for the URL of the 'blessed' repo.
- As soon the Maintainer pushed the branch to the public repository the Contributors can check out the remote branch 'project-x' to their local machine
    - Hint: `use git checkout -b project-x integrate/project-x`
- Switch to the new branch 'project-x'

#### Create and integrate project file

Next all Project members jointly edit the project overview page.

**Maintainer & Contributor**

- Merge your personal ('jdoe') branch to the 'project-x' branch
- Then add a link to your personal info page into the project page below title members.
  (use relativ links to the jdoe.md page)
- Commit the changes on your local computer
- Push the changes to your public repository 

**Contributors** 

Create a push-request:

- Go to your public GitHub repository
- Select the branch 'project-x'
- Create a Pull-Request from '*contributor*/project-x' to '*maintainer*/project-x' 
- Wait until your request is accepted

**Maintainer**

Receive and accept/integrate all push requests:

- Wait vor Pull-Requests
- Verify the content and result of the Pull-Request
- Accept or Reject the request
- Repeat until all Requests are OK
    - Also try to do a request manually. (See instructions in GitHub, next to the Accept button)

**Contributors**

- periodically pull the updates from the 'integrate' repositoy until the project is complete on all repositories.
- Finally push all updates to your public server

> This concludes part 3 of the lab. You should now a way how to contribute using the GitHub Integration Workflow.

### Closing the Lab


#### If you still have time left. 

- Check out or import the repository in your favorite IDE. And try to do some changes. 
- Add your collected Tips and Tricks or interesting links about Git to the tips.md file and commit to your public repo.

#### Finally, send pull request to main repository

The main repository 'PROG2-lab-IT...' contains a branch (*yourlogin*) for each student.

- All students:  
  To declare that you finished the lab, send a Pull-Request to 'your personal branch' in the main repository you forked in the beginning of the lab.  
  (Pull request from *yourrepo*/master to PROG2-lab-IT.../*yourlogin*)


- Maintainer:  
  In addition send a Pull Request from *yourrepo*/'project-x' to PROG2-Lab-IT.../master
  (It is only used to verify the result and will not be merged)

> **Congratulations! You finished the Lab Git & GitHub**

