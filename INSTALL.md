# First installation

This is a quick summary of the "one true way" of setting up a Jupyter Notebook locally on your Windows machine with python installed.
We will just be going over the key steps and commands run.

The following installation guide will use Mambaforge (a tiny version of Anaconda distribution). If you do not like Anaconda or Mambaforge for some reason, they you can install python 3 and use `pip` to install the required libraries manually (this is not recommended, unless you really know what you are doing). We recommend using Python 3.7 and [newer version](https://endoflife.date/python). More resources about `pip` are given on this [tutorial](https://learnpython.com/blog/python-requirements-file/).

But please follow this tutorial depending on your machine's operating system. This can be intimidating compared to a simple setup like MATLAB, but welcome to the real world, where you have to tinker and learn to use a computer yourself.

> [!IMPORTANT]
> If you are running on Linux or macOS, you can directly go to ["Installing the Mambaforge distribution from scratch"](#installing-python-with-mambaforge-from-scratch).

---

<details>

<summary>If you are a Windows user, expand the following section</summary>

## Windows users prerequisites

This section is only useful if you're using a Windows 10 or 11 configuration (unfortunately, many engineers and teachers still think Windows is a useful operating system).

If, like us, you have the misfortune to use Windows and nothing is already installed on your machine, please follow this tutorial from here.

If you already master WSL (Windows Subsystem Linux) and got a clean install without an existing environment, go directly to [the Mambaforge install setup section](#installing-python-with-mambaforge-from-scratch).

### Run a terminal and install WSL for Windows 10 or 11

Follow the steps below to install WSL correctly:

- Go to the Windows Store and install the [Windows Terminal](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=fr-ch&gl=ch&rtc=1), you need to have a [Microsoft account](https://support.microsoft.com/en-us/account-billing/how-to-create-a-new-microsoft-account-a84675c3-3e9e-17cf-2911-3d56b15c0aaf). You can also install it without using a microsoft account. Terminal is **already pre-installed on Windows 11**!
- Run the Windows Terminal as *administrator* and make sure you are using PowerShell
- Install WSL from the terminal: `wsl --install`.
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

### Best practice with the new Windows Terminal and Ubuntu

To get the right terminal, every time you start the Windows Terminal, just go to the <kbd>+</kbd> terminal icon (at the right top corner), then in *Settings*, in the *Startup* section, make sure *Ubuntu* with the little Penguin icon is selected.

Restart your terminal, and you've got the right terminal with the right location on WSL. To check that you're located correctly, type the following:

```bash
pwd
```

you will get the following with your defined `<username>`:

```bash
> /home/<username>
```

</details>

---

## Installing Python with Mambaforge from scratch

We now need to make sure that there is nothing in your operating system that could interfere with the configuration we are going to install. In your terminal (WSL, macOS or Linux), please type the following:

```bash
python
```

If you've got nothing, that's good news as we will start from the beginning. If you have something, we will remove it and start a new setup.

```bash
which python 
```

Go to the [Mambaforge distribution](https://github.com/conda-forge/miniforge#mambaforge) page and find the Linux distribution that corresponds to the type of CPU (architecture) you are using, and right-click and copy the link under this [table](https://github.com/conda-forge/miniforge#miniforge3).

> [!IMPORTANT] 
> Do not select an installer under *Miniforge-pypy3* but *Miniforge3*.

On most Windows laptop and computer, the architecture is likely to be AMD64, but you can make sure by going on your *Settings* (the operating system one), click on *System*, click on the *About tab*, under *Device specifications*, the *System type* indicates which CPU you have.

> [!NOTE]
> If you are on a macOS, you should do the same procedure but for [Mac computers](https://support.apple.com/en-us/HT211814).
> When using WSL, you are on Linux, so you do not have to install Mamba on Windows.

Make sure you are in the right `home` directory by typing the following command:

```bash
pwd
```

It has to generate `/home/<username>`.

Create a `downloads` folder with:

```bash
mkdir downloads
```

Use `wget` to download the mambaforge distribution, using the link you copied earlier (pay attention: the example is with the link for an amd64 architecture):

```bash
wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
```

Now we need to run the `.sh` script by running:

```bash
bash Miniforge3-Linux-x86_64.sh
```

Agree to the terms. Press `Enter` whenever the terminal asks you to do it. Do not type anything other than "yes" when prompted. Also you will have to accept the home directory as the default location.

The last prompt will ask: "Do you wish the installer to initialize `{INSTALLER_NAME}` by running conda init?", type `yes`.

The installation is starting...

- Restart terminal for Ubuntu.
- You should see `(base)` at the beginning of prompt.

> [!NOTE]
> Everytime you open a new Ubuntu terminal, you should see `(base)` environment. That means your configuration setup works well for this course and labs.

At this point, we have to check if your configuration works fine:

- Run `which python`, you should see that the python you are running is in the mambaforge directory: `home/<username>/mambaforge/bin/python` on Linux/WSL and `/Users/<username>/mambaforge/bin/python`.
- This means everything was just setup correctly.

If you encounter any difficulties during your installation, you can follow the [Troubleshooting section](#troubleshooting-in-the-setup-guide) or start from scratch with this [beginner's guide](https://qbiwan.github.io/fastpages/mamba-installation).

---

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

---

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
> Enter a file in which to save the key (/home/username/.ssh/id_ed25519): [Press enter]
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

1. In the "Access" section of the sidebar, click **SSH and GPG keys**.
2. Click New SSH key or Add SSH key.
3. In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal laptop, you might call this key "Personal laptop".
4. Select the type of key, either authentication or signing. If you just want to access repositories, then all you need is an authentication key.
5. In the "Key" field, paste your public key.
6. Click **Add SSH key**.
7. If prompted, confirm access to your account on GitHub.

> [!NOTE]
> If you receive an error that `~/.ssh` doesn't exist, you do not have an existing SSH key pair in the default location. You can create a new SSH key pair in the next step. If you have several SSH keys already, that means you aren't a complete beginner, so you can directly follow [this tutorial](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

You can now clone the working repo by running into the terminal:

```bash
mkdir git
cd git
git clone git@github.com:heig-vd-iese/rht.git
```

Type "yes" when prompted.

You can install packages with mamba from an `.yml` file directly in the base environment by running the following command in your terminal:

<!-- This content will not appear in the rendered Markdown -->

```bash
cd rht
mamba env update -n base --file environment.yml
```

<!-- ```bash
cd rht
mamba env create -f environment.yml
``` -->

This will install the packages listed in the `environment.yml` file into the `(base)` environment.

<!-- This will create a new environment with the packages listed in the `environment.yml` file into the `(rhtlab)` environment. -->

You're finally done with the most important setup. Now we are going to configure Git correctly in order to keep versioning and history of your projects with GitHub.

### Commiting your work with Git

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

> [!IMPORTANT]
> You are done with the setup.
> If you did not get any trouble, you can continue with the tutorials for this course [github.com's notebook viewer](./index.ipynb).

If you get many problems with your git branch or repo, please get in touch with [Luca](mailto:luca.tomasini@heig-vd) or [Antoine](mailto:antoine.giraldi@heig-vd.ch).

---

## Troubleshooting in the setup guide

This section is designed to help you solve problems before contacting support directly. Try one of the following steps, depending on which part of the guide is giving you trouble.

---

<details>

<summary>Installation automation (to optimize later on)</summary>

### Install an isolated Python environment with `setup-conda.sh` (not necessary to follow)

We are going to run the following script from the terminal `setup-conda.sh`. Don't worry, we will guide you through the all process.

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

</details>

---

<details>

<summary>Only if you encounter difficulties with WSL</summary>

### Troubleshooting with WSL

There is no need to enable 'Windows Subsystem for Linux' in the `Turn Windows features on or off` settings unless you get in trouble with your installation setup. In such case, it is recommended to follow this [tutorial](https://learn.microsoft.com/en-us/windows/wsl/troubleshooting) or get back to assistance.

- [Enable WSL correctly for Windows 10](https://code.visualstudio.com/docs/remote/wsl-tutorial#_enable-wsl)

</details>

<details>

<summary>Only if you encounter difficulties with Mambaforge</summary>

### Troublehsooting with Mambaforge

- `rm -rf mambaforge`
- Remove conda initializing commands from `\\wsl.localhost\Ubuntu\home\<username>`: `.bashrc` file (with a text editor). Delete everything at the end of the script between these commands:

```bash
# >>> conda initialize >>>
__conda_setup=
...
# <<< conda initialize <<<
```

---

> [!NOTE]
> Uncollapse these section depending where you need more help to solve troubleshootings.

</details>

<details>

<summary>Only if you encounter difficulties with GitHub</summary>

### Troubleshooting with GitHub

We regularly update the notebooks to fix issues and add support for new librarires. So make sure you update this project regularly.

For this, open a terminal, and run the following:

```bash
cd $HOME # or whatever development directory you chose earlier
cd rht # go to this project's directory
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

</details>

---

## Further references for the setup (not necessary to follow)

<details>

<summary>References (not necessary to follow – backup)</summary>

> [!NOTE]
> Notice that it is however using `conda install`, which we will replace with `mamba install`.

### For the complete setup from scratch

> [!WARNING]
> More information about it can be found [here](https://github.com/conda-forge/miniforge/pull/277) and [here](https://github.com/conda-forge/miniforge/releases/tag/23.3.1-0).
> *Mambaforge (Discouraged as of September 2023)*, that means "the packages and configuration of Mambaforge and Miniforge3 are now identical. The only difference between the two is the name of the installer and, subsequently, the default installation directory."

1. [Beginner's Guide to Mambaforge Installation](https://qbiwan.github.io/fastpages/mamba-installation)
2. [Mambaforge setup page](https://github.com/conda-forge/miniforge#mambaforge)
3. [Fastsetup script](https://raw.githubusercontent.com/fastai/fastsetup/master/setup-conda.sh)
4. [Jeremy Howard's Live Coding Sessions](https://forums.fast.ai/t/official-course-walk-thrus/96617)
5. [Mamba Installation](https://mamba.readthedocs.io/en/latest/mamba-installation.html)
6. [Mamba Installation with Docker](https://hub.docker.com/r/condaforge/mambaforge)
7. [Miniforge3 23.3.1-0](https://github.com/conda-forge/miniforge/releases/tag/23.3.1-0)

### For VS Code and WSL details

1. [Windows Subsystem for Linux Documentation](https://learn.microsoft.com/en-us/windows/wsl/)
2. [Open a WSL project in Visual Studio Code](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode#open-a-wsl-project-in-visual-studio-code)
3. [Open a remote folder or workspace](https://code.visualstudio.com/docs/remote/wsl#_open-a-remote-folder-or-workspace)
4. [Install Ubuntu on WSL2 and get started with graphical applications](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-11-with-gui-support#1-overview)
5. [Install Ubuntu on WSL2 on Windows 10](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-10#1-overview)
6. [How to get access to your Linux (WSL) Files in Windows 10 or 11](https://www.howtogeek.com/426749/how-to-access-your-linux-wsl-files-in-windows-10/)
7. [What're the differences between these 2 ways of launching WSL?](https://superuser.com/questions/1765100/whatre-the-differences-between-these-2-ways-of-of-launching-wsl)
8. [Get started with Docker remote containers on WSL 2](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-containers)
9. [Advanced: Opening a WSL 2 folder in a container](https://code.visualstudio.com/docs/remote/wsl#_advanced-opening-a-wsl-2-folder-in-a-container)
10. [Get started tutorial for Python in VS Code](https://code.visualstudio.com/docs/python/python-tutorial#_configure-and-run-the-debugger)
11. [Add User to WSL Linux Distro in Windows 10](https://winaero.com/add-user-wsl-linux-distro-windows-10/)
12. [Switch user in WSL Linux Distro in Windows 10](https://winaero.com/switch-user-wsl-linux-distro-windows-10/)

### For Git and SSH

1. [Quickstart with GitHub](https://docs.github.com/en/get-started/quickstart/set-up-git)
2. [What is a Git SSH Key?](https://www.atlassian.com/git/tutorials/git-ssh)
3. [Checking for existing SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)
4. [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
5. [Generating a new SSH key for a hardware security key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux#generating-a-new-ssh-key-for-a-hardware-security-key)
6. [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
7. [Multiple SSH Keys settings for different github account](https://gist.github.com/jexchan/2351996)
8. [Working with SSH key passphrases](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases)
9. [About commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification)
10. [Do I need authentication as well as signing keys on GitHub?](https://stackoverflow.com/questions/73673920/do-i-need-authentication-as-well-as-signing-keys-on-github)

### JupyterLab Desktop and Python environment

1. [Connect to an existing JupyterLab server](https://github.com/jupyterlab/jupyterlab-desktop/blob/master/user-guide.md#connecting-to-an-existing-jupyterlab-server) (with the link you just copied from your terminal session)
2. [The python requirements file and how to create it](https://learnpython.com/blog/python-requirements-file/)
3. [Conda install requirements](https://linuxhint.com/conda-install-requirements-txt/)
4. [Introducing the new JupyterLab Desktop!](https://medium.com/jupyter-blog/introducing-the-new-jupyterlab-desktop-bca1982bdb23)

</details>
