# Quickstart

installation
```bash
# -- entrypoint
sudo -i
# -- base
parted /dev/sda -- mklabel msdos
parted /dev/sda -- mkpart primary 1MB -8GB
parted /dev/sda -- mkpart primary linux-swap -8GB 100%
mkfs.ext4 -L nixos /dev/sda1
mkswap -L swap /dev/sda2
swapon /dev/sda2
mount /dev/disk/by-label/nixos /mnt
# -- config
nixos-generate-config --root /mnt
vim /mnt/etc/nixos/configuration.nix # can use git here
# -- install
nixos-install
# if messed up something here use nixos-rebuild switch
reboot
```

nix-shell
```bash
nix-shell -p <nix.pkgs> # install packages on a ephemeral shell
```

nix-env
```bash
nix-env -iA <nix.pkgs> # install
```

# Links

[Firewall](https://nixos.wiki/wiki/Firewall)
[Nginx](https://nixos.wiki/wiki/Nginx)
[Grafana](https://nixos.wiki/wiki/Grafana)