# Chocolatey

## About

[Choco](https://chocolatey.org/) (short, "Chocolatey") is a package manager for Windows that simplifies the process of installing, managing, and updating software packages on your system. It provides a command-line interface (CLI) through which you can search for, install, and uninstall software packages with ease.

With Choco, you can install popular software applications, development tools, utilities, and other packages directly from the command line, without the need to manually download and install them from individual websites. Choco manages the entire process for you, including dependency resolution and version tracking.

## Prerequisites
None.

## Sources
* https://chocolatey.org/install
* https://community.chocolatey.org/packages/chocolatey
* https://docs.chocolatey.org/en-us/choco/commands/

## First-time setup
Open a new PowerShell instance (Administrator), run the following command:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Once done, make sure Choco is up to date by running:

```powershell
# to install a stable version < 2:
choco upgrade chocolatey
# to install a prerelease beta version >= 2.0:
choco upgrade chocolatey --pre # USE AT YOUR OWN RISK!
```

## Package installation

To install a new packages, run:
```powershell
choco install firefox -y
```

The `-y` flag will auto-accept any prompted installation disclaimer.

Note that Choco will look up the Chocolatey Community Repository for any installed corresponding with your query.

You can even query can a regex such as '`fire*`'.

It is a good practice to run the `search` command before installing, so you can select the exact package you are looking for:
```powershell
choco search firefox
```

The output will look something like this:
```PowerShell
Chocolatey v1.3.1
Firefox 113.0.1 [Approved]
firefox-quantum-nox 1.8.12 [Approved]
librefox-firefox 2.1 [Approved]
...
```

Choose your desired package (with its exact listed name) and run the install command.

It is recommended to only install packages which are marked as Approved.

## Package removal

To remove a specific package, run:
```powershell
choco uninstall firefox -y
```

If you are not sure the package's exact name, you can list all the locally installed packages with running:
```powershell
choco search --local # version < 2.0
choco list # version => 2.0
```

To remove all installed packages, run:
```powershell
choco uninstall all -y
```

## Package list export/import

To export your list of locally installed packages, you can run:
```powershell
choco export
```

This will create a file with the following path: `%USERPROFILE%/packages.config`

To import and install packages from such file, run:
```powershell
choco install "path/to/packages.config"
```