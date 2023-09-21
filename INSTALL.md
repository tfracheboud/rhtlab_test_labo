# First installation

This is a quick summary of the "one true way" of setting up a Jupyter Notebook locally on your Windows machine with python installed. 
We will just be going over the key steps and commands run.

The following installation guide will use Mambaforge (a tiny version of Anaconda distribution). If you do not like Anaconda or Mambaforge for some reason, they you can install python 3 and use `pip` to install the required libraries manually (this is not recommended, unless you really know what you are doing). We recommend using Python 3.7 and [newer version](https://endoflife.date/python). More resources about `pip` are given on this [tutorial](https://learnpython.com/blog/python-requirements-file/).

But please follow this tutorial depending on your machine's operating system. This can be intimidating compared to a simple setup like MATLAB, but welcome to the real world, where you have to tinker and learn to use a computer yourself.

> [!IMPORTANT]
> If you are running on Linux or macOS, you can directly go to [the Mambaforge install setup section](#install-an-isolated-python-environment-with-setup-mambash-recommended-for-beginners).

## Windows users prerequisites

This section is only useful if you're using a Windows 10 or 11 configuration (unfortunately, many engineers and teachers still think Windows is a useful operating system).

If, like us, you have the misfortune to use Windows and nothing is already installed on your machine, please follow this tutorial from here.

## Installation requirements on Windows 10 and 11

If you already master WSL (Windows Subsystem Linux) and got a clean install without an existing environment, go directly to [the Mambaforge install setup section](#install-an-isolated-python-environment-with-setup-mambash-recommended-for-beginners).

### Run a terminal and install WSL for Windows 10 or 11

Follow the steps below to install WSL correctly:

- Go to the Windows Store and install the [Windows Terminal](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=fr-ch&gl=ch&rtc=1), you need to have a [Microsoft account](https://support.microsoft.com/en-us/account-billing/how-to-create-a-new-microsoft-account-a84675c3-3e9e-17cf-2911-3d56b15c0aaf). You can also install it without using a microsoft account. Terminal is **already pre-installed on Windows 11**!
- Open PowerShell (go to Windows Menu/<kbd>WIN</kbd>+<kbd>S</kbd> and type "PowerShell") in **administrator mode** by right-clicking and selecting "Run as administrator".
- Enter the `wsl --install` command.
- After everything has been installed, restart your computer.
- This part is an idle point, it takes some time to initialize...
- Ubuntu will ask for a username (small letters) and password.
- You can now close the Ubuntu terminal, go back to Windows Terminal, and open a new tab for Ubuntu if you wish:
  - Tip: you can go to the terminal's settings and set Ubuntu as your default shell (Settings -> default profile).

> [!NOTE]
> If you get into trouble after those few steps you can go directly to this [section](#troubleshooting-with-wsl-only-if-you-encounter-difficulties----if-not-go-to-the-next-section) or call for assistance to solve it for you :innocent:.

Finally, it is important to update your Linux distribution, from a WSL terminal session as follows:

```bash
sudo apt-get update
```

Also, we need to make sure the `wget` command is already available by running this command in the next step:

```bash
sudo apt-get install wget ca-certificates
```

## Install an isolated Python environment with `setup-mamba.sh` (recommended for beginners)

We are going to run the following script from the terminal `setup-mamba.sh`. Don't worry, we will guide you through the all process.

Go to your download folder by typing the following command in your terminal:

```bash
cd downloads
wget https://github.com/fastai/fastsetup/blob/master/setup-conda.sh
```

Then, you can type the following command into the terminal:

```bash
chmod u+x setup-conda.sh
```

In a nutshell, those commands help to change the permissions to add executable permission to the current user (yourself). Then type:

```bash
 ./setup-conda.sh
```

The installation is starting...

- Restart terminal for Ubuntu.
- You should see `(base)` at the beginning of prompt.

> [!NOTE]
> Everytime you open a new Ubuntu terminal, you should see `(base)` environment. That means your configuration setup works well for this course and labs.

At this point, we have to check if your configuration works fine:

- Run `which python`, you should see that the python you are running is in the mambaforge directory: `home/<username>/mambaforge/bin/python` on Linux/WSL and `/Users/<username>/mambaforge/bin/python`.
- This means everything was just setup correctly.

## Install important basic packages

For both mamba and conda, the base environment is meant to hold their dependencies. It is strongly discouraged to install anything else in the base envionment. Doing so may break mamba and conda installation (meaning `pip` kind of install).

Note that if you replace `conda` with `mamba` the install process will be much faster and more reliable.

Install the different important libraries and packages:

```bash
mamba install ipython jupyterlab ipywidgets
```

- Accept all with `Y`

Then you can update Mambaforge to be sure to run the last version:

```bash
mamba update mamba
```

You're almost there! You just need to register the `(base)` environment to Jupyter. The notebooks in this project will default to the environment named python3, so it's best to register this environment using the name python3 (if you prefer to use another name, you will have to select it in the **Kernel > Change kernel...** menu in Jupyter every time you open a notebook):

```bash
python3 -m ipykernel install --user --name=python3
```

Check your configuration with the following steps:

- Run: `jupyter lab --no-browser`.
- You should see a link to JupyterLab in the terminal at this point.
- Either <kbd>Ctrl</kbd>+<kbd>click</kbd> on the link or copy it and paste it in your web browser.

> [!NOTE]
> The `--no-browser` flag prevents jupyter from trying to open a browser for you. It won't be able to do this, as it's running in Linux, but the browser or the JupyterLab Desktop IDE you'll be using is in Windows. You can also run `alias jlnb="jupyter lab --no-browser", then`jlnb`. The advantage of this method will be the`jlnb` command if you have to restart the server for any reason.

If you have done everything correctly, you should now be running a Jupyter Lab instance in an isolated Python environment.

## Git setup

Before going to anything else in this tutorial, you should make sure git is installed correctly on your computer by following [this quick tutorial](https://linuxhint.com/add-git-bash-windows-terminal/).

### Setting your Git username for every repository on your computer (maybe this step isn't necessary)

Open the terminal and type the following command and the correct name and email:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.name@example.ch"
```

Confirm that you have set the Git username correctly:

```bash
$ git config --global user.name
> Your Name
$ git config --global user.email
> your.name@example.ch
```

### With SSH (strongly recommended for security purposes)

An SSH key is a credential for accessing the SSH (secure shell) network protocol. This secure, authenticated and encrypted network protocol is used for remote communication between machines on an open, unsecured network. SSH is used for remote file transfer, network management and remote access to the operating system. The acronym SSH is also used to describe a set of tools used to interact with the SSH protocol.

If you have an existing SSH key, you can use the key to authenticate Git operations over SSH.

Before you generate a new SSH key, you should check your local machine for existing keys by typping the following command:

```bash
ls -al ~/.ssh
```

This is going to list the files in your .ssh directory, if they exist. If not the command sends back an error like ~/.ssh that means does not exist.

If you get some keys as follows:

```bash
id_rsa.pub
id_ecdsa.pub
id_ed25519.pub
```

You can generate a new SSH key on your local machine. After you generate the key, you can add the public key to your account on GitHub.com to enable authentication for Git operations over SSH. Please go through the following steps:

Copy-paste the text below, substituting in your GitHub email address:

```bash
ssh-keygen -t ed25519 -C "your_email@example.ch"
```

This will prompt the following message in the terminal:

```bash
> Generating public/private ed25519 key pair
```

When you're prompted to "Enter a file in which to save the key", you can press Enter to accept the default file location. Please note that if you created SSH keys previously, `ssh-keygen` may ask you to rewrite another key, in which case we recommend creating a custom-named SSH key. To do so, type the default file location and replace `id_ssh_keyname` with your custom key name.

```bash
> Enter a file in which to save the key (/home/username/.ssh/id_ed25519):[Press enter]
```

At the prompt, type a secure passphrase if you need one (not necessary).

```bash
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

We have now to add the SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys (as mentioned above) and generated a new SSH key.

Start the ssh-agent in the background.

```bash
eval "$(ssh-agent -s)"
```

The following text appears in your terminal:

```bash
> Agent pid 59566
```

Add your SSH private key to the ssh-agent. If you created your key with a different name, or if you are adding an existing key that has a different name, replace `id_ed25519` in the command with the name of your private key file.

```bash
ssh-add ~/.ssh/id_ed25519
```

Copy the SSH public key to your clipboard (copy the contents of the id_ed25519.pub file). It will display in the terminal to your clipboard by typing the content displayed in the terminal

```bash
cat ~/.ssh/id_ed25519.pub
```

If your **SSH public key** file has a different name than the example code, modify the filename to match your current setup. When copying your key, don't add any newlines or whitespace. **Do not copy-paste the private key, it is really important to understand that**!

> [!NOTE]
> Alternatively, you can locate the hidden .ssh folder (`\\wsl.localhost\Ubuntu\home\username\.ssh`), open the file in your favorite text editor, and copy it to your clipboard.

Going back to your GitHub account, in the upper-right corner of any page, click your profile photo, then click *Settings*.

![Select settings to get access SSH parameters](https://docs.github.com/assets/cb-65929/mw-1440/images/help/settings/userbar-account-settings.webp)

1. In the "Access" section of the sidebar, click **SSH and GPG keys**.
2. Click New SSH key or Add SSH key.
3. In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal laptop, you might call this key "Personal laptop".
4. Select the type of key, either authentication or signing. If you just want to access repositories, then all you need is an authentication key.
5. In the "Key" field, paste your public key.
6. Click **Add SSH key**.
7. If prompted, confirm access to your account on GitHub.

> [!NOTE]
> If you receive an error that `~/.ssh` doesn't exist, you do not have an existing SSH key pair in the default location. You can create a new SSH key pair in the next step. If you have several SSH keys already, that means you aren't a complete beginner, so you can directly follow [this tutorial](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

Next, clone this project by typing the following commands, **you have to get the correct address** of the repository by clicking on "<kbd><></kbd> <kbd>Clone</kbd>" then copy the SSH URL:

```bash
mkdir git
cd git
git clone git@github.com:heig-vd-iese/rhtlab2023-NAME-TEAM.git
```

Type "yes" when prompted.

You can install packages with mamba from an `.yml` file directly in the base environment by running the following command in your terminal:

<!-- This content will not appear in the rendered Markdown -->
<!--
```bash
cd rhtlab
mamba env update -n base --file environment.yml
``` -->

<!-- ```bash
cd rhtlab
mamba env create -f environment.yml
``` -->

<!-- This will install the packages listed in the `environment.yml` file into the `(base)` environment. -->

This will create a new environment with the packages listed in the `environment.yml` file into the `(rhtlab)` environment.

You're finally done with the most important setup.

<!-- Now we are going to install a nice IDE (Integrated development environment). -->

<!-- > **Note**: we can also change the last command to `mamba install --file requirements.txt`, if you prefer to use the `requirement.txt` file. -->

More information about how SSH keys work in general:

- [What is a Git SSH Key?](https://www.atlassian.com/git/tutorials/git-ssh)
- [Checking for existing SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)
- [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
- [Generating a new SSH key for a hardware security key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux#generating-a-new-ssh-key-for-a-hardware-security-key)
- [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
- [Multiple SSH Keys settings for different github account](https://gist.github.com/jexchan/2351996)
- [Working with SSH key passphrases](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases)
- [About commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification)
- [Do I need authentication as well as signing keys on GitHub?](https://stackoverflow.com/questions/73673920/do-i-need-authentication-as-well-as-signing-keys-on-github)

### Commiting your work with Git

Coming soon...

To add all the changes you've made:

```bash
git add .
```

To commit them:

```bash
git commit -m "MY MESSAGE HERE"
```

> [!NOTE] 
> `-m` is the message flag here. The message is really important in order for tracking your work via git.

You can also put those steps together like this:

```bash
git commit -a -m "MY MESSAGE HERE"
```

To push your committed changes from your local repository to your remote repository:

```bash
git push origin master
```

It is possible to get some type in your username/password for github. Unless you have configured [SSH keys correctly](#section-ssh-key)..

More information about these steps:

- [How to commit and push?](https://stackoverflow.com/questions/19576116/how-to-add-multiple-files-to-git-at-the-same-time)

## Troubleshooting in the setup guide (only if you encounter difficulties)

This section is designed to help you solve problems before you contact the helpdesk directly. Try following one of these steps, depending on which part of the guide you're having trouble with.

### Troubleshooting with WSL

There is no need to enable 'Windows Subsystem for Linux' in the `Turn Windows features on or off` settings unless you get in trouble with your installation setup. In such case, it is recommended to follow this [tutorial](https://learn.microsoft.com/en-us/windows/wsl/troubleshooting) or get back to assistance.

- [Enable WSL correctly for Windows 10](https://code.visualstudio.com/docs/remote/wsl-tutorial#_enable-wsl)

## Troublehsooting with Mambaforge (only if you encounter difficulties)

- `rm -rf mambaforge`
- Remove conda initializing commands from `\\wsl.localhost\Ubuntu\home\<username>`: `.bashrc` file (with a text editor). Delete everything at the end of the script between these commands:

```bash
# >>> conda initialize >>>
__conda_setup=
...
# <<< conda initialize <<<
```

## Troubleshooting with GitHub (only if you encounter difficulties)

We regularly update the notebooks to fix issues and add support for new librarires. So make sure you update this project regularly.

For this, open a terminal, and run the following:

```bash
cd $HOME # or whatever development directory you chose earlier
cd rhtlab2023-NAME-TEAM # go to this project's directory
git pull
```

If you get an error, it's probably because you modified a notebook. In this case, before running `git pull` you will first need to commit your changes. I recommend doing this in your own branch, or else you may get conflicts:

```bash
git checkout -b my_branch # you can use another branch name if you want
git add -u
git commit -m "Describe your changes here"
git checkout main
git pull
```

Next, let's update the libraries. First, let's update `mamba` itself:

```bash
mamba update -c defaults -n base mamba
mamba activate base
jupyter lab --no-browser
```

## Further references for the setup (not necessary to follow)

> [!NOTE]
> Notice that it is however using `conda install`, which we will replace with `mamba install`.

1. [Jeremy Howard's Live Coding Sessions](https://forums.fast.ai/t/official-course-walk-thrus/96617)
2. [Mambaforge setup page](https://github.com/conda-forge/miniforge#mambaforge)
3. [Fastsetup script](https://raw.githubusercontent.com/fastai/fastsetup/master/setup-conda.sh)
4. [Beginner's guide to Mambaforge installation](https://qbiwan.github.io/fastpages/mamba-installation)
5. [Another blog post that goes into the details about the global process](https://carvermichael.github.io/2022/11/28/fast.ai-live-coding-session-1-summary.html)
6. [Introducing the new JupyterLab Desktop!](https://medium.com/jupyter-blog/introducing-the-new-jupyterlab-desktop-bca1982bdb23)
7. [The python Requirements File and How to Create it](https://learnpython.com/blog/python-requirements-file/)
8. [What is a Git SSH Key?](https://www.atlassian.com/git/tutorials/git-ssh)
9. [Connect to an existing JupyterLab Server](https://github.com/jupyterlab/jupyterlab-desktop/blob/master/user-guide.md#connecting-to-an-existing-jupyterlab-server) (with the link you just copied from your terminal session)
10. [Windows Subsystem for Linux Documentation](https://learn.microsoft.com/en-us/windows/wsl/)
11. [Conda Install Requirements](https://linuxhint.com/conda-install-requirements-txt/)
12. [Beginner's Guide to Mambaforge Installation](https://qbiwan.github.io/fastpages/mamba-installation)
13. [How to get access to your Linux (WSL) Files in Windows 10 or 11](https://www.howtogeek.com/426749/how-to-access-your-linux-wsl-files-in-windows-10/)
