.. index::
	single: Installation

Installation
============

.. note::
	
	As per the official information, Elastica 5.1.0 is compatible with all elasticsearch 5.x releases. It was tested with elasticsearch v5.1.2.

Download
--------

You can download this project in either `zip <http://github.com/ruflin/Elastica/zipball/master>`_ or `tar <http://github.com/ruflin/Elastica/tarball/master>`_ formats.

The prefered way is to clone Elastica with `Git <http://git-scm.com/>`_ by running:

.. code-block:: bash

		$ git clone git://github.com/ruflin/Elastica

Composer
--------

You can also install Elastica by using composer:

.. code-block:: javascript
	
		{  
   			"require":{  
      			"ruflin/elastica":"dev-master"
   			}
		}

Include in your project
-----------------------

If you’ve used composer to install Elastica it’s very easy. Assuming your document root index file is in /htdocs/myproject/web/ and composer installed the vendor file in /htdocs/myproject/vendor your index.php has to look like this:

.. code-block:: php

	<?php

	require_once '../vendor/autoload.php';

If you don’t use composer in your project you have to include Elastica. Best way to do this is to use PHP spl_autoload_register. This function is automatically called in case you are trying to use a class/interface which hasn’t been defined yet.

So let’s assume you installed Elastica to ``/var/www/Elastica``. When you make an instance of ``\Elastica\Client``, the function will check if there is a file with that class in ``/var/www/Elastica/Client`` and load it.

.. code-block:: php

	<?php

        function __autoload_elastica ($class) {
       	    $path = str_replace('\\', '/', substr($class, 1));

    	    if (file_exists('/var/www/' . $path . '.php')) {
    	    	require_once('/var/www/' . $path . '.php');
            }
        }
        spl_autoload_register('__autoload_elastica');

        //Or using anonymous function PHP 5.3.0>=
        spl_autoload_register(function($class){
            if (file_exists('/var/www/' . $class . '.php')) {
          	    require_once('/var/www/' . $class . '.php');
          	}
        });