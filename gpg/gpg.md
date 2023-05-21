# GPG key generation and setup for signing Github commits

## About
[GnuPG](https://gnupg.org/) (GNU Privacy Guard) is a free and open-source implementation of the OpenPGP (Pretty Good Privacy) standard. It provides cryptographic privacy and authentication for data communication, including email encryption, file encryption, and digital signatures.

GnuPG allows users to generate key pairs, consisting of a public key and a corresponding private key. The public key can be freely distributed to others, while the private key is kept securely by the key owner. The public key is used to encrypt data that can only be decrypted with the corresponding private key, ensuring confidentiality. Additionally, the private key can be used to digitally sign messages, verifying the authenticity and integrity of the data.

GnuPG supports various encryption algorithms and features, including symmetric-key encryption, public-key encryption, key management, and certification. It is compatible with many email clients and other software applications, making it widely used for secure communication and data protection.

GnuPG is available for various operating systems, including Windows, macOS, and Linux. It is a popular choice for individuals and organizations seeking to secure their communications and protect sensitive information.


## Sources
* https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key
* https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits


## Prerequisites
* [Git](https://git-scm.com/)


## Recommendations
* [Chocolatey](https://chocolatey.org/): Choco is a great tool for Windows devs.  
For those who don't want to use it - open a Git Bash instance instead, and skip to **step 5**.  
It should be noted that you can even install Git using Choco.


## Steps

0. **Install Chocolatey:**  
    Open a PowerShell instance (Administrator).  
    Run the following command in the shell:  
    ```powershell
    Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
    ```

0. **Install GnuPG:**  
    Run the following command in the shell:  
    ```powershell
    choco install gpg -y
    ```
    After that, **restart you machine**.  
    *This is done to refresh the shell's environment variables, so it will recognize the `gpg` command.

0. **Configurate Git to use Choco's install of GnuPG:**  
    Open a PowerShell instance (Administrator).  
    Run the following command in the shell:  
    ```powershell
    git config --global gpg.program "C:\Program Files (x86)\gnupg\bin\gpg.exe"
    ```

0. **Generate a new key and copy its ID:**  
    Run the following command in the shell, replacing the placeholders with your Github account credentials:  
    ```powershell
    gpg --quick-generate-key "GITHUB_USERNAME <GITHUB_EMAIL>" rsa sign
    ```
    You will be prompted to enter a **passphrase**.  
    *Make sure you write it down, since GnuPG will ask for it whenever pushing commits to a remote!  
    Once done, run this:  
    ```powershell
    gpg --list-secret-keys --keyid-format long
    ```
    The output will be something like this:
    ```
    gpg: checking the trustdb
    gpg: marginals needed: 3  completes needed: 1  trust model: pgp
    gpg: depth: 0  valid:   2  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 2u
    gpg: next trustdb check due at 2025-04-16
    C:\Users\user\AppData\Roaming\gnupg\pubring.kbx
    -----------------------------------------------
    sec   rsa3072/FGFQZF4ERXDVALSJ 2023-04-17 [SC] [expires: 2025-04-16]
          IC0437TYUL8PL6R553BGQGVZPBCGOKJINYE8VHJ6
    uid                 [ultimate] GITHUB_USERNAME <GITHUB_EMAIL>
    ```
    The key's id is ```FGFQZF4ERXDVALSJ```, copy it.  

0. **Configurate Git to use the generated key:**  
    Run the following command in the shell, replace the placeholder with the key's id:
    ```powershell
    git config --global user.signingkey "KEY_ID"
    ```

0. **Export the key:**  
    Run the following command in the shell, replace the placeholder with the key's id:
    ```powershell
    gpg --armor --export "KEY_ID"
    ```
    The output will be something like this:
    ```
    -----BEGIN PGP PUBLIC KEY BLOCK-----
    mQGNBGRpvPEBDAC1KQVTkRN9HIaoHTyGMd3rEJsPdTYgzJfg4C9wGBaPAvgWF/BW..
                              ...
    ..KNaqDi2zGnLghahN6NbToqGPkGeKvyy+ScD7r5Pgs8i1KW5ZKQYEgAw==
    =CcT7
    -----END PGP PUBLIC KEY BLOCK-----
    ```
    Copy the entire above block, including the ```"-----BEGIN..."``` and ```"-----END..."``` lines.

0. **Associate the exported key with your Github account:**  
    
    Go to: https://github.com/settings/keys.  
    Click on "New GPG Key".  
    Paste the block you copied earlier.  
    *It is optional yet recommended to give your new key a memorable title.  
    Click on "Add GPG Key" and you are done!  

0. **Optional: activate [Vigilant mode](https://docs.github.com/en/authentication/managing-commit-signature-verification/displaying-verification-statuses-for-all-of-your-commits)**  
    Check "Flag unsigned commits as unverified" on the same Github page.
