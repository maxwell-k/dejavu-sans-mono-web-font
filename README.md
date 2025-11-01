# dejavu-sans-mono-web-font

This repository is based on [dejavu-fonts]. On 31 October 2025 it uses the
[latest release], version 2.37. It focuses on the four [font faces] below. It
includes instructions for generating `.woff` and `.woff2` files.

1. DejaVu Sans Mono
2. DejaVu Sans Mono Bold
3. DejaVu Sans Mono Bold Oblique
4. DejaVu Sans Mono Oblique

[font faces]: https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face
[dejavu-fonts]: https://github.com/dejavu-fonts/dejavu-fonts
[latest release]: https://github.com/dejavu-fonts/dejavu-fonts/releases

## Creating the web fonts

_A process to download the '.ttf' files and create the '.woff' and '.woff2'
files, using Alpine Linux._

<details>

<summary>Steps to setup a container environment using Incus</summary>

Command to launch a suitable Alpine Linux container:

    incus launch images:alpine/3.22 c1

Commands to copy the `convert.pe` script into the container and start an
interactive shell:

    incus file push convert.pe c1/root/convert.pe \
    && incus exec c1 -- sh

</details>

The below commands:

1. Install FontForge
2. Download the font archive
3. Extract the files and
4. Run [`convert.pe`](/convert.pe) on each file

Commands:

    apk add wcurl fontforge \
    && wcurl https://github.com/dejavu-fonts/dejavu-fonts/releases/download/version_2_37/dejavu-fonts-ttf-2.37.tar.bz2 \
    && tar x -f dejavu-fonts-ttf-2.37.tar.bz2 --strip-components 1 \
    && for i in ttf/DejaVuSansMono*.ttf ; do ./convert.pe "$i" || break ; done

The output files should then be in the `ttf/` subdirectory.

<details>

<summary>Steps to retrieve the files and clean up the container environment</summary>

Command to download the files from the container:

    for j in -Bold -BoldOblique -Oblique "" ; do \
        for i in woff woff2 ; do \
            incus file pull "c1/root/ttf/DejaVuSansMono$j.$i" . ; \
        done ; \
    done

Command to stop and delete the container:

    incus stop c1 \
    && incus delete c1

</details>

## Secure Shell

This repository provides web fonts that can restore the old appearance of Secure
Shell on Chrome OS. To use these set the 'Custom CSS (URI)' in Secure Shell App
Profile Settings ('Ctrl-Shift-P') to
<https://cdn.jsdelivr.net/gh/maxwell-k/dejavu-sans-mono-web-font@2.37/index.css>

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

—<https://dejavu-fonts.github.io/>

The
["hterm" FAQ](https://chromium.googlesource.com/apps/libapps/+/master/nassh/doc/FAQ.md#how-do-i-use-web-fonts)
includes an example using <https://github.com/wernight/powerline-web-fonts/>
which is loosely based upon <https://github.com/powerline/fonts>, which in turn
includes a modified version of DejaVu. This repository is simpler in its goal,
to provide the latest version of upstream DejaVu Sans Mono as a web font.

---

For license information, see [`LICENSE`](./LICENSE).
