---
title: Installing GOG games that run under DOSbox via Ansible
modified: 2018-07-24
tags: [gog,games]
layout: post
---

I've created an Ansible role that can install any GOG game that is packaged with DOSbox, see [https://github.com/rgibert/ansible-role-dosbox-gog](https://github.com/rgibert/ansible-role-dosbox-gog) (or [rgibert.dosbox_gog](https://galaxy.ansible.com/rgibert/dosbox_gog) from Ansible Galaxy)

Here is an example use case:

{% highlight yaml %}
- hosts:
    - laptop
- roles:
    - role: rgibert.dosbox_gog
      dosbox_gog_app_name_long: Quest for Glory 2
      dosbox_gog_app_name_short: qfg2
      dosbox_gog_app_bin: "{{ dosbox_root }}/app/SCIV.EXE"
      dosbox_gog_installer_path: /volume1/share0/apps/gog/quest_for_glory_2-2.1.0.34.exe
      dosbox_gog_desktop_img: /home/richard/.local/share/icons/qfg2.png
    tags:
    - dosbox-gog-qfg2
{% endhighlight %}
