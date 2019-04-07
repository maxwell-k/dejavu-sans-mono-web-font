# "dejavu-sans-mono-web-font"

Based on https://github.com/dejavu-fonts/dejavu-fonts, focussing on four font
faces:

- "DejaVu Sans Mono"
- "DejaVu Sans Mono Bold"
- "DejaVu Sans Mono Bold Oblique"
- "DejaVu Sans Mono Oblique"

For license information, see [`LICENSE`](./LICENSE).

As of 7 April 2019, the [latest release] is 2.37

To download ".ttf" files and create ".woff" files, run the following steps on
Alpine Linux:

```
releases=https://github.com/dejavu-fonts/dejavu-fonts/releases
curl -OL "$releases/download/version_2_37/dejavu-fonts-ttf-2.37.tar.bz2"
unset releases
tar xvf dejavu-fonts-ttf-2.37.tar.bz2
cp dejavu-fonts-ttf-2.37/ttf/DejaVuSansMono*.ttf .
git clean -f -d

sudo apk add fontforge@edge-testing
for i in *.ttf ; do ./convert.pe "$i" ; done
sudo apk del fontforge
```

[latest release]: https://github.com/dejavu-fonts/dejavu-fonts/releases