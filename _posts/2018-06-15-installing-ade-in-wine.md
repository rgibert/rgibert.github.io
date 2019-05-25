---
title: Installing ADE 4.5.x in WINE
modified: 2018-07-24
tags: [wine,ade]
layout: post
---

Here is how to get Adobe Digital Editions (ADE) to work under WINE on Linux.

1. Download ADE 4.5.0 & the latest version (4.5.0 can be found at [https://filehippo.com/download_adobe_digital_editions/63548/](https://filehippo.com/download_adobe_digital_editions/63548/)).
2. ```WINEARCH=win32 wine wineboot```
3. ```winetricks corefonts dotnet40```
4. ```winetricks ddr=gdi```
5. ```wine ADE_4.5.0_Installer.exe```
6. Unpack ADE_4.5.LATEST_Installer.exe and copy DigitalEditions.exe, log4net.dll, and rmsdk_wrapper.dll from 4.5.LATEST to the WINE install from running the 4.5.0 installer

I've made an Ansible role that installs ADE 4.5.0 (skips the LATEST portion of above), see [https://github.com/rgibert/ansible-role-wine-ade45](https://github.com/rgibert/ansible-role-wine-ade45) or [rgibert.wine_ade45](https://galaxy.ansible.com/rgibert/wine_ade45) from Ansible Galaxy
