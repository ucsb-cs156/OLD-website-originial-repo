---
topic: "Windows: WSL"
desc: "Setting up a development environment under Windows Subsystem for Linux"
indent: true
category_prefix: "Windows: "
---

_Note that these instructions may be slightly outdated, as they were written in Match / April, but they should stil work. We're working on verifying that these instructions are still up-to-date._

For advanced users who are looking to have a full Linux command-line interface on their Windows machine (which may be helpful for CMPSC 156 work), we recommend using Windows Subsystem for Linux (WSL). WSL is a tool that basically creates a separate Linux environment alongside your Windows environment, with access to your local filesystem. This will allow you to access package managers (such as `apt-get` for Ubuntu/Debian) and the full suite of UNIX commands.

Note that the reference platform for the course remains "CSIL"; we cannot commit to being "tech support" for every conceivable platform.  On your own machine, you *are* your own tech support.  But we'll help as best we can, given the time constraints we are under.

The first step is ensuring that you have a compatible machine. You will need:
* Windows 10, build 16215 or later (but we recommend 18917 or later to use new [WSL 2 features](https://devblogs.microsoft.com/commandline/announcing-wsl-2/) and the new [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701)).
* Administrator privileges on your machine

The following guides from Microsoft detail the installation instructions for WSL 1 and 2: <https://docs.microsoft.com/en-us/windows/wsl/install-win10>. When choosing a distribution, we recommend Ubuntu 18.04 LTS, as this is what the course staff uses.

Once installation is complete, you should be able to launch your distribution from the Windows Start Menu.

For users who want a nicer looking terminal, complete with tabs, emojis, and more customization features, you can optionally install the new [Windows Terminal from the Microsoft Store](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701).

Keep in mind that WSL uses UNIX line endings (LF) while Windows uses CRLF line endings. If you checked out your code natively in Windows (i.e. using Git Bash or GitHub Desktop), your Git repository may be using CRLF line endings, and therefore may cause Shell scripts (and other programs that parse based on line endings) and Git commits to act differently or fail.

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

WSL should come with git, but the pre-installed version is usually outdated (you can check by running `git --version`). If it is not installed, then follow the instructions at this link: https://peteoshea.co.uk/setup-git-in-wsl/

If you want to work remotely via SSH, you will have to generate new SSH keys specific to the WSL environment. For instructions on how to do that, take a look at this page: https://ucsb-cs56.github.io/topics/github_ssh_keys/
   * You don't need to set up SSH keys, since you can always work remotely with repos via HTTPS, but using SSH keys just makes it easier since you will not have to re-enter your GitHub login information whenever you want to clone a repo or push/pull.

### Heroku on WSL

The Heroku CLI is normally installed with snap, but the WSL doesn't currently support snap so you won't be able to install it with the commands that would be used in a normal Linux environment. Instead, run `curl https://cli-assets.heroku.com/install.sh | sh` to install the CLI.

### Node and npm on WSL

[Visit this page](/topics/node_windows/#windows-subsystem-for-linux-wsl) for instructions on how to install Node and npm on WSL.

For this class, we recommend the latest version of Node 12.x and npm 6.x. 

### WSL with VSCode

If you are currently a VS Code user (or considering becoming one), you can install an extension to be able to access/edit/track files in the WSL from VS Code. Follow the instructions [here](LINK) to get started.
