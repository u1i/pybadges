# pybadges

pybadges is a Python library and command line tools that allows you to create
Git-hub styles badges as SVG images. For example:

![pip installation](tests/golden-images/pip.svg)
![pip installation](tests/golden-images/license.svg)
![pip installation](tests/golden-images/build-passing.svg)

The aesthetics of the generated badges matches the  visual design of Shields badges
[specification](https://github.com/badges/shields/blob/master/spec/SPECIFICATION.md).

The implementation of the library was heavily influenced by
[Shields.io](https://github.com/badges/shields) and the JavaScript
[gh-badges](https://github.com/badges/shields#using-the-badge-library) library.

## Getting Started

These instructions will get you a copy of the project up and running on your
local machine for development and testing purposes. See deployment for notes on
how to deploy the project on a live system.

### Installing

pybadges can be installed using [pip](https://pypi.org/project/pip/):

```sh
pip install pybadges
```

To test that installation was successful, try:
```sh
python -m pybadges --left-text=build --right-text=failure --right-color=#c00 --browser
```

You will see a badge like this in your browser or other image viewer:

![pip installation](tests/golden-images/build-failure.svg)

## Usage

pybadges can be used both from the command line and as a Python library.

The command line interface is a great way to experiment with the API before
writing Python code.

### Command line usage

Complete documentation of pybadges command arguments can be found using the help
argument:

```sh
python -m pybadges --help
```

But the following usage demonstrates every interesting option:
```sh
python -m pybadges \
    --left-text=complete \
    --right-text=example \
    --left-color=green \
    --right-color=#fb3 \
    --left-link=http://www.complete.com/ \
    --right-link=http://www.example.com \
    --logo='data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAIAAAACCAIAAAD91JpzAAAAD0lEQVQI12P4zwAD/xkYAA/+Af8iHnLUAAAAAElFTkSuQmCC' \
    --browser
```

![pip installation](tests/golden-images/complete.svg)

Note that the `--logo` option can include a regular URL:

```sh
python -m pybadges \
    --left-text="python" \
    --right-text="3.2, 3.3, 3.4, 3.5, 3.6" \
    --whole-link="https://www.python.org/" \
    --browser \
    --logo='https://dev.w3.org/SVG/tools/svgweb/samples/svg-files/python.svg'
```

![pip installation](tests/golden-images/python.svg)

### Library usage

pybadges is primarily meant to be used as a Python library.

```python
from pybadges import badge
s = badge(left_text='coverage', right_text='23%', right_color='red')
# s is a string that contains the badge data as an svg image.
print(s[:40]) # => <svg height="20" width="191.0" xmlns="ht
```

The keyword arguments to `badge()` are identical to the command flags names
described above except with keyword arguments using underscore instead of
hyphen/minus (e.g. `--left-width` => `left_width=`)

### Caveats

 - pybadges uses a pre-calculated table of text widths and
   [kerning](https://en.wikipedia.org/wiki/Kerning) distances
   (for western glyphs) to determine the size of the badge.
   So Eastern European languages may be rendered less well than
   Western European ones:

   ![pip installation](tests/golden-images/saying-russian.svg)

   and glyphs not present in Deja Vu Sans (the default font) may
   be rendered very poorly:

    ![pip installation](tests/golden-images/saying-chinese.svg)

 - pybadges does not have any explicit support for languages that
   are written right-to-left (e.g. Arabic, Hebrew) and the displayed
   text direction may be incorrect:

    ![pip installation](tests/golden-images/saying-arabic.svg)

## Development

```sh
git clone TODO
cd TODO
python -m virtualenv py
source py/bin/activate
# Installs in edit mode and with development dependencies.
pip install -e .[dev]
nox
```

If you'd like to contribute your changes back to pybadges, please read the
[contributer guide.](CONTRIBUTING.md)

## Versioning

We use [SemVer](http://semver.org/) for versioning.

## License

This project is licensed under the Apache License - see the [LICENSE](LICENSE) file for details

This is not an officially supported Google product.