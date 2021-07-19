# [Docs](../README.md) > [Setup](../setup/index.html) > Windows Development QuickStart

<!-- markdownlint-disable MD033 - no-inline-html -->

<a href="chocolatey.org"><img src="https://chocolatey.org/assets/images/global-shared/logo-square.svg" alt="drawing" width="100" style="float: right"/></a>

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
5. **Python** - a software language useful for developing new programs and scripts, and also used for its package managers `pip` and `pipx`, which allows even non-developers to install Python programs written by others.
6. **VS Code** - a robust, fast, and lightweight development environment (IDE).

## Installing Chocolatey and Core Tools

1. Open Command Prompt ("cmd.exe") as Administrator.

    ![command-prompt-admin](./resources/command-prompt-admin.gif)

2. Paste and run the [Chocolatey.org](https://chocolatey.org/docs/installation#install-with-cmdexe) install script:

    ```cmd
    @"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command " [System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
    ```

    <a href="https://git-scm.com/"><img src="https://git-scm.com/images/logo@2x.png" alt="drawing" width="45" style="float: right"/></a>

3. Install Git and Python if they are not already installed:

    ```cmd
    choco install -y git.install --params "/GitOnlyOnPath /SChannel /NoAutoCrlf /WindowsTerminal"
    choco install -y python --version=3.8.10
    ```

4. Install additional tools, including VS Code:

    ```cmd
    choco install -y sudo choco-protocol-support chocolateygui github-desktop vscode
    ```

5. Install WSL2 for Linux support (recommended):

    ```cmd
    # Install WSL (Windows Subsystem for Linux) version 2:
    choco install -y wsl2

    # You may need to restart your machine before the next step:
    choco install -y wsl-ubuntu-2004

    # Finally test that WSL is working and initialize a username for your linux environment:
    wsl
    ```

   - Note: When setting up your linux user account, you may use the same username as your Windows account, but please password updates will not be synced across these accounts.

6. Install Docker (recommended):

    ```cmd
    choco install -y docker-desktop
    ```

- **NOTE:** See the [Troubleshooting](#troubleshooting) tips below if you run into any difficulties during this process.

## Test drive a Linux Dev Container in VS Code

To prove that Docker and VS Code are working correctly, let's open a Dev Container in VS Code using a GitHub project's `Open in VS Code` badge.

1. Open the GitHub repo here: https://github.com/meltano/meltano-cicd-lab-template
2. Click on the `Open in VS Code` badge.
3. Follow the guided steps to open the dev container, installing any missing components if prompted.
4. Test that the Linux container is working correctly by copy-pasting the sample code from the repo's readme into the VS Code terminal window.

## Installing additional tools (Optional)

Now that you have the core tools installed, you can click to install any of the below that would be useful for your project, or find additional packages using [chocolatey.org/packages](https://chocolatey.org/packages) index or the **ChocolateyGUI** Windows app.

- [choco://7zip](choco://7zip)
- [choco://anaconda3](choco://anaconda3) or [choco://miniconda](choco://miniconda)
- [choco://atom](choco://atom)
- [choco://awscli](choco://awscli)
- [choco://azure-cli](choco://azure-cli)
- [choco://azure-data-studio](choco://azure-data-studio)
- [choco://db-visualizer](choco://db-visualizer)
- [choco://dbeaver](choco://dbeaver)
- [choco://ditto](choco://ditto)
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
- [choco://terraform](choco://terraform)
- [choco://r.project](choco://r.project)
- [choco://sublimetext3](choco://sublimetext3)
- [choco://sql-server-management-studio](choco://sql-server-management-studio)
- [choco://winmerge](choco://winmerge)
- [choco://wsl](choco://wsl)
- [choco://wsl2](choco://wsl2)
- [choco://wsl-ubuntu-1804](choco://wsl-ubuntu-1804)
- [choco://wsl-ubuntu-2004](choco://wsl-ubuntu-2004) (Samrat Update, Ubuntu 2004)

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
- A native Windows Package Manager ("winget") is coming soon. For more info see the [`winget-cli` GitHub Repo](https://github.com/microsoft/winget-cli)
