.. image:: https://secure.travis-ci.org/brutasse/djangopeople.png
   :alt: Build Status
   :target: https://secure.travis-ci.org/brutasse/djangopeople

This is the codebase behind what used to be djangopeople.net and now lives at
people.djangoproject.com.

If you want to add features or make big changes, please `create a new issue`_
first!

.. _create a new issue: https://github.com/brutasse/djangopeople/issues/new

Hacking
-------

You need `Daemontools`_ and `Foreman`_ installed.

.. _Daemontools: http://cr.yp.to/daemontools.html
.. _Foreman: https://github.com/ddollar/foreman

::

    git clone git@github.com:brutasse/djangopeople.git
    cd djangopeople
    mkvirtualenv -p python2 djangopeople
    pip install -r requirements.txt
    add2virtualenv .

Check ``env/DATABASE_URL`` to configure a local DB.

Then::

    make db
    make run

The development server is now running on http://localhost:8000.

To run the tests::

    make test

Deploying on Heroku
-------------------

Set a bunch of environment variables:

* ``AWS_ACCESS_KEY``
* ``AWS_SECRET_KEY``
* ``AWS_BUCKET_NAME``
* ``DATABASE_URL``
* ``SECRET_KEY``
* ``SENTRY_DSN``
* ``DJANGO_SETTINGS_MODULE`` (set it to ``djangopeople.settings``)
* ``FROM_EMAIL``
* ``API_PASSWORD``

Optionally:

* ``CANONICAL_HOSTNAME`` (e.g. people.djangoproject.com)
* Add the redistogo addon

First deploy::

    git push heroku master
    heroku run django-admin.py syncdb --noinput
    heroku run django-admin.py collectstatic
    heroku run django-admin.py fix_counts

Subsequent deploys::

    git push heroku master
    heroku run django-admin.py collectstatic

-------

Original README from Simon Willison:

This is an unmodified (except removal of secrets and API keys) dump of the
code now running on djangopeople.net - the vast majority of which was
developed between January and April 2008 by Simon Willison and Natalie Downe.

It originally ran on Django r7400, but has recently been updated for Django 1.1.

This code was not originally intended for public consumption, so there are
probably one or two eyebrow raising design decisions. In particular, the
machine tags stuff for user profiles was an ambitious experiment which I
wouldn't mind seeing the back of.
