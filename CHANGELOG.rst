``gcovr`` Release History and Change Log

.. program is needed to resolve option links
.. program::  gcovr

Future Directions
-----------------

.. warning::

   Python 2.7 will reach its end of life on Jan 1, 2020.
   With its first release on or after that date,
   gcovr will drop support for Python 2.7 and 3.4.
   Subsequently, gcovr will only support Python versions
   that enjoy upstream support.

   Please note that gcovr does not use a strict SemVer version number.
   When support for a Python version is dropped,
   gcovr will not necessarily increment its major version.

Unreleased
----------

Breaking changes:

 - Format flag parameters like :option:`--xml` or :option:`--html`
   now take an optional output file name.
   This potentially changes the interpretation of search paths.
   In ``gcovr --xml foo``,
   previous gcovr versions would search the ``foo`` directory for coverage data.
   Now, gcovr will try to write the Cobertura report to the ``foo`` file.
   To keep the old meaning, separate positional arguments like
   ``gcovr --xml -- foo``.

Improvements and new features:

 - :ref:`Configuration file <configuration>` support (experimental).
   (:issue:`167`, :issue:`229`, :issue:`279`, :issue:`281`, :issue:`293`)
 - Handle cyclic symlinks correctly during coverage data search.
   (:issue:`284`)
 - Simplification of :option:`--object-directory` heuristics.
   (:issue:`18`, :issue:`273`, :issue:`280`)
 - Exception-only code like a ``catch`` clause is now shown as uncovered.
   (:issue:`283`)
 - New :option:`--exclude-throw-branches` option
   to exclude exception handler branches. (:issue:`283`)
 - Support ``--root ..`` style invocation,
   which might fix some CMake-related problems. (:issue:`294`)
 - Fix wrong names in report
   when source and build directories have similar names. (:issue:`299`)
 - Stricter argument handling. (:issue:`267`)
 - Reduce XML memory usage by moving to lxml.
   (:issue:`1`, :issue:`118`, :issue:`307`)
 - Can write multiple reports at the same time
   by giving the output file name to the report format parameter.
   Now, ``gcovr --html -o cov.html`` and ``gcovr --html cov.html``
   are equivalent.

Known issues:

 - The :option:`--keep` option only works when using existing gcov files
   with :option:`-g`/:option:`--use-gcov-files`.
   (:issue:`285`, :issue:`286`)
 - Gcovr may get confused
   when header files in different directories have the same name.
   (:issue:`271`)
 - Gcovr may not work when no en_US locale is available.
   (:issue:`166`)

Documentation:

 - :ref:`Exclusion marker <exclusion markers>` documentation.
 - FAQ: :ref:`exception branches` (:issue:`283`)
 - FAQ: :ref:`uncovered files not shown`
   (:issue:`33`, :issue:`100`, :issue:`154`, :issue:`290`, :issue:`298`)

Internal changes:

 - More tests. (:issue:`269`, :issue:`268`, :issue:`269`)
 - Refactoring and removal of dead code. (:issue:`280`)
 - New internal data model.

4.1 (2 July 2018)
-----------------

 - Fixed/improved --exclude-directories option. (:issue:`266`)
 - New "Cookbook" section in the documentation. (:issue:`265`)

4.0 (17 June 2018)
------------------

Breaking changes:

 - This release drops support for Python 2.6. (:issue:`250`)
 - PIP is the only supported installation method.
 - No longer encoding-agnostic under Python 2.7.
   If your source files do not use the system encoding (probably UTF-8),
   you will have to specify a --source-encoding.
   (:issue:`148`, :issue:`156`, :issue:`256`)
 - Filters now use forward slashes as path separators, even on Windows.
   (:issue:`191`, :issue:`257`)
 - Filters are no longer normalized into pseudo-paths.
   This could change the interpretation of filters in some edge cases.

