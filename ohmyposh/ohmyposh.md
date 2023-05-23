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

## Recommendations
* [Consolas Nerd Font](https://github.com/wclr/my-nerd-fonts/blob/master/Consolas%20NF/Consolas%20Nerd%20Font%20Complete%20Mono%20Windows%20Compatible.ttf) 🏴‍☠️

## First-time setup

1. **Install OMP with Choco:**

    Open a PowerShell instance (Administrator) and run the following command:
    ```powershell
    choco install oh-my-posh
    ```

1. **Install a Nerd Font:**

    OMP requires "Nerd Fonts", which are Monospace fonts augmented with symbols and icons.  
    Without them, most of the themes will not display shell prompts correctly.  
    Run the following command:
    ```powershell
    oh-my-posh font install
    ```
    A menu will be listed, of all possible (free-to-use) Nerd Fonts catered by OMP.  
    Select one of your liking to install.

1. **Set a Nerd Font for PowerShell and VSCode integrated terminal:**

    In PowerShell, right click the title bar, then select "Properties">"Font".  
    Select your installed font from the list and hit "OK".  

    In VSCode, hit Ctrl+Shift+P, then type "settings.json" and hit Enter.  
    Paste the following key-values inside the JSON object, replacing the placeholders with your installed font's name:  
    ```json
    "editor.fontFamily": "NERD_FONT_NAME",
    "terminal.integrated.fontFamily": "NERD_FONT_NAME",
    ```

1. **Configure theme:**  
    Run the following command:
    ```PowerShell
    Get-PoshThemes
    ```
    This will demonstrate in the shell all of OMP's endorsed themes.  
    Once you settled on one, say the "aliens" theme, find its Github URL in [Themes](https://ohmyposh.dev/docs/themes), go to its Github page, select "RAW", and copy the RAW Github URL.

    Open your `$PROFILE` file via some text editor:
    ```powershell
    code $PROFILE
    ```

    Paste in the file the following line, where the URL is your selected theme's:
    ```PowerShell
    oh-my-posh init pwsh --config 'https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/aliens.omp.json' | Invoke-Expression
    ```
    
    Save and restart your shell.

## Removal
Open a PowerShell instance (Administrator), and run the following command:
```powershell
scoop uninstall oh-my-posh
```
