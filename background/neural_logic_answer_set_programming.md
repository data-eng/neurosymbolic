# Neural Logic and Answer Set Programming

____
**All works below aim to propose methods that can train a neural network with the given background knowledge.**

## DeepProbLog

Paper: manhaeve-etal:2018

Code: https://github.com/ML-KULeuven/deepproblog

 *DeepProbLog* is a probabilistic logic programming language, that extends ProbLog, as it incorporates deep learning by means of **neural predicates**. 
 The neural predicate represents probabilistic facts whose probabilities are parameterized by neural networks. DeepProbLog supports (i) both symbolic and subsymbolic 
 representations and inference, (ii) program induction, (iii) probabilistic (logic) programming, and (iv) (deep) learning from examples.

Specifically, it has two components connected via neural predicates (neural annotated disjunctions): the neural component and the symbolic component. 
These components treat each other as black boxes.  The symbolic part consists of a ProbLog program, which is a set of rules and ground probabilistic facts. 
DeepProbLog inherits ProbLog's semantics and, to some extent, its inference. DeepProblog computes the probabilities of the neural predicates via neural networks, 
as opposed to ProbLog, which updates the probabilistic facts using Algebraic ProbLog and semirings.
The symbolic part calculates the loss and its gradient with respect to the output of the neural network. This information is used for backpropagation to 
update the weights of the neural network, enabling it to compute the probabilities of the neural predicates more accurately.

Despite the language's expressiveness, training can be time-consuming due to ProbLog's inference mechanism. For each query, 
this mechanism involves grounding the logic program, rewriting the grounded logic program into a propositional logic formula, 
compiling the formula into a Sequential Decision Diagram (SDD), and evaluating the SDD to calculate the success probability of the query. 
As a result, these steps must be performed for every data point during training.


## DeepStochLog

Paper: winters-etal:2022

Code: https://github.com/ML-KULeuven/deepstochlog

*DeepStochLog* is an optimized version of DeepProbLog based on stochastic definite clause grammars. It scales well 
(certainly better than its predecessor) and demonstrates good accuracy in various neural symbolic computation tasks. 
DeepStochLog utilizes resolution to derive a goal G from a sequence T, resulting in an SLD resolution tree. However, 
since SLD resolution involves proving many intermediate goals multiple times, this framework applies SLG resolution and
tabling to prevent redundant proofs and the recomputation of components within the corresponding AND/OR circuit. This 
is the primary reason why DeepStochLog scales better than DeepProbLog. Additionally, DeepStochLog is based on 
computationally more efficient random walk semantics, as opposed to the possible world semantics utilized by DeepProbLog
and NeurASP.


## NeurASP

Paper: yang-etal:2020

Code: https://github.com/azreasoners/NeurASP

*NeurASP* integrates answer set programs with neural networks, similar to the approaches mentioned earlier. 
It employs the neural network's output as the probability distribution over atomic facts in answer set programs, 
enabling the fusion of sub-symbolic and symbolic computation.

One distinction from DeepProbLog and DeepStochLog is its utilization of the (clingo) ASP solver instead of circuit 
construction. NeurASP calculates the probability of a set of observations and utilizes this information to compute 
and update the neural network's parameters, maximizing the log-likelihood of observations within the extended NeurASP 
program. In certain use cases, it proves to be less time-consuming during training compared to DeepProbLog, as 
generating the SDD is more time-consuming than enumerating stable models, which NeurASP efficiently handles.

## SLASH

Paper: skryagin-etal:2023

Code: https://github.com/ml-research/SLASH

*SLASH* extends the concept of the other Deep Probabilistic Programming Languages by introducing a +/− notation for answering various types of probabilistic queries. It is based on answer set programming (ASP). Its scalability is achieved by pruning the stochastically insignificant parts of the (ground) program, speeding up reasoning without sacrificing the predictive performance.
