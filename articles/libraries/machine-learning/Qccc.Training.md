

# Classifier Training Process and Results

Training of a circuit-centric quantum classifier is a process with many moving parts that require the same (or slightly larger) amount of
calibration by trial and error as training of traditional classifiers. Here we define the main concepts and ingredients of this training process. 

# Training/testing schedules
In the context of classifier training a *schedule* describes a subset of data samples in an overall training or testing set. A schedule is usually defined as a
collection of sample indices.

# Parameter/bias scores
Given a candidate parameter vector and a classifier bias, their *validation score* is measured relative to a chosen validation schedule S and is expressed by a number of misclassifications
 counted over all the samples in the schedule S


# Hyperparameters
The model training process is governed by certain pre-set values called *hyperparameters*:

## Learning rate (LR) 

is one of key hyperparameters. It defines how much current stochastic gradient estimate impacts the parameter update. The size of parameter update delta is 
proportional to LR. Smaller LR values lead to slower parameter evolution and slower convergence, but excessively large values of LR may break the convergence 
altogether as the gradient descent never commits to a particular local minimum. While LR is adaptively adjusted by the training algorithm to some extent, selecting a good initial value for it is important. A usual default initial value for LR is 0.1. Selecting the best value of LR is a fine art (see, for example, section 4.3 of Goodfellow et al.,"Deep learning", MIT Press, 2017).

## Minibatch size (MBS). 

Defines how many data samples is used for a single estimation of stochastic gradient. Larger values of MBS generally lead to more robust and more monotonic 
convergence but can potentially slow down the training process, as the cost of any one gradient estimation is proportional to MBS. 
A usual default value of MBS is 10.


## Training epochs, tolerance, gridlocks

"Epoch" means one complete pass through the scheduled training data.
The maximum number of epochs per a training thread (see below) should be capped. 
The training thread is defined to terminate (with the best known candidate parameters) when the maximum number of epochs has been executed. However such training
 would terminate earlier when misclassification rate on validation schedule falls below a chosen tolerance. Suppose, for example, that misclassification tolerance
 is 0.01 (1%); if on validation set of 2000 samples we are seeing fewer than 20 misclassifications, then the tolerance level has been achieved. A training thread
 also terminates prematurely if the validation score of the candidate model has not shown any improvement over several consecutive epochs (a gridlock). The logic
 for the gridlock termination is currently hardcoded.

## Measurements count

Estimating the training/validation scores and the components of the stochastic gradient on a quantum device amounts to estimating quantum state overlaps that requires multiple 
measurements of the appropriate observables. The number of measurements should scale as $O(1/\epsilon^2)$ where $\epsilon$ is the desired estimation error.
As a rule of thumb, the initial measurements count could be approximately $1/\mbox{tolerance}^2$ (see definition of tolerance in the previous paragraph). One
would need to revise the measurement count upward if the gradient descent appears to be too erratic and convergence too hard to achieve.

## Training threads

The likelihood function which is the training utility for the classifier is very seldom convex, meaning that it usually has a multitude of local optima 
in the parameter space that may differ significantly by quality. Since the SGD process can converge to only one specific optimum, it is important to explore 
multiple starting parameter vectors. Common practice in machine learning is to initialize such starting vectors randomly. The Q# training API accepts an 
arbitrary array of such starting vectors but the underlying code explores them sequentially. On a multicore computer or in fact on any parallel computing 
architecture it is advisable to perform several calls to Q# training API in parallel with different parameter initializations across the calls.