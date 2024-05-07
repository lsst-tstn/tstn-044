.. image:: https://img.shields.io/badge/tstn--044-lsst.io-brightgreen.svg
   :target: https://tstn-044.lsst.io
.. image:: https://github.com/lsst-tstn/tstn-044/workflows/CI/badge.svg
   :target: https://github.com/lsst-tstn/tstn-044/actions/

###################
Night Planning Tool
###################

TSTN-044
========

This technote describes the design of an integrated night planning tool. This is a tools that allows our team to collect a group of Jira tickets that describes a set of tests, allows us to organize these into a coherent list of tests to execute, that can later be loaded and executed at the summit.

**Links:**

- Publication URL: https://tstn-044.lsst.io
- Alternative editions: https://tstn-044.lsst.io/v
- GitHub repository: https://github.com/lsst-tstn/tstn-044
- Build system: https://github.com/lsst-tstn/tstn-044/actions/


Build this technical note
=========================

You can clone this repository and build the technote locally if your system has Python 3.11 or later:

.. code-block:: bash

   git clone https://github.com/lsst-tstn/tstn-044
   cd tstn-044
   make init
   make html

Repeat the ``make html`` command to rebuild the technote after making changes.
If you need to delete any intermediate files for a clean build, run ``make clean``.

The built technote is located at ``_build/html/index.html``.

Publishing changes to the web
=============================

This technote is published to https://tstn-044.lsst.io whenever you push changes to the ``main`` branch on GitHub.
When you push changes to a another branch, a preview of the technote is published to https://tstn-044.lsst.io/v.

Editing this technical note
===========================

The main content of this technote is in ``index.rst`` (a reStructuredText file).
Metadata and configuration is in the ``technote.toml`` file.
For guidance on creating content and information about specifying metadata and configuration, see the Documenteer documentation: https://documenteer.lsst.io/technotes.
