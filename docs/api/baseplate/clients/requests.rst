``baseplate.clients.requests``
==============================

TODO give some intro text here

:doc:`Requests <requests:user/quickstart>` is a library.

.. automodule:: baseplate.clients.requests

Example
-------

To integrate ``requests`` with your application, add the appropriate client
declaration to your context configuration::

   baseplate.configure_context(
      {
         ...
         # see above for when to use which of these
         "foo": ExternalRequestsClient(),
         "bar": InternalRequestsClient(),
         ...
      }
   )

configure it in your application's configuration file:

.. code-block:: ini

   [app:main]

   ...

   # optional: the number of connections to cache
   foo.pool_connections = 10

   # optional: the maximum number of connections to keep in the pool
   foo.pool_maxsize = 10

   # optional: how many times to retry DNS/connection attempts
   # (not data requests)
   foo.max_retries = 0

   # optional: whether or not to block waiting for connections
   # from the pool
   foo.pool_block = false

   ...


and then use the attached :py:class:`~requests.Session`-like object in
request::

   def my_method(request):
       request.foo.get("https://zombo.com")

Configuration
-------------

.. autoclass:: ExternalRequestsClient

.. autoclass:: InternalRequestsClient

.. autofunction:: http_adapter_from_config

Classes
-------

.. autoclass:: BaseplateSession
   :members:

.. autoclass:: RequestsContextFactory
   :members: