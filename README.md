# dotfiles

My personal configuration files for linux

## Setup on a fresh machine

1. Install Arch, get a working internet connection, install `git` and `base-devel` (for `yay`/AUR).
2. Clone this repo as a bare repo directly into `$HOME`:
```bash
   git clone --bare git@github.com:justpramod/dotfiles.git $HOME/.dotfiles
```
3. Define the `dotfiles` alias for this shell session:
```bash
   alias dotfiles='/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
```
4. Back up any pre-existing config files that would conflict, then checkout:
```bash
   mkdir -p ~/.dotfiles-backup
   dotfiles checkout 2>&1 | grep -E "\s+\." | awk '{print $1}' | xargs -I{} mv {} ~/.dotfiles-backup/{} 2>/dev/null
   dotfiles checkout
```
5. Hide untracked files from `dotfiles status`:
```bash
   dotfiles config --local status.showUntrackedFiles no
```
6. Re-source your shell config:
```bash
   source ~/.zshrc
```
7. Reinstall packages from the saved lists:
```bash
   sudo pacman -S --needed - < ~/pkglist.txt
   yay -S --needed - < ~/pkglist-aur.txt
```
8. Reboot into Hyprland or log into the Plasma session — configs should already be in place.

## Daily usage

Treat `dotfiles` exactly like `git`:

```bash
dotfiles status
dotfiles add ~/.config/hypr/hyprland.conf
dotfiles commit -m "tweak hyprland keybinds"
dotfiles push
```

To update the package lists before a commit:
```bash
pacman -Qqen > ~/pkglist.txt
pacman -Qqem > ~/pkglist-aur.txt
```


