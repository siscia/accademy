---
title: Statistic
layout: post
---

# Statistic

In the first lesson we are going to define basic elements that will need later.

We define `Probability` as the proportion of time an event will occur in the long run.

In the `long run` is not a precise and some ambiguities may be present, the best approximation could be as we approach infinity.

Since in the real world is impossible to approach infinity we can use the measure `Relative Frequency` as approximation of the probability.

We define the `Relative Frequency` as the ratio between the observed successful event and the attempt we made.

As the number of attempt we made approach infinity the relative frequency will approach the probability.

## Inference

Suppose that we toss a coin 10 and suppose that we obtain 10 heads, it will be fair to ask if the coin is a fair one.

Of course, it is possible that a fair coin will yield 10 times a head, but how likely is that ?

Let's try to answer such question.

We define the `Null hypothesis`, H0, as if the coin is fair.

If the coin is fair, then the probability of obtain an head is P(Head) = 0.5

Now we define the `Alternative hypothesis`, Ha, given the Null hypothesis what is the probability that we observed the result we had.

In this case 10 toss of a coin that yield 10 head, has a probability of:

A = {10 toss of a coin yield 10 head}

P(A) = P(Head) ^ 10 = 0.5 ^ 10 = 0,000976563

or P(A) = 1/2 ^ 10 = 1/1024

This means that the probability to obtain 10 heads is one every 1024 attempt.

If such probability is small enough we can conclude that there is something wrong, in our case an unfair coin.

`small` again is not very precise and is very open to interpretation, in statistic however the value of 5% is wildly accept and used.

Going back to the example we can see that the probability of the alternative hypothesis is P(A) = 0,000976563 = 0,0976563 % way smaller that 5% so we can conclude that the coin is not fair.

## Probabilistic Model

We define the `Experiment` as the procedure that let us observe an event.

The `Event`, (outcome of the experiment) is defined as simple or compounded.

A compounded event can be decomposed is simple events.

More abstractly we can defined a `Sample point` as the projection in an abstract field of the simple event.

The sum of all possible distinct sample point is called `Sample Space` that we denote with `S`

The sample space can either be discrete or continuous.

## Axioms of Probability

Given P(A) as the probability that an event A occur in the Space S, the following hold true.

* P(A) <= 0

* P(S) = 1

* if A1, A2,... are disjoint event in S, then P(A1 u A2 u ...) = /sigma_1 P(Ai)

