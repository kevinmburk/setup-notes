# Setup Notes for New MacBook Pro


### Apps to Download
- VS Code
- iTerm2


### Setup in CLI
1. Install Xcode Command Line Tools:
    ```bash
    xcode-select --install
    ```
2. Install Homebrew:
    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
3. Install Node:
    ```bash
    brew install node
    ```
4. Set up SSH keys: (link for reference: `https://www.freecodecamp.org/news/git-ssh-how-to/`)
    - Check if SSH keys exist: (likely no)
      ```bash
      ls -al ~/.ssh
      ```
    - If no such file or directory exists, make one:
      ```bash
      mkdir ~/.ssh
      ```
    - Generate a new set of keys:
      ```bash
      ssh-keygen -t rsa -b 4096 -C kevin.burk@sebrands.com
      ```
    - It will ask you what to name the files for your new SSH keys, just name them: 
      ```bash
      id_rsa
      ```
    - Check that your keys exist:
      ```bash
      ls -al ~/.ssh
      ```
5. Add new SSH key to ssh-agent:
    - Check to see if `ssh-agent` is running:
        ```bash
        eval "$(ssh-agent -s)"
        ```
    - Next, add your private key to `ssh-agent`:
      ```bash
      ssh-add ~/.ssh/id_rsa
      ```
6. Copy your public SSH key and add to GitHub:
    - Print the contents of your public key:
      ```bash
      cat ~/.ssh/id_rsa.pub
      ```
    - Highlight and copy the output.
    - Go to [GitHub settings](https://github.com/settings/keys) and click the `New SSH Key` button.
    - Name the key something recognizable, and paste the contents of your public SSH key.
    - Enable SSO with Anytime Fitness.
    - Check authentication:
      ```bash
      ssh -T git@github.com
      ```
    - You should see this output: `Hi your_user_name! You've successfully authenticated, but GitHub does not provide shell access.`


### Install .NET
- Visit [here](https://dotnet.microsoft.com/download) and download .NET Core 5.0


### Setup NuGet
- Follow [this wiki](https://wiki.sebrands.com/pages/viewpage.action?spaceKey=PLAT&title=GitHub+Package+Repository) up through `List NuGet Sources`.


### Download Repos
- Use SSH to clone
- [af-coach-site](https://github.com/anytimefitness/af-coach-site)
- [react-app-template](https://github.com/anytimefitness/af-react-app-template)


### Required VS Code Extensions
- C#
- Path Intellisense


### Fun Stuff
- Import dank mono, set as default for iTerm and VS Code
- Install oh-my-zsh:
    ```bash
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    ```
- Install Typewritten:
    ```bash
    git clone https://github.com/reobin/typewritten.git $ZSH_CUSTOM/themes/typewritten
    ln -s "$ZSH_CUSTOM/themes/typewritten/typewritten.zsh-theme" "$ZSH_CUSTOM/themes/typewritten.zsh-theme"
    ln -s "$ZSH_CUSTOM/themes/typewritten/async.zsh" "$ZSH_CUSTOM/themes/async"
    ```
- Add the following to your `.zshrc` file:
    ```bash
    ZSH_THEME="typewritten"
    export TYPEWRITTEN_PROMPT_LAYOUT="pure"
    export TYPEWRITTEN_CURSOR="block"
    ```

- VS Code extensions:
  - Prettier
  - Material Theme Icons
  - Material Theme _(set accent color in command palette)_
  - Bracket Pair Colorizer, then add to `settings.json`:
      ```json
      "bracket-pair-colorizer-2.forceIterationColorCycle": true,
      ```
  - GitLens
  - Code Spell Checker
  - Auto Close Tag
  - Auto Rename Tag
