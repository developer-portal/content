---
title: PEAR
page: php
section: tech-languages
---

## PEAR Installation


The PHP Extension and Application Repository is a repository of PHP software code. 
To install PEAR, type:

```
# dnf install php-pear
```

### Upstream PEAR modules
Use pear command to install PEAR extensions. To install Mail_Mime package (for example), type:

```
# pear install Mail_Mime
```
You can [find more PEAR modules](http://pear.php.net/packages.php).


### PEAR modules from official Fedora repositories
Many PEAR modules are packaged and available in base Fedora to install. Not all these packages have php-pear- prefix to upstream PEAR names, but you can browse [list of them online](http://rpms.remirepo.net/rpmphp/rpm.php?type=pear).

To install Mail_Mime you therefore install php-pear-Mail-Mime package:

```
# dnf install php-pear-Mail-Mime
```