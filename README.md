# General configs for windows setup

# Install the development Software
## 1 - Installing Software on Fresh install
Before starting installing software, be sure that you update the system, remove trash apps and software. Clean the system, change privacy settings and customize the theme.

Now you can starting installation of the software:
* This software is the basic for my daily uses:
  ```
     winget install Piriform.CCleaner; winget install Spotify.Spotify --force; winget install VideoLAN.VLC; winget install Microsoft.VCRedist.2015+.x86; winget install Microsoft.VCRedist.2015+.x64; winget install Microsoft.VCRedist.2013.x86; winget install Microsoft.VCRedist.2013.x64; winget install Microsoft.VCRedist.2012.x86; winget install Microsoft.VCRedist.2012.x64; winget install Microsoft.DotNet.SDK.8; winget install Microsoft.DotNet.DesktopRuntime.8; winget install Microsoft.DotNet.AspNetCore.8; winget install Microsoft.DotNet.Runtime.8; winget install Microsoft.DotNet.Runtime.6; winget install Microsoft.DotNet.Runtime.5; winget install Microsoft.DotNet.Runtime.3_1; winget install 7zip --source winget; winget install Valve.Steam --source winget; winget install Discord.Discord --source winget; winget install NZXT.CAM; winget install Logitech.GHUB; winget install Brave.Brave; winget install Bitwarden.Bitwarden; winget install EpicGames.EpicGamesLauncher;

  ```
  
* Install from appstore: itunes, msi center and ambiance,

* Install new nvidia app. Still in beta but works incredible and merge nvidia control panel and geforce experience: https://www.nvidia.com/es-es/software/nvidia-app/
___

## 2 - Configure Software
* Clean the system with ccleaner.
* Now starting adding accounts to the main web browser (Brave in my case).
* Open MSI Center and update the drivers and reboot.
* Starts Nvidia App and update GPU drivers (3080 in my case).
* Finally config nvidia panel and done.

___

# Development Setup
## 1 - Development setup

* First of all, we should able wsl. Open a terminal on admin mode and launch this command:
  ```
  wsl --install
  ```
  Restart and continue.


* Install the development software 
  ```
  winget install Microsoft.VisualStudioCode; winget install Git.Git; winget install GitHub.GitLFS; winget install Microsoft.GitCredentialManagerCore; winget install Amazon.AWSCLI; winget install JetBrains.Toolbox; winget install SlackTechnologies.Slack; winget install Notion.Notion; winget install Docker.DockerDesktop; winget install Nvidia.CUDA;
  ```
___
## 2 - Config ssh key for git porpouses
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

* Disable AWS telemetry: setx AWS_CLI_TELEMETRY_DISABLED 1
___
## 3 - Clone this repository
When you clone the repo, you'll have 2 files. The user_profile and a json, this files contain the powershell config and the oh my posh theme.

Then create a folder into your home folder, called .config. Then copy the powershell config and leave it inside .config.
___

## 4 - Install requirements for config files
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
  Install-Module -Name PSReadLine -Scope CurrentUser -Force -SkipPublisherCheck
  ```

* Install fzf
  ```
  scoop install fzf
  Install-Module -Name PSFzf -Scope CurrentUser -Force
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
## 5 - Python version manager and lib manager

* First of all, you should install pyenv as version manager:
  
  ```
    Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/pyenv-win/pyenv-win/master/pyenv-win/install-pyenv-win.ps1" -OutFile "./install-pyenv-win.ps1"; &"./install-pyenv-win.ps1"
  ```

* If you we an **UnauthorizedAccess**, then run this follow command on powershell as admin and rerun the command above:

  ```
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine
  ```
  Now reopen terminal, and if you exec pyenv, should get a list with all commands availible.
</br>
  Exec: pyenv install "your prefer python version", without quotes and when it finish use pyenv rehash.
</br>
* Next, setup a global python version with pyenv global "your python version" and remove python.exe aliases on windows settings

* Install pipx for use it in some apps, exec the commands 1 by 1:
  ```
    scoop install pipx
    pipx ensurepath
    python -m pip install --user pip
  ```

* Is time for install poetry dependency manager:
  ```
    pipx install poetry
  ```

  When finish, you can exec poetry on terminal and we will use this for libs installation, virtualenvs, and more

# LLMS and AI installation
## 1 - Ollama installation and models.
* Ollama installation url: https://ollama.com/download

  Restart terminal and run: ollama run llama3, this will pull the llama3 AI model and starts. Now exec /bye for exit the model.

</br>

 * Web ui for ollama installation is pretty simple with pipx, but first need exec scoop command and then install the webui:
  ```
    scoop install ffmpeg
    pipx install open-webui
  ```

  * With this you have the web ui installed, now you can enter into the url: http://localhost:8080, configure at your preferences.

## 2 - Automatic1111 image AI generator
* For install this AI image creator, enter in this repo and follow guide for windows. https://github.com/AUTOMATIC1111/stable-diffusion-webui
* Once finish the installation, expose api for use it on llama3.


# Last tweaks
## 1 - Git config
* We'll config our git, create a file on your user path called .gitconfig and paste this lines:
  ```
    [filter "lfs"]
      clean = git-lfs clean -- %f
      smudge = git-lfs smudge -- %f
      process = git-lfs filter-process
      required = true
    [user]
      name = yourusername
      email = youremail
    [core]
      editor = code --wait
    [diff]
      tool = vscode
    [difftool "vscode"]
      cmd = code --wait --diff $LOCAL $REMOTE
    [merge]
      tool = vscode
    [mergetool "vscode"]
      cmd = code --wait $MERGED
  ```
