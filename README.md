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

<div align="center">
  <img width="671" alt="截屏2024-11-26 18 42 47" src="https://github.com/user-attachments/assets/8c3d02c3-d2ba-43d1-b23b-5a9b85de5729">
</div>


#### Coherence

Coherence refers to the degree of connection between words within a topic, and is a measurement of the interpretability and relevance of the generated topic. Generally speaking, the consistency range is between 0 and 1, and the higher the score, the more meaningful the topic is. There are many ways to measure coherence and the method chosen in this research is c_v. Moreover, we use the 'CoherenceModel' in the gensim library to calculate consistency. Having find the best topic model, we could further extract keywords under each topic and present them clearly through visualization methods such as drawing word clouds. This helps to conduct indepth research on the theme content in the future, helping to explore and understand the connotation of each topic.

<div align="center">
  <img width="654" alt="截屏2024-11-26 18 43 37" src="https://github.com/user-attachments/assets/8958f9de-bd74-496a-a3d3-3d0eb680076b">
</div>

### Find dominant topic for each document

By selecting the combination of TF-IDF method and 10 topics, the correlated best model is chosen based on the coherence as the evaluation indicator.

The output of LDA includes the distribution probability of different topics in the document, so finding the dominant topic in the document is needed, which is the topic with the highest probability value associated with the document. After obtaining the output of LDA, we can group the entire corpus of documents and place them with the highest probability, which is to assign each document to their own dominant theme. The word cloud for each potential topic are:

<div align="center">
  <img width="398" alt="截屏2024-11-26 18 44 44" src="https://github.com/user-attachments/assets/98820408-5226-4b65-9b7d-20f7d38e6ec2">
</div>

Then I made a table which shows the topic clusters formed by LDA, as well as the number of documents belonging to each topic and topic keywords. Possible topics are manually annotated based on topic keywords. Only four topics have certain interpretability, namely topic 0, 2, 7, and 9. It can also be observed that Topic 5 has the highest frequency of occurrence in text data from table [1], indicating topic 5 is the dominant topic in the entire dataset, and its content may be related to the focus of the study or the characteristics of the data source. Theme 9 and Theme 0 appear less frequently, but they may still play important roles in specific fields or contexts, thus possessing special importance.

<p align="center">

| Topic | Number of tweets | Possible topics | Topic keywords |
|:------|:-----------------|:----------------|:---------------|
| Topic 0 | 10229 | Covid Education Infrastructure | Recit, bologna, sat, eftour, specif, pa, virushygien, dakota, 6549lmartin, usouthflorida, childcar, minut, delet, fiscal, iowacaucas, stellar, publish, kcmo, statement, infrastructur |
| Topic 1 | 1536 | (Not Interpretable) | Blo, stood, whack, sold, snapchat, hysteria, dearth, gs5734, ge, virul, Thailand, timecovid19, liabil, 25, startl, dudeklinda, stricken, golden, wallstreet, putempcduk |
| Topic 2 | 9243 | Covid Political Spread | strand, forecast, beck, father, seed, chinaviru, withregram, 29, realdonaldtrump, everybody, bustl, youtub, buddi, editor, tempestchas, notso, indu, diseasethey, whirlwind, stronger |
| Topic 3 | 5923 | (Not Interpretable) | Coronaha, mixup, harrietnix, repercuss, eve, lrpow79, guid, imma, sc, debunk, univers, predict, flashlight, melt, oval, cdcgov, lonely, vintag, wgal, dwight |
| Topic 4 | 6047 | (Not Interpretable) | small, latter, preval, 05, techrose11, rhymestyl, choic, danlairdmd, toppl, seat, bexar, 1015, second, note, highwaymen, burk, eleven, forbidden, hog, kc |
| Topic 5 | 105711 | (Not Interpretable) | Phase, epic, newschannel9, omw, buri, malthu, imfunni, doctorwho, squiggli, Stanford, liner, memori, caresha, dream, dod, wheel, 780, batteri, 2, propheci |
| Topic 6 | 2667 | (Not Interpretable) | Gag, incl, narrow, 3d, bannon, backtrack, graph, forgodandcount9, mmerkington, 69, fell, reciev, thetetonway, scam, cum, 12000, sputter, decenc, roddreh, meltdown |
| Topic 7 | 8958 | Medical Treatment Channel | surgeon, psbj, felipaythebil, proverb, dvillella, 153032, static, wil, unfit, future, mega, 75, nyc, creator, lovelyy_jul, audio, channel, xle, 80000hour, refuge |
| Topic 8 | 4634 | (Not Interpretable) | Shock, cremat, sweati, anywhere, heyassant", beta, forwardthink, transfer, tabl, dollarsgo, gooooo, diamondeugene1, tarmac, jake, preblam, uncheck, delta, msnbc, modest, horni |
| Topic 9 | 10874 | Covid News Report | Westwingreport, dispos, episode, sslection, angl, lite, fixat, globalspartan, djdretakingover89, drunk, two, jare, thotsunemiku, exclus, 2nd, contribut, anima, cannabi, simul |

