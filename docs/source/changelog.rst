Changelog
=========

.. vX.Y.0 / 2019-MM-DD
.. -------------------
..
.. New Features
.. ++++++++++++
..
.. Enhancements
.. ++++++++++++
..
.. Bug Fixes
.. +++++++++

v0.6.4 / 2019-03-21
-------------------

Bug Fixes
+++++++++

- (:pr:`54`) Psi4's Engine implementation now checks its key words in a case insensitive way to give the same value
  whether you called Psi4 or Engine to do the compute.
- (:pr:`55`) Fixed an error handling routine in Engine to match Psi4.
- (:pr:`56`) Complex inputs are now handled better through Psi4's wrapper which caused Engine to hang while trying
  to write to ``stdout``.


v0.6.3 / 2019-03-15
-------------------

New Features
++++++++++++

- (:pr:`28`) TeraChem is now a registered executor in Engine! Thanks to @ffangliu for implementing.
- (:pr:`46`) MP2D is now a registered executor in Engine! Thanks to @loriab for implementing.

Enhancements
++++++++++++

- (:pr:`46`) ``dftd3``'s workings received an overhaul. The ``mol`` keyword has been replaced with ``dtype=2``,
  full Psi4 support is now provided, and an MP2D interface has been added.

Bug Fixes
+++++++++

- (:pr:`50` and :pr:`51`) Executing Psi4 on a single node with multiprocessing is more stable because Psi4 temps are
  moved to scratch directories. This behavior is now better documented with an example as well.
- (:pr:`52`) Psi4 calls are now executed through the ``subprocess`` module to prevent possible multiprocessing issues
  and memory leak after thousands of runs. A trade off is this adds about 0.5 seconds to task start-up, but its safe.
  A future Psi4 release will correct this issue and the change can be reverted.


v0.6.2 / 2019-03-07
-------------------

Enhancements
++++++++++++

- (:pr:`38` and :pr:`39`) Documentation now pulls from the custom QC Archive Sphinx Theme, but can fall back to the standard
  RTD theme. This allows all docs across QCA to appear consistent with each other.
- (:pr:`43`) Added a base model for all ``Procedure`` objects to derive from. This allows
  procedures' interactions with compute programs to be more unified. This PR also ensured
  GeomeTRIC provides Provenance information. 

Bug Fixes
+++++++++
- (:pr:`40`) This PR improved numerous back-end and testing quality of life aspects.
  Fixed ``setup.py`` to call ``pytest`` instead of ``unittest`` when running tests on install.
  Some conda packages for Travis-CI are cached to reduce the download time of the larger computation codes.
  Psi4 is now pinned to the 1.3 version to fix build-level pin of libint.
  Conda-build recipe removed to avoid possible confusion for everyone who isn't a Conda-Forge
  recipe maintainer. Tests now rely exclusively on the ``conda env`` setups.


v0.6.1 / 2019-02-20
-------------------

Bug Fixes
+++++++++

- (:pr:`37`) Fixed an issue where RDKit methods were not case agnostic.

v0.6.0 / 2019-02-28
-------------------

Breaking Changes
++++++++++++++++

- (:pr:`36`) **breaking change** Model objects are returned by default rather than a dictionary.

New Features
++++++++++++

- (:pr:`18`) Add the ``dftd3`` program to available computers.
- (:pr:`29`) Adds preliminary support for the ``Molpro`` compute engine.
- (:pr:`31`) Moves all computation to ``ProgramExecutor`` to allow for a more flexible input generation, execution, output parsing interface.
- (:pr:`32`) Adds a general ``execute`` process which safely runs subprocess jobs.

Enhancements
++++++++++++

- (:pr:`33`) Moves the ``dftd3`` executor to the new ``ProgramExecutor`` interface.
- (:pr:`34`) Updates models to the more strict QCElemental v0.3.0 model classes.
- (:pr:`35`) Updates CI to avoid pulling CUDA libraries for ``torchani``.
- (:pr:`36`) First pass at documentation.


v0.5.2 / 2019-02-13
-------------------

Enhancements
++++++++++++

- (:pr:`24`) Improves load times dramatically by delaying imports and cpuutils.
- (:pr:`25`) Code base linting.
- (:pr:`30`) Ensures Psi4 output is already returned and Pydantic v0.20+ changes.

v0.5.1 / 2019-01-29
-------------------

Enhancements
++++++++++++

- (:pr:`22`) Compute results are now returned as a dict of Python Primals which have
  been serialized-deserialized through Pydantic instead of returning un-processed Python objects
  or json-compatible string.

v0.5.0 / 2019-01-28
-------------------

New Features
++++++++++++

- (:pr:`8`) Adds the TorchANI program for ANI-1 like energies and potentials.
- (:pr:`16`) Adds QCElemental models based off QCSchema to QCEngine for both validation and object-based manipulation of input and output data.

Enhancements
++++++++++++

- (:pr:`14`) Migrates option to Pydantic objects for validation and creation.
- (:pr:`14`) Introduces NodeDescriptor (for individual node description) and JobConfig (individual job configuration) objects.
- (:pr:`17`) NodeDescriptor overhauled to work better with Parsl/Balsam/Dask/etc.
