# Data used in the paper "Faster GPU-based convolutional gridding via thread coarsening"

This repository contains no code. It contains just the data used to generate
the results in the [paper](http://arxiv.org/abs/1605.07023). The data consists
of UVW coordinates, pre-quantised to a grid and a subgrid.

## Data format

The data are stored in an HDF5 file, containing a single dataset called `vis`,
with shape 1 × 9 × 825378. The first dimension can be ignored. The second
dimension is the W slice for W-stacking. The third dimension contains UVW
coordinates for a single W slice. Since not all W slices have the same number
of visibilities, the dataset contains an attribute called `length` which
contains the number of visibilities in each slice. Note that the last two W
slices contain zero visibilities.

The data type in the dataset is a compound type with the following fields:
- `uv`: integer grid coordinates.
- `sub_uv`: integer subgrid coordinates. The subgrid is an 8×8 oversampling,
  so `uv + sub_uv / 8` will give the higher-resolution coordinates.
- `weights`: a floating-point weight (a single-element array)
- `vis`: a complex visibility (a single-element array).
- `w_plane`: w coordinate, quantised to a W plane.

## Parameters

The file does not encode enough information to actually produce a useful
astronomical image, since it lacks all information about the grid sampling
rate, frequency, pointing, w planes etc. It is intended purely for
apples-to-apples benchmarking of gridding algorithms.

For completeness, here are the parameters used in the simulation:
- Phase centre: RA 0, Declination -45°
- Start time: Sat Jan  1 12:00:00 UTC 2000
- Integration time: 2 seconds
- Duration: 7200 seconds
- Frequency: 1.412 GHz
- UV cell size: 5.568m
- Pixel size: 1.707 arcsec
- Image size: 4608 × 4608
- W planes per W slice: 1229

The weights and visibilities are all set to 1, so an image will contain a point
source at the phase centre.

## Licence

This data may be used under the [Creative Commons
CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) licence.
