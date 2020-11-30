GetSimpleTuple_sim
======================

# Requirements

* **ROOT** (version 6.14 onwards)

* **ClasTool**

# Compilation

To compile, just execute `make` in the current directory. The binary file (or execution file) will be located in directory `bin/`

# Execution

A ClasTool-formatted root file must be located in the same directory as the binary file. Usage is:

* To print usage and exit program:

  ```
  ./GetSimpleTuple_sim -h
  ```

* To select the file to read: (filename scheme must be: `recsis<target>_<run number>.root`)

  ```
  ./GetSimpleTuple_sim -t[target] -r[run number]
  ``` 

  For example, to read a file called `recsisD_00.root`, one should execute:

  ```
  ./GetSimpleTuple_sim -tD -r00
  ``` 

# Structure of the program

* `src/GetSimpleTuple_sim.cxx`

  This is the **source** code. It iterates on the events of the input file. From each event, it will (1) read the **GSIM** bank, (2) identify the generated particles, (3) read the **EVNT** bank, (4) identify the reconstructed particles. To store each particle, it will save the iteration number (from the **GSIM** and **EVNT** iterations) into a `RVec<Int_t>` object for each kind of particle, this will allows us to do a further management of the particles. Such as sorting them by kind of particle, by momentum and by **angular matching**.

* `include/GetSimpleTuple_sim.hxx`

  This library is in charge of all the **input-output operations** of the `TTree` objects, as well as the **vector operations** for each `RVec<Int_t>` object, such as `SortByMomentum()` and `AngularMatching()`.

* `include/GSTtree.h`

  This library contains the definition of the **data structures** that will store the input and output variables.

* `include/TIdentificatorV2.h`

  This is the historical program **Analyser** condensed into a single-file standalone library.
