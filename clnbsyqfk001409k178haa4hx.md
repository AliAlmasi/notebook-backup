---
title: "“How to verify git commits” — Easy guide for beginners"
seoTitle: "“How to verify git commits” — Easy guide for beginners"
seoDescription: "A helpful summary of GitHub documentation for beginners"
datePublished: Wed Oct 04 2023 13:46:57 GMT+0000 (Coordinated Universal Time)
cuid: clnbsyqfk001409k178haa4hx
slug: how-to-verify-git-commits
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1696429537802/6ecbd94d-58c5-4c53-b1ee-1f39f1184a8f.png

---

What is “Verified” Git commits? How can I verify my Git commits?

These were the questions I asked myself when I saw “verified” commits on GitHub.

![A verified Git commit is shown on GitHub](https://cdn-images-1.medium.com/max/800/1*tDWPrz5OhWuqzIN_Y-c1XQ.png align="center")

After lots of searching, I found out it is one of the most cool features of Git.

> When it comes to commits in large open-source projects, it's all about ensuring that the commits being made are legitimate and coming from the correct source and the correct person. GPG keys are a way to digitally sign commits, which provides an extra layer of security and verification. This can be especially important for open-source projects where multiple contributors are making changes to the codebase.

After weeks, I discovered that GitHub has a complete (but complex) document on this.

I read the documentation and was finally able to do this on both GNU/Linux & Windows.  
Now I want to write a helpful summary of GitHub documentation here for beginners so that I can help them in this regard.

> *Using GPG or SSH, you can sign tags and commits. These tags or commits are marked as verified on GitHub so other people can be confident that the changes come from a trusted source.*

## GNU/Linux

### Step 1 — Inspecting tools

First, we need to make sure that we have `git`, `gnupg` and `github-cli` installed.

```bash
[alialmasi@parch ~]$ git --version
git version 2.42.0

[alialmasi@parch ~]$ gpg --version
gpg (GnuPG) 2.2.41
libgcrypt 1.10.2-unknown

[alialmasi@parch ~]$ gh version
gh version 2.35.0 (2023-09-19)
https://github.com/cli/cli/releases/tag/v2.35.0
```

In most GNU/Linux distros, these are pre-installed (except for `github-cli`.) If you didn't have these installed, you can use your distro's package manager to install them.

[You can install `github-cli` with any GNU/Linux distro you have.](https://github.com/cli/cli/blob/trunk/docs/install_linux.md)

> *Note: we’ll use* `gnupg` *to generate a GPG key pair. we'll also use* `github-cli` *to authenticate ourselves to GitHub (logging into our account with our cli).*

### Step 1.1 — Initialize your `git`

If you’re new to Git, you probably have to initialize it first. (It’s just a little “Name/Email” configuration, don’t worry.) Open a terminal and do these:

1. Set your name:
    

```bash
git config --global user.name "YOUR NAME"
```

> *Tip: You can confirm that you have set the username correctly by using* `git config --global` [`user.name`](http://user.name)

1. Set your email:
    

```bash
git config --global user.email "YOUR@EMAIL.COM"
```

> *Tip: You can confirm that you have set the email correctly by using* `git config --global` [`user.email`](http://user.email)

### Step 1.2 — Authenticate to GitHub in cli

To push a local repository to GitHub, we need access. The easiest way to gain access is to authenticate using `github-cli`.

> GitHub CLI is an open-source tool for using GitHub from your computer’s command line. When you’re working from the command line, you can use the GitHub CLI to save time and avoid switching contexts.

1. Authenticate with GitHub by running this command from your terminal:
    

```bash
gh auth login
```

1. Select [`GitHub.com`](http://GitHub.com) and Follow the on-screen prompts.
    

> GitHub CLI automatically stores your Git credentials for you when you **choose HTTPS as your preferred protocol** for Git operations and **answer “yes” to the prompt asking if you would like to authenticate to Git with your GitHub credentials**. This can be useful as it allows you to use `git push`, `git pull`, and so on, without needing to set up a separate credential manager or use SSH.

### Step 2 — Generate a GPG key

Now that you’ve initialized your Git, you need to generate your own GPG key pair and add it to your GitHub account. This is where `gnupg` will help us. Open a terminal and do these:

1. Generate a GPG key pair:
    

```bash
gpg --full-generate-key
```

1. At the prompt, specify the kind of key you want, or press `Enter` to accept the default. (`RSA and RSA` is recommended.)
    
2. At the prompt, specify the key size you want, or press `Enter` to accept the default.
    
3. Enter the length of time the key should be valid. Press `Enter` to specify the default selection, indicating that the key doesn't expire. Unless you require an expiration date. (Default is recommended.)
    
4. Verify that your selections are correct.
    
5. Enter your information.
    

> *Note: When asked to enter your email address, ensure that you enter the verified email address for your GitHub account.*

1. Type a secure passphrase.
    

### Step 2.1 — Copy your public key

Congratulations, we’ve generated your GPG key pair. Now, you need to copy your public key to add it to your GitHub account.

1. Use the `gpg --list-secret-keys --keyid-format=long` command to list the long form of the GPG keys for which you have both a public and private key.
    

> *Note: Some GPG installations on Linux may require you to use* `gpg2 --list-keys --keyid-format LONG` *to view a list of your existing keys instead. In this case, you will also need to configure Git to use* `gpg2` *by running* `git config --global gpg.program gpg2`*.*

1. From the list of GPG keys, copy the long form of the GPG key ID you’d like to use. In this example, the GPG key ID is **3AA5C34371567BD2**:
    

```bash
$ gpg --list-secret-keys --keyid-format=long
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2037-03-10 [expires: 2037-05-10]
uid                          YOUR NAME <YOUR@EMAIL.COM>
ssb   4096R/4BB6D45482678BE3 2037-03-10
```

3\. Paste the text below, substituting the GPG key ID you’d like to use. In this example, the GPG key ID is **3AA5C34371567BD2**:

```bash
gpg --armor --export 3AA5C34371567BD2
```

> *Prints the GPG key ID, in ASCII armor format.*

4\. Copy your GPG key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----`.

Now that you have copied your public key, head over to *Step 3* to add your public key to your GitHub account.

### Step 3 — Add your public key to your GitHub account

> To sign commits associated with your account on GitHub, you can add a public GPG key to your account.  
> You can add multiple public keys to your account on GitHub. Commits signed by any of the corresponding private keys will show as verified. If you remove a public key, any commits signed by the corresponding private key will no longer show as verified.  
> To verify as many of your commits as possible, you can add expired and revoked keys. If the key meets all other verification requirements, commits that were previously signed by any of the corresponding private keys will show as verified and indicate that their signing key is expired or revoked.

To add your public key to your GitHub account, open a terminal and do these:

1. In the upper-right corner of any page, click your profile photo, then click **Settings**.
    
2. In the “Access” section of the sidebar, click **SSH and GPG keys**.
    
3. Next to the “GPG keys” header, click **New GPG key**.
    
4. In the “Title” field, type a name for your GPG key.
    
5. In the “Key” field, paste the GPG key you copied when you generated your GPG key in *Step 2.1*.
    
6. Click **Add GPG key**.
    
7. To confirm the action, authenticate to your GitHub account.
    

And you’re done adding your public key to your GitHub account. Now you have to tell `git` about your GPG key.

### Step 4 — Tell `git` about your GPG key.

> If you’re using a GPG key that matches your committer identity and your verified email address associated with your account on [GitHub.com](http://GitHub.com), then you can begin signing commits and signing tags.

Open a terminal and follow along:

1. Use the `gpg --list-secret-keys --keyid-format=long` command to list the long form of the GPG keys for which you have both a public and private key. **Private key is required for signing commits**.
    

> *Note: Some GPG installations on Linux may require you to use* `gpg2 --list-keys --keyid-format LONG` *to view a list of your existing keys instead. In this case, you will also need to configure Git to use* `gpg2` *by running* `git config --global gpg.program gpg2`*.*

1. From the list of GPG keys, copy the long form of the GPG key ID you’d like to use. In this example, the GPG key ID is **3AA5C34371567BD2**:
    

```bash
$ gpg --list-secret-keys --keyid-format=long
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
uid                          Hubot <hubot@example.com>
ssb   4096R/4BB6D45482678BE3 2016-03-10
```

1. To set your primary GPG signing key in Git, paste the text below, substituting the GPG primary key ID you’d like to use. In this example, the GPG key ID is **3AA5C34371567BD2**:
    

```bash
git config --global user.signingkey 3AA5C34371567BD2
```

1. To configure Git to sign all commits by default, enter the following command:
    

```bash
git config --global commit.gpgsign true
```

1. To add your GPG key to your .bashrc startup file, run the following command:
    

```bash
[ -f ~/.bashrc ] && echo -e '\nexport GPG_TTY=$(tty)' >> ~/.bashrc
```

## Windows

### Step 1 — Inspecting tools

First, we need to make sure that we have `git`, `gnupg` and `github-cli` installed.

```powershell
PS C:\> git --version
git version 2.42.0.windows.1

PS C:\> gpg --version
gpg (GnuPG) 2.4.3
libgcrypt 1.10.2

PS C:\> gh version
gh version 2.35.0 (2023-09-19)
https://github.com/cli/cli/releases/tag/v2.35.0
```

> *Note: we’ll use* `gnupg` *to generate a GPG key pair. we'll also use* `github-cli` *to authenticate ourselves to GitHub (logging into our account with our cli).*

If you don’t have these installed, you can use `winget` or other package managers for Windows to install these, or you can download installers from their websites.

* [Git official website](https://git-scm.com/download/win)
    

```powershell
winget install --id Git.Git -e --source winget
```

* [GnuPG official website](https://gnupg.org/download/index.html)
    

```powershell
winget install -e --id GnuPG.GnuPG
```

* [GitHub CLI official website](https://github.com/cli/cli#windows)
    

```powershell
winget install --id GitHub.cli
```

> *Note: The Windows installer modifies your PATH. You will need to open a new terminal after you’ve installed these tools, for the changes to take effect. (Simply opening a new tab will not be sufficient.)*

### Step 1.1 — Initialize your `git`

If you’re new to Git, you probably have to initialize it first. (It’s just a little “Name/Email” configuration, don’t worry.) Open a terminal (or Git bash) and do these:

1. Set your name:
    

```powershell
git config --global user.name "YOUR NAME"
```

> *Tip: You can confirm that you have set the username correctly by using* `$ git config --global` [`user.name`](http://user.name)

1. Set your email:
    

```powershell
git config --global user.email "YOUR@EMAIL.COM"
```

> *Tip: You can confirm that you have set the email correctly by using* `$ git config --global` [`user.email`](http://user.email)

### Step 1.2 — Authenticate to GitHub in cli

To push a local repository to GitHub, we need access. The easiest way to gain access is to authenticate using `github-cli`.

> GitHub CLI is an open-source tool for using GitHub from your computer’s command line. When you’re working from the command line, you can use the GitHub CLI to save time and avoid switching contexts.

1. Authenticate with GitHub by running this command from your terminal (or Git bash):
    

```powershell
gh auth login
```

1. Select [`GitHub.com`](http://GitHub.com) and Follow the on-screen prompts.
    

> GitHub CLI automatically stores your Git credentials for you when you **choose HTTPS as your preferred protocol** for Git operations and **answer “yes” to the prompt asking if you would like to authenticate to Git with your GitHub credentials**. This can be useful as it allows you to use `git push`, `git pull`, and so on, without needing to set up a separate credential manager or use SSH.

### Step 2 — Generate a GPG key

Now that you’ve initialized your Git, you need to generate your own GPG key pair and add it to your GitHub account. This is where `gnupg` will help us. Open a terminal (or Git bash) and do these:

1. Generate a GPG key pair:
    

```powershell
gpg --full-generate-key
```

1. [At](http://2.At) the prompt, specify the kind of key you want, or press `Enter` to accept the default. (`RSA and RSA` is recommended.)
    
2. At the prompt, specify the key size you want, or press `Enter` to accept the default.
    
3. Enter the length of time the key should be valid. Press `Enter` to specify the default selection, indicating that the key doesn't expire. Unless you require an expiration date. (Default is recommended.)
    
4. Verify that your selections are correct.
    
5. Enter your information.
    

> *Note: When asked to enter your email address, ensure that you enter the verified email address for your GitHub account.*

1. Type a secure passphrase.
    

### Step 2.1 — Copy your public key

Congratulations, we’ve generated your GPG key pair. Now, you need to copy your public key to add it to your GitHub account.

1. Use the `gpg --list-secret-keys --keyid-format=long` command to list the long form of the GPG keys for which you have both a public and private key.
    
2. From the list of GPG keys, copy the long form of the GPG key ID you’d like to use. In this example, the GPG key ID is **3AA5C34371567BD2**:
    

```powershell
PS C:\> gpg --list-secret-keys --keyid-format=long
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2037-03-10 [expires: 2037-05-10]
uid                          YOUR NAME <YOUR@EMAIL.COM>
ssb   4096R/4BB6D45482678BE3 2037-03-10
```

1. Paste the text below, substituting the GPG key ID you’d like to use. In this example, the GPG key ID is **3AA5C34371567BD2**:
    

```powershell
gpg --armor --export 3AA5C34371567BD2
```

> *Prints the GPG key ID, in ASCII armor format.*

1. Copy your GPG key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----`.
    

Now that you have copied your public key, head over to *Step 3* to add your public key to your GitHub account.

### Step 3 — Add your public key to your GitHub account

> To sign commits associated with your account on GitHub, you can add a public GPG key to your account.  
> You can add multiple public keys to your account on GitHub. Commits signed by any of the corresponding private keys will show as verified. If you remove a public key, any commits signed by the corresponding private key will no longer show as verified.  
> To verify as many of your commits as possible, you can add expired and revoked keys. If the key meets all other verification requirements, commits that were previously signed by any of the corresponding private keys will show as verified and indicate that their signing key is expired or revoked.

To add your public key to your GitHub account, open a terminal (or Git bash) and do these:

1. In the upper-right corner of any page, click your profile photo, then click **Settings**.
    
2. In the “Access” section of the sidebar, click **SSH and GPG keys**.
    
3. Next to the “GPG keys” header, click **New GPG key**.
    
4. In the “Title” field, type a name for your GPG key.
    
5. In the “Key” field, paste the GPG key you copied when you generated your GPG key in *Step 2.1*.
    
6. Click **Add GPG key**.
    
7. To confirm the action, authenticate to your GitHub account.
    

And you’re done adding your public key to your GitHub account. Now you have to tell `git` about your GPG key.

### Step 4 — Tell `git` about your GPG key.

> If you’re using a GPG key that matches your committer identity and your verified email address associated with your account on [GitHub.com](http://GitHub.com), then you can begin signing commits and signing tags.

Open a terminal (or Git bash) and follow along:

1. Use the `gpg --list-secret-keys --keyid-format=long` command to list the long form of the GPG keys for which you have both a public and private key. **Private key is required for signing commits**.
    
2. From the list of GPG keys, copy the long form of the GPG key ID you’d like to use. In this example, the GPG key ID is **3AA5C34371567BD2**:
    

```powershell
PS C:\> gpg --list-secret-keys --keyid-format=long
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2037-03-10 [expires: 2037-05-10]
uid                          YOUR NAME <YOUR@EMAIL.COM>
ssb   4096R/4BB6D45482678BE3 2037-03-10
```

1. To set your primary GPG signing key in Git, paste the text below, substituting the GPG primary key ID you’d like to use. In this example, the GPG key ID is **3AA5C34371567BD2**:
    

```powershell
git config --global user.signingkey 3AA5C34371567BD2
```

1. To configure Git to sign all commits by default, enter the following command:
    

```powershell
git config --global commit.gpgsign true
```

Now you’ve completed setting up your GPG key pair to sign your Git commits on GitHub.

Try and make some commits, push them to GitHub and Check them out. There must be a little “Verified” tag on the commits you’ve made. 😃