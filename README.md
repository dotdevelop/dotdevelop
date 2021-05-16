**PLEASE NOTE!**

This is an effort to get MonoDevelop open sourced again.

**DotDevelop** will hopefully be a full-featured integrated development environment (IDE) for .NET using GTK.

**Current Status**

This fork is based on the last commit on 29 Jan 2020 (https://github.com/mono/monodevelop/commit/96b42aa0741af179a8e501f426b6ff5451c27264).

It was refactored to compile / run again on Linux. Other platforms will follow.

**Contributors**

To hack around, use a Ubuntu 20.04 machine and follow the steps below,

1. Acquire all dependencies,

```
sudo apt install intltool fsharp gtk-sharp2
```

2. Check out the code and compile,

```
git clone -b main https://github.com/dotdevelop/dotdevelop.git

cd dotdevelop/

./configure --profile=gnome

make

```

> Take a look at [the CI manifest](https://github.com/dotdevelop/dotdevelop/blob/main/.github/workflows/monodevelop.yml) in case the latest steps differ from above.
>
> Other Linux distributions/versions require different ways to acquire dependencies. Open [a new issue
](https://github.com/dotdevelop/dotdevelop/issues) and point out which Linux distribution/version you use, so others might help.

# (outdated) ReadMe from MonoDevelop:

Directory organization
----------------------

There are two main directories:

 * `main`: The core MonoDevelop assemblies and add-ins (all in a single
    tarball/package).
 * `extras`: Additional add-ins (each add-in has its own
    tarball/package).

Compiling
---------

If you are building from Git, make sure that you initialize the submodules
that are part of this repository by executing:
`git submodule update --init --recursive`

If you are running a parallel mono installation, make sure to run all the following steps
while having sourced your mono installation script. (source path/to/my-environment-script)
See: http://www.mono-project.com/Parallel_Mono_Environments

To compile execute:
`./configure ; make`

There are two variables you can set when running `configure`:

* The install prefix: `--prefix=/path/to/prefix`

  * To install with the rest of the assemblies, use:
  `--prefix="pkg-config --variable=prefix mono"`

* The build profile: `--profile=profile-name`

  * `stable`: builds the MonoDevelop core and some stable extra add-ins.
  * `core`: builds the MonoDevelop core only.
  * `all`: builds everything
  * `mac`: builds for Mac OS X

**PS:** You can also create your own profile by adding a file to the profiles directory containing a list of the directories to build.

Disclaimer: Please be aware that the 'extras/JavaBinding' and 'extras/ValaBinding' packages do not currently work. When prompted or by manually selecting them during the './configure --select' step, make sure they stay deselected. (deselected by default)

Running
-------

You can run MonoDevelop from the build directory by executing:
`make run`

Debugging
---------

You can debug MonoDevelop using Visual Studio (on Windows or macOS) with the
`main/Main.sln` solution. Use the `DebugWin32` configuration on Windows and the
`DebugMac` configuration on macOS.

Installing *(Optional)*
----------

You can install MonoDevelop by running:
`make install`

Bear in mind that if you are installing under a custom prefix, you may need to modify your `/etc/ld.so.conf` or `LD_LIBRARY_PATH` to ensure that any required native libraries are found correctly.

*(It's possible that you need to install for your locale to be
correctly set.)*

Packaging for OS X
-----------------

To package MonoDevelop for OS X in a convenient MonoDevelop.app
file, just do this after MonoDevelop has finished building (with
`make`): `cd main/build/MacOSX ; make app`.
You can run MonoDevelop: `open MonoDevelop.app` or build dmg package: `./make-dmg-bundle.sh`

Dependencies
------------

- [Windows](https://github.com/mono/md-website/blob/gh-pages/developers/building-monodevelop.md#prerequisites-and-source)
- [Unix](http://www.monodevelop.com/developers/building-monodevelop/#linux)

Special Environment Variables
-----------------------------

**BUILD_REVISION**

	If this environment variable exists we assume we are compiling inside wrench.
	We use this to enable raygun only for 'release' builds and not for normal
	developer builds compiled on a dev machine with 'make && make run'.


Known Problems
-----------------------------

```
"The type `GLib.IIcon' is defined in an assembly that is not referenced"
```

This happens when you accidentally installed gtk-sharp3 instead of the 2.12.x branch version.
Make sure to 'make uninstall' or otherwise remove the gtk-sharp3 version and install the older one.

xbuild may still cache a reference to assemblies that you may have accidentally installed into your mono installation,
like the gtk-sharp3 as described before. You can delete the cache in $HOME/.config/xbuild/pkgconfig-cache-2.xml



References
----------

**[MonoDevelop website](http://www.monodevelop.com)**

**[Gnome Human Interface Guidelines (HIG)](https://developer.gnome.org/hig/stable/)**

**[freedesktop.org standards](http://freedesktop.org/Standards/)**

Discussion, Bugs, Patches
-------------------------

https://github.com/dotdevelop/dotdevelop/issues/new *(submit bugs and patches here)*

