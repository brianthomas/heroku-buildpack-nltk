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

SciPy:
  * 0.16.0 (compiled against NumPy 1.9.2)

NLTK:
  * 3.0.5 (compiled against NumPy 1.9.2, Scipy 0.16.0)

Gensim:
  * 0.12.2 (compiled against NumPy 1.9.2, Scipy 0.16.0)

NLTK support includes downloading (all of the) corpora (some of which 
are needed by the gensim package, and will import textblob package to
do so).

This package will also install compiled runtime libraries for BLAS, LAPACK,
ATLAS, and Fortran, which are needed by NumPy and SciPy at runtime.

### Known Issues and TODOs (from the original project we forked from, not sure
now how much these apply) 

  1. Scikit-learn can be installed, but may not pass all tests. For example,
     scikit-learn 0.14.1 installed with NumPy 1.9.0 and SciPy 0.13.3 did not
     pass all tests. You can see the failed tests in [this issue][issue9].
     Another user [reported][issue11] that scikit-learn 0.15.2 installed fine, although
     he did not post any test results.
  2. This buildpack may not work well with Multipack apps (e.g., see [this
     issue][issue15]).
  3. I was getting some minor test failures for NumPy 1.9.2 that I wasn't able
     to resolve. See more information [here][issue19]. Please contact me if
     you have a problem related to this.

Some issues from forked site (may or may not apply still):
[issue9]: https://github.com/thenovices/heroku-buildpack-scipy/issues/9#issuecomment-61660727
[issue11]: https://github.com/thenovices/heroku-buildpack-scipy/issues/11#issuecomment-85143132
[issue15]: https://github.com/thenovices/heroku-buildpack-scipy/issues/15
[issue19]: https://github.com/thenovices/heroku-buildpack-scipy/issues/19

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

