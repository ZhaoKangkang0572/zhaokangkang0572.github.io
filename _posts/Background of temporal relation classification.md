---
layout: post
title: Background of temporal relation classification
category: Temporal-Relation
tags: Introduction
description: first part of my works  
---
@Author
Guoliang Ji, Kang Liu, Shizhu He, Jun Zhao

AAAI 2017

#### 1. Introduction


#### 1.1 Begging
Temporal relation classification plays an important role in the field of natural language processing. Long short-term memory (LSTM) has been widely used to classify temporal relations. However, existing LSTM-based models usually fail to capture the important information by just using the final hidden state to produce the label. To overcome this drawback, we propose a simple attention-based LSTM model for the temporal relation classification task, which mainly focuses on the awareness of event words and time expressions in processing the final hidden state. We show that our approach outperforms the state-of-the-art on publicly available "Timebank-Dense" corpus. 




#### 1.2 Significance 
As a subtask of natural language processing (NLP), temporal relation classification has benefitted various NLP related tasks. Take news search [1] as an example, due to the rapid development of information technology, news on the Internet is exploding. Helping users to search for the news they want more quickly become a problem that needs to be handled. Temporal relation classification can be beneficial for timelines construction with which a search engine can provide more accurate results and tips. 

#### 1.3 Task Description
 The main task of temporal relation classification is to ordering temporal relations between events and temporal expression within a text. Here, we descripbe them in details.
1.3.1 Event in temporal relation classification
News text
新闻总是不可避免地带有各种事件，而这些事件带有时间属性。例如在下面的新闻中，出现了XXX，XXX等几个事件，而且隐藏

1.3.2 Temporal expression
为了使得报导更加准确，报纸在描述事件时通常会带有时间描述，例如
2.1.3.3 Temporal relation

Temporal relation classiﬁcation aims to identify temporal relations (e.g. BEFORE, OVERLAP, or AFTER) between events and time. For instance, the following sentence shows an example of BEFORE relation between event said and event barred. 

>Example 1: He said he believed the "conditions for a meeting" between Mr Trump and Mr Rouhani "in the next few weeks" had been established. 



#### contributions
Over the years, several feature-based methods have been explored to address temporal relation classification [2,3,4]. However, most of them rely on manually annotated features and rules which are very time consuming as well as labor intensive. For instance, to improve temporal ordering, Chambers and Jurafsky [5] summarized more than 20 features which range from lexical aspect to grammatical aspect. Moreover, some 
features require a large quantity of hand tagged attributes in corpus. 

Recently, due to the success of neural networks, various of neural networks-based models such as CNNs [6] and RNNs [7] have been employed to address temporal relation classification. Neural networks-based models have many advantages over feature-based methods. For example, feature-based methods need complex hand-crafted Rules to ensure high performance, while neural networks-based models can automatically learn the rules as well as achieve higher performance simply with more input data. 

However, neural networks mentioned above [6, 7] ignore that not all words contribute equally in classifying the right relation. Consider the sentence in example 1, some words (e.g. had, been) are obviously important than other words (e.g. meeting, Trump) in deciding the correct temporal relation. In this paper, we explore to use a word attention to identify such important words in a sentence. The contributions of this paper can be summarized as follows. 

1. We employ bi-LSTMs to extract sentence level features from the input text. 
2. We explore an attention unit to identify critical words by using event expressions and time expressions. Our proposed attention unit are able to detect which parts are important in the input sentence for classifying temporal relation correctly. 
3. We conduct experiments using the "Timebank-Dense" corpus. The experimental results show that the proposed model can effectively improve the performance. 

1.4

The rest of this paper is organized as follows. Section 2 summarizes some related works which include feature-based methods and neural network-based methods. Section 3 presents our model in detail. Section 4 describe some experimental settings. Section 5 details the experimental results. The summary of our paper and future work are concluded in section 6. 