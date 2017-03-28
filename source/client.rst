.. index::
	single: Working with Elastica Client Object

Working with Elastica Client Object
===================================

Connecting to Elasticsearch
---------------------------

.. note::

	Assuming you have elasticsearch set up and running.

Running a single node
~~~~~~~~~~~~~~~~~~~~~

When your single elasticsearch node is running on ``localhost:9200``, which is the default, you can simply connect:

.. code-block:: php

	<?php

	$elasticaClient = new \Elastica\Client();

Running a cluster
~~~~~~~~~~~~~~~~~

Elasticsearch was built with the cloud / multiple distributed servers in mind. It is quite easy to start a elasticsearch cluster simply by starting multiple instances of elasticsearch on one server or on multiple servers. To start multiple instances of elasticsearch on your local machine, just run the command to start an instance in the elasticsearch folder twice.

One of the goals of the distributed search index is availability. If one server goes down, search results should still be served. But if the client connects to only the server that just went down, no results are returned anymore. Because of this, ``\Elastica\Client`` supports multiple servers which are accessed in a round robin algorithm. This is the only and also most basic option at the moment. So if we start a node on port 9200 and port 9201 above, we pass the following arguments to ``\Elastica\Client`` to access both servers:

.. code-block:: php

	<?php

	$elasticClient = new \Elastica\Client(array(
	    'servers' => array(
	        array('host' => 'localhost', 'port' => 9200),
	        array('host' => 'localhost', 'port' => 9201)
	    )
	));

Client Configurations
---------------------

Lookup the current client configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Generally, an elastica client object consists of the following parameters:

================ ============= ===============
Parameter        Default Value Additional Info
================ ============= ===============
host             ``null``
port             ``null``
path             ``null``
url              ``null``
proxy            ``null``
transport        ``null``
persistent       ``true``
timeout          ``null``
connections      ``[]``
roundRobin       ``false``
log              ``false``     Set to true, to enable logging, set a string to log to a specific file
retryOnConflict  ``0``         Used while updating a document.
bigintConversion ``false``     Set to true to enable the JSON bigint to string conversion option (see issue `#717 <https://github.com/ruflin/Elastica/issues/717>`_)
username         ``null``
password         ``null``
================ ============= ===============

.. note::

	You may find an additional ``connectionStrategy`` parameter which is set to ``RoundRobin`` or ``Simple`` depending on the ``roundRobin`` flag being ``true`` or ``false`` respectively.

The current configuration of an elastica client can be found using the ``getConfig()`` and ``getConfigValue()`` methods.

The ``getConfig()`` method returns the whole config of the elastica client object as an array.

.. code-block:: php

	<?php

	$elasticClient->getConfig();

Optionally, a key can be passed to ``getConfig()`` to fetch specific information.

.. code-block:: php

	<?php

	$elasticClient->getConfig('host');

	//OR

	$elasticClient->getConfig('port');



