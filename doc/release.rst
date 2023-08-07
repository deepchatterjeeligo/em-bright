EM-Bright Release Instructions
------------------------------

This is a checklist meant to guide maintainers of the em-bright package through a release.

Once all the changes to be included in release have been pushed to ``main``, we may begin following the instructions. 
An a general rule of thumb, the version number follows the convention ``X.Y.Z``, where minor changes bump ``Z``, i.e.: ``1.0.0 -> 1.0.1``, and major changes bump ``Y``, ``i.e.: 1.0.1 -> 1.1.0``.

Initial Checklist:

#. All CI pipelines on Gitlab pass. In our case, this includes unit tests, docs, dist, and lint.
#. The Changelog has been updated to reflect changes under the proper version number.
#. All major changes to code have been thoroughly reviewed and tested.

Next we tag the release:

#. Make sure we are on ``main``

#. Update the links and tags in the ``__init__.py``, ``pyproject.toml``, and the unit tests. Be careful that package links do not point to the ``main`` branch, but instead to the version tag! Below is shown where to look for this in the ``__init__.py`` file::

    __version__ = 'X.Y.Z'

    PACKAGE_DATA_BASE_URL = (
        'https://git.ligo.org/emfollow/em-properties/em-bright/'
        f'-/raw/v{__version__}/ligo/em_bright/data'
    )

#. Commit the changes::

    git commit .

#. Tag the release:: 

    git tag -a vX.Y.Z -m "version X.Y.Z"

#. Push the changes::

    git push && git push --tags

Then we get ready to build and publish the package:

#. Clear the dist folder::

    rm -rf dist

#. Build the package::

    poetry build

#. Now, it is good practice to first upload to testpypi to ensure things go smoothly::

    poetry publish -r testpypi --username {your_username} --password {your_password}

#. Once uploading to testpypi has succeeded, upload to pypi. This cannot be undone::

    poetry publish --username {your_username} --password {your_password}

Finally, we update the Changelog and prepare the repo for further work:

#. Update the Changelog, following the established convention::

    ## [{New X.Y.Z version number}] - Unreleased

    - No changes yet

#. Commit the changes, it is okay to skip the CI here::

    git commit -m "Back to development [skip-ci]"

#. Push the updated Changelog::

    git push

Now that the release is completed, there are two more tasks to take care of:

#. Update the dependencies in places where em-bright is used in production, like gwcelery. Simply restrict the em-bright dependency of gwcelery to the new and released version.
#. Make a SCCB request, in the form of a gitlab issue. Follow the template provided, and feel free to reference previous em-bright requests.
