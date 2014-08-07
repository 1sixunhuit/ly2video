# ly2video

ly2video is a Python script which converts music represented by a [GNU
LilyPond](http://lilypond.org) file into a video containing a
horizontally scrolling music staff which is synchronized with a
MIDI-generated audio rendering of the music.

## Examples

Here are some [examples of videos generated by ly2video](http://www.youtube.com/playlist?list=PLfRwjd606WZlxRU_kaUPagX3-Uv-SYRMH).

## Requirements

**Please also read the Installation section below before you start installing anything!**

*   GNU LilyPond >= 2.15.41
    (needs [`one-line-breaking`](http://www.lilypond.org/doc/v2.17/Documentation/notation/one_002dline-page-breaking) support)
*   FFmpeg (if you are on Ubuntu or Debian, see first see
    [issue 32](https://github.com/aspiers/ly2video/issues/32))
*   TiMidity++
*   Python 2.7
*   Python's [pip installer](http://www.pip-installer.org)
*   [swig](http://www.swig.org/) and ALSA development libraries
    (`python-midi` requires these in order to build its sequencer
    code successfully, although ly2video doesn't use that code)

## Installation

### Installing dependencies on openSUSE 12.2

Install the `ffmpeg` package from Packman via [1-click
install](http://packman.links2linux.org/install/ffmpeg) (you can also
find the button on [this
page](http://packman.links2linux.org/package/ffmpeg)), or via [YaST
and/or
zypper](http://wiki.links2linux.de/packman:faq_en#software_installation_updates_deinstallation).

You can ensure the remaining dependencies are installed via something
like:

    sudo zypper install lilypond timidity python-pip python-imaging alsa-devel

### Installing dependencies on Debian- and Ubuntu-based Linux distributions

There is currently a known issue on these distributions, since [Debian
and Ubuntu switched from `ffmpeg` to the `libav
fork`](https://github.com/aspiers/ly2video/issues/32).  See [issue #32](https://github.com/aspiers/ly2video/issues/32) for a suggested
workaround.

Additionally, Debian and Ubuntu both currently ship very old versions
of LilyPond, so you might need to install a newer one via the
"Generic Packages" section near the top of: http://lilypond.org/unix.html

You can ensure the remaining dependencies are installed via something
like:

    sudo apt-get install timidity python-pip python-imaging swig libasound-dev

### Installing dependencies on Arch-based Linux distributions

Download the source tarball from [the Arch User Repository](https://aur.archlinux.org/packages/ly2video/), extract it, and run

    makepkg -si

in the directory you extracted to in order to pull all the dependencies (python and otherwise)
from the main repos and then install ly2video. The other dependencies
from the AUR will have to be installed manually; however, they will all be listed
if you run `makepkg` in the same directory.

If you have an AUR helper such as [yaourt](https://wiki.archlinux.org/index.php/Yaourt) installed, this entire process can be shortened to one step:

    yaourt -S ly2video

where yaourt would be replaced by the name of your AUR helper if you have a different helper installed.

Regardless, after installing the package, you can use the script by running `ly2video.py` with the required arguments.

### Installing dependencies on other platforms

If you have figured out how to install the dependencies and get
ly2video working on another platform, please [file a new
issue](https://github.com/aspiers/ly2video/issues) containing the
information, so that this README can be updated.  Thanks!

### Installing required Python module dependencies

[ly2video requires some specific Python modules](https://github.com/aspiers/ly2video/blob/master/pip-requires.txt) - **do NOT install these manually!** (unless you are a Python expert.)
They can be installed system-wide via:

    sudo pip install -r pip-requires.txt

or for the current user via:

    pip install --user -r pip-requires.txt

You can optionally protect against the risk of installation of these
Python modules destabilising any other Python applications you may
use, by isolating them in a virtual environment using
[`virtualenv`](http://www.virtualenv.org/en/latest/).  The most
convenient way to do this is via
[`virtualenvwrapper`](http://virtualenvwrapper.readthedocs.org/en/latest/).
Once you have `virtualenvwrapper` installed, it's as simple as:

    mkvirtualenv ly2video
    pip install -r pip-requires.txt

### Installing ly2video itself

Just run

    python2 setup.py install --root=INSTALLATION_DIR
    
from the main directory to install it to some directory INSTALLATION_DIR. Running
`python2 setup.py build` first will build it separately from the install step, if desired.

## Usage

Run `./ly2video.py --help` to display usage information.

You must ensure that your `.ly` input file contains both `\layout { }`
and `\midi` commands, which ensure that valid `.midi` and `.png` files
are generated when it is run through `lilypond --png`.

## Support, bugs, development etc.

Please check the [issue tracker](https://github.com/aspiers/ly2video/issues)
for known issues, and if yours is not there, please submit it.
I can't guarantee that I'll be able to fix it, or even respond,
but I'll try, and even if I can't help, this is github, so anyone else
can potentially help you out too.

If you know how to fix a problem or contribute an enhancement, you are
extremely welcome to [fork this repository](https://github.com/aspiers/ly2video/fork),
commit your fix, and then send a [pull request](https://help.github.com/articles/using-pull-requests)!

## Acknowledgements

Huge credits for the initial implementation go to Jiří "FireTight"
Szabó, who wrote it as part of his Bachelor's degree.  If you are
lucky enough to understand Czech, you can read his thesis on ly2video
in the `doc/thesis/` subdirectory, or
[online](http://is.muni.cz/th/359741/fi_b/text_prace.pdf) :-) Work on
an English translation has begun and is being tracked in
[issue 15](https://github.com/aspiers/ly2video/issues/15) but is
unlikely to be finished any time soon unless someone else volunteers
to help out.

Very big thanks also to Jan Nieuwenhuizen not only for co-inventing
LilyPond in the first place, but also for helping me implement the
complete revamp of the synchronization algorithm, which should be
much more robust than the previous one.

And finally of course, much gratitude to the many great people who
have contributed to LilyPond over the years.  This would not have
been possible without you.

## License

ly2video is released under the [GNU GPL v3](http://www.gnu.org/licenses/gpl.html).


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/aspiers/ly2video/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

