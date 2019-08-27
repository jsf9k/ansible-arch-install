# arch-install #

Some Ansible playbooks to help install Arch Linux.

## Usage ##

After booting from the Arch installation media, you will need to:
1. Set the root password using the `passwd` command.
2. Use `vim` to edit the file `/etc/ssh/sshd_config` by changing the
   `ChallengeResponseAuthentication` setting to `yes`.
3. Restart the ssh service using `systemctl restart sshd`.
4. Create a keyfile on your local host containing the password for
   your LUKS root volume via `echo -n "your_password" > keyfile`.

At this point we are able to login remotely as root, so we can
populate `baremetal-inventory.yml` and run the "baremetal" playbook:

```console
ansible-playbook -i baremetal-inventory.yml baremetal-playbook.yml
```

Note that you may have to fiddle with the UEFI settings in the BIOS in
order to get the new installation to boot.

In order to run the "ui" playbook, you first need to generate a
password hash for your personal account:

```console
mkpasswd --method=sha-512
```

With this in hand you can populate `ui-inventory.yml` and run the "ui"
playbook:

```console
ansible-playbook -i ui-inventory.yml ui-playbook.yml
```

At this point your new Arch Linux system is ready to be used.
