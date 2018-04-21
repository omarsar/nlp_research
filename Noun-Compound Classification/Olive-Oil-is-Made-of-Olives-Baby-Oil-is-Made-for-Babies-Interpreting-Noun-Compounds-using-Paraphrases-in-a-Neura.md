# Olive Oil is Made of Olives, Baby Oil is Made for Babies: Interpreting Noun Compounds using Paraphrases in a Neural Model
---
***Basic Overview***
This [paper](https://arxiv.org/pdf/1803.08073.pdf) addresses an important NLP task — the automatic interpretation of the relation between the constituents of a noun compound.

***Motivation***
Consider the following noun compound examples: ***olive oil*** and ***baby oil***. You can observe that the word ***“olive”*** in the phrase ***“olive oil”*** describes a SOURCE relation, and the word ***“baby”*** in ***“baby oil”*** describes a PURPOSE relation. This distinction is important because it can be used for various applications that require complex text understanding capabilities.

***Example***
Imagine you asked Google search what olive oil is made up of. If Google search is smart it should response “olive”. Now imagine you asked Google what baby oil is made up of. Definitely not babies! The answer should be other ingredients of oil or the main ingredient of oil. This is a very important distinction! It’s a challenging task because the meaning of both types of oils is not easy to interpret given the meaning of its constituent words.

Can you think of more examples? Try and you will see why this area of NLP research is important. As an NLP researcher, I can even see how this is useful for disambiguating between sentiment phrases. (More on this in another article.)

***Literature Review***
Two very common approaches are used to address this issue: ***paraphrases*** and ***noun-compound representations***. The first approach maps relationships between constituents and the latter approach makes use of distributional representations of the individual constituents. (Don’t panic, I will explain what they mean in a little bit.)

A more recent work [(Dima, 2016)](https://doi.org/10.18653/v1/W16-1604) showed that constituent embeddings are effective to represent the noun-compounds (hereinafter also referred to as NCs. The main reason for why it works is attributed to a phenomenon referred to as [lexical memorization](http://www.aclweb.org/anthology/N15-1098).

***Contribution***
This paper proposes a neural paraphrasing approach that combines path embeddings (which represents the relationships between NCs) and distributional information (obtained directly from word embeddings) to conduct the NC classification task. The authors also experiment with settings where *lexical memorization* is avoided to show that their method is more robust and their results are not attributed to this phenomenon. 

***Model***
The authors used [HypeNET](http://www.aclweb.org/anthology/P16-1226) to learn patterns connecting the joint occurrences of instances of constituents in a corpus. These are also referred to as *path embeddings*.

Three models were combined to perform the NCs relation classification: *path-based*, *integrated*, and *integrated-NC*. Each model incrementally adds new features (in this case different distributional inputs) which essentially adds more contextualized information to the overall input vector. This process can be seen more clearly in the diagram below:

![](https://d2mxuefqeaa7sj.cloudfront.net/s_AC1B3978E73E9CD63DF4B2D2FE8C2BC7240AA65B01D3F5F88EE9E9D058C2A827_1524054559735_file.png)


The path embeddings (colored purple in the diagram) are learned using a vanilla LSTM with input vectors representing a concatenation of the following vectors: *lemma*, *part-of-speech tag*, *dependency label*, and *direction vectors*. (See paper for more details). NC labels (relations) are obtained using a [distant supervision](https://en.wikipedia.org/wiki/Semi-supervised_learning) approach via the output of the LSTM.

***Evaluation***
Two datasets, obtained from [Tratz (2011)](http://digitallibrary.usc.edu/cdm/ref/collection/p15799coll3/id/176191), were used to evaluate the proposed neural paraphrasing model. Several comparison models were proposed, including several baseline models and re-trained models adopted from previous work and the state-of-the-art method. (See paper for more details on the experimental setup).


![](https://d2mxuefqeaa7sj.cloudfront.net/s_AC1B3978E73E9CD63DF4B2D2FE8C2BC7240AA65B01D3F5F88EE9E9D058C2A827_1524057286629_file.png)


Table 1 shows that for most cases the integrated models (*Int* and *Int-NC*) outperform all other models on the using different data splitting strategies (shown in Split column). There is very little difference between the results obtained from the ***Int*** model and ***Int-NC*** model, indicating that the NC embeddings did not contribute much to the classification task.

***Analysis***
Further analysis was conducted on the random splitting strategy to analyze variations in results of the different models. In Table 3, you can observe some of the relations that yielded reasonable performance (e.g., MEASURE and PERSONAL TITLE)


![](https://d2mxuefqeaa7sj.cloudfront.net/s_AC1B3978E73E9CD63DF4B2D2FE8C2BC7240AA65B01D3F5F88EE9E9D058C2A827_1524058336820_file.png)


The authors also discovered that complex relations perform poorly such as LEXICALIZED for the NC, “*soap opera”* and OBJECTIVE for NC, “*recovery plan”.* (See more interesting examples in the paper).

Table 4 below provides examples of NC embeddings obtained from the test set (*left*) and an example of the most similar NC in the embeddings (*right*). The authors observed that only 27.61% of the NCs were mostly similar to NCs with the same label. They attributed this behavior to inconsistent annotations rather than quality of embeddings. 

![](https://d2mxuefqeaa7sj.cloudfront.net/s_AC1B3978E73E9CD63DF4B2D2FE8C2BC7240AA65B01D3F5F88EE9E9D058C2A827_1524059277002_file.png)


***My*** ***Further Ideas and Conclusion***

- Visualize NC vector embeddings to observe relation clusters and patterns that may have similar properties.
- Study more closely the lexical memorization phenomena, which the paper helps to *“slightly”* address using the path-based component of the whole model. 
- Overall, the performance was improved but there is still a lot more room for improvement in terms of data quality and modeling. 
- The NC embeddings are not helping the current model, so it provides a feasible future research direction without changing the overall structure of the model.

***Resources***

- [The original paper](https://arxiv.org/pdf/1803.08073.pdf) | [*Code Repository*](https://github.com/tensorflow/models/tree/master/research/lexnet_nc) *(Tensorflow implementation)* 


