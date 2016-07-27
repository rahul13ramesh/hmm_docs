Example
=======

This notebook illustrates the usage of the functions in this package,
for a discrete hidden markov model. In the example below, the HMM has
two states 's' and 't'. There are two possible observation which are 'A'
and 'B'. The start probabilities, emission probabilities and transition
probabilities are initialized as below. There are two observation
sequences 'obs1' and 'obs2'. The variable 'quantities\_observations'
indicates the number of times, the sequences obs1 and obs2 are seen.

.. code:: python

    # Import required Libraries
    import numpy as np
    from hidden_markov import hmm
Parameter Intialization
-----------------------

.. code:: python

    # ====Initializing Parameters ====
    
    # States
    states = ('s', 't')
    
    # list of possible observations
    possible_observation = ('A','B' )
    
    # The observations that we observe and feed to the model
    obs1 = ('A', 'B','B','A')
    obs2 = ('B', 'A','B')
    
    # Number of observation sequece 1 and observation sequence 2
    quantities_observations = [10, 20]
    
    observation_tuple = []
    observation_tuple.extend( [obs1,obs2] )
     
    # Input parameters as Numpy matrices
    start_probability = np.matrix( '0.5 0.5 ')
    transition_probability = np.matrix('0.6 0.4 ;  0.3 0.7 ')
    emission_probability = np.matrix( '0.3 0.7 ; 0.4 0.6 ' )

A class object called 'test' is initialized with parameters. Note that
the parameters are mandatory and default arguments do not exist.
Additionally, the start probabilities, transition probabilities and
emission probabilites are all numpy matrices. The observations and
states are both tuples and the observation\_tuples variable is a list of
observations.

.. code:: python

     test = hmm(states,possible_observation,start_probability,transition_probability,emission_probability)
Forward Algorithm
-----------------

The forward algorithm find the probability of occurence of an
observation sequence. The function inputs an observation sequence and
returns the probability. The transition, start and emission
probabilities used, are the same as those specified in the class object
definition.

.. code:: python

    #Forward Algorithm Results on 'obs1'
    test.forward_algo(obs1)



.. parsed-literal::

    0.051533999999999996



Viterbi Algorithm
-----------------

The Viterbi algorithm finds the most probable sequence of states for a
given sequence of observations. The function inputs an observation
sequence and returns the most probable sequence of states.

.. code:: python

    #Output of the Viterbi algorithm 
    test.viterbi(obs1)



.. parsed-literal::

    ['t', 't', 't', 't']



Baum-welch Algorithm
--------------------

Using the principles of expectation maximization, the Baum-algorithm
finds the emission, start and transition probabilities that represent a
list of observation sequences. We use log-probability in order to
prevent an overflow error. The function inputs as parameters, a set of
observation sequences, the number of times each observation sequence
occurs and the number of iterations. The function then returns the final
emission, start and transition probabilities.

.. code:: python

    prob = test.log_prob(observation_tuple, quantities_observations)
    print ("probability of sequence with original parameters : %f"%(prob))

.. parsed-literal::

    probability of sequence with original parameters : -67.920122


.. code:: python

    #Sequence on which Baum welch algoritm aws applide on
    print(observation_tuple)
    print(quantities_observations)

.. parsed-literal::

    [('A', 'B', 'B', 'A'), ('B', 'A', 'B')]
    [10, 20]


.. code:: python

    #Apply Baum-welch Algorithm
    num_iter=1000
    emission,transition,start = test.train_hmm(observation_tuple,num_iter,quantities_observations)
.. code:: python

    #Print output after applying the algorithm
    print(emission)

.. parsed-literal::

    [[ 0.36193015  0.63806985]
     [ 0.41111482  0.58888518]]


.. code:: python

    print(start)

.. parsed-literal::

    [[ 0.49431308  0.50568692]]


.. code:: python

    print(transition)

.. parsed-literal::

    [[ 0.58184591  0.41815409]
     [ 0.29789921  0.70210079]]


Notice that the probability of occurence of an observation sequence has
increased for the new model parameters

.. code:: python

    prob = test.log_prob(observation_tuple, quantities_observations)
    print ("probability of sequence after %d iterations : %f"%(num_iter,prob))

.. parsed-literal::

    probability of sequence after 1000 iterations : -67.356668

