(authenticated_git)=

# Getting started with Git, Github, and Gitlab

```{note}
Here we assume that Git is already installed on your platform. Contact your system's administrator if it is not so.
```

In this tutorial you will learn:

 - What Git is.
 - How to configure Git.
 - How to configuration authentication to Github or Gitlab via the command line.

# What is Git

"Git is a distributed version control software system that is capable of managing versions of source code or data" ([Wikipedia](https://en.wikipedia.org/wiki/Git)). A version control system is "a system that records changes to a file or set of files over time so that you can recall specific versions later." ([Pro Git book](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)). Put simply, **Git can help you save a full history of all your work in a clean way so that you never have to worry about modifying files or losing previous work**.

All of Git's functionality can be used via the command-line. In addition, online platforms such as [Github](https://github.com/) provide a graphical interface to perform certain Git operations. They also provide additional functionality beyond pure Git, and are very helpful when collaborating as a team on the same project.

# First time Git setup

In order to use Git's most useful features, you must tell it your name and email address using the following commands:

```sh
git config --global user.name "John Lennon"
git config --global user.email john.lennon@beatles.com
```

If you prefer, you may use a pseudonym instead of your real name.

In order to avoid receiving email spam, we recommend you do **not** use you actual email address. Github and Gitlab provide a "no-reply" address that you can use instead. You can find this address in the "Emails" (Github) or "Profile" (Gitlab) section of your account's settings.

# How to connect to Github or Gitlab via the command line

Certain Github and Gitlab operations require you to be authenticated. Here we will configure a commonly-used authentication method based on SSH keys. The first step is to create an SSH key:

```sh
ssh-keygen
```

Press Enter to accept the default location and name for the SSH key, and then define your password. Please use a good and unique password, especially on multi-user systems. This will prevent other users as well as system administrators to be able to perform authenticated Git operations in your stead.

The above command should create two files, typically (names can vary):

 - `~/.ssh/id_ed25519` is your private key, that you should never share with anyone.
 - `~/.ssh/id_ed25519.pub` is your public key, that can be shared when authentication is needed.

Now change file permissions so that other users cannot read your keys:

```sh
chmod 400 ~/.ssh/id*
```

The last step is to upload your public key to Github or Gitlab:

 1. Copy the content of your public key (you can see it with `less ~/.ssh/id_ed25519.pub`).

 2. In your web browser, go to your Github account settings and, under "SSH and GPG keys", click "New SSH key". On Gitlab, go into your accont settings then "Access", then "SSH Keys", then "Add new key".

You are now all set, you can now perform authenticated operations to Github or Gitlab from the command-line.
