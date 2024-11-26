## Data Mining with Twitter Dataset about Covid-19

### Background of Study

The WHO declared the COVID-19 as a world health emergency in January 2020[1], while on January 20, the first case of COVID-19 in the US was confirmed and announced to the public [2]. The unpredictability and limited understanding of COVID-19 have led to a sharp increase in the usage of social media, leading to a substantial increase in the number of posts, including topics related to social, political and economic life. Therefore, understanding how the public discusses the epidemic on social media is crucial, which helps to understand the public's psychological state, level of attention and perception towards the epidemic.

According to [3], 68% of American adults rely on social media for news. Twitter, as one of the popular social platforms in the world, is especially well performed in sharing preventive health information and reports[4]. Research on the trend of public posting on Twitter is quite meaning for in identifying people's thoughts and opinions. However, the method of manually identifying information tweets requires high time and labor cost [5]. Natural Language Processing (NLP) is one of the effective methods for analyzing social media texts, extracting meaningful information from unstructured text data [6]. Therefore, the purpose of study is to use NLP technology to analyze Twitter discussions to gain a deeper understanding of the public's thoughts and viewpoints during the pandemic. We believe that it could provide valuable insights for coping with the COVID-19 epidemic and similar health crises in the future, and help to better understand the role of social media in crisis communication.

### Topic Introduction

In this study, a common topic modeling technique Latent Dirichlet Allocation (LDA) will be used to analyze approximately 160000 texts collected from USA to identify potential topics. This study helps analyzing the discussion on COVID-19 on social media, especially the views and trends on different topics, which also helps discover public's response to the COVID-19 epidemic and the role of social media in the spread of the epidemic. The research mainly focuses on:

1) Evaluate and compare Document Term Matrix and TF-IDF processed data as input to LDA to analyze their effectiveness.
2) Select the optimal model to extract potential topics and conduct exploratory analysis about the changes and correlations of topics in time, space, and emotions.

### Data Prepocessing

#### Document-TermMatrix

DTM is a text data representation method that divides the text content into documents and word lists, meaning that the relationship between documents and words will be encoded as a matrix. When building DTM, the 'corporate. Dictionary' of the Gensim library is used to create a word dictionary, while the 'doc2bow' is used to convert documents into a bag of word, ultimately generating a document-word bag matrix. DTM is an intuitive method for representing text data, and the number of occurrences or weights of each word in the document can be counted, making the text data easier to understand and analyze.

#### TermFrequency-InverseDocumentFrequency

TF-IDF is used for measuring the importance of words in documents, combining word frequency and inverse document frequency. When building TF-IDF, the ‘TfidVectorizer’ of the sklearn library was used to calculate the TF-IDF value. Among them, 'max_ df' is set to 0.8 and 'min_ df 'is set to 10 respectively to control the maximum and minimum document frequency thresholds.
TF-IDF considers the importance of words in documents, not just their frequency. This means important terms that appear in specific documents will have higher weights, which helps capturing the contribution of words. Simultaneously, TF-IDF algorithm can filter out overly common or rare vocabulary, thereby reducing noise and improving model performance.

### LDA topic modeling

Latent Dirichlet Allocation (LDA) is a probabilistic topic model that infers the distribution of document topics for topic clustering or text classification. It can automatically discover topic structures in text data without prior knowledge, which is beneficial for large-scale datasets to reveal hidden themes and topics. Meanwhile, as our dataset does not have labels for topics, therefore selecting this unsupervised learning algorithm LDA is suitable for this dataset.
In this study, LDA was used to analyze the topics of the covid related tweets. We used the 'LdaModel' from the Gensimk library to construct LDA models, using text processed through DTM and TF-IDF features as input, and set the range of k to 3-12, where k is the number of possible topics.

### Choose the best model

#### Perplexity

One of the evaluation indicators, perplexity, is used to measure and capture the degree of fit of the topic model to an unseen new text. Generally speaking, the lower the degree of confusion, the better the performance of the model on unprecedented data. We use the function "log_perplexity" that comes with the sklearn library to calculate confusion.

#### Coherence

Coherence refers to the degree of connection between words within a topic, and is a measurement of the interpretability and relevance of the generated topic. Generally speaking, the consistency range is between 0 and 1, and the higher the score, the more meaningful the topic is. There are many ways to measure coherence and the method chosen in this research is c_v. Moreover, we use the 'CoherenceModel' in the gensim library to calculate consistency. Having find the best topic model, we could further extract keywords under each topic and present them clearly through visualization methods such as drawing word clouds. This helps to conduct indepth research on the theme content in the future, helping to explore and understand the connotation of each topic.

### Find dominant topic for each document

The output of LDA includes the distribution probability of different topics in the document, so finding the dominant topic in the document is needed, which is the topic with the highest probability value associated with the document. After obtaining the output of LDA, we can group the entire corpus of documents and place them with the highest probability, which is to assign each document to their own dominant theme.