</p>

### Further analysis of topic trends

By combining topics for further temporal, spatial, and emotional analysis, more comprehensive insights can be obtained to better understand discussions, trends, and emotional changes on social media during the pandemic.

#### Time analysis

We can intuitively compare the quantitative and instantaneous number changes of different topics over time based on the below 2 images. The number of posts on each topic has a certain similarity in periodicity. Specifically, during the period from February 1st, 2020 to February 22nd, 2020, the number of posts was relatively small, while by March 17th, 2020, the number of posts increased to varying degrees, which sharply decreased from March 17th to March 20th, and then significantly increased again. Some of the topics reached their peak post count around March 12th, while others reached their peak around March 28th. The peak and trough phenomena during this time period may be related to specific events or activities, and it is worth further research to understand the underlying reasons.

<div style="display: flex; justify-content: center; gap: 20px;">
   <img width="503" alt="左图" src="https://github.com/user-attachments/assets/106fd3a5-2510-4bd6-aa58-8f17fed2080b" style="width: 50%;" />
   <img width="506" alt="右图" src="https://github.com/user-attachments/assets/a20fdb2c-a291-43e8-a7b7-76c591ecf29b" style="width: 50%;" />
</div>

#### Spatial analysis

For spatial analysis, bar charts and geospatial maps are drawn to visually display the relationship between the number of posts and the state. It can be observed from figure below (left side) that regardless of the topic, California, Florida, Texas, New York, and Pennsylvania are almost always among the top five states in terms of post count. In figure below (right side), The distribution of these states is generally located in four directions of the United States: southeast, southwest, northeast, and northwest. Meanwhile, these geospatial maps also reveal an interesting trend that the number of posts in the eastern and western regions of the United States is generally higher than that in the central region, and the reasons for this phenomenon need further analysis.

<div style="display: flex; justify-content: center; gap: 20px;">
   <img width="394" alt="左图" src="https://github.com/user-attachments/assets/54f3cf7b-6036-4a76-b04e-723bc4081abe" style="width: 50%;" />
   <img width="352" alt="右图" src="https://github.com/user-attachments/assets/51e6f392-d2a1-4569-894d-a948c7d478cc" style="width: 50%;" />
</div>

#### Segment analysis

Eventually, I also conducted segment analysis under each topic. Overall, the emotions under each topic exhibit similar patterns. We can observe from figure below that most of the posts on each topic are neutral about the COVID-19, the proportion of which is about 50%. Among the rest of the population, people who have positive attitutes towards COVID-19 is slightly more than those who have negative attitudes. This may reflect that the understanding of the epidemic was not deep enough at the time, or that people were still in the wait-and-see stage.

<div align="center">
  <img width="395" alt="截屏2024-11-26 18 54 32" src="https://github.com/user-attachments/assets/f4726771-cbe2-4854-849d-071844277e7b">
</div>
