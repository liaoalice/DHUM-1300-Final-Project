# DHUM-1300-Final-Project
An Exploration of Billboard Hot 100 Hit Lyrics During the 2010s

# Introduction
The Billboard Hot 100 is a chart that measures and ranks the best-performing songs in the United States. As popular songs and popular culture as a whole are often reflective of society's attitudes and perspectives, trends in popular songs may indicate how members of the general public think of themselves in terms of culture, politics, and demographics. This project examines lyrics of Billboard Hot 100 singles from the years 2010 through 2019 to answer the following question: "How did the lyrics of popular songs change over the course of the 2010s?"
As this project will focus on conducting a text analysis, there will be little to no analysis related to music theory, production, vocals, and marketing. However, the lyrics and poetic structure of the songs may reflect the aforementioned other aspects of popular music.

# Process Overview
After perusing the Billboard Hot 100’s charts to refresh myself with the top singles of the 2010s decade, I puzzled over how I could build a dataset of the songs. From Towards Data Science’s Carl Sharpe, I found a Github repository for his Python study of aggression in Billboard hits. Following Carl Sharpe’s repository, I wrote a function that collected Billboard singles from 2010 through 2019 into a pandas dataframe.

However, I needed more than just metadata. The main focus of my project was to conduct text analysis on lyrics. Fortunately, I found a tutorial from Towards Data Science on [how to use Python and Genius.com’s public Application Programming Interface (API) to collect song lyrics as a dataset](https://towardsdatascience.com/song-lyrics-genius-api-dcc2819c29). Accessing Genius.com’s API was by far the most time-consuming and frustrating portion of the project, despite Genius.com’s comprehensive and friendly public documentation. It took three tries for my code to generate lyrics from their API, and each run lasted at least 10 minutes, thanks to the number of songs my loop had to browse. On the successful run, I saw that nine minutes into the process, my loop had only just accessed Beyoncé’s “Partition”—a song released in 2013!

Eventually, I figured that my code failed to work the first two times because of an incorrect client access token; creating my own Genius.com account and generating my own access token allowed it to work successfully. The loop I wrote appended a lyrics column into the Billboard dataset.

After collecting song lyrics for each Billboard hit, I cleaned up the dataset by dropping songs for which no lyrics could be found. Then, I used the free, open-source spaCY natural language processing (NLP) library to extract the lyrics—the text corpus of this exploratory analysis project—from the dataset and placed them into their own dataframe. This process was also a lengthy one. The processor took at least fifty minutes to extract the lyrics the first time. Debugging the code became such a time-consuming process—several hours long—that I ended up eschewing Google Colaboratory in favor of running JupyterLab through my local terminal.

Once I was finished extracting the text corpus, it was time to create data visualizations. I decided to look at term frequencies and conduct sentiment analysis on the lyrics for a general overview of what topics were popular in 2010s hits, as well as how sentiment possibly changed over the course of the decade. I used a word cloud to represent the most common terms, and after running the lyrics dataframe through Vader for sentiment analysis, I used a scatterplot to examine whether any trends appeared.

Before creating my word cloud, I decided to clean the text again with my own custom stopword list. I chose non-lexical vocables like “la” and “na,” as well as common words like “hey” and “baby,” in the hopes that I would be able to see words with more value.

<p align="center">
  <img src="https://github.com/lee-oww/DHUM-1300-Final-Project/blob/main/billboard_wordcloud.png" />
</p>

From the word cloud, I found that “love” was one of the most common words in 2010s Billboard hits, as I expected. Love is a frequent topic in songwriting, given its universality and breadth. As pop music is intended to draw commonality among the masses, it is prone to centering around universal themes in general. Pop music in the 2010s also often centered around living in the moment, as reflected by words like “time,” “night,” and “tonight.” Given that pop music is traditionally driven by youth, it is no wonder that many of these terms reflect immediate pleasure.

The positive sentiment analysis scatter plot was more interesting to me. To create this plot, I used a groupby() and mean() method to aggregate the positive sentiment scores of each Billboard year. 

<p align="center">
  <img src="https://github.com/lee-oww/DHUM-1300-Final-Project/blob/main/billboard_sentiment.png" />
</p>

I found that the scatter plot reflected a clear trend in sentiment—one that I predicted myself. However, I never thought that the trend would reflect my speculations in such a definite manner. Among pop music enthusiasts, 2013 is notable for being the year in which Lorde debuted with her single “Royals.” When “Royals” was released, pop music had been following a maximalist sound for several years. “Royals,” on the other hand, was starkly minimalist, with more restrained percussion and synths. In the years to come, pop music would become more minimalist with Justin Bieber’s “Love Yourself,” Rihanna’s “Stay,” and Billie Eilish’s “bad guy.” Additionally, hip hop began to climb the charts more and more after 2015, leading to different sounds as well. Most hip hop genres are more reliant on percussion in comparison to early 2010s mainstream pop. 

Although I was aware of these trends in terms of production—in other words, aural elements that would not be detected by natural language processing—I was delighted to see through data that indeed, positive sentiment significantly dropped after 2013 and took a downward trend instead. In other words, the minimalist sound production in hits that became popular after 2013 was reflected in lyrical content as well.

# Conclusions

If I had more time on this project, I would program a custom tokenizer for spaCY to not split intra-hyphenated words. I realized too late into the process that spaCY was splitting hyphenated words, including vocalizations like “He-e-e-e-ey” from Train’s “Hey, Soul Sister,” which skewed the results of word counts and sentiment analysis.

I would also ensure that the stop words process would not automatically eliminate non-English words. During the 2010s decade, songs like Psy’s “Gangnam Style” and Luis Fonsi’s “Despacito” became cultural phenomena in the U.S., despite the former being in Korean and the latter being in Spanish. To exclude non-English hits from analysis is to ignore the millions of U.S. residents who speak languages other than English, including myself, and the universality of music itself.

Finally, the process of extracting songs from Genius.com’s API and the Billboard website gave me metadata with more potential research possibilities for the future. While the main purpose of this project was to focus on text analysis of lyrics, the dataframes I set up had columns that could be analyzed in tandem with the lyrical content—seeing whether songs with more negative sentiment tended to rank higher or lower by the end of the decade would be interesting. For this angle, I would apply NLTK to each row of the billboard_df dataframe. I would use NLTK to garner summary statistics and draw relationships between each column. Overall, I think that a refined version of this project would be of interest to songwriters, A&R divisions, and sociologists. On the other hand, as streaming democratizes music listening practices more and more—leading to a less consolidated musical mainstream—data on Billboard hits of the 2020s could possibly be more haphazard. 
