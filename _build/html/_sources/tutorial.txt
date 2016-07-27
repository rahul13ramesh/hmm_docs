Tutorial
========

Introduction
------------
A Hidden Markov model is a Markov chain for which the states are not explicitly observable .We instead make indirect observations about the state by events which result from those hidden states .Since these observables are not sufficient/complete to describe the state, we associate a probability with each of the observable coming from a particular state . In other words, if the probability falls to either 1 or 0,it reduces to a Markov model.


**1st order Markov assumption** :The probability of occurrence of an event  at time 't' depends only on the observation at time 't-1' and not on the events that happened before 't-1'. In other words, the observations O1,O2,...Ot-1 do not impact the observation Ot. Hidden Markov models work on this assumption.The initial probability array, transition array and observation/emission array can completely define a HMM.

Basic Definitions
-----------------

* *O : { O1, O2 , …. OT }* : Sequence of observations
* *Q : {Q1 , Q2 , …. QT }* : Sequence of corresponding hidden states
* *S : {S1 , S2, ……, Sn }* : Set of unique states in the Hidden Markov model    
* *M : {M1 , M2, ……, Mn }* : Set of unique observations in the Hidden Markov model    
* *n* : Number of hidden states in the model
* *m* : Number of unique observations in the model
* *T* : Transition matrix
* *E* : Emission matrix
* *Pi*: Initial/ Start probability
* *Alpha* : Forward probability values
* *Beta* : backward probability values


Forward/Backward Probability
----------------------------

Given an observation sequence O={O1 , O2,.... OT}, the forward probability Alpha[i,t] is the probability for the sequence O0, O1,...,Ot to end in the state S[i] after 't' stages or at time 't'.

                *Alpha(i) = P(Qt= Si , O1, O2,...,OT )*

Given an observation sequence O={O0 , O1,.... OT}, the backward probability Beta(i) for a state Siat time t is the probability for the sequence Ot+1, Ot+2,...,Ot is observed given the state is Si at time 't'. 

                *Beta(i) = P(Ot+1, Ot+2,...,OT | Qt= Si )*


Forward Algorithm 
-----------------
The forward algorithm gives us the probability of an observed sequence in the HMM. So why do we need to find the probability of an observed sequence? This type of problem occurs in speech recognition where a large number of Markov models are used, and each one modelling a particular word. Each utterance of a word, will now give us a set of observation variables. 

Hence we will use the Markov model that has the highest probability of this observation sequence. The Forward algorithm is also an important sub-routine of the forward-backward algorithm. The algorithm works by calculating Alpha over various 't'. The sum of alpha for all states for time = 'T'

Viterbi Algorithm
-----------------
Viterbi algorithm is used to find out the most likely sequence of hidden states that can generate  the given set of observations.  For example, in speech recognition, the acoustic signal is treated as the observed sequence of events, and a string of text is considered to be the "hidden cause" of the acoustic signal. The Viterbi algorithm finds the most likely string of text given the acoustic signal.
  
So, what we essentially do is in each step of algorithm, we calculate the probabilities of landing up in another state from any present state. We compare transition probabilities between states. We choose whichever is higher and move on.


Forward-Backward Algorithm
--------------------------
The third and probably the most important of the three algorithms is the forward backward algorithm. Often, the emission, transition and start probabilities are not known. This algorithms aims to find the best model parameters based on the principles of expectation maximization. The algorithm works iteratively and in each iteration, the model parameters are updated, such that the probability of occurrence of a set of observations increase.

See Also
--------
`Check this link <http://www.python.org/>`_ to view the more detailed tutorial.
