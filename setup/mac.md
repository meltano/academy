# [Docs](../README.md) > [Setup](../setup/index.html) > Mac OSX Development QuickStart

<!-- markdownlint-disable MD033 - no-inline-html -->

<a href="https://brew.sh"><img src="https://brew.sh/assets/img/linuxbrew.png" alt="drawing" width="100" style="float: right"/></a>

<!-- markdownlint-capture -->
<!-- markdownlint-disable -->
<!-- markdownlint-restore -->

_These scripts leverage Homebrew, the package manager for Mac. [Click here](https://brew.sh) to learn more about Homebrew._

## QuickStart Overview

Starting out in DataOps requires a new set of tools from what developers may have used previously. Thankfully, package managers like Chocolatey and Homebrew exist to streamline the process of getting new software installed (and keeping it updated) on your machine.

The package manager reduces the time to get software installed, saving hours of time and ensuring everyone's machines are setup correctly with minimal effort. Here's a quick overview of the tools you'll install in the next section:

1. A **package manager**: Chocolatey (for Windows) or Homebrew (for Mac)
2. **Docker** - to run containerized apps and create your own.
3. **Git** - a version control platform used to store and manage code.
4. **GitHub Desktop** - a friendly GUI which works with Git and GitHub.com.
5. **Python** - a software language useful for developing new programs and scripts, and also used for its popular package managers `pip` and `pipx`, which allows even non-developers to install and use Python programs written by others.
6. **VS Code** - a robust, fast, and lightweight development environment (IDE).

## Installing Homebrew and Core Tools

1. Open "Terminal".
2. Paste and run the [Homebrew](https://brew.sh) install script:

   ```bash
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

   <a href="https://git-scm.com/"><img src="https://git-scm.com/images/logo@2x.png" alt="drawing" width="45" style="float: right"/></a>

3. Install git.

   ```cmd
   brew install git
   ```

4. Install dev tools:

   ```cmd
   brew install python3 terraform cakebrew visual-studio-code
   ```

5. Install docker.

   ```cmd
   brew install --cask docker
   ```

## Installing additional tools (Optional)

After following the instructions from the above, you should now have the **Cakebrew** app installed, which gives a friendly GUI on top of the Homebrew installer.

To install any additional programs, either open the **Cakebrew** app or copy-paste the below samples into a Terminal window. (You can also find additional packages at [https://brew.sh](https://brew.sh).)

- `brew install awscli`
- `brew install aws-sam-cli` **You might first need to run: `brew tap aws/tap`
- `brew install azure-cli`
- `brew install elasticsearch`
- `brew install gradle`
- `brew install --cask anaconda`
- `brew install --cask dbeaver-community`
- `brew install --cask firefox`
- `brew install --cask github`
- `brew install --cask google-chrome`
- `brew install --cask microsoft-teams`
- `brew install --cask pgadmin4`
- `brew install --cask r`
- `brew install --cask slack`
- `brew install --cask selenium-server-standalone`
- `brew install --cask terraform`

## Extra Credit: Create a GitHub Account

For extra credit, visit [GitHub.com](https://github.com/) and register a new account. Once you've created a GitHub account and installed the core software, you are all all set to contribute to open source projects in GitHub, including this one!

- _Tip: Rather than create multiple accounts, we recommend using a single GitHub account for both work and personal development projects._

## Related Links

- [Windows Setup QuickStart](windows.md)
- Brew QuickSetup Script: [https://docs.dataops.tk/setup/brew_install.sh](brew_install.sh) ([source](https://github.com/slalom-ggp/dataops-docs/blob/master/setup/brew_install.sh))
