# Exercise 3 - Machine Translation
This exercise is about **data management** and **Machine Translation**. You have to answer questions by commenting on your answers.

Suppose you work for a company that offers Machine Translation to its customers.

You have access to a large amount of translation data (i.e., parallel files containing a sentence in a source language and the corresponding translation in the target language). Some of this data comes from public datasets, others have been produced by professional translators working for your own company.

## Questions:
1. How would you design a data pipeline for a Machine Translation system? (e.g. necessary steps, main challenges, etc.)
2. What would you do to collect new and good quality data from the web? Assume you want to use them to train a neural model for Machine Translation.
3. Suppose that low quality translations created by the system are post-edited by professional translators. How would you use this process to monitor the quality of the Machine Translation system?


## Responses:

1. 
    It needs many steps:
    - **Data collecting**: collect the data from the web, from the customers, from the translators, etc. It's challenging because there are many low resources languages, and the data is not always available.
    - **Data cleaning**: remove the noise, such as the html tags, normalize the punctuation, the numbers, the special characters, etc. It might be complex and really time-consuming. https://www.defined.ai/blog/machine-translation-101-part-2/
    - **Data splitting**: split the data into training, validation and test sets. It's important to have a good split, and to have a good representation of the data in each set. So mixing the data from different sources and different translators is important. 
    - **Training**: train the model on the training set. 
    - **Evaluation**: evaluate the quality of the MT system using human and automatic evaluation. The human approach it's slower but more accurate. Meanwhile, the automatic approach can use many metrics, but it's not always accurate. https://www.intechopen.com/chapters/68953

2. I would not collect everything from the web but search for good authority sources and collect the data from there. While also using the data from the customers and the translators. 
It's important to have a good representation of the data, so gathering from different domains would be really beneficial.
We also need to keep track of the data to align the source and target sentences otherwise the NMT model will not be able to learn.

1. We can use the post-edited data to retrain the model and improve the quality of the MT system. Not only that, but we can also use the post-edited data to evaluate the difference between the MT system and the human translation. It might be useful to get statistics about the errors and the corrections because we might lack data related to those errors.


