# NLP-The-Office-Language-Model
 
Collection of NLP methods to analyze the scripts of the famous TV Series the office. 
The project aims to analyze in detail the lines of the show text and try to understand the behavior of some of the main characters and the script as a whole. It will be not easy as I think that much of the comicality in the show is not due to the lines but to the ability of the actors to pronounce them properly. In particular, we will try to reveal character nuances by analyzing their lines using the tools studied in the NLP course. Further detail about how the analysis has been developed and its results will be found in each section.

## Data 

For the project we are going to use in a conjoint way two dataset:

The "The Office" we can find every line from the show. Available in googlesheet: https://docs.google.com/spreadsheets/d/18wS5AAwOh8QO95RwHLS95POmSNKA2jjzdt0phrxeAE0/edit#gid=747974534 [Found on the web] Will be analyzed the lines from the 'The Office' TV-Series. In the dataset are available information about the season, the episode, the scene in which a certain line has been pronounced and the character who is telling it.

The reviews' dataset. Obtained trough Beautiful soup [*External library]. It is a series of reviews posted on IMDB about 'The Office'. The data have been defined respecting the structure of the main dataset. Are represented the season and the episode to which the review is referred, the review score, who posted the review, when the review was posted, the review_text, and how many found the review useful.

Further information about the applied preprocessing steps are in the next sections.

## Data Pre Processing 

* Filter out deleted scenes;
* Remove text in brackets ([]) and put in a new column called actions;
* There are 4000+ instances of ??? found in the data mainly in the last two seasons. The ??? replaces … - ’ and “. For now I’m just going to replace all instances with ’ since - that seems to be the majority of the cases
* Change speaker to lower case since there is some inconsistent capitalization
* Some entries for speakers have actions ([]), which I’ll remove
* Fix misspellings in the speaker field (e.g. Micheal instead of Michael)
* Remove wrong entries in speaker: By a fast analysis is possible to notice that there are 3 WRONG OCCURENCES, in the set of speakers, these are listed in wrong_entries and will be dropped through a left join.
* Remove lines with no text but just actions

## Data Analytics

Several techniques has been used for Data Analytics: 
* TFIDF analysis
* Word embeddings
* Topic models
* Dimensionality reduction

## Language Model

'That's what she said' is one of the most famous catchphrase of the show. In this section I want to try if the MichaelScott language model is able to reproduce it in a 10.000 trial setting.
As expected, n-grams language models are not much sensical but we can see that it is generally able to grasp develop meaningful sentence. Given the high variety of words that are used and the fact that the lines are very short, sometimes it seems to reproduce lines from the script, as the porbability of words repeating in a certain way, is skewed towards sentences whihc happened not so often in the script.

In this analysis i have decided to implement the LM in a peculiar way to simulate a real conversation between two of the main_ch of the series. Writing a new 'script' is possible by just selecting the character's name and how long you mean to continue the conversation. It is strongly suggested to use just characters that are in the main_ch list.

We can notice that sometime, the sentences of each character are referred to other character of the series,in fact the conversation hardly make sense as a whole. Being language models based on stochasticity and n-grams we could not expect more. Would be interesting to implement it in such a way in which, depending on the specific character who is called in the conversation her/him intervenes.


## Data Visualization 

Barplots to represent word frequencies (for the scripts filtered on the main characters the 'pam' script and the reviews)
Scatterplots to evaluate TfIdf (for the scripts filtered on the main characters and the reviews)
Bi-dimensional and tri-dimensional reduction applied to tfidf to evaluate clusters (for the scripts filtered on the main characters and the reviews)
t-SNE bidimensional representation of distances in doc2vec
