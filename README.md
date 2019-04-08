# dejavu-sans-mono-web-font

This repository provides web fonts that can restore the old appearance of Secure
Shell on Chrome OS. To use these set the 'Custom CSS (URI)' in Secure Shell App
Profile Settings ('Ctrl-Shift-P') to
<https://cdn.jsdelivr.net/gh/maxwell-k/dejavu-sans-mono-web-font@2.37/index.css>

As at 7 April 2019, the [latest release] is 2.37.

For license information, see [`LICENSE`](./LICENSE).

## Contents

This repository is based on <https://github.com/dejavu-fonts/dejavu-fonts>. It
focuses on four
[font faces](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face):

- DejaVu Sans Mono
- DejaVu Sans Mono Bold
- DejaVu Sans Mono Bold Oblique
- DejaVu Sans Mono Oblique

To download the '.ttf' files and create the '.woff' files, run the following
shell script on Alpine Linux in a checkout of this repository:

```
releases=https://github.com/dejavu-fonts/dejavu-fonts/releases &&
curl -OL "$releases/download/version_2_37/dejavu-fonts-ttf-2.37.tar.bz2" &&
unset releases &&
tar xf dejavu-fonts-ttf-2.37.tar.bz2 &&
cp dejavu-fonts-ttf-2.37/ttf/DejaVuSansMono*.ttf . &&

sudo apk add --quiet fontforge@edge-testing &&
for i in *.ttf ; do ./convert.pe "$i" ; done &&
sudo apk del fontforge &&

git clean -f -d
```

## Background and goal

The default font shown in Secure Shell under Chrome OS before version 73 was
[DejaVu Sans Mono](https://dejavu-fonts.github.io/). The Google system fonts now
don't include DejaVu, but instead use
[Noto](https://www.google.com/get/noto/#mono-mono)

> The DejaVu fonts are a font family based on the
> [Vera Fonts](http://gnome.org/fonts/). Its purpose is to provide a wider range
> of characters while maintaining the original look and feel through the process
> of collaborative development (see
> [authors](https://dejavu-fonts.github.io/Authors.html)), under a
> [Free license](https://dejavu-fonts.github.io/License.html).

-- <https://dejavu-fonts.github.io/>

The
["hterm" FAQ](https://chromium.googlesource.com/apps/libapps/+/master/nassh/doc/FAQ.md#how-do-i-use-web-fonts)
includes an example using <https://github.com/wernight/powerline-web-fonts/>
which is loosely based upon <https://github.com/powerline/fonts>, which in turn
includes a modified version of DejaVu. This repository is simpler in its goal,
to provide the latest version of upstream DejaVu Sans Mono as a web font.

[latest release]: https://github.com/dejavu-fonts/dejavu-fonts/releases
