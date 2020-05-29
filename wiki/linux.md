# Linux

## Compress a File Without Removing It
~~~
gzip < file > file.gz
~~~

## Setting OS Limits with systemd
1. Edit /etc/systemd/user.conf and /etc/systemd/systemd.conf, add the following line to each file:
~~~
DefaultLimitNOFILE=NEW_LIMIT
~~~
1. Edit /etc/security/limits.conf and set the usual limit details:
~~~
USER soft nofile NEW_LIMIT
USER hard nofile NEW_LIMIT
~~~
1. Restart your system for the changes to take effect.

## Loop Over Unique Pairings of Items
~~~
set -- item0 item1 item2
for outer; do
    shift
    for inner; do
        echo "${outer}-${inner}"
    done
done
~~~

## Recursively Set +x for Only Directories
Set the executable bit for directories (and not files) using +X (upper case) instead of +x (lower case).
~~~
chmod g+rX *
~~~

## Prevent sudo Password Prompts

If you don't have NOPASSWD set in sudoers, you can still bypass the password prompt by setting SUDO_ASKPASS to a binary that echos your password.
~~~
echo "echo mypassword" > ~/.local/bin/sudopass.sh
chmod 755 ~/.local/bin/sudopass.sh
export SUDO_ASKPASS=${HOME}/.local/bin/sudopass.sh
~~~
