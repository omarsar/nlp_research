# Exploring Emoji Usage and Prediction Through a Temporal Variation Lens
***Overview***  
Emoji usage has become a new form of social communication, which is important because it can help to improve communication systems, such as chat applications. This paper investigates the *usage* and *semantics of emojis* over time to analyze *seasonal variation* of emoji usage. In addition, they develop an emoji prediction model based on the time information.

***Contribution***  
Multiple emoji predictions studies have been carried out in the past (see notable work by [Felbo et al,., 2017](https://arxiv.org/abs/1708.00524)), but non have considered *temporal information*. Temporal correlation between emojis and seasonal events are explored and used to disambiguate emoji meanings.

***Example***  
Consider the leaf clover emoji (🍀), it is usually associated with good luck wishes all year round except in March, where it is mostly used to express event situations such as *parties* and *drinking* (due to St. Patrick day).

***Challenges***  
- This study demonstrates that temporal information is useful for emoji prediction even for emojis that are not associated with time (💪 and ❤️ ).
- Emojis are innately subjective, which is why it is difficult to analyze their semantic meaning.

***Dataset***  
Twitter is used to collect 100 million US tweets corpus and organized as follows: 

- *Seasonal Emoji Dataset* — data is divided into four subsets by seasons: Spring, Summer, Autumn, and Winter (see figure below)
- *Emoji Prediction Dataset* — data is reduced to tweets that only contain one frequent emoji (emoji must belong to the 300 frequent emojis)
![Frequent emojis grouped by seasons](https://d2mxuefqeaa7sj.cloudfront.net/s_6E9CDDC1A9CC4F74AB1DDC669443AB48A69AE757AAE04BB6E6FBE84825D58A60_1525398110231_image.png)


***Seasonal Emoji Semantic and Usage***   
Skip-gram word embedding models are trained using the four subsets of the seasonal datasets. These models provide information that basically helps to describe emojis in terms of their semantic similarity to each other. (see paper for more details)

By comparing the top 10 emojis associated to each emoji in the embedding space, it was discovered that emojis related to music, animal, sweets, and emotions were not influenced by seasonality (e.g., 🎶 , 🎼 , 🍦 , 🐠 , 😂, 🎸). This means that these emojis preserved meaning across seasons.

In contrast, sport-related emojis (e.g., 🏀, 🏆) varied in meaning across seasons, probably due to the high-peak seasons when sports are played. Another interesting emoji related to school (🎓), changed meaning across seasons; during Spring it was associated with party emojis, and during Autumn it was associated with school-related emojis. Check out the top 10 associated emojis per season for the pine emoji (🌲) in the figure below — very season-dependent don’t you think? Can you guess why? (hint: outdoors vs Christmas). See paper for tons of interesting findings.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_6E9CDDC1A9CC4F74AB1DDC669443AB48A69AE757AAE04BB6E6FBE84825D58A60_1525402218512_image.png)


***Emoji Prediction***  
The second dataset, which includes 300 emoji classes and 900,000 tweets (3,000 tweets per class) , is used for emoji prediction. The architecture of the emoji prediction model is as follows: character embeddings, word embeddings, and data embeddings are combined through an early fusion approach and a late fusion approach. This produces two models (*Early* and *Late*). A third model is trained (*W/O*) which ignores the data embeddings. (see paper to find out how these embeddings are constructed)

![](https://d2mxuefqeaa7sj.cloudfront.net/s_6E9CDDC1A9CC4F74AB1DDC669443AB48A69AE757AAE04BB6E6FBE84825D58A60_1525405246658_image.png)


***Results***  
Precision, Recall, and F1 scores are reported for all models in the table below. We can observe that by combining time information using early fusion, the *Early* model outperforms the others. 

![](https://d2mxuefqeaa7sj.cloudfront.net/s_6E9CDDC1A9CC4F74AB1DDC669443AB48A69AE757AAE04BB6E6FBE84825D58A60_1525406833346_image.png)


The emojis that had higher gains in F1 score (without data vs. early date) are presented in the table below. You can definitely observe that many emojis are season-specific (e.g., 🍀 , 🌙 ) and thus benefit from the date embeddings. Even emojis that are not associated to time (e.g., 🖤, ❤️, 💪) benefit from the temporal information. 

![](https://d2mxuefqeaa7sj.cloudfront.net/s_6E9CDDC1A9CC4F74AB1DDC669443AB48A69AE757AAE04BB6E6FBE84825D58A60_1525407864101_image.png)


***Conclusion & Future Work***  

- A multimodal architecture was proposed to conduct emoji prediction based on deep neural networks. 
- More analysis on the emoji semantics and usage over specific time of the day or week may be able to help improve the date embeddings and the overall predictive models. 

***References***  

- Ref: https://arxiv.org/abs/1805.00731 — “Exploring Emoji Usage and Prediction Through a Temporal Variation Lens**”**

