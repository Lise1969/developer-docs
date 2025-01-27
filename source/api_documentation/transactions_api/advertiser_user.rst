#####################
Advertiser / Merchant
#####################

URL
---

The API follows REST conventions. Perform an HTTPS GET to the URL with the format in which you’d like to receive data. The following response formats are supported, where 33 is the advertiser id.

.. list-table::
  :widths: 8 40
  :header-rows: 1
  :class: parameters

  * - Format
    - Description and URL

  * - csv
    - Comma-Separated Values, or really Anything-Separated Values (see column_separator= below). Returns an optional header row followed by one row for each transaction, with delimited values for each row. ``https://mynetwork.invoca.net/api/@@TRANSACTION_API_VERSION/advertisers/transactions/33.csv``

  * - xml
    - Returns an XML document with an array of Transaction elements. ``https://mynetwork.invoca.net/api/@@TRANSACTION_API_VERSION/advertisers/transactions/33.xml``

  * - json
    - Returns a JSON array of transaction objects. ``https://mynetwork.invoca.net/api/@@TRANSACTION_API_VERSION/advertisers/transactions/33.json``


.. include:: _intro.rst
.. include:: _intro_constants.rst


Response
--------

General Parameters
******************

.. include:: _advertiser_param_table.rst

.. include:: _dnpr_param_table.rst

.. include:: _adwords_param_table.rst

.. include:: _conversion_reporting_param_table.rst

.. include:: _custom_data_params.rst

.. include:: _signal_param_table.rst

.. include:: _demographics_param_table.rst

Additional Feature Parameters
*****************************

.. include:: _advertiser_optional_param_table.rst

.. include:: _example.rst



Example 1: Get the next 20 transactions that occurred after transaction id C624DA2C-CF3367C3:

.. code-block:: bash

  curl -k 'https://mynetwork.invoca.net/api/@@TRANSACTION_API_VERSION/advertisers/transactions/33.csv?limit=20&start_after_transaction_id=C624DA2C-CF3367C3&oauth_token=YbcFH'


Example 2: Get 50 rows from a specific time period with only the transaction_id and all Custom Data columns:

.. code-block:: bash

  curl -k 'https://mynetwork.invoca.net/api/@@TRANSACTION_API_VERSION/advertisers/transactions/33.csv?limit=50&include_columns=transaction_id,$invoca_custom_columns&exclude_columns=$invoca_default_columns&from=2015-03-26&to=2015-03-27&oauth_token=YbcFH'


Example 3: Get 50 rows that exclude a few columns such as Caller ID and Call Recordings:

.. code-block:: bash

  curl -k 'https://mynetwork.invoca.net/api/@@TRANSACTION_API_VERSION/advertisers/transactions/33.csv?limit=50&exclude_columns=calling_phone_number,recording&start_after_transaction_id=C624DA2C-CF3367C3&oauth_token=YbcFH'


Example 4: Get All Transactions from a specific time period that are of transaction_type Signal:

.. code-block:: bash

  curl -k 'https://mynetwork.invoca.net/api/@@TRANSACTION_API_VERSION/advertisers/transactions/33.csv?transaction_type=Signal&from=2015-03-24&to=2015-03-27&oauth_token=YbcFH'


Example 5: Get All Transactions from a specific time period that are of transaction_type Call and Signal:

.. code-block:: bash

  curl -k 'https://mynetwork.invoca.net/api/@@TRANSACTION_API_VERSION/advertisers/transactions/33.csv?transaction_type[]=Call&transaction_type[]=Signal&from=2015-03-24&to=2015-03-27&oauth_token=YbcFH'

Example 6: Get All Transactions from a specific time period with oauth token in the request header:

.. code-block:: bash

  curl -k -H 'Authorization: YbcFH' 'https://mynetwork.invoca.net/api/@@TRANSACTION_API_VERSION/advertisers/transactions/33.csv?transaction_type[]=Call&transaction_type[]=Signal&from=2015-03-24&to=2015-03-27'


Endpoint:

``https://invoca.net/api/@@TRANSACTION_API_VERSION/advertisers/transactions/<advertiser_id>.<format>``
