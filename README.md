# widelands-flatpak

**Widelands** is an open source (GPLed), realtime-strategy game.

![widelands-flatpak screenshot](widelands-flatpak.png)

[Homepage](https://wl.widelands.org)

This repo is about the flatpak package.

## Instructions

### Requirements

* [flatpak](https://github.com/flatpak/flatpak)
* [flatpak-builder](https://github.com/flatpak/flatpak-builder)

For EL7:

```
# yum install 'flatpak' 'flatpak-builder'
```

You may also wish to install the `xdg-desktop-portal*` packages:

```
# yum install 'xdg-desktop-portal*'
```

See also:

* [flatpak setup](https://flatpak.org/setup)

### Adding repository

```
$ flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

See also:

* [flathub setup](http://docs.flatpak.org/en/latest/using-flatpak.html#add-a-remote)

### Prepare

```
$ flatpak install flathub "org.freedesktop.Sdk//18.08"
```

```
$ flatpak install flathub "org.freedesktop.Platform//18.08"
```

```
$ git submodule init
```

```
$ git submodule update
```

### Build

```
$ mkdir -p "build" && flatpak-builder "build" "org.widelands.widelands.yaml" --force-clean --install-deps-from="flathub"
```

### Test

```
$ flatpak-builder --run "build" "org.widelands.widelands.yaml" "sh"
```

### Test run

```
$ flatpak-builder --run "build" "org.widelands.widelands.yaml" "widelands"
```

### Install

```
$ flatpak-builder --repo="repo" --force-clean "build" "org.widelands.widelands.yaml"
```

```
$ flatpak --user remote-add --no-gpg-verify "widelands" "repo"
```

```
$ flatpak --user install "widelands" "org.widelands.widelands"
```

### Run

```
$ flatpak run "org.widelands.widelands"
```

### Uninstall

```
$ flatpak --user uninstall "org.widelands.widelands"
```

```
$ flatpak --user remote-delete "widelands"
```

See also: [Building your first Flatpak](http://docs.flatpak.org/en/latest/first-build.html)

## FAQ

### Does the game have access to the host file system?

No, it is completely sandboxed.

### Does flatpak-ed Widelands run as superuser?

[No](https://github.com/flatpak/flatpak/issues/1557). It is a [MATE](https://github.com/mate-desktop)/[marco](https://github.com/mate-desktop/marco) [issue](https://github.com/mate-desktop/marco/issues/301).

### Why not use an RPM package?

I already provided [COPR repo](https://copr.fedorainfracloud.org/coprs/scx/widelands) with (S)RPM packages for EL and Fedora.

### Are you the author of Widelands?

No, I only created the flatpak package for it.

See also:

* [Widelands Development Team](https://wl.widelands.org/developers)

