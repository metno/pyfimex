# Python bindings for fimex
- see [fimex](http://github.com/metno/fimex/)
- a python module `pyfimex0` has been part of the fimex source code for a while,
  this package supersedes that package
- installation requires local development files for fimex, a c++ compiler, cmake, ...

# Use of xarray backend
The xarray backend included here supports opening paths, like in

```python
ds = xarray.open_dataset("data.nc", engine="fimex")
```


In addition, it supports retrieving data from a `CDMReader` object, like in

```python
reader = pyfimex1.createFileReader("netcdf", "data.nc")
ds = xarray.open_dataset(reader, engine="fimex")
```

As the reader may be any `pyfimex1.CDMReader` this allows using the interpolation,
vertical interpolation, extraction, merge, and other functions from fimex / pyfimex
as input to xarray instead of directly using a file.

See the tests for some examples.


# Development
Install in a local venv with `pip install -e .`. Run `pytest`. The
tests require the `xarray` python package and NetCDF support in
fimex.

Build sdist package with `python3 -m build --sdist`. Do not build wheels as the package
depends on fimex, which is installed locally and not available on pypi.

When test installing from test.pypi.org, use `python3 -m pip install --index-url https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple/ pyfimex` to have the main pypi repo available for build dependencies.
