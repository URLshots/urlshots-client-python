.. highlight:: python
.. currentmodule:: urlshots

.. _Pytool: http://pypi.python.org/pypi/pytool
.. _Pyconfig: http://pypi.python.org/pypi/pyconfig
.. _Urllib3: http://pypi.python.org/pypi/urllib3


URLshots Python API Documentation
#################################

This documentation contains information about the URLshots Python API client.

.. contents::


Tutorial
========

This tutorial will familiarize you with the installation and usage of
the URLShots python client.

Installation
------------

The URLShots client requires Pytool_ (``>=2.3.2``), Pyconfig_ (``>=1.2.0``),
and Urllib3_. These are install for you automatically when you install the
URLshots client via ``pip`` or ``easy_install``.

.. code-block:: bash

    $ pip install -U urlshots-api    # preferred
    $ easy_install -U urlshots-api   # without pip

To get the latest development version of the Urlshots client, clone the code
via bitbucket and install:

.. code-block:: bash

    $ git clone https://bitbucket.org/urlshots/urlshots-api.git
    $ cd urlshots-api
    $ python setup.py install

Quickstart
----------

Once you have the urlshots client installed you can begin to take screenshots
right away. No configuration is required, other than providing your API key.

An API key can be acquired by signing up at `URLshots.net
<http://urlshots.net>`_. If you are using a private `Amazon EC2 cluster
<http://urlshots.net/>`_ , then no API key is needed.

::

    >>> import urlshots
    >>> urlshots_api = urlshots.API(api_key='DEMO')  # Replace with your API key
    >>> image_data = urlshots_api.image('http://www.google.com')
    >>> with open('google.png', 'w') as image_file:
    ...     image_file.write(image_data)

Of course, the default parameters that the client uses probably aren't what
you're looking for. In order to learn how to set parameters to get exactly what
you need, read on!

API Parameters
--------------

This section will detail how you can get more control out of your screenshot
request.

For a full listing of paramters and their description please refer to the
:ref:`api`.

As shown above you will want to start with creating an instance of the API.

::

    >>> from urlshots import API
    >>> urlshot = API()

.. rubric:: Delay

Next you can define how long the page should wait after initial load
(in seconds).  This can come in handy in the case of javascript rendering extra
elements on the page after ``onLoad``.
(Max: 5 seconds)

::

    >>> urlshot.opts.delay = 4      # Page will wait 4 seconds before grabbing
    the screenshot.

.. rubric:: JPEG

You can set the JPEG quality on your screenshot as any value between 1 ``min``
and 100 ``max``.  Alternatively setting this value to ``0`` will return an
uncompressed PNG.

::

    >>> urlshot.opts.jpeg = 100   # Will return a JPEG image with 100% quality.
    >>> urlshot.opts.jpeg = 75    # Will return a JPEG image with 75% quality.
    >>> urlshot.opts.jpeg = 25    # Will return a JPEG image with 25% quality.
    >>> urlshot.opts.jpeg = 0     # Will return an uncompressed PNG image

.. rubric:: Compression

Setting the compression flag to a 1 will compress your PNG screenshot to an
8-bit indexed image. (Default: 0)

::

    >>> urlshot.opts.compression = 1      # compression = True

.. rubric:: Timeout

Timeout will tell the page how long to wait for the page to become responsive
before returning an error. (Default: 20 seconds)

::

    >>> urlshot.opts.timeout = 10      # Page will wait 10 seconds and return
    an error if no response from the server

.. rubric:: Actions

::

    # Screenshot will crop to this specific box size
    >>> urlshot.opts.actions = 'crop:0,0,800,600'

    # Screenshot will be 75% of it's original resolution
    >>> urlshot.opts.actions = 'scale:.75'

    # Both of the above in order
    >>> urlshot.opts.actions = 'scale:.75|crop:0,0,800,600'

.. rubric:: Concurrency

::

    >>> urlshot.opts.concurrency = 1      # How many concurrent requests can
                                          # your application handle?

.. rubric:: Window

::

    # Window resolution to render the page at
    >>> urlshot.opts.window = (1024, 768)

.. rubric:: Host (expert)

::

    # Only use if you have a special instance assigned to your api key
    >>> urlshot.opts.host = 'api123.urlshots.net'

.. _api:

API Documentation
=================

This section includes documentation of the URLshots API modules.

:class:`urlshots.API`
---------------------

.. autoclass:: urlshots.API
   :members:


Changelog
=========

.. currentmodule:: urlshots

0.2.0
-----

* Add `script` and `api_key` parameters to :class:`API`.


.. Indices and tables
.. ==================

.. * :ref:`genindex`
.. * :ref:`modindex`
.. * :ref:`search`

