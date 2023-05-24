# Oh My Posh

## About
[Oh My Posh](https://ohmyposh.dev/) (OMP) is a framework for customizing and enhancing the prompt in your command-line interface (CLI), primarily designed for PowerShell. It provides a highly customizable and visually appealing prompt, allowing you to personalize your command-line experience.

OMP offers various features, including:

1. Themes: It comes with a collection of pre-configured themes that you can choose from, allowing you to customize the appearance of your prompt.

1. Segments: OMP allows you to add segments to your prompt, such as displaying the current Git branch, the current directory, or the status of your Git repository.

1. Customization: You can further customize your prompt by modifying the themes, creating your own custom themes, or adding and configuring segments according to your preferences.

1. Compatibility: OMP is designed to work with various shells, including PowerShell, PowerShell Core, Windows Terminal, and more.

Note that OMP is primarily focused on PowerShell, and if you are using a different shell, there might be alternative prompt customization frameworks available specific to that shell.

## Sources
* https://ohmyposh.dev/docs/installation/windows

## Prerequisites
* [Choco](https://github.com/yuval-ro/guides/blob/master/choco/choco.md)

## First-time setup

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
