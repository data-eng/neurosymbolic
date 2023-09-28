# Concept Whitening

Paper: rudin-etal:2020

Code: https://github.com/zhiCHEN96/ConceptWhitening

_Concept whitening (CW)_ replaces the batch norm layer between the
feature extraction layers and the classfication layers with a CW layer
that forces the activations of the features to "align" with a
pre-defined, fixed set of concepts. The concepts are flat labels,
each defined by a set of "characteristic" instances. No guidelines are
provides wrt. what makes an instance characteristic, or how the method
suffers from bad choice of instances when defining labels.

Training is organized by alternating many (19 in the paper) classifier
training epochs where features & CW are frozen with one CW-layer
training epoch where the features are frozen. The method builds on
pre-trained feature extraction networks; This is not obligatory, and
the whole network could, in principle, be updated during the epochs
that learn the end-goal but the authors use pre-trained vision
networks and do not discuss the impact of starting from scratch.

The CW is trained by solving the linear optimization problem of
finding a transformation upon the output of the feature extraction
layer such that the new latent space has the "alignment"
property. This means that there is a CW activation is that higher for
instances of a given label that for instances of any other
label. There is no notion of representing in this new space any
hierarchy, similarity, or any other organization between labels.
Furthermore, the optimizaition task is defined slightly differently
that what is epxressed in the text: Instead of making explicit that an
activation must be higher for instances of a label than for instances
of any other label, it maximizes the activation for instances of a
label without looking across labels.

Possible experiments:

Define superset/subset labels, e.g. "person", "woman", and observe
what happens.
