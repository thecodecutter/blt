# BLT installation

* Do not clone BLT as a means of using it. The only reason to clone BLT is to contribute to it.*

## System requirements

You must have the following tools on the command line of your *host operating system*:

* [Git](https://git-scm.com/)
* [Composer](https://getcomposer.org/download/)
* [PHP 7.1+](http://php.net/manual/en/install.php)

Instructions for installing _all_ requirements for various operating systems are listed below. In general, make sure all installed tools are the most recent version unless otherwise noted.

### Networking considerations

Building project dependencies requires that your local machine make HTTP and HTTPS requests to various software providers on the internet. Please ensure that your local and network level security settings permit this to happen.

If you need to make requests via a proxy server, please [configure git to use a proxy](http://stackoverflow.com/a/19213999). This will cover all git based requests made by Composer

## Installing requirements

### macOS

Ensure that [Xcode](https://itunes.apple.com/us/app/xcode/id497799835?mt=12) is installed (primarily in order to support Homebrew). On OSX 10.9+ you can install Xcode with:

        sudo xcodebuild -license
        xcode-select --install

Then install the minimum dependencies for BLT. The preferred method is via Homebrew, though you could install these yourself without a package manager.

        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
        brew install php71 git composer 
        composer global require hirak/prestissimo:^0.3
        composer global require zaporylie/composer-drupal-optimizations:^1.1

Note that the recommended installation method for Drush has changed recently. Drush should only be installed as a dependency of individual projects, rather than being installed system-wide. BLT will manage this dependency for you on projects, but in order for you to run Drush commands independently of BLT commands you need to install the Drush Launcher: [Drush Launcher Installation](https://github.com/drush-ops/drush-launcher#installation---phar).

If you'd like to use [Drupal VM](https://www.drupalvm.com/) with BLT, Drupal VM has additional requirements. See the [Drupal VM Requirements](https://blt.readthedocs.io/en/latest/local-development/#using-drupal-vm-for-blt-generated-projects) to add these. If you'd like to use a LAMP stack other than Drupal VM, see [Local Development](local-development.md).

If you are not using a VM, and you'd like to execute Behat tests from the host machine, you will need Java:

        brew cask install java
        brew cask install chromedriver

BLT ships with the [Cog Base Theme](https://github.com/acquia-pso/cog) by default. Cog uses [npm](https://www.npmjs.com/) to install front end tools. If you intend to use Cog, you should also install the following tools:

        brew install npm nvm

### Windows

Windows is currently supported only when using the [Bash on Ubuntu on Windows](https://msdn.microsoft.com/en-us/commandline/wsl/about) feature available in the latest version of Windows 10.

Pre-requisite requirements:
  - You must be running a 64-bit version of Windows 10 Anniversary update (build 14393 or later)
  - Access to a local account with administrative rights for initial install

Follow the official [installation guide](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).

Note you **must** create a UNIX username with a password when prompted at the final step in the process. Certain BLT commands will not function correctly if you install with a passwordless root account.

Once complete follow the [BLT on Windows installation instructions](windows-install.md).

### Linux

Linux is fully supported by BLT and DrupalVM and shares many of the same dependencies as MacOS (except Xcode, of course).

#### Ubuntu / Debian

        apt-get install git composer drush
        composer global require hirak/prestissimo:^0.3
        composer global require zaporylie/composer-drupal-optimizations:^1.1

#### Fedora

        sudo dnf install -y git composer drush
        composer global require "hirak/prestissimo:^0.3"
        # To use NFS with Vagrant, nfs-utils package needs to be installed and nfs-server needs to be running.
        # https://developer.fedoraproject.org/tools/vagrant/vagrant-nfs.html
        sudo dnf install -y nfs-utils && sudo systemctl enable nfs-server
        # Enable nfs, rpc-bind and mountd services for firewalld
        sudo firewall-cmd --permanent --add-service=nfs \
            && sudo firewall-cmd --permanent --add-service=rpc-bind \
            && sudo firewall-cmd --permanent --add-service=mountd \
            && sudo firewall-cmd --reload

# Installing BLT

After you have successfully installed the prerequisites, you can now proceed with installing BLT.

* [Creating a new project with BLT](creating-new-project.md)
* [Adding BLT to an existing project](adding-to-project.md)

If BLT is already setup for a project and you need instructions on how to get started please see:
* [Cloning an existing BLT project](onboarding.md)

If you are trying to update Acquia BLT please see:
* [Upgrading BLT](updating-blt.md)
