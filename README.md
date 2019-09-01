# ansible-arch #

Some Ansible playbooks to help install and configure Arch Linux.

## Usage ##

After booting from the Arch installation media, you will need to:
1. Set the root password using the `passwd` command.
2. Use `vim` to edit the file `/etc/ssh/sshd_config` by changing the
   `ChallengeResponseAuthentication` setting to `yes`.
3. Restart the ssh service using `systemctl restart sshd`.
4. Create a keyfile on your local host containing the password for
   your LUKS root volume via `echo -n "your_password" > keyfile`.
5. Generate a hash for the password to be used on your personal
   account using `mkpasswd --method=sha-512`.

At this point we are able to login remotely as root, so we can
populate `install/inventory.yml` and run `install/playbook.yml`:

```console
cd install
ansible-playbook -i inventory.yml playbook.yml
```

Note that you may have to fiddle with the UEFI settings in the BIOS in
order to get the new installation to boot.

Once the new installation boots, you can populate
`configure/inventory.yml` and run `configure/playbook.yml`:

```console
cd configure
ansible-playbook -i inventory.yml playbook.yml
```

At this point your new Arch Linux system is ready to be used.
