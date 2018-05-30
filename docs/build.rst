Building kitty from source
==============================

|kitty| is designed to run from source, for easy hackability. Make sure
the following dependencies are installed first.

Dependencies
----------------

* python >= 3.5
* harfbuzz >= 1.5.0
* zlib
* libpng
* freetype (not needed on macOS)
* fontconfig (not needed on macOS)
* ImageMagick (optional, needed to use the ``kitty icat`` tool to display images in the terminal)
* pygments (optional, need for syntax highlighting in ``kitty +kitten diff``)
* gcc or clang (required only for building)
* pkg-config (required only for building)
* For building on Linux in addition to the above dependencies you might also need to install the ``-dev`` packages for ``xcursor``, ``xrandr``, ``libxi``, ``xinerama``, ``libgl1-mesa`` and ``xkbcommon-x11``, if they are not already installed by your distro.

Install and run from source
------------------------------

.. code-block:: sh

    git clone https://github.com/kovidgoyal/kitty && cd kitty

Now build the native code parts of |kitty| with the following command::

    make

You can run |kitty|, as::

    python3 .

If that works, you can create a script to launch |kitty|:

.. code-block:: sh

    #!/usr/bin/env python3
    import runpy
    runpy.run_path('/path/to/kitty/dir', run_name='__main__')

And place it in :file:`~/bin` or :file:`/usr/bin` so that you can run |kitty| using
just ``kitty``.

Note for Linux/macOS packagers
----------------------------------

While kitty does use python, it is not a traditional python package, so please
do not install it in site-packages.
Instead run::

    python3 setup.py linux-package

This will install kitty into the directory :file:`linux-package`. You can run kitty
with :file:`linux-package/bin/kitty`.  All the files needed to run kitty will be in
:file:`linux-package/lib/kitty`. The terminfo file will be installed into
:file:`linux-package/share/terminfo`. Simply copy these files into :file:`/usr` to install
kitty. In other words, :file:`linux-package` is the staging area into which kitty is
installed. You can choose a different staging area, by passing the ``--prefix``
argument to :file:`setup.py`.

You should probably split kitty into two packages, :file:`kitty-terminfo` that
installs the terminfo file and :file:`kitty` that installs the main program.
This allows users to install the terminfo file on servers into which they ssh,
without needing to install all of kitty.

You also need :file:`tic` to compile the terminfo files, it is usually found in
the development package of :file:`ncurses`.

This applies to creating packages for kitty for macOS package managers such as
brew or MacPorts as well.