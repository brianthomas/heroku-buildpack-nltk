Heroku buildpack for Textmining (Gensim, NLTK, Numpy, Scipy)
====================================================

This is a custom [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks)
for Python apps that use any combination of Gensim, NLTK, NumPy and/or SciPy, 
powered by [pip](http://www.pip-installer.org/) and compiled for Python 3.

Please open a GitHub for any problems encountered or feature requests.

Details
-------

This buildpack currently supports:

Python:
  * 3.4.x

NumPy:
  * 1.9.2  
  * 1.11.1  

SciPy:
  * 0.16.0 (compiled against NumPy 1.9.2)
  * 0.17.1 (compiled against NumPy 1.11.1)

NLTK:
  * 3.0.5 (compiled against NumPy 1.9.2, Scipy 0.16.0)
  * 3.2.1 (compiled against NumPy 1.11.1, Scipy 0.17.1)

Gensim:
  * 0.12.2 (compiled against NumPy 1.9.2, Scipy 0.16.0)
  * 0.13.1 (compiled against NumPy 1.11.1, Scipy 0.17.1)

NLTK support includes downloading (all of the) corpora (some of which 
are needed by the gensim package, and will import textblob package to
do so).

This package will also install compiled runtime libraries for BLAS, LAPACK,
ATLAS, and Fortran, which are needed by NumPy and SciPy at runtime.

NOTE: because the package is under (irregular) development, I try to supply
tags which indicate stable points in the codebase (master branch). These
currently include:
 
    * py34_v1 : Python 3.4 ver 1, initial set of working binaries
    * py34_v2 : Python 3.4 ver 2, added updated gensim, nltk, numpy, scipy binaries 

### (Possible) Known Issues and TODOs 

These all come from the original project we forked from, not sure now how much 
these apply to this project.

  1. This buildpack may not work well with Multipack apps (e.g., see [issue15]: 
     https://github.com/thenovices/heroku-buildpack-scipy/issues/15
  2. [issue9]: https://github.com/thenovices/heroku-buildpack-scipy/issues/9#issuecomment-61660727
  3. [issue11]: https://github.com/thenovices/heroku-buildpack-scipy/issues/11#issuecomment-85143132
  4. [issue19]: https://github.com/thenovices/heroku-buildpack-scipy/issues/19

If any of these issues are immediately impacting you, please open a Github
issue so that I know that they are higher priority items.

Usage
-----
For a new app:

    heroku create --buildpack https://github.com/brianthomas/heroku-buildpack-textmining

For an existing app:

    heroku buildpacks:set https://github.com/brianthomas/heroku-buildpack-textmining

You must specify your exact desired version in `requirements.txt` (e.g.,
`numpy==1.9.2`). If no version is specified, the latest version available will
be used. At this time, this buildpack does not support requirements of the
form `numpy>=1.9`.

Demo
----

    $ mkdir testheroku
    $ cd testheroku
    $ git init
    $ heroku create --buildpack https://github.com/brianthomas/heroku-buildpack-textmining
    $ echo "nltk==3.0.5\nnumpy==1.9.2\nscipy==0.16.0" > requirements.txt
    $ git add requirements.txt
    $ git commit -m 'Added requirements'
    $ git push heroku master


Acknowledgments
---------------

This fork is taken from @thenovices who previously forked from @dbrgn. Many thanks to those
fellows and others setting up a lot of the code here.

