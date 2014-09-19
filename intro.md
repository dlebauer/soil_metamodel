## Introduction

At the ecological forecasting workshop, we discussed using Stan for data assimilation in Ecosystem models. 
I proposed that ecosystem models we were working with (e.g. ED2, BioCro), are too complex to make it worthwhile (and require a lot of time and money) to re-implement (e.g. within Stan). The workflows group was in some ways a set of tools that embed simulation models within workflows for making inference (e.g. PEcAn).

Unlike the modern cast of ecosystem simulation models, the soil carbon dynamics routines are relatively simple, and can be further simplified (Bolker et al 1998, Manzoni and Porporato 2008, Sierra et al 2012). 
This provides the opportunity to make advances in statistical computing as well as ecosystem science. 
This suite of linear models have been implemented (e.g. in the SoilR package and in a set of C functions following Xia et al 2013), and should be straightforward too reimplement again if neither of these are suitable for integration into Stan, and in any case we will want to add models that are more complex to this (e.g. models that can not be decomposed (or at least no one has done this) into a matrix operation because there are two-way feedbacks among pools). 

A key challenge of this inference will be sampling across models of varying complexity and parameters. 

