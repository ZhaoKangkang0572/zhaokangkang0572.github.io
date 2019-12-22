---
layout: post
title: Related work
category: Temporal-Relation
tags: Introduction
description: second part of my works  
---
@Author
Guoliang Ji, Kang Liu, Shizhu He, Jun Zhao

AAAI 2017

#### 1. Related
Machine learning approaches have obtained very high performance in many NLP tasks, such as question and answering, machine translation and so on. Machine learning methods for NLP  aim at using machine learning algorithms the meaning of sentences, paragraphs and documents. Machine learning approaches also applies to temporal relation classification task.
Similarly, those feature-based methods were wildly used by researchers in classifing temporal relations and have achieved great success.
At first, to make machine learning algorithms work, 
convert unstructured text into numeric representation that can be understood by machine learning algorithms
However, with NN-based method, we can simply feed unstructured text into ,instead of complex hand creaft features, and features will be automatically calculated by the neural network.
In this part, we will introduce those two kinds of method respectively,
##### Feature-based methods
In earlier studies, feature-based methods are  most popular methods in natural language processing. The main purpose of feature-based methods is convert unstructured text into numeric representation that can be understood by machine learning algorithms.
Including term frequency-inverse document frequency(TF-IDF), Bag of Words (BOW) so on. 
While they are effective methods for extracting features from text
Sometimes, feature engineering is even more imprtant than algorithm itself.

Researchers provide different feateures for their machine learning methods/

Chambers and Jurafsky [1] provides a  logistic regression classifiers to temporal relation classification. Their feature engineering is based on deep syntactic parser, 
With deep syntactic parser, they extract features by exploiting path relations between event words  across different structures:
1)path and the lengths between event words in phrase structure trees
2)pathes and subgraphs between event words in predicate argument structures
For instance, **Mirza et al. [11]** employed L2-regularized logistic regression to classify temporal relations by incorporating word embeddings features and their experiments proved its effectiveness. 

However, Mirza&Tonelli view feature engineering with a different perspective, they claim that comparing with complex features based on semantic role labelling and deep semantic
parsing, a simple feature set can be more effectively.[12]






It is always difficult to descorve explicit markers for describeing temporal relations, which is always the most difficult part to temporal relation. To ease that, [12]  find that distributional semantic information about event words can benefit supervised classification of other types of pairs.

resorting to features that focus on the semantic content of the event words may be very beneficial for inferring implicit relations

However, most of them rely on manually annotated features and rules which are very time consuming and laborious. 
For instance, to improve temporal ordering, Chambers and Jurafsky [1] summarized more than 20 features ranging from lexical grammatical aspects including
Moreover, some features require a large quantity of manually tagged attributes in the corpus. 


##### NN-based methods

Recently, thanks to the success of neural networks, various of neural networks-based models such as CNNs [8] and RNNs [14] have been employed to address temporal relation classification. Neural networks-based models have many advantages over feature-based methods. For example, feature-based methods need the complex hand-crafted rules to ensure high performance, while neural networks-based models can not only automatically learn the rules but also achieve higher performance simply with more input data. 
CNNs , RNNs and their variants are widely used in temporal relaiton classification.

 > CNNs

> RNNs


> attention unit
However, aforementioned neural network models [8,14] ignore that not all words contribute equally in classifying the right relation. Consider the sentence in Example 1, some words (e.g. had, been) are obviously more important than other words (e.g. meeting, Trump) in deciding the correct temporal relation.