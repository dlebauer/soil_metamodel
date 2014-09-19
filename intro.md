## Introduction

At the ecological forecasting workshop, we discussed using Stan for data assimilation in Ecosystem models. 
I proposed that ecosystem models we were working with (e.g. ED2, BioCro), are too complex to make it worthwhile (and require a lot of time and money) to re-implement (e.g. within Stan). The workflows group was in some ways a set of tools that embed simulation models within workflows for making inference (e.g. PEcAn).

Unlike the modern cast of ecosystem simulation models, the soil carbon dynamics routines are relatively simple, and can be further simplified (Bolker et al 1998, Manzoni and Porporato 2008, Sierra et al 2012). 
This provides the opportunity to make advances in statistical computing as well as ecosystem science. 
This suite of linear models have been implemented (e.g. in the SoilR package and in a set of C functions following Xia et al 2013), and should be straightforward too reimplement again if neither of these are suitable for integration into Stan, and in any case we will want to add models that are more complex to this (e.g. models that can not be decomposed (or at least no one has done this) into a matrix operation because there are two-way feedbacks among pools). 

A key challenge of this inference will be sampling across models of varying complexity and parameters. 

---


### Unknown parameters

In that particular model (Sierra et al 2013, eqn 2), which are parameters are unknown? 

1. squiggle = f(temperature, water, ...); 
 * squiggle may have many different and unrelated functional forms and parameterizations
 * most letters other than T and M, many of the constants in Table 1 
2. k, the decay rate, can be loosly related to enzyme activity data
3. Ratio of C1:N, can be loosley related to (priors set based on) density fractionation (described below)

### I couldn't tell if it was the squiggle only or the squiggle and some of the other components. 

squiggle could be a prior on the probability of the selection, combination, and probabilities / skills of models in Table 1.  

We can also measure the maximum rates, temperature responses, and moisture responses of the squiggle (Sierra eqn 9,  table 1) has the different models of temperature and moisture responses.

```
squiggle ~ f(temperature, water)

f(temperature, water) ~ multinomial( , , P(Temperature_Model 1:N * Moisture_Model_1:N))
```

We want to estimate P(different soil C models) ~ f(temperature, moisture)

dC/dt ~ some probability of each model, with heirarchical time dependent models on the vector of model probabilities

> dcdt_model *  1:N multinomial( n_dcdt, k_dcdt, P(dcdt_model 1:N) ) 

 (PH, Clay, other factors are also very important ... but these relationships are less well understood ... )


### Observinng Total Carbon, estimating pool sizes / distribution of fast, slow pools

We will know total carbon, e.g. C1 + C2 + ... CN. Individual C pools are not only 'unobserved', but 'unobservable' at this approximation of 1000s of compounds into fast, slow and versy slow decomposing. Unlike the substrates in pharmacological reactions, these are an approximation that limits scientific inference (e.g. a better mechanistic understanding; these equations will be mostly 'abiotic'; though 'adding the biology' to these models is what everyone wants to figure out how to do, in a robust manner. But reality is that these compounds are not only diverse, but they exist and interact within a matrix of soil, water, goo, microbes, roots, invertebrates in a way that has thus far been impossible to make sense of in a way that will make useful predictions. i.e. the spread (60Gt/yr) across global models in the IPCC in predictions of global dC/dt is greater than the mean (30Gt/yr) (off the top of my head. cite Dave Moore, Yiqi Luo). 

### Soil Fractionation

However, Jennifer referred to some data that she has that could be used to set priors on C1,C2,C3, i.e., C1 ~= 'stuff that floats on water", C2 ~= "stuff that floats on a dense liquid" and C3~= "stuff that does not float on either". 

### Enzyme Activities

Reference Allison, Moorehead & Sinsabaugh 

There are other metrics, e.g. the maximum value of the k's can be estimated by potential activity of enzymes that degrate C1:C3 - this would be in the dataset I mentioned, half of which is published in (LeBauer 2010) ... (the other half is a different species of litter). 

### Analogies / differences with models of Photosynthesis and gas exchange

and applications of this approach to modeling photosynthesis (models that are much more useful)


