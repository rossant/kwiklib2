kwiklib2
========

This is a rewrite of the Python library providing I/O access to files in the kwik format and in the previous Buzsaki format. Compared to the previous kwiklib implementation, this new version should provide:

* Python 3 support with `six`
* An implementation based exclusively on h5py instead of PyTables
* A saner API and implementation


## Interfaces

There will be two interfaces for data access.

### High-level API

High-level API with user-friendly functions for common use-cases: accessing spike times and spike clusters for a given shank, get the features and the waveforms, etc.

### Low-level API

A very simple API that basically provides a single function to access any part of the HDF5 file, given the full HDF5 path.

### Data conversion

There will also be simple facilities to convert from/to the old Buzsaki format.

### Mock datasets

Early on, we should create a complete suite of utilities to generate random data (but not "stupid" random: waveforms should look like waveforms, etc.). The random data could be generated in memory or in files (Buzsaki or Kwik format). This will be crucial for unit testing.


## API Specification

The very first thing to do is to work out the complete specification of the APIs: list of classes, methods, and functions with their docstrings and code examples.

We could start writing unit tests and code examples before working on the implementation ([test-driven development](http://en.wikipedia.org/wiki/Test-driven_development)).


## Best practices

* **Pure Python** (no Cython, no C, etc.)
* Dependencies: NumPy and h5py only
* Unit testing framework with `nose`
* Test coverage with `coverage`
* Python 2.7/3.3+ support with `six`
* Continuous integration with Travis CI, that runs unit tests, code coverage, on both Python 2 and Python 3
* Contributions by pull requests exclusively as early as possible
* Local development on Python 3 (Anaconda 64-bit for Python 3)

Anaconda is the only Python distribution we'll officially support (much simpler in terms of maintenance/support). This distribution is free and works on all operating systems.


## Misc notes

* We'll need a special data structure that derives from ndarray, with special index labels (absolute/relative indexing)
* We should also think about a good data structure for time-dependent data (continuous signals, spike times, event, epochs, etc.). See [Neo](http://neuralensemble.org/neo/) for some inspiration.
* Decide early on common conventions, data structures, ontology for the objects (like in sklearn and skimage).
	* Data type/units for spike times: int64 exclusively, in samples, for perfect precision. 
	* No floating point data type for spike times, and convert at the last moment only.
	* Data structure for a single spike train: int64 (N,)
	* Data structure for spike trains: int64 (N, 2) (spike time, cluster index)
* Use native data structs as much as possible (see native `collections` module for example)
* Prefer pure functions over classes as much as possible