Improvements and new features:

 - Improved --help output. (:issue:`236`)
 - Parse the GCC 8 gcov format. (:issue:`226`, :issue:`228`)
 - New --source-encoding option, which fixes decoding under Python 3.
   (:issue:`256`)
 - New --gcov-ignore-parse-errors flag.
   By default, gcovr will now abort upon parse errors. (:issue:`228`)
 - Detect the error when gcov cannot create its output files (:issue:`243`,
   :issue:`244`)
 - Add -j flag to run gcov processes in parallel. (:issue:`3`, :issue:`36`,
   :issue:`239`)
 - The --html-details flag now implies --html. (:issue:`93`, :issue:`211`)
 - The --html output can now be used without an --output filename
   (:issue:`223`)
 - The docs are now managed with Sphinx.
   (:issue:`235`, :issue:`248`, :issue:`249`, :issue:`252`, :issue:`253`)
 - New --html-title option to change the title of the HTML report.
   (:issue:`261`, :issue:`263`)
 - New options --html-medium-threshold and --html-high-threshold
   to customize the color legend. (:issue:`261`, :issue:`264`)

Internal changes:

 - Huge refactoring. (:issue:`214`, :issue:`215`, :issue:`221` :issue:`225`,
   :issue:`228`, :issue:`237`, :issue:`246`)
 - Various testing improvements. (:issue:`213`, :issue:`214`, :issue:`216`,
   :issue:`217`, :issue:`218`, :issue:`222`, :issue:`223`, :issue:`224`,
   :issue:`227`, :issue:`240`, :issue:`241`, :issue:`245`)
 - HTML reports are now rendered with Jinja2 templates. (:issue:`234`)
 - New contributing guide. (:issue:`253`)

3.4 (12 February 2018)
----------------------

 - Added --html-encoding command line option (:issue:`139`).
 - Added --fail-under-line and --fail-under-branch options,
   which will error under a given minimum coverage. (:issue:`173`, :issue:`116`)
 - Better pathname resolution heuristics for --use-gcov-file. (:issue:`146`)
 - The --root option defaults to current directory '.'.
 - Improved reports for "(", ")", ";" lines.
 - HTML reports show full timestamp, not just date. (:issue:`165`)
 - HTML reports treat 0/0 coverage as NaN, not 100% or 0%. (:issue:`105`, :issue:`149`, :issue:`196`)
 - Add support for coverage-04.dtd Cobertura XML format (:issue:`164`, :issue:`186`)
 - Only Python 2.6+ is supported, with 2.7+ or 3.4+ recommended. (:issue:`195`)
 - Added CI testing for Windows using Appveyor. (:issue:`189`, :issue:`200`)
 - Reports use forward slashes in paths, even on Windows. (:issue:`200`)
 - Fix to support filtering with absolute paths.
 - Fix HTML generation with Python 3. (:issue:`168`, :issue:`182`, :issue:`163`)
 - Fix --html-details under Windows. (:issue:`157`)
 - Fix filters under Windows. (:issue:`158`)
 - Fix verbose output when using existing gcov files (:issue:`143`, :issue:`144`)


3.3 (6 August 2016)
-------------------

 - Added CI testing using TravisCI
 - Added more tests for out of source builds and other nested builds
 - Avoid common file prefixes in HTML output (:issue:`103`)
 - Added the --execlude-directories argument to exclude directories
   from the search for symlinks (:issue:`87`)
 - Added branches taken/not taken to HTML (:issue:`75`)
 - Use --object-directory to scan for gcov data files (:issue:`72`)
 - Improved logic for nested makefiles (:issue:`135`)
 - Fixed unexpected semantics with --root argument (:issue:`108`)
 - More careful checks for covered lines (:issue:`109`)


3.2 (5 July 2014)
-----------------

 - Adding a test for out of source builds
 - Using the starting directory when processing gcov filenames.
   (:issue:`42`)
 - Making relative paths the default in html output.
 - Simplify html bar with coverage is zero.
 - Add option for using existing gcov files (:issue:`35`)
 - Fixing --root argument processing (:issue:`27`)
 - Adding logic to cover branches that are ignored (:issue:`28`)


3.1 (6 December 2013)
---------------------

 - Change to make the -r/--root options define the root directory 
   for source files.
 - Fix to apply the -p option when the --html option is used.
 - Adding new option, '--exclude-unreachable-branches' that
   will exclude branches in certain lines from coverage report.
 - Simplifying and standardizing the processing of linked files.
 - Adding tests for deeply nested code, and symbolic links.
 - Add support for multiple —filter options in same manner as —exclude 
   option.


