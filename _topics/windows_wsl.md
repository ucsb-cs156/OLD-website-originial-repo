---
topic: "Windows: WSL"
desc: "Setting up a development environment under Windows Subsystem for Linux"
indent: true
category_prefix: "Windows: "
---

For advanced users who are looking to have a full Linux command-line interface on their Windows machine (which may be helpful for CMPSC 156 work), we recommend using Windows Subsystem for Linux (WSL). WSL is a tool that basically creates a separate Linux environment alongside your Windows environment, with access to your local filesystem. This will allow you to access package managers (such as `apt-get` for Ubuntu/Debian) and the full suite of UNIX commands.

Note that the reference platform for the course remains "CSIL"; we cannot commit to being "tech support" for every conceivable platform. On your own machine, you *are* your own tech support. But we'll help as best we can, given the time constraints we are under.

## Compatibility

The first step is ensuring that you have a compatible machine. You will need:
* One of the following operating systems:
   * Windows 11, any build
   * Windows 10, build 16215 or later (but we recommend 18917 or later to use new [WSL 2 features](https://devblogs.microsoft.com/commandline/announcing-wsl-2/) and the new [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701)).
* Administrator privileges on your machine

## Installation

On Windows 11 machines and Windows 10 machines with build 19041 or higher, installing WSL is very simple:

1. Open Command Prompt or PowerShell as administrator
   * This can be done by searching for either program in the Start Menu, right-clicking on the result, and selecting "Run as administrator"
2. Run the following command:

```
wsl --install
```

This will enable and install WSL with the default configuration:

* WSL 2
* The latest LTS release of Ubuntu (currently 20.04 LTS)

More information on the above steps can be found [here](https://docs.microsoft.com/en-us/windows/wsl/install).

If your machine doesn't meet the criteria to use the one-line install command, you can follow the manual installation instructions [here](https://docs.microsoft.com/en-us/windows/wsl/install-manual). Unless you know exactly what you're doing, we recommend Ubuntu 20.04 LTS as your distribution.

The better / safer solution is to update your Windows 10 machine to a more recent build, so we recommend doing that and using the one-line install command instead.

Once installation is complete, you should be able to launch your distribution from the Windows Start Menu.

## (Recommended) Windows Terminal Install

For users who want a nicer looking terminal, complete with tabs, full Unicode support (for emojis!), custom colors / fonts, and more customization features, you can optionally install the new Windows Terminal.

Windows Terminal is already the default terminal for Windows 11 users, so no installation is needed.

For Windows 10 users, you can install Windows Terminal from the [Microsoft Store](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701).

## A note about Line Endings on Windows

Keep in mind that WSL uses UNIX line endings (LF) while Windows uses CRLF line endings. If you check out your code natively in Windows (i.e. using Git Bash or GitHub Desktop), your checked-out code will use CRLF line endings, and therefore may cause Shell scripts (and other programs that parse based on line endings) and Git commits to act differently or fail.

For this course, since most of our work will be done in WSL, you should try to use LF line endings whenever possible.



# THE FOLLOWING INSTRUCTIONS HAVE NOT BEEN UPDATED YET DO NOT USE

### Java on WSL

Run the following commands to get your Java environment set up:

* To install the Java JDK <br />
`sudo apt-get update` <br />
`sudo apt-get install default-jdk` <br />
 To verify Java JDK has been installed <br />
 `java --version`

* To install Ant <br />
`sudo apt install ant` <br />
To check  <br />
`ant -version`

* To install Maven<br />
`sudo apt install maven`<br />
To check <br />
`mvn -version`

**Make sure you have Java-11, not an earlier version!**

### Git on WSL

WSL should come with git, but the pre-installed version is usually outdated (you can check by running `git --version`). If it is not installed, then follow the instructions at this link: <https://peteoshea.co.uk/setup-git-in-wsl/>

If you want to work remotely via SSH, you will have to generate new SSH keys specific to the WSL environment. For instructions on how to do that, take a look at [this page](/topics/github_ssh_keys/).
   * You don't need to set up SSH keys, since you can always work remotely with repos via HTTPS, but using SSH keys just makes it easier since you will not have to re-enter your GitHub login information whenever you want to clone a repo or push/pull.

### Heroku on WSL

The Heroku CLI is normally installed with snap, but the WSL doesn't currently support snap so you won't be able to install it with the commands that would be used in a normal Linux environment. Instead, run `curl https://cli-assets.heroku.com/install.sh | sh` to install the CLI.

### Node and npm on WSL

[Visit this page](/topics/node_windows/#windows-subsystem-for-linux-wsl) for instructions on how to install Node and npm on WSL.

For this class, we recommend the latest version of Node 12.x and npm 6.x. 

### WSL with VSCode

If you are currently a VS Code user (or considering becoming one), you can install an extension to be able to access/edit/track files in the WSL from VS Code. Follow the instructions [here](https://code.visualstudio.com/docs/remote/wsl) to get started.
