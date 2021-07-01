# [Docs](../README.md) > [Setup](../setup/index.html) > Windows Development QuickStart

<!-- markdownlint-disable MD033 - no-inline-html -->

<a href="chocolatey.org"><img src="https://chocolatey.org/content/images/logo_square.svg" alt="drawing" width="100" style="float: right"/></a>

<!-- markdownlint-capture -->
<!-- markdownlint-disable -->
<!-- markdownlint-restore -->

_These scripts leverage Chocolatey, the package manager for windows. [Click here](https://chocolatey.org/why-chocolatey) to learn more about Chocolatey._

## QuickStart Overview

Starting out in DataOps requires a new set of tools from what developers may have used previously. Thankfully, package managers like Chocolatey and Homebrew exist to streamline the process of getting new software installed (and keeping it updated) on your machine.

The package manager reduces the time to get software installed, saving hours of time and ensuring everyone's machines are setup correctly with minimal effort. Here's a quick overview of the tools you'll install in the next section:

1. A **package manager**: Chocolatey (for Windows) or Homebrew (for Mac)
2. **Docker** - to run containerized apps and create your own.
3. **Git** - a version control platform used to store and manage code.
4. **GitHub Desktop** - a friendly GUI which works with Git and GitHub.com.
5. **Python** - a software language useful for developing new programs and scripts, and also used for its popular package manager `pip`, which allows users to install Python programs written by others.
6. **Terraform** - the leading cross-platform solution for automating Infrastructure as Code (IaC).
7. **VS Code** - a robust, fast, and lightweight development environment (IDE).

## Installing Chocolatey and Core Tools

1. Open Command Prompt ("cmd.exe") as Administrator.

    ![command-prompt-admin](../labs/resources/command-prompt-admin.gif)

2. Paste and run the [Chocolatey.org](https://chocolatey.org/docs/installation#install-with-cmdexe) install script:

    ```cmd
    @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command " [System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
    ```

    <a href="https://git-scm.com/"><img src="https://git-scm.com/images/logo@2x.png" alt="drawing" width="45" style="float: right"/></a>

3. Install git:

    ```cmd
    choco install -y git.install --params "/GitOnlyOnPath /SChannel /NoAutoCrlf /WindowsTerminal"
    ```

4. Install core tools:

    ```cmd
    choco install -y choco-protocol-support chocolateygui sudo terraform vscode github-desktop
    choco install -y python3
    choco install -y docker-desktop
    ```

- **NOTE:** See the [Troubleshooting](#troubleshooting) tips below if you run into any difficulties during this process.

## Installing additional tools

Now that you have the core tools installed, you can click to install any of the below that would be useful for your project, or find additional packages using [chocolatey.org/packages](https://chocolatey.org/packages) index or the **ChocolateyGUI** Windows app.

- [choco://7zip](choco://7zip)
- [choco://anaconda3](choco://anaconda3) or [choco://miniconda](choco://miniconda)
- [choco://awscli](choco://awscli)
- [choco://azure-cli](choco://azure-cli)
- [choco://dbeaver](choco://dbeaver)
- [choco://firefox](choco://firefox)
- [choco://filezilla](choco://filezilla)
- [choco://github-desktop](choco://github-desktop)
- [choco://GoogleChrome](choco://GoogleChrome)
- [choco://gradle](choco://gradle)
- [choco://javaruntime](choco://javaruntime)
- [choco://jdk8](choco://jdk8)
- [choco://jdk11](choco://jdk11)
- [choco://microsoft-teams.install](choco://microsoft-teams.install)
- [choco://microsoft-windows-terminal](choco://microsoft-windows-terminal)
- [choco://microsoftazurestorageexplorer](choco://microsoftazurestorageexplorer)
- [choco://notepad++](choco://notepadplusplus)
- [choco://powerbi](choco://powerbi)
- [choco://tableau-desktop](choco://tableau-desktop)
- [choco://r.project](choco://r.project)
- [choco://sql-server-management-studio](choco://sql-server-management-studio)
- [choco://winmerge](choco://winmerge)
- [choco://wsl](choco://wsl)
- [choco://wsl2](choco://wsl2)
- [choco://wsl-ubuntu-1804](choco://wsl-ubuntu-1804)
- [choco://wsl-ubuntu-2004](choco://wsl-ubuntu-2004) (Samrat Update, Ubuntu 2004)
- [choco://azure-data-studio](choco://azure-data-studio)
- [choco://db-visualizer](choco://db-visualizer)
- [choco://ditto](choco://ditto)
- [choco://sublimetext3](choco://sublimetext3)
- [choco://atom](choco://atom)

## Extra Credit: Create a GitHub Account

For extra credit, visit [GitHub.com](https://github.com/) and register a new account. Once you've created a GitHub account and installed the core software, you are all all set to contribute to open source projects in GitHub, including this one!

- _Tip: Rather than create multiple accounts, we recommend using a single GitHub account for both work and personal development projects._

## Troubleshooting

If you run into issues during this process, here are some tips which might help:

1. If the batch script approach does not appear to be working, it may be caused by security protections. Try the manual approach of copy-pasting the needed install command, and also make sure you are running the command prompt "as administrator".
2. If the manual approach still does not work, try again to copy-paste the command [from here](https://chocolatey.org/docs/installation#install-with-cmdexe) on the Chocolatey.org website. _(The install command does not change often, but very occasionally there are security patches which require small adjustments to that process.)_
3. If all else fails or if you find a bug in this documentation, please [click here to report the issue as a bug](https://github.com/slalom-ggp/dataops-docs/issues/new). So that we can provide the fastest response possible, please be sure to paste your error message and any other symptoms which may help in the debugging process.

## Related Links

- [Mac Setup QuickStart](mac.md)
- _You can alternatively try any of the URLs below to download and run the automated setup:_
  - [https://docs.dataops.tk/setup/choco_min.bat](choco_min.bat) ([source](https://github.com/slalom-ggp/dataops-docs/blob/master/setup/choco_min.bat)) - Installs a bare-minimum set of tools to get started: `Chocolatey`, `python`, and `git`
  - [https://docs.dataops.tk/setup/choco_devops.bat](choco_devops.bat) ([source](https://github.com/slalom-ggp/dataops-docs/blob/master/setup/choco_devops.bat)) - The above, plus additional development tools: `vscode`, `terraform`, and `docker`
