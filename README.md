# youtube-dl-flatpak
Command line flatpak that gives the user access to the youtube-dl tool. This is likely solely of use to people who use Linux computers with minimal read only root filesystems and run all applications inside flatpak containers, such as users of [Endless OS](https://endlessos.com/).

Instructions:
-------------

(1) Install the flatpak repository for GNOME:
```
flatpak remote-add --from gnome https://sdk.gnome.org/gnome.flatpakrepo

```
(2) Install the required runtimes
```
  flatpak install gnome org.freedesktop.Sdk
```
(3) Build the app from this directory:
```
flatpak-builder --force-clean --ccache --require-changes --repo=repo app org.youtubedl.YouTubeDl.json
```
(4) Add a remote to your local repo and install it:
```
flatpak --user remote-add --no-gpg-verify youtube-dl-repo /path/to/your/flatpak/repo
flatpak --user install youtube-dl-repo org.youtubedl.YouTubeDl
```
(5) Run the DevApp:
```
flatpak run org.youtubedl.YouTubeDl
```

Note that if you do further changes in the `appdir` (e.g. to the metadata), you'll need to re-publish it in your local repo and update before running it again:
```
flatpak build-export /path/to/your/flatpak/repo /path/to/flatpak/appdir
flatpak --user update org.youtubedl.YouTubeDl
```

Last, you can bundle it to a file with the `build-bundle` subcommand:
```
flatpak build-bundle /path/to/your/flatpak/repo org.youtubedl.YouTubeDl.flatpak org.youtubedl.YouTubeDl
```
