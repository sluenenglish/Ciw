.. _m-m-1:

==============================
Example - Simulate M/M/1 Queue
==============================

Here, an example of an M/M/1 queue will be given, and results compared to to those obtained using standard queueing theory.
This will walk through an example of an M/M/1 queue with Poisson arrivals of rate 3 and Exponential service times of rate 5.

Standard queueing theory gives the expected wait in an M/M/1 queue as :math:`\mathbb{E}[W] = \frac{\rho}{\mu(1-\rho)}`. With arrival rate :math:`\lambda = 3` and service rate :math:`\mu = 5`, we get traffic intensity :math:`\rho = \frac{\lambda}{\mu} = 0.6`, and so :math:`\mathbb{E}[W] = 0.3`.

We set up the parameters in Ciw::

    >>> params_dict = {'Arrival_distributions': {'Class 0': [['Exponential', 3.0]]},
    ...                'Service_distributions': {'Class 0': [['Exponential', 5.0]]},
    ...                'Simulation_time': 250,
    ...                'Transition_matrices': {'Class 0': [[0.0]]},
    ...                'Number_of_servers': [1]
    ...                }

The following code repeats the experiment 100 times, only recording waits for those that arrived after a warm-up time of 50.
It then returns the average wait in the system::
    
    >>> import ciw
    >>> from random import seed
    >>> def iteration(warmup):
    ...     Q = ciw.Simulation(params_dict)
    ...     Q.simulate_until_max_time()
    ...     records = Q.get_all_records(headers=False)
    ...     waits = [row[4] for row in records if row[3] > warmup]
    ...     return sum(waits)/len(waits)
    
    >>> seed(27)
    >>> ws = []
    >>> for i in range(100):
    ...     ws.append(iteration(50))
    
    >>> print sum(ws)/len(ws)
    0.292014274888

We see that the results of the simulation are in agreement with those of standard queueing theory.
