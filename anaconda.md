# Anaconda Hints and Techniques

## Contents

- [Installation of Miniconda](#installation-of-miniconda)
- [Useful Commands](#useful-commands)

---

Silent installation of Miniconda for Linux and OS X is a simple as specifying the -b and -p arguments of the bash installer. The following arguments are supported:

- -b, batch mode
- -p, installation prefix/path
- -f, force installation even if prefix -p already exists

Batch mode assumes that you agree to the license agreement, and it does not edit the .bashrc or .bash_profile files.

A complete example:

```console
$wget http://repo.continuum.io/miniconda/Miniconda3-3.7.0-Linux-x86_64.sh -O ~/miniconda.sh
$bash ~/miniconda.sh -b -p $HOME/miniconda
$export PATH="$HOME/miniconda/bin:$PATH"
```

# Useful Commands

Check conda is installed and in your `PATH`

```console
$conda -V
```

Check conda is up to date

```console
$conda update conda
$conda search "^python$"
```

Create a virtual environment for the project

```console
$conda create -n yourenvname python=x.x anaconda
```

Activate your environment

```console
$source activate yourenvname
```

Install additional Python packages to a virtual environment.

```console
$conda install -n yourenvname [package]
$source deactivate
$conda remove -n yourenvname -all
```