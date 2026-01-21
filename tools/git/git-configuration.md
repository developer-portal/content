---
title: Configuring Git
subsection: git
order: 3
---

# Configuring Git

The git can be extensively configured.

## Basic configuration

Set the author identity by saving the name and email address with the following command. Execute without the  `--global` flag if the identity is to be retained only for the current repository.


Setting up your git commit e-mail adresses globally

```
git config --global user.email "<your-email-address>"
```

Setting up your git commit username(nickname or your name) globally

```
git config --global user.name "<your-full-name>"
```

Setting up your `core.editor`

```
git config --global core.editor vim
```

It can be change various editors such as `emacs`,`vi`,`nano`,`neovim`,`Kate` and more

For more information about changing `core.editor` config please check out [Appendix C: Git Commands - Setup and Config](https://git-scm.com/book/en/v2/Appendix-C%3A-Git-Commands-Setup-and-Config)



## More customizible settings

Please check out [Customizing Git - Git Configuration](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)
