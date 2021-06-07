# g_ics
Simple IC generator for gadget/gizmo

Requires gfortran, shouldn't need any other libraries.

Builds a basic disc with a hole in the centre, with circular velocities to match some external potential (self-gravity may also be included, but it's not an exact solver).
Particle positions are _random_, so it will seed some instabilities. But as this is designed for gas-only ICs, pressure should even these things out.

Build with:

```
cd src
make
```

Run with

```
./disc_ICs prams/[PARMETER_FILE].param
```

See `prams/` for examples of parameter file options.

To create ICs based on a snapshot dump, you need to use gtools to produce a position-velocity-temperature file from a snapshot, from here: https://github.com/Astrokiwi/gtools
You can then do

```
from gtools import gizmo_tools
gizmo_tools.convert_pvfile("path/to/snapshot_xxx.hdf5","path/to/ic_pvfile.dat")
```

You can then set `pvfile` to "path/to/ic_pvfile.dat" in the .param file, as shown in one of the examples.
You must also set `N_in` to the number of gas particles in the snapshot, or it will not work. You may set `N` to a lower number, to only include the inner N particles, slicing out the outer particles.
