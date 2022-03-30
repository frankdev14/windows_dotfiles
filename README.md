# General configs for windows setup

Before we start customizing, we will have to configure the system.
# Install the development Software
## 1 - installing Software
## 2 - Configure Software
# Customize the prompt
## 1 - Clone the repository
When you clone the repo, you'll have 2 files. The user_profile and a json, this files contain the powershell config and the oh my posh theme.

Then create a folder into your home folder, called .config. Then copy the powershell config and leave it inside .config.

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
  iwr -useb get.scoop.sh | iex
  ```

* Install neovim:
  ```
  scoop install neovim
  ```

* Install Oh My Posh
  ```
  Install-Module posh-git -Scope CurrentUser -Force
  Install-Module oh-my-posh -Scope CurrentUser -Force
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

* Edit the host profile to use our profile.
  ```
  nvim $PROFILE.CurrentUserCurrentHost
  ```

  Add the following line to the last edit:
  ```
  . $env:USERPROFILE\.config\powershell\user_profile.ps1
  ```