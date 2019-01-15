# Setting Up Zsh Terminal on Windows 10

> _It is very important to follow these steps in the correct order. It is strongly recommended that you read through the documentation of each of the technologies we will be using in this guide to familiarize yourself with them._

## Things to do before starting this guide _(3 hours)_

- Before starting this guide make sure you are running Windows 10 Fall Creators Update (build 16215) or later. If unsure, follow these steps to [check your build](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#check-your-build-number).
- To install the latest version of windows click Start > Settings > Update & Security > Windows Update, and then select Check for updates. If updates are available, install them.
- Please be aware that updating Windows may take a long time.
- **_Important_**: if for some reason you cannot update Windows to at least build 16215 or it takes over 3 hours, then do not follow any of the Linux setup directions in this guide.

## 1. Install Cmder console emulator

We will be using [**Cmder**](http://cmder.net/) for its customizabilty, usability, and ability to run multiple different shells in different tabs depending on your needs (cmd, PowerShell, Bash). **_However, you may use any console emulator you are comfortable with (ie. Hyper, ConEmu, etc.)._**

1. Download the full version cmder [**here**](https://github.com/cmderdev/cmder/releases/download/v1.3.6/cmder.zip).
   > The full version includes many valuable Unix commands for the default Cmder shell & Git for Windows.
2. Unzip the downloaded file `cmder.zip`
3. Cmder is a fully portable appication, so you may move it without the application breaking. Move the entire root folder to `C:\`.
4. You may run Cmder now. By default it will utilize the default Windows Command line in a Cmder shell.
5. Pin Cmder to your Windows task bar. (Right click Cmder.exe > Pin to Taskbar)

## 2. Install & Configure Linux Subsytem for Windows

### **Install Linux**

_For additional reference you may refer to [Microsoft's documentation](https://docs.microsoft.com/en-us/windows/wsl/install-win10) and [Ubuntu's documentation](https://tutorials.ubuntu.com/tutorial/tutorial-ubuntu-on-windows) on installing the Linux subsystem on Windows._

1. Hit the Start/Windows key and type `Turn windows features on or off`; click Enter. This will require your Admin account, and will prompt you to enter your Admin username and password.
2. Ensure that `Windows Subsystem for Linux` feature is enabled.
   > Alternatively you can open PowerShell as Admin and run `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`, then restart when prompted.
3. Hit the Start/Windows key and type `Microsoft Store`; click Enter.
4. Use the search box in the top right and search for `Ubuntu`.
5. From the Ubuntu store page, select 'Get'.
6. After installation is complete, we need to initialize Ubuntu. Hit the Start/Windows key and type `Ubuntu` and click Enter.
   > The first time Ubuntu runs, a Console window will open, and it will take a minute or two for the installation to complete.
7. After the installation is complete, Ubuntu with prompt you to set up your new Linux user account
   > **Important**: This user account is for the normal non-admin user that you'll be logged-in as by default when launching a distro.<br>You can choose any username and password you wish - they have no bearing on your Windows username.<br><br>When you open a new Ubuntu instance, you won't be prompted for your password, but if you elevate a process using `sudo` (basically the same as running something as admin in Windows), you will need to enter your password, so make sure you choose a password you can easily remember!

### **Install Zsh & Oh My Zsh**

_The default command line shell for Linux is Bash, which is fine. However, we are going to use Zsh (also known as Z-Shell). Zsh has many ease of use benifits as well as the ability to customize your Linux shell with Oh-My-Zsh. Oh-My-Zsh allows us to install many useful plugins as well as change the look and feel of your terminal which can greaty increase developer productivity when working in the command line._

Some of the time saving and convenience benifits of using Zsh with Oh-My-Zsh include:

- Command validation
- Spelling correction
- Sharing command history between multiple running shells
- Themeable prompts
- Directory history
- Strong auto complete functionality
- Many useful plugins

**_i. Install Zsh_**

1. Open Ubuntu
2. Install Zsh by running `sudo apt-get install zsh` in the command line and entering your linux user password when prompted.

**_ii. Make Zsh the default Linux shell instead of Bash_**

3. Next, type `cd ~` and click enter to navigate to your linux home directory.
   > **Note**: In the next step we will be using a text editor inside the Linux shell. Ubuntu comes with two text editors already installed: [Vim](https://www.vim.org/docs.php) and [Nano](https://www.nano-editor.org/docs.php). Experienced Linux users worship Vim as the greatest code editor of all time, however it has a very steep learning curve. As such, if you are not familiar with Linux code editors, please use Nano to complete the following steps.
4. Use either Vim or Nano to text edit the .bashrc file located in this directory. To do this type either `vim .bashrc` or `nano .bashrc` and click enter. (_Nano is a little easier to use if you are not familiar with console code editors._)
   > **Important**: It is not recommended to edit files within your Linux subsystem using Windows text or code editors. It is important to understand that the Linux subsystem is basically a second operating system running within Windows, and as such has its own filesystem.
5. At the very beginning of the .bashrc file add the following lines of code:

```c
# if running in terminal...
if test -t 1; then
# start zsh
exec zsh
fi
```

> If using Nano to edit the file, simply use the arrow keys to navigate. Enter the text as you normally would using only the keyboard. Press `Ctrl + O` and then `Enter` to confirm you are naming the file `.bashrc`. Then press `Ctrl + X` to exit Nano.

**_iii. Make Linux Start in your Windows Filesystem_**

_Normally when Bash or Zsh loads, it is pointing to your home directory in the Linux filesystem. To reduce possible confusion and to save developer time, we want to make sure Linux is pointing to our Windows User folder._

6. `vim .zshrc` or `nano .zshrc`
7. At the very bottom of the file, add `cd /mnt/c/Users/<YourUserName>`, and save the file.

   > You can change this to any folder you like, but be aware that the path to your C:\ drive from ubuntu is `/mnt/c`.

**_iv. Update & Upgrade all your Ubuntu packages_**

These steps make sure you have the latest versions of all packages in Ubuntu. They may take severeal minutes.

8. run `sudo apt-get update`
9. run `sudo apt-get upgrade`

**_v. Install Oh-My-Zsh (Optional)_**

Using Oh-My-Zsh is entirely optional. However it can make your developer workflow more effecient and your life easier. Please refer to the documentation for examples of all the plugins and customizations available to you: https://github.com/robbyrussell/oh-my-zsh.

1.  run `sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`

> If oh-my-zsh seems confusing, you are not alone. Here is a [**great blog post**](https://medium.com/wearetheledger/oh-my-zsh-made-for-cli-lovers-installation-guide-3131ca5491fb) that can help you install just a few simple plugins that make working in the command line much easier.

### **Set up Linux Zsh Shell in Cmder**

1. Open Cmder
2. Press `Win + Alt + T` to open the settings dialog for Tasks. (Alternatively you can open up the hamburger menu on the bottom right of the window and navigate to Settings -> Startup -> Tasks.)
3. Create a new Task by clicking on the ‘+‘ Button at the bottom and enter the details.
4. The first input field of the dialog is the task name. Name it `zsh::ubuntu`.
5. To set ubuntu as your default shell, select the two checkboxes underneath the name.
6. In the “Task parameters” input you can configure an icon. If you want to use the Ubuntu icon enter `/icon "%USERPROFILE%\AppData\Local\lxss\bash.ico"`.
7. In the large 'Commands' text box on the bottom right, enter `%windir%\system32\bash.exe ~ -cur_console:p`.

## 3. Install Git for Linux

1. In your Linux terminal run `sudo apt install git`

## 4. Install Node.js for Linux

We are going to install a utility called Node Version Manager to handle our Node installations. It allows us to manage multiple versions of node should you need to change versions for different tasks. Please refer to the NVM documentation to understand all the capabilities of this lovely little package.

1. To install NVM run the following code in your Linux terminal: `curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash`
   > Restart your terminal and run `nvm --version` to make sure it was properly installed. If you get an error, you may try to run `command -v nvm`, restart the console, and try to check the version again. For further information, please consult the [**docs**](https://github.com/creationix/nvm)
2. Now install the LTS version of Node using NVM: `nvm install --lts`
   > At the time of writing this document, the LTS version of Node was 8.12.0. The version of the Vue CLI released at the time of this document requires version 8.9 or above (8.11.0+ recommended). Luckily, NVM makes it easy for developers to switch between versions of Node they want to use at any given time.
3. Make sure you are using the LTS version of node by running `nvm use --lts`

## 5. Install Git for Windows (_Optional_)

> **NOTE**: Git for Windows is included in the full version of Cmder. Only complete this step if you are not using Cmder.
> <br>
> Since we do not use Git for version control at Precise, many of the options presented during installation will end up being irrelevant. The purpose of having Git for us, is that it allows us to more easily interact with open source code we will be using in our projects.

1. Download Git for Windows [**here**](https://git-scm.com/download/win).
2. Click 'Next' and on the following `Select Components` screen, choose at least the following options and click 'Next':
   - Git LFS(Large File Support)
   - Associate .git \* configuration files with the default text editor
   - Associate .sh files to be run with Bash
3. Choose `Use Visual Studio Code as Git's default editor`. Click 'Next'.
4. Choose `Use Git from the Windows Command Promt`. Click 'Next'.
5. Choose `Use the OpenSSL library`. Click 'Next'.
6. Choose `Checkout as-is, commit Unix-style line endings`. Click 'Next'.
7. This step is installing a new console emulator called GitBash. Although you will not likely be using it, the MinTTY version is preferable. Select it, and click 'Next'.
8. Click through the remaining screens leaving the default options selected, and Install.

## 6. Install Node for Windows (optional)

Although we will primarily be working from the Linux command line, it is useful to have Node.js installed on Windows as well. This gives us the ability to interact with and use Node inside Visual Studio as well as in the Windows command line and Powershell.

1. Go to https://nodejs.org/en/download/ and download and run the LTS Windows Installer.

## 7. Install Microsoft Visual Studio Code

We will be using Microsoft Visual Studio Code for client side Vue development.

1. Visit https://code.visualstudio.com/ and download VSCode.
   > You should be redirected to https://code.visualstudio.com/docs/?dv=win. Please take the time to read though the documentation and familiarize yourself with VSCode.
2. Install the downloaded VSCode setup file.

### Make Linux the default VSCode terminal

1. Click `Ctrl + ,` to open VSCode's settings
2. Enter the below code under the user settings on the left hand side.

```json
  "terminal.integrated.shell.windows": "C:\\Windows\\System32\\bash.exe",
```
