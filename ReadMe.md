# Welcome to Tips & Tricks !

Hi! I'm your first Markdown file in **StackEdit**. If you want to learn about StackEdit, you can read me. If you want to play with Markdown, you can edit me. Once you have finished with me, you can create new files by opening the **file explorer** on the left corner of the navigation bar.

# Table of Contents
1. [Script](https://github.com/Raouf25/Tips-Tricks#Script)
2. [Database](https://github.com/Raouf25/Tips-Tricks#Database)
3. [Git](https://github.com/Raouf25/Tips-Tricks#Git)
4. [Fourth Example](#fourth-examplehttpwwwfourthexamplecom)

# Script

### How can I kill whatever process is using port 8080 ?

Open your mac terminal, and copy this command:
```shell 
kill $(lsof -t -i:8080)
```
lsof -t returns the PID of port 8080 and passes that to kill.





# Database

## To connect to Database 
To connect to database from terminal : 

```shell 
$ psql -U postgres -W  -h localhost
Mot de passe pour l'utilisateur postgres :
psql (9.4.15)
Attention : l'encodage console (850) diffère de l'encodage Windows (1252).
            Les caractères 8 bits peuvent ne pas fonctionner correctement.
            Voir la section « Notes aux utilisateurs de Windows » de la page
            référence de psql pour les détails.
Saisissez « help » pour l'aide.

postgres=# \l 

postgres=# \q
```

## But.., how for remote Database ?
How can I connect to remote Database  jdbc:postgresql://dgopaabsupa01.int.xyz.com:5432/supplier_review
	
 ```shell
$ psql -h dgopaabsupa01.int.xyz.com -p 5432 -u supplier_review
 ```

 ## To drop a database 
 
 ```shell
$ dropdb -U supplier_review_db supplier_review_user
Mot de passe :
```

# Dump

## To export data in sql file 
```shell
$ pg_dump supplier_review > /home10/pgmi/postgresql-9.6/dump/supplier_review_PRD_27_06_2019.sql  
```
 
## To import data from sql file
```shell
$ psql -d supplier_review_db  supplier_review_user < dump_dev_20190710.sql
Mot de passe pour l'utilisateur supplier_revie_user :
```

You can see [psql](https://chartio.com/resources/tutorials/how-to-list-databases-and-tables-in-postgresql-using-psql/) for other functions.


# Git
## How Can I ignore file ?
If you want to ignore a file that you've committed in the past, you'll need to delete the file from your repository and then add a .gitignore rule for it.
```shell
 $ echo debug.log >> .gitignore
 $ git rm --cached debug.log
 $ git commit -m "chore(.gitignore): Start ignoring debug.log"
```
 Using the --cached option with git rm means that the file will be deleted from your repository, but will remain in your working directory as an ignored file.
You can omit the --cached option if you want to delete the file from both the repository and your local file system.

see [.gitignore
git add git commit git diff git stash .gitignore ](https://www.atlassian.com/git/tutorials/saving-changes/gitignore)
## How can I delete remote branch 
```shell
$ git push origin --delete feature/updateDAC
```
see [How do I delete a Git branch locally and remotely?](https://stackoverflow.com/a/10999165)


## git tag 
```shell
git tag 0.1.10-RC87 && git push -f origin 0.1.10-RC87 

alias tag='function _tag(){ git tag $1; git push -f origin $1 ; echo "Tag: $1 is created and pushed"; };_tag'
tag 0.1.10-RC87 
```

## git avoid git push --set-upstream
https://pawelgrzybek.com/auto-setup-remote-branch-and-never-again-see-an-error-about-the-missing-upstream/

# Docker 
```shell
 $ docker build -t image_name .  
 ```
-t => image name  
. => current directory

```shell
 $ docker run -p 80:80 image_name  
  ```
-p => port

```shell
 $ docker ps   
   ```
=> show containers list

```shell
 $ docker image ls   
   ```
=> show images list

```shell
 $ docker-compose up
  ```
```shell
 $ docker stop   
   ```
=> stop container

```shell
 $ docker rmi image  
   ```
remove image


# Redis
unboca à lopo => bonne chance  
 redis-cli flushdb

 ======================== GIT ===================
 git push origin --delete feature/kafka-avro-rebasegit commit --amend --no-edit  
git merge develop --allow-unrelated-histories  
git remote -v  
git push --set-upstream origin feature/client


# Maven

```shell
 $ mvn release:perform -Darguments="-Dmaven.javadoc.skip=true"
 ```
 
```shell
 $ mvn install -Dmaven.test.skip=true -Pjpa2ddl
```

# Developing and deploying Spring Boot microservices on Kubernetes
link : https://learnk8s.io/spring-boot-kubernetes-guide

## Create files and folders

The file explorer is accessible using the button in left corner of the navigation bar. You can create a new file by clicking the **New file** button in the file explorer. You can also create folders by clicking the **New folder** button.

## Switch to another file

All your files and folders are presented as a tree in the file explorer. You can switch from one to another by clicking a file in the tree.

## Rename a file

You can rename the current file by clicking the file name in the navigation bar or by clicking the **Rename** button in the file explorer.

## Delete a file

You can delete the current file by clicking the **Remove** button in the file explorer. The file will be moved into the **Trash** folder and automatically deleted after 7 days of inactivity.

## Export a file

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.


# Synchronization

Synchronization is one of the biggest features of StackEdit. It enables you to synchronize any file in your workspace with other files stored in your **Google Drive**, your **Dropbox** and your **GitHub** accounts. This allows you to keep writing on other devices, collaborate with people you share the file with, integrate easily into your workflow... The synchronization mechanism takes place every minute in the background, downloading, merging, and uploading file modifications.

There are two types of synchronization and they can complement each other:

- The workspace synchronization will sync all your files, folders and settings automatically. This will allow you to fetch your workspace on any other device.
	> To start syncing your workspace, just sign in with Google in the menu.

- The file synchronization will keep one file of the workspace synced with one or multiple files in **Google Drive**, **Dropbox** or **GitHub**.
	> Before starting to sync files, you must link an account in the **Synchronize** sub-menu.

## Open a file

You can open a file from **Google Drive**, **Dropbox** or **GitHub** by opening the **Synchronize** sub-menu and clicking **Open from**. Once opened in the workspace, any modification in the file will be automatically synced.

## Save a file

You can save any file of the workspace to **Google Drive**, **Dropbox** or **GitHub** by opening the **Synchronize** sub-menu and clicking **Save on**. Even if a file in the workspace is already synced, you can save it to another location. StackEdit can sync one file with multiple locations and accounts.

## Synchronize a file

Once your file is linked to a synchronized location, StackEdit will periodically synchronize it by downloading/uploading any modification. A merge will be performed if necessary and conflicts will be resolved.

If you just have modified your file and you want to force syncing, click the **Synchronize now** button in the navigation bar.

> **Note:** The **Synchronize now** button is disabled if you have no file to synchronize.

## Manage file synchronization

Since one file can be synced with multiple locations, you can list and manage synchronized locations by clicking **File synchronization** in the **Synchronize** sub-menu. This allows you to list and remove synchronized locations that are linked to your file.


# Publication

Publishing in StackEdit makes it simple for you to publish online your files. Once you're happy with a file, you can publish it to different hosting platforms like **Blogger**, **Dropbox**, **Gist**, **GitHub**, **Google Drive**, **WordPress** and **Zendesk**. With [Handlebars templates](http://handlebarsjs.com/), you have full control over what you export.

> Before starting to publish, you must link an account in the **Publish** sub-menu.

## Publish a File

You can publish your file by opening the **Publish** sub-menu and by clicking **Publish to**. For some locations, you can choose between the following formats:

- Markdown: publish the Markdown text on a website that can interpret it (**GitHub** for instance),
- HTML: publish the file converted to HTML via a Handlebars template (on a blog for example).

## Update a publication

After publishing, StackEdit keeps your file linked to that publication which makes it easy for you to re-publish it. Once you have modified your file and you want to update your publication, click on the **Publish now** button in the navigation bar.

> **Note:** The **Publish now** button is disabled if your file has not been published yet.

## Manage file publication

Since one file can be published to multiple locations, you can list and manage publish locations by clicking **File publication** in the **Publish** sub-menu. This allows you to list and remove publication locations that are linked to your file.


# Markdown extensions

StackEdit extends the standard Markdown syntax by adding extra **Markdown extensions**, providing you with some nice features.

> **ProTip:** You can disable any **Markdown extension** in the **File properties** dialog.


## SmartyPants

SmartyPants converts ASCII punctuation characters into "smart" typographic punctuation HTML entities. For example:

|                |ASCII                          |HTML                         |
|----------------|-------------------------------|-----------------------------|
|Single backticks|`'Isn't this fun?'`            |'Isn't this fun?'            |
|Quotes          |`"Isn't this fun?"`            |"Isn't this fun?"            |
|Dashes          |`-- is en-dash, --- is em-dash`|-- is en-dash, --- is em-dash|


## KaTeX

You can render LaTeX mathematical expressions using [KaTeX](https://khan.github.io/KaTeX/):

The *Gamma function* satisfying $\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$ is via the Euler integral

$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$

> You can find more information about **LaTeX** mathematical expressions [here](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference).


## UML diagrams

You can render UML diagrams using [Mermaid](https://mermaidjs.github.io/). For example, this will produce a sequence diagram:

```mermaid
sequenceDiagram
Alice ->> Bob: Hello Bob, how are you?
Bob-->>John: How about you John?
Bob--x Alice: I am good thanks!
Bob-x John: I am good thanks!
Note right of John: Bob thinks a long<br/>long time, so long<br/>that the text does<br/>not fit on a row.

Bob-->Alice: Checking with John...
Alice->John: Yes... John, how are you?
```

And this will produce a flow chart:

```mermaid
graph LR[enter link description here](https://github.com/Raouf25/Tips-Tricks/new/master?readme=1)
A[Square Rect] -- Link text --> B((Circle))
A --> C(Round Rect)
B --> D{Rhombus}
C --> D
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM3NDI0OTE2OSwtMjEwNDE1NDk1NSw3Nz
EwNjE4ODUsMTQ2NzgwMDUzMCwxMjEyNzA2NzM2LC03NTUwNzI0
NDcsMjExMzg0MzU3NF19
-->
