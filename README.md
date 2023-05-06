# General configs for windows setup

# Install the development Software
## 1 - Installing Software
Before starting installing software, be sure that you update the system, remove trash apps and software. Clean the system, change privacy settings and customize the theme.

Now you can starting installation of the software:
* This software is the basic for my daily uses:
  ```
    winget install Nvidia.GeForceExperience; winget install Piriform.CCleaner; winget install Spotify.Spotify --force; winget install VideoLAN.VLC; winget install Microsoft.VCRedist.2015+.x86; winget install Microsoft.VCRedist.2015+.x64; winget install Microsoft.VCRedist.2013.x86; winget install Microsoft.VCRedist.2013.x64; winget install Microsoft.VCRedist.2012.x86; winget install Microsoft.VCRedist.2012.x64; winget install Microsoft.DotNet.Runtime.6; winget install Microsoft.DotNet.AspNetCore.6; winget install Microsoft.DotNet.SDK.6; winget install Microsoft.DotNet.Runtime.5; winget install Microsoft.DotNet.Runtime.3_1; winget install 7zip --source winget; winget install Valve.Steam --source winget; winget install Discord.Discord --source winget; winget install KeeWeb; winget install NZXT.CAM; winget install Logitech.GHUB; winget install SteelSeries.GG; winget install Brave.Brave

  ```

* Install the development software 
  ```
  winget install Microsoft.VisualStudioCode; winget install Git.Git; winget install GitHub.GitLFS; winget install Microsoft.GitCredentialManagerCore; winget install GitHub.GitHubDesktop; winget install Amazon.AWSCLI; winget install WinMerge.WinMerge;
  ```

* Install from appstore: itunes, msi center and ambiance,

* Open a terminal in admin mode, and launch:
  ```
  wsl --install
  ```

  This will install all necessary for WSL machines, after the installation finish, reboot the system.

* Now configurate SSH machine certification. For this you need install openssh in the additional features in the configuration app. Then run the next code blocks.

  Launch terminal in admin mode and launch:
  ```
  Get-Service -Name sshd | Set-Service -StartupType Automatic
  Start-Service sshd
  ```

  Then in normal mode launch:
  ```
  ssh-keygen -t rsa -C "youremail"
  ```

  Run as admin:
  ```
  Get-Service ssh-agent | Set-Service -StartupType Manual
  Start-Service ssh-agent
  Get-Service ssh-agent
  ```

  And finally add your ssh key, this in normal mode:
  ```
  ssh-add ~\.ssh\id_rsa
  ```

* For deploy your ssh key go to github, and add the public key into ssh and gpg management. If you did it right, run: ssh -T git@github.com

This is the basic software, after this you can install additional software as pycharm, VStudio Community, etc.

___

## 2 - Configure Software
* Clean the system with ccleaner.
* Now starting adding accounts to the main web browser (Brave in my case).
* Open MSI Center and update the drivers and reboot.
* Starts Nvidia GeforceExperience and update GPU drivers (3080 in my case).
* Finally config nvidia panel and done.
___
# Customize the prompt
## 1 - Clone the repository
When you clone the repo, you'll have 2 files. The user_profile and a json, this files contain the powershell config and the oh my posh theme.

Then create a folder into your home folder, called .config. Then copy the powershell config and leave it inside .config.
___

## 2 - Install requirements for config
* First should download Nerd Fonts, and install the Windows Compatible. The font is your choice, I pref Hack NF.

* Now, we should config windows terminal. Go to windows terminal configuration and enable acrylic mode (As your choice). Then we should download a theme from net and add it to the json config, in the themes section. Select it in the visual config and done.

* Install powershell from the windows store. Restart the window and select windows terminal as default, the same with the shell.

* Install scoop in our system. Is a package manager for normal users. Exec the next command with admin launched terminal:
  ```
  Set-ExecutionPolicy RemoteSigned -scope CurrentUser
  ```
  Then install the package manager without admin launched terminal:
  ```
  Invoke-WebRequest get.scoop.sh | Invoke-Expression
  ```

* Install neovim:
  ```
  scoop install neovim
  ```

* Install Oh My Posh
  ```
  Install-Module posh-git -Scope CurrentUser -Force
  winget install JanDeDobbeleer.OhMyPosh -s winget
  ```

* Instal Terminal Icons
  ```
  Install-Module -Name Terminal-Icons -Repository PSGallery -Force
  ```

* Install z Directory jumper
  ```
  Install-Module -Name z -Force
  ```

* Install PSReadline
  ```
  Install-Module -Name PSReadLine -AllowPrerelease -Scope CurrentUser -Force -SkipPublisherCheck
  ```

* Install fzf
  ```
  scoop install fzf
  Install-Module -Name PSFzf -Scope CurrentUser -Force
  ```
* Install neovim configuration and setup
  ```
  scoop install ripgrep
  scoop install mingw
  git clone https://github.com/NvChad/NvChad $HOME\AppData\Local\nvim --depth 1 && nvim
  ```
* Edit the host profile to use our profile.
  ```
  nvim $PROFILE.CurrentUserCurrentHost
  ```

  Add the following line to the last edit:
  ```
  . $env:USERPROFILE\.config\powershell\user_profile.ps1
  $env:VIRTUAL_ENV_DISABLE_PROMPT = 1
  ```