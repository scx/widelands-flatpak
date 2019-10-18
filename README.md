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
$ flatpak remote-add --if-not-exists "flathub" "https://dl.flathub.org/repo/flathub.flatpakrepo"
```

See also:

* [flathub setup](http://docs.flatpak.org/en/latest/using-flatpak.html#add-a-remote)

### Prepare

```
$ flatpak install "flathub" "org.freedesktop.Sdk//19.08"
```

```
$ flatpak install "flathub" "org.freedesktop.Platform//19.08"
```

Clone this repository, then checkout the right branch.

```
$ git submodule init
```

```
$ git submodule update
```

### Build

```
$ flatpak-builder "build" "org.widelands.Widelands.yaml" --force-clean --install-deps-from="flathub"
```

### Test

```
$ flatpak-builder --run "build" "org.widelands.Widelands.yaml" "sh"
```

### Test run

```
$ flatpak-builder --run "build" "org.widelands.Widelands.yaml" "widelands"
```

### Create repo

```
$ flatpak-builder --repo="repo" --force-clean "build" "org.widelands.Widelands.yaml"
```

### Install

```
$ flatpak --user remote-add --no-gpg-verify "widelands" "repo"
```

```
$ flatpak --user install "widelands" "org.widelands.Widelands"
```

### Run

```
$ flatpak run "org.widelands.Widelands"
```

### Uninstall

```
$ flatpak --user uninstall "org.widelands.Widelands"
```

```
$ flatpak --user remote-delete "widelands"
```

### Build single-file bundle

```
$ flatpak build-bundle "repo" "widelands.flatpak" "org.widelands.Widelands" --runtime-repo="https://flathub.org/repo/flathub.flatpakrepo"
```

### Install single-file bundle

If you have already [installed](#install) the package, you have to [uninstall](#uninstall) it before continuing.

```
$ flatpak --user install "widelands.flatpak"
```

See also:
* [Building your first Flatpak](http://docs.flatpak.org/en/latest/first-build.html)
* [Single-file bundles](http://docs.flatpak.org/en/latest/single-file-bundles.html#single-file-bundles)

## FAQ

### Does the game have access to the host file system?

No, it is completely sandboxed.

### Does flatpak-ed Widelands run as superuser?

[No](https://github.com/flatpak/flatpak/issues/1557). It is a [MATE](https://github.com/mate-desktop)/[marco](https://github.com/mate-desktop/marco) [issue](https://github.com/mate-desktop/marco/issues/301).

### Why not a RPM package?

I already provided [COPR repo](https://copr.fedorainfracloud.org/coprs/scx/widelands) with (S)RPM packages for EL and Fedora.

### Are you the author of Widelands?

No, I only created the flatpak package for it.

See also:

* [Widelands Development Team](https://wl.widelands.org/developers)

