---
title: 'Casting Actors for Your Movie'
author: 'A. Ben Mustapha, F. Briki, Y. Lin, N. Tian'
---

# Casting Actors for Your Movie
## Can the Process of Casting Actors Be Automated?
<br>

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

## Proposed datasets: 
<!---
List the additional dataset(s) you want to use (if any), and some ideas on how you expect to get, manage, process, and enrich it/them. Show us that you’ve read the docs and some examples, and that you have a clear idea on what to expect. Discuss data size and format if relevant. It is your responsibility to check that what you propose is feasible.
-->
- [CMU Movie Summary Corpus dataset](http://www.cs.cmu.edu/~ark/personas/): dataset that contains the metadata for 81,741 movies and 450,669 characters aligned to them, extracted from the November 4, 2012 dump of Freebase and the movie plot summaries extracted from the
November 2, 2012 dump of English-language Wikipedia for 42,306 of those movies.
- [CMU Movie Summary Corpus supplement](http://www.cs.cmu.edu/~ark/personas/): supplement to the previous dataset, that contains ll of the plot summaries from above, run through the Stanford CoreNLP pipeline (tagging, parsing, NER and coref).
- [Oscar Awards dataset](https://www.kaggle.com/datasets/unanimad/the-oscar-award): dataset that contains past Academy Award winners and nominees between 1927 and 2018. 
- [IMDB dataset](https://www.imdb.com/interfaces/): dataset that contains the names of the movies on IMDB alongside their average rating and the number of votes. 
  
## Methods

> Does hiring the best actors guarantee a successful movie?

As it is hard to quantify how good an actor is at doing their job, we choose to base this definition on whether or not the actor was awarded an Oscar by the Academy of Motion Picture Arts and Sciences, as this represents the opinion of other professionals in the field. We define a movie to be successful if it has a high rating by the general audience and the critics. 
After (pre-processing?) the data, we investigate how good of an indicator having a successful actor is for a movie to be successful. 

> Do the best actors play the same roles over and over again?

We investigate the previous roles  of the actors from the [original] dataset who were nominated or have won an Oscar to determine if they typically choose more similar or less similar roles than other actors.
To learn the personas of the characters the actors have played, we follow the method used in the paper (ref) “Learning Latent Personas of Film Characters”; we use the structured representation of the plot summaries output from the Stanford CoreNLP to extract linguistic features for each character (agent verbs, patient verbs, attributes). We then do a soft clustering over words to topics, a soft clustering over topics to personas and a hard clustering over characters to personas. 

Once we have the personas of the characters that actors have played, we define a similarity measure between the different personas and we investigate whether a correlation (or anticorrelation) exists between being a successful actor and playing similar characters.

> How can you pick the most appropriate actor for your movie?

A first step is to filter the potential actors by the constraints on the metadata imposed by the role we want to cast for (like gender, age, ethnicity,..). A second step is generating the list of personas each actor that is left has played following the method discussed in the previous point, and whether or not they have been nominated or have won an Oscar. We then train a model, that is yet to be determined according to the results of the first and second research questions, to predict how successful each actor that is left would be in a specific role, hence generating a ranking on the list of actors according to how appropriate they will be for that role.


## Proposed timeline


## Organization within the team: 
A list of internal milestones up until project Milestone P3.
