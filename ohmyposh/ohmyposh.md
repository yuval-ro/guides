# Oh My Posh

<img src='https://raw.githubusercontent.com/jandedobbeleer/oh-my-posh/main/website/static/img/logo.png' height='200px'></img>


## Table of contents
* [About](#about)
* [Sources](#sources)
* [Prerequisites](#prerequisites)
* [Installation](#installation)
* [Removal](#removal)


## About
From the [Oh My Posh](https://ohmyposh.dev/) site:

A prompt theme engine for any shell.

### Colors:
Oh My Posh enables you to use the full color set of your terminal by using colors to define and render the prompt.

### Customizable:
Easily adjust existing themes or create your own. From standard segments all the way to custom implementations.

### Portable:
No matter which shell you're using, or even how many, you can carry the configuration from one shell and/or machine to another for the same prompt everywhere you work.


## Sources
* https://ohmyposh.dev/docs/installation/windows


## Prerequisites
* [Choco](https://github.com/yuval-ro/guides/blob/master/choco/choco.md)


## Installation

1. **Install OMP with Choco:**

    Open a PowerShell instance (Administrator) and run the following command:
    ```powershell
    choco install oh-my-posh
    ```

1. **Install a Nerd Font and configurate shells to use it:**

    OMP requires "Nerd Fonts", which are monospaced fonts augmented with symbols and icons.
    
    Without them, most of the themes will not display shell prompts correctly.
    
    Run the following command which will list all possible Nerd Fonts OMP offers:
    ```powershell
    oh-my-posh font install
    ```
    
    Select one you like, say 'Hack', and install it by pressing Enter.

    After that, configure the following to use 'Hack' as their display font:

    * PowerShell:
        * Right-click the title bar and select "Properties".
        * From "Font" tab select "Hack Nerd Font Mono" from the dropdown.
    
    * Terminal:
        * Right-click the title bar and select "Settings".
        * From "Profiles" select "Windows PowerShell".
        * From "Additional Settings" select "Appearance".
        * From "Font Face" select "Hack Nerd Font Mono" from the dropdown.

    * VSCode:
        * Hit Ctrl+Shift+P, type "settings.json", hit Enter.
        * Paste the following key-values inside the JSON object in the openeed file, replacing the placeholders with your installed font's name:
            ```json
            "editor.fontFamily": "Hack Nerd Font Mono",
            "terminal.integrated.fontFamily": "Hack Nerd Font Mono"
            ```

1. **Configure OMP theme:**  
    Run the following command, which will demo all of OMP's included themes:
    ```PowerShell
    Get-PoshThemes
    ```
    
    Select one you like, say 'nu4a', and open your `$PROFILE` file via some text editor:
    ```powershell
    code $PROFILE
    ```

    Paste in the opened file the following lines:
    ```PowerShell
    # This will call the OMP init script every time a PowerShell instance is started,
    #  and set the theme to the one defined by the local .json file as follows:
    oh-my-posh init pwsh --config 'C:\Program Files (x86)\oh-my-posh\themes\nu4a.omp.json' | Invoke-Expression
    # This will remove the "(venv) " prompt prefix that pip embeds in your shell whenver you are within an activated venv.
    # Instead, the OMP theme will have its own good-looking prefix.
    $env:VIRTUAL_ENV_DISABLE_PROMPT = 1
    ```

    Save and restart your shell.


## Removal
Open a PowerShell instance (Administrator), and run the following command:
```powershell
choco uninstall oh-my-posh
```
