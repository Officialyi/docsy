---
title: Testing Models
description: Statisticians have a few different ways to determine the significance of an experiment. Here's a breakdown of 2 models utilized.
# categories: [testing, experimentation]
weight: 5
---

## Bayesian Inference:
In the context of hypothesis testing, Bayesian inference involves comparing competing hypotheses by specifying separate prior distributions for each hypothesis and computing the marginal likelihoods of the models. The ratio of the marginal likelihoods is known as the Bayes factor, which quantifies the extent to which the data supports one hypothesis over another.

## P-Value:
In frequentist inference, the p-value is a measure of the strength of evidence against a specific null hypothesis. It represents the probability of obtaining data as extreme or more extreme than what was observed, assuming that the null hypothesis is true.

* Note on P-value testing: p-value tends to be a ‘standard practice’ for observed significance level, but there are studies that show the inaccuracy and potential bias of relying on p-values to generate conclusions. [article](https://people.eecs.berkeley.edu/~jordan/courses/260-spring09/readings/berger-sellke.pdf)


Bayesian inference and p-value significance (frequentist inference) are two different approaches to statistical inference, each with its own strengths and applications. The choice between Bayesian inference and p-value significance depends on various factors, including the specific research question, available prior information, and the researcher's preferences.

Here are some scenarios on use of Bayesian and p-value significance:

| P-Value [[article](https://online.stat.psu.edu/statprogram/reviews/statistical-concepts/hypothesis-testing/p-value-approach) , [video](https://www.youtube.com/watch?v=KS6KEWaoOOE)]      | Bayesian [[article](https://academic.oup.com/ntr/article/22/7/1244/5613971) , [video](https://www.youtube.com/watch?v=Ma1G4-aKR9A)]         |
|-----------|-----------------|
| Large sample sizes: Frequentist methods are known to perform well in large sample settings. Asymptotic properties of frequentist estimators, such as consistency and efficiency, are well-established. When dealing with a large amount of data, frequentist methods may provide precise estimates and hypothesis tests without the need for strong prior beliefs.   | Complex models or small sample sizes: Bayesian inference can handle complex models more easily, especially when the likelihood function is not analytically tractable. It can also provide more reliable results when dealing with small sample sizes. In such cases, Bayesian methods, such as Markov chain Monte Carlo (MCMC) techniques, can be used to estimate posterior distributions even when traditional approaches may be problematic.        |
| Hypothesis testing in a single direction: Frequentist methods can handle one-sided hypothesis tests more straightforwardly. If the research question is specifically focused on determining whether an effect is either positive or negative, frequentist inference provides a more direct and traditional framework for testing such hypotheses.   | Bayesian inference provides a natural way to quantify and propagate uncertainty. It allows for decision-making based on posterior probabilities and the calculation of expected values or utilities. This is useful when decisions need to be made considering trade-offs, risks, and uncertainties.        |
| Simplicity and computational efficiency: Frequentist methods often have simpler computational requirements compared to Bayesian methods, especially for complex models. Frequentist procedures, such as maximum likelihood estimation, have closed-form solutions in many cases, making them computationally efficient and easier to implement.   | Decision-making and updating of beliefs: Bayesian inference naturally lends itself to decision-making by considering the relative probabilities of different hypotheses. It allows researchers to update their beliefs as new data become available, which can be particularly useful in sequential analysis or adaptive experimentation.        |

Ultimately, the choice between Bayesian inference and p-value significance depends on the specific research question, available data, prior knowledge, and the researcher's preferences.