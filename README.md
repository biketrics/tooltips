# tooltips
A repository whose README.md contains concise command/tool notes that biketrics developers use frequently.

---
## Table of Contents
  - [SSH](#ssh)
    - [SSHing Using Password Authentication:](#ssh-ing-using-password-authentication)
  - [Git](#git)
    - [Generate an SSH key pair:](#generate-an-ssh-key-pair)
    - [Add your SSH key to GitHub:](#add-your-ssh-key-to-github)
    - [Cloning a repo using SSH:](#cloning-a-repo-using-ssh)

---
## SSH
### SSH-ing Using Password Authentication:
```
ssh <username>@<ip/hostname>
```
If you are prompted with something along the lines of the following, simply type `yes`. 
```
The authenticity of host '192.168.1.27 (192.168.1.27)' can't be established.
ED25519 key fingerprint is SHA256:XXXX.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

You will be prompted to type in the password for the user. Type in the password and press ENTER (the characters typed will not appear in the terminal).

__Example:__
```
example@machine >> ssh biketrics@192.168.1.27
biketrics@192.168.1.27's password:
```

---
## Git
### Generate an SSH key pair:
```
ssh-keygen -t rsa -C "<email>"
```

When prompted to specify a location, if you do not have a particular location in mind, press ENTER to place the key in the deafult location (most likely ~/.ssh).

When prompted for a passphrase, choose wisely, as you will need this passphrase to be able to view/access the private key. Or if you do not wish to passphrase protect the key, simply press ENTER.
__Example:__
```
example@machine >> ssh-keygen -t rsa -C "example@sample.com"

Generating public/private rsa key pair.
Enter file in which to save the key (/home/example/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/example/.ssh/id_rsa
Your public key has been saved in /home/example/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:O6TcyEl8VSW1fBGP1rE2fg9sjY/jR9QRVO6YtTdUYys sample@example.com
The key's randomart image is:
+---[RSA 3072]----+
|            oo+O*|
|           . o.*O|
|          .  E=*O|
|     .   .   o=O=|
|      o S     B==|
|     + B .   . +*|
|      * +     o.o|
|         .   . ..|
|              .. |
+----[SHA256]-----+
```

### Add your SSH key to GitHub:
1. Press your profile icon at the top right, then click "Settings"
2. Select "SSH and GPG keys" (likely on the left side of the page).
3. Click the "New SSH key" button.
4. In the "Title" textbox provide a name (something like your name/username and something that identifies the machine the key belongs to).
5. On the command line, navigate to the directory your keys are stored in (e.g. `cd ~/.ssh`).
6. Run `cat <filename>.pub` (e.g. `cat id_rsa.pub`) to print out the contents of your public key.

⚠️ __DANGER:__ Make sure the file you `cat` ends in .pub, otherise you could risk exposing your private key!

7. Copy the output of the `cat` command (from the "ssh-rsa ..." to the end of the email), and paste it into the key textbox on the GitHub web page from step 4.
8. Click the "Add SSH key" button.

### Cloning a repo using SSH:
__NOTE:__ You must have completed [Generate an SSH key pair](generate-an-ssh-key-pair) and [Add your SSH key to GitHub](add-your-ssh-key-to-github) before you will be able to successfully clone a repo using SSH.
```
git clone ssh://git@github.com/<user>/<repository name>.git
```
__Example:__
```
git clone ssh://git@github.com/biketrics/tooltips.git
```
