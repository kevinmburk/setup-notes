# Setup Notes for New MacBook Pro


### Apps to Download
- VS Code
- iTerm2
- Google Chrome _(if not already installed)_


### Setup in CLI
1. Open iTerm2, and install Xcode Command Line Tools:
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
4. Set up SSH keys: ([Check out this article for more info](https://www.freecodecamp.org/news/git-ssh-how-to/))
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
      ssh-keygen -t rsa -b 4096 -C your.email@sebrands.com
      ```
    - It will ask you what to name the files for your new SSH keys, just name them: 
      ```bash
      id_rsa
      ```
    - Check that your keys exist:
      ```bash
      ls -al ~/.ssh
      ```
5. Add your newly created SSH key to ssh-agent:
    - Check to see if `ssh-agent` is running:
        ```bash
        eval "$(ssh-agent -s)"
        ```
    - Next, add your private key to `ssh-agent`:
      ```bash
      ssh-add ~/.ssh/id_rsa
      ```
6. Copy your public SSH key and add to your GitHub profile:
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
    - You should see this output: 

      `Hi your_user_name! You've successfully authenticated, but GitHub does not provide shell access.`


### Install .NET
- Visit [.NET](https://dotnet.microsoft.com/download) and download `.NET Core 5.0` and `.NET Core 3.1`, you'll need both.


### Setup NuGet
- Follow [this SEB wiki](https://wiki.sebrands.com/pages/viewpage.action?spaceKey=PLAT&title=GitHub+Package+Repository) up to the `List NuGet Sources` section.


### Download Repos
- Use SSH to clone
- [af-coach-site](https://github.com/anytimefitness/af-coach-site)
- [react-app-template](https://github.com/anytimefitness/af-react-app-template)


### Required VS Code Extensions
- C#
- Path Intellisense

### Setup the `.vscode` Folder in `af-coach-site`
- This folder is included in the .gitignore, so you need to make one to use locally.
1. Create a folder called `.vscode`, and two files inside: `launch.json` and `tasks.json`
2. In `launch.json`, add the following code:
    ```json
    {
      // Use IntelliSense to find out which attributes exist for C# debugging
      // Use hover for the description of the existing attributes
      // For further information visit https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger-launchjson.md
      "version": "0.2.0",
      "configurations": [
        {
          "name": ".NET Core Launch (web)",
          "type": "coreclr",
          "request": "launch",
          "preLaunchTask": "build",
          // If you have changed target frameworks, make sure to update the program path.
          "program": "${workspaceFolder}/Af.Coach.Web/bin/Debug/netcoreapp3.1/Af.Coach.Web.dll",
          "args": [],
          "cwd": "${workspaceFolder}/Af.Coach.Web",
          "stopAtEntry": false,
          // Enable launching a web browser when ASP.NET Core starts. For more information: https://aka.ms/VSCode-CS-LaunchJson-WebBrowser
          "serverReadyAction": {
            "action": "openExternally",
            "pattern": "^\\s*Now listening on:\\s+(https?://\\S+)"
          },
          "env": {
            "ASPNETCORE_ENVIRONMENT": "Development",
            "ASPNETCORE_URLS": "http://localhost:6002"
          },
          "sourceFileMap": {
            "/Views": "${workspaceFolder}/Views"
          }
        },
        {
          "name": ".NET Core Attach",
          "type": "coreclr",
          "request": "attach",
          "processId": "${command:pickProcess}"
        }
      ]
    }
    ```
3. In `tasks.json`, add the following code:
    ```json
    {
      "version": "2.0.0",
      "tasks": [
        {
          "label": "build",
          "command": "dotnet",
          "type": "process",
          "args": [
            "build",
            "${workspaceFolder}/Af.Coach.Web/Af.Coach.Web.csproj",
            "/property:GenerateFullPaths=true",
            "/consoleloggerparameters:NoSummary"
          ],
          "problemMatcher": "$msCompile"
        },
        {
          "label": "publish",
          "command": "dotnet",
          "type": "process",
          "args": [
            "publish",
            "${workspaceFolder}/Af.Coach.Web/Af.Coach.Web.csproj",
            "/property:GenerateFullPaths=true",
            "/consoleloggerparameters:NoSummary"
          ],
          "problemMatcher": "$msCompile"
        },
        {
          "label": "watch",
          "command": "dotnet",
          "type": "process",
          "args": [
            "watch",
            "run",
            "${workspaceFolder}/Af.Coach.Web/Af.Coach.Web.csproj",
            "/property:GenerateFullPaths=true",
            "/consoleloggerparameters:NoSummary"
          ],
          "problemMatcher": "$msCompile"
        }
      ]
    }
    ```


### Install React Developer Tools Extension to Chrome
- Visit [here](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) and add the extension to your Chrome browser.
- The React Developer Tools `Components` tab is essential to find your way around the UI of the app and find the component you need to work on.


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
