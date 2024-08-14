# How to Style Your IPT

For simple customization in versions 2.6 or higher please use [UI Management](administration.adoc).

<dl><dt><strong>⚠️ WARNING</strong></dt><dd>

Customization using `custom.css` does not work in version 2.5.0, see [this issue](https://github.com/gbif/ipt/issues/1634).

Basic customizations can be made by editing `$tomcat/webapps/ipt/styles/main.css`.
</dd></dl>

**❗ IMPORTANT**\
Styling an IPT requires deployment using a servlet container like Tomcat.  A deployment from Linux packages or Docker could only be styled by overriding the `custom.css` file in a forward proxy.

## Introduction

The following guide explains how to customize the IPT, and preserve your customization when upgrading your IPT’s version.

In short, customization can be achieved by applying CSS overrides.

1. Apply your desired CSS overrides in `custom.css` (choose a different colour scheme for example). You can find this file inside the deployed WAR folder, e.g. `$tomcat/webapps/ipt/styles`. The original [custom.css](https://github.com/gbif/ipt/blob/master/src/main/webapp/styles/custom.css) comes pre-populated with a set of example CSS overrides to change the colours used in buttons, links, etc.
2. Upon completion, backup the `custom.css` file somewhere safe so that it can be added once again after each IPT upgrade, which unfortunately will overwrite the `custom.css` file each time.

Take a look at the screenshot to see the effect of changing the default CSS.

![IPTCustomizedStyle](ipt2/customization/IPTCustomizedStyle.png)
