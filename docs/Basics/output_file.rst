.. _output-file:

===============
The Output Data
===============

Once a simulation has been run, the following method may be called to write a data file::

    >>> Q.write_records_to_file(<path_to_file>) # doctest:+SKIP

This file contains does not contain summary statistics, but all the information that happened during the simulation in raw format.
Each time an individual completes service at a service station, a data record of that service is kept.
This file contains all these data records for all services of all customers at all nodes during the simulation run time.

The following table summarises the columns:

    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-----------------------+-------------------------+
    | I.D number | Class | Node | Arrival Date | Waiting Time | Service Start Date | Service Time | Service End Date | Time Blocked | Exit Date | Queue Size at Arrival | Queue Size at Departure |
    +============+=======+======+==============+==============+====================+==============+==================+==============+===========+=======================+=========================+
    | 227592     | 1     | 1    | 245.601      | 0.0          | 245.601            | 0.563        | 246.164          | 0.0          | 246.164   | 0                     | 2                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-----------------------+-------------------------+
    | 411239     | 0     | 1    | 245.633      | 0.531        | 246.164            | 0.608        | 246.772          | 0.0          | 246.772   | 1                     | 5                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-----------------------+-------------------------+
    | 001195     | 0     | 2    | 247.821      | 0.0          | 247.841            | 1.310        | 249.151          | 0.882        | 250.033   | 0                     | 0                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-----------------------+-------------------------+
    | ...        | ...   | ...  | ...          | ...          | ...                | ...          | ...              | ...          | ...       | ...                   |                         |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-----------------------+-------------------------+

The :code:`write_records_to_file` method writes a header as default. To disable this feature, input :code:`headers=False`::

    >>> Q.write_records_to_file(<path_to_file>, header=False) # doctest:+SKIP
