---
title: 'Casting Actors for Your Movie'
author: 'A. Ben Mustapha, F. Briki, Y. Lin, N. Tian'
---

# Casting Actors for Your Movie
## Can the Process of Casting Actors Be Automated?
<br>

## Data Story: 
The Data story can be found [here](https://farahbriki.github.io/ADA-CNxTN/#section1).

## Abstract
Casting is the process of selecting actors who will play various characters in a movie. Typically, a casting director is hired to find the best possible talent for the roles and present these options to the directors and producers who then make their final casting decisions. Casting is one of the most crucial parts of the filmmaking process; choosing the actors can make or break a film. Choosing the wrong actor might diminish a particular character’s believability, which would affect negatively the movie. However, even the best casting directors have a certain bias from their experience in the industry; this can come from their previous interactions with actors (or lack thereof). This project aims to predict how successful an actor would be if they were cast in a specific role. This allows to rank the actors by the most appropriate for the role to the least appropriate, which would serve as casting suggestions to the directors and producers. 

<!---
Casting is one of the most crucial parts of the filmmaking process; choosing the actors can make or break a film. Our project aims to use data about actors’ personal information and previous roles to predict how successful they would be in a new role. This can allow for making casting suggestions to help casting directors pick out who to call in for an audition. In order to measure how successful an actor will be in a new role, we investigate the relationship between the success of actors and the success of the movies that they played in, and the similarity (or not) of the different roles a successful actor played in; the personas of the characters that actors played can be leveraged from plot summaries of the movies by using NLP tools. 
-->

## Research Questions
- Does hiring the best actors guarantee a successful movie?
  <!---
  'Best actor' here refers to the actors who were awarded an Oscar by the Academy of Motion Picture Arts and Sciences, as it is hard to quantify how good an actor is apart from leveraging the opinion of other professionals in the field. 
  A movie is said to be successful if it has a high rating by the general audience and the critics.
  -->
  
- Do the best actors play the same roles over and over again?
  <!---
  There's a strong association in the general viewer's mind between some actors and the characters they portray as their roles are minor variations of each other, whereas other actors' range of characters played is very wide. We are interested in seeing whether the best actors tend to do the former or the latter. 
  -->
- How can you pick the most appropriate actor for your movie?
   <!---
  The main question in this project is finding the best actors suited for a role. The role is described by the persona of the character, and by other distinctive information like age, gender, ethnicity,.. 
  -->

## Additional datasets: 
<!---
List the additional dataset(s) you want to use (if any), and some ideas on how you expect to get, manage, process, and enrich it/them. Show us that you’ve read the docs and some examples, and that you have a clear idea on what to expect. Discuss data size and format if relevant. It is your responsibility to check that what you propose is feasible.
-->
- [CMU Movie Summary Corpus dataset](http://www.cs.cmu.edu/~ark/personas/): dataset that contains the metadata for 81,741 movies and 450,669 characters aligned to them, extracted from the November 4, 2012 dump of Freebase and the movie plot summaries extracted from the November 2, 2012 dump of English-language Wikipedia for 42,306 of those movies.
- [CMU Movie Summary Corpus supplement](http://www.cs.cmu.edu/~ark/personas/): supplement to the previous dataset, that contains the plot summaries from above, run through the Stanford CoreNLP pipeline (tagging, parsing, NER and coref).
- [Oscar Awards dataset](https://www.kaggle.com/datasets/unanimad/the-oscar-award): dataset that contains past Academy Award winners and nominees between 1927 and 2018. 
- [IMDB dataset](https://www.imdb.com/interfaces/): dataset that contains the names of the movies on IMDB alongside their average rating and the number of votes. 
  
## Methods

> Does hiring the best actors guarantee a successful movie?

As it is hard to quantify how good an actor is at doing their job, we choose to base this definition on whether or not the actor was awarded an Oscar by the Academy of Motion Picture Arts and Sciences, as this represents the opinion of other professionals in the field. We define a movie to be successful if it has a high rating by the general audience and the critics. 
We do a matched analysis comparing the actors who have won an Oscar, with actors that have not been nominated. To make matches more comparable, we consider pairs who have the same (…). After doing a 1-1 matching, we use linear regression model to estimate the effect of having won an Oscar in the final movie rating, which we find to be positive and quite significant.

> Do the best actors play the same roles over and over again?

We investigate the previous roles of the actors from the CMU Movie Summary Corpus dataset who have won an Oscar to determine if they typically choose more similar or less similar roles than other actors. 
To learn the personas of the characters the actors have played, we were inspired by the method used in the paper [“Learning Latent Personas of Film Characters”](http://www.cs.cmu.edu/~dbamman/pubs/pdf/bamman+oconnor+smith.acl13.pdf); we use the structured representation of the plot summaries output from the Stanford CoreNLP to extract linguistic features for each character (agent verbs, patient verbs, attributes). We cluster the bag of words to personas.
After defining the personas, we do a matched analysis comparing the actors who have won an Oscar, with actors that have not been nominated. We use linear regression model to estimate the effect of having won an Oscar in the ratio of the total roles played that have the same persona as their maximum occurrence persona, which we find to be positive and quite significant; an Oscar award winner is plays on average two times as much their maximum occurrence persona. 

Additionally, we investigate the effect of having played the same role before directly in the movie rating. We do a matched analysis comparing the actors who have played the role before, with actors that have not. We use linear regression model to estimate the effect of having played the role before in the final movie rating. The results of this analysis are inconclusive.

> How can you pick the most appropriate actor for your movie?

In order to predict how successful picking a specific actor for your movie is, we combine features about the actors' abilities (Oscar wins or nominations, list of personas played) with the actors’ metadata, and we train a model to predict the final movie rating.
To pick which features should or shouldn’t go into the model, we use forward feature selection.
The model can then be used by specifying the persona of the role we want to cast for, as well as any important metadata (e.g. gender or ethnicity). We filter the list of actors by the necessary metadata constraints and calculate the relevant additional features that comes from the persona of the role (e.g. the number of previous roles the actor has played that fit into the relevant persona). We then predict the final movie rating for each actor that fits into the metadata constraints using the model previously mentioned, and sort in decreasing order.

## External libraries
- numpy
- pandas
- matplotlib
- seaborn
- xml
- statsmodels
- networkx
- sklearn
- plotly

## The CNxTN team contributions: 
Farah: Generating bag of words from NLP output in RQ2, RQ3, Datastory
Raed: RQ1, RQ2 models, RQ3, Datastory
Lin: Data preprocessing, Clustering in RQ2
Nana: Load the IMDB dataset