3.0 (10 August 2013)
--------------------

 - Adding the '--gcov-executable' option to specify
   the name/location of the gcov executable. The command line option
   overrides the environment variable, which overrides the default 'gcov'.
 - Adding an empty "<methods/>" block to <classes/> in the XML output: this
   makes out XML complient with the Cobertura DTD. (#3951)
 - Allow the GCOV environment variable to override the default 'gcov' 
   executable.  The default is to search the PATH for 'gcov' if the GCOV
   environment variable is not set. (#3950)
 - Adding support for LCOV-style flags for excluding certain lines from
   coverage analysis. (#3942)
 - Setup additional logic to test with Python 2.5.
 - Added the --html and --html-details options to generate HTML.
 - Sort output for XML to facilitate baseline tests.
 - Added error when the --object-directory option specifies a bad directory.
 - Added more flexible XML testing, which can ignore XML elements
   that frequently change (e.g. timestamps).
 - Added the '—xml-pretty' option, which is used to
   generate pretty XML output for the user manual.
 - Many documentation updates


2.4 (13 April 2012)
-------------------

 - New approach to walking the directory tree that is more robust to
   symbolic links (#3908)
 - Normalize all reported path names

   - Normalize using the full absolute path (#3921)
   - Attempt to resolve files referenced through symlinks to a common
     project-relative path

 - Process ``gcno`` files when there is no corresponding ``gcda`` file to
   provide coverage information for unexecuted modules (#3887)
 - Windows compatibility fixes

   - Fix for how we parse ``source:`` file names (#3913)
   - Better handling od EOL indicators (#3920)

 - Fix so that gcovr cleans up all ``.gcov`` files, even those filtered by
   command line arguments
 - Added compatibility with GCC 4.8 (#3918)
 - Added a check to warn users who specify an empty ``--root`` option (see #3917)
 - Force ``gcov`` to run with en_US localization, so the gcovr parser runs
   correctly on systems with non-English locales (#3898, #3902).
 - Segregate warning/error information onto the stderr stream (#3924)
 - Miscellaneous (Python 3.x) portability fixes
 - Added the master svn revision number as part of the verson identifier


2.3.1 (6 January 2012)
----------------------

 - Adding support for Python 3.x


2.3 (11 December 2011)
----------------------

 - Adding the ``--gcov-filter`` and ``--gcov-exclude`` options.


2.2 (10 December 2011)
----------------------

 - Added a test driver for gcovr.
 - Improved estimation of the ``<sources>`` element when using gcovr with filters.
 - Added revision and date keywords to gcovr so it is easier to identify
   what version of the script users are using (especially when they are
   running a snapshot from trunk).
 - Addressed special case mentioned in [comment:ticket:3884:1]: do not
   truncate the reported file name if the filter does not start matching
   at the beginning of the string.
 - Overhaul of the ``--root`` / ``--filter`` logic. This should resolve the
   issue raised in #3884, along with the more general filter issue
   raised in [comment:ticket:3884:1]
 - Overhaul of gcovr's logic for determining gcc/g++'s original working
   directory. This resolves issues introduced in the original
   implementation of ``--object-directory`` (#3872, #3883).
 - Bugfix: gcovr was only including a ``<sources>`` element in the XML
   report if the user specified ``-r`` (#3869)
 - Adding timestamp and version attributes to the gcovr XML report (see
   #3877).  It looks like the standard Cobertura output reports number of
   seconds since the epoch for the timestamp and a doted decimal version
   string.  Now, gcovr reports seconds since the epoch and 
   "``gcovr ``"+``__version__`` (e.g. "gcovr 2.2") to differentiate it 
   from a pure Cobertura report.


2.1 (26 November 2010)
----------------------

 - Added the ``--object-directory`` option, which allows for a flexible
   specification of the directory that contains the objects generated by
   gcov.
 - Adding fix to compare the absolute path of a filename to an exclusion
   pattern.
 - Adding error checking when no coverage results are found. The line and
   branch counts can be zero.
 - Adding logic to process the ``-o``/``--output`` option (#3870).
 - Adding patch to scan for lines that look like::

        creating `foo'

   as well as
   ::

        creating 'foo'

 - Changing the semantics for EOL to be portable for MS Windows.
 - Add attributes to xml format so that it could be used by hudson/bamboo with
   cobertura plug-in.


2.0 (22 August 2010)
--------------------

 - Initial release as a separate package.  Earlier versions of gcovr
   were managed within the 'fast' Python package.

