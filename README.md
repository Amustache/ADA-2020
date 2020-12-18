# "A Wolf in Sheep's Clothing": Linguistic Cues in Social Deduction Games

## Abstract
We studied [[Niculae et al., 2015]](#niculae) and it enabled us to highlight certain clues of language linked to the imminence of betrayal. We would like to apply similar techniques to detect betrayal in social deduction games, like [Town of Salem](#salem), [Secret Hitler](#hitler), [Among Us](#amongus) or [Werewolf/Mafia](#mafia). Is it possible, by studying the public exchanges of the players during a textual game, to spot the "traitor"? The major difference with the basic article is that we are not looking for a betrayal to come - the breaking of a friendship - but a betrayal that has already taken place - for instance, the "wolf" seeks to win by posing as a "villager". As such, we are going to analyse textual exchanges of different games, and try to apply the same methods to multiple sessions.

## Research questions
1. Is it possible to apply the techniques seen in the article to other games?
2. Is it possible to identify betrayal on a "long term" basis, i.e. deception (vs. in the article on a specific point in time)?
3. What are the clues to identify "traitors" in social deduction games?

## Proposed dataset
For the project, we found the following datasets that could be of interest for us:

- **Linguistic Harbingers of Betrayal** ([[Niculae et al., 2015]](#niculae)): [Dataset direct link](https://vene.ro/betrayal/diplomacy_data_1.0.zip).
- **Town of Salem** ([Town of Salem](#salem)): [Dataset direct link](https://drive.google.com/file/d/1vLKzVjKXep9ig0DOcVJQJziOFFxY3AIT/view).
- **The Mafiascum Dataset** ([[de Ruiter et al., 2018]](#deruiter)): [Dataset direct link](https://bitbucket.org/bopjesvla/thesis/src/master/).
- **Werewolf for Telegram** ([Werewolf/Mafia](#mafia)): Custom datasets from the famous Telegram bot version of the game.

### Town of Salem
**Town of Salem**'s dataset lists 8'833 ranked games scraped from the "[Trial System](https://town-of-salem.fandom.com/wiki/Trial_System)" of the online plateform of the [game](#salem). The dataset is organized as a JSon file where each game is represented as a python dictionnary with four keys:
- `players`: General information about each of the 15 players of the game such as their account and pseudonym as well as information dealing with their involvement in the game (role, faction, time of their ingame death, ...).
- `entries`: Chat logs displayed on the interface which can be messages from the players (eg. "i think we have an sk") catalogued into python dictionnaries (with keys `type` containing different channels, ` author`, `text`, and `time`) or moderating informations such as the ingame time or trials outcome. Note that the minimum number of entries for a game is 89, maximum is 1'539, with mean 526 and median 509.
- `ranked`: Boolean, `True` for each listed game.
- `reportId`: Unique identifier of the "Trial System" characterizing a game.

### The Mafiascum Dataset
**The Mafiascum Dataset** is a collection of over 700 games of [Mafia](#mafia) played on an Internet forum. The interactions between players are scraped from this plateform. The data repository consists of several JSon files that contain different informations about each game and each player and messages, and are divided as follow:
- Files with suffix `games` includes general identifier of the games, e.g. `id`, `title`, `moderator`, or number of posts. 
- Files with suffix `slots` contains informations about the players such as the id of the game in which they took part, their role, and how their game ended (eg. "lynched Day 2", "died Night 5" or "survives").
- Files without specific suffix gather all textual interactions, their authors as well as the id of the games, and the index of the post within the game (random examples of messages: "i don't wanna be a chicken i don't wanna be a duck", "Also, Egg - I don't particularly find the peacemaker routine a town-thing generally."). 

### Werewolf for Telegram
Finally **Werewolf for Telegram**'s dataset is a raw set of text messages exchanged on [Telegram](https://en.wikipedia.org/wiki/Telegram_(software)) directly scraped from online groups. It would represent an important workload in terms of cleaning and shaping the data, therefore we don't plan to focus on this one. However, if time allows or for further investigations, it could be a great substrate to work on.

### Chosen datasets
To sum up, we plan to use the initial database (Linguistic Harbingers of Betrayal) in order to develop and test the algorithm supposed to analyze different features of futher datasets.

Moreover, among the three new deduction games databases, we think that "The Mafiascum Dataset" is the one that will have the best chance to reproduce a successful result. It is cleaner and has already been used in another study.

## Methods
The methodology will be the same than in [[Niculae et al., 2015]](#niculae) parts 4.2 and 4.3.

- **Preprocessing**: Manual study of each datasets.
- **Sentiment**: Sentiment quantification using the Stanford Sentiment Analyzer ([[Socher et al., 2013]](#socher)).
- **Planning**:
	- Explicit discourse connectors per sentence measurment ([[Prasad et al., 2008]](#prasad)).
	- Average number of claim and premise markers per sentence calculation ([[Stab et al., 2014]](#stab)).
	- Number of request sentences in each message measurment using the heuristics in the Stanford Politeness classifier ([[Danescu-Niculescu-Mizil et al., 2013]](#danescu)).
- **Politeness**: Politeness measurment of each message using the Stanford Politeness classifier (*ibidem*) - using [CovoKit](#convkit) toolkit.
- **Talkativeness**: Number of messages sent, average number of sentences per message, average number of words per sentence.
- **Model**: Logistic regression for classification, "traitor" vs. "innocent".

For this project, we would like to focus on politeness and talkativeness. Because of the short time we have at our disposal, it would not be possible to analyze all the "harbingers".

## Proposed timeline
- **Week 0**: Preliminary considerations
	- 09.11: Release of P3 instructions
- **Week 1**: Thoughts on what we want to do.
- **Week 2**: Let's do this.
	- 27.11: Deadline. P3 is due.
- **Week 3**: Implementation of the different methods and tests on the initial dataset.
- **Week 4**: Exploration on the others datasets.
- **Week 5**: [Wrapping up](https://youtu.be/9jK-NcRmVcw).
	- 18.12: Deadline. P4 is due.

## Organization within the team
We have four "harbingers" to study, namely talkativeness, politeness, argumentation and sentiment. Because of the time we will try to focus on politeness and talkativeness, but we will try to work on the other "harbingers" as well.

1. Reproduction: Create a notebook with a reproduction of the aformentionned methods on the original dataset.
	- _(Study the impact of "positive sentiment" and see if we get the same results.)_
	- _(Study the impact of "planning discourse markers" and see if we get the same results.)_
	- Study the impact of "politeness" and see if we get the same results.
	- Study the impact of "talkativeness" and see if we get the same results.
2. Abstraction: "Abstract"/"Factorize" the elements of the notebook to create an API applicable to other games.
	- Dataset in, results out.
	- Compare results from each others.
3. Application: For each database (depending on the time):
	- Sanitize and normalize the dataset to be used with our API.
	- Apply the methods using our API.
	- Compare results with the original paper.
	
## So who did what ?

* Noé and Emmanuel did the data concierging as well as the analysis of talkativeness. 
* Hugo and Neil handled politeness
* Noé did an API to plot all the data (that was a real time saver for the others)
* Hugo handled the data story
* Hugo wrote the pitch for the video
* Neil performed in the video
* Of course, everyone reviewed every part he did not do and contributed, it's a team work !

## References
- <a name="danescu">**[Danescu-Niculescu-Mizil et al., 2013]**</a>: Cristian Danescu-Niculescu-Mizil, Moritz Sudhof, Dan Jurafsky, Jure Leskovec, Christopher Potts, *A computational approach to politeness with application to social factors*, ACL, 2013. [Original paper](https://nlp.stanford.edu/pubs/politeness.pdf).
- <a name="niculae">**[Niculae et al., 2015]**</a>: Vlad Niculae, Srijan Kumar, Jordan Boyd-Graber, Cristian Danescu-Niculescu-Mizil, *Linguistic Harbingers of Betrayal: A Case Study on an Online Strategy Game*, Proceedings of ACL, 2015. [Original paper](https://vene.ro/betrayal/niculae15betrayal.pdf), [website](https://vene.ro/betrayal/).
- <a name="prasad">**[Prasad et al., 2008]**</a>: Rashmi Prasad, Nikhil Dinesh, Alan Lee, Eleni Miltsakaki, Livio Robaldo, Aravind Joshi, Bonnie Webber, *The Penn Discourse TreeBank 2.0*, LREC, 2008. [Original paper](http://www.lrec-conf.org/proceedings/lrec2008/pdf/754_paper.pdf).
- <a name="deruiter">**[de Ruiter et al., 2018]**</a>: Bob de Ruiter, George Kachergis, *The Mafiascum Dataset: A Large Text Corpus for Deception Detection*, 2018. [Original paper](https://arxiv.org/pdf/1811.07851.pdf).
- <a name="socher">**[Socher et al., 2013]**</a>: Richard Socher, Alex Perelygin, Jean Wu, Jason Chuang, Christopher Manning, Andrew Ng, Christopher Potts, *Recursive Deep Models for Semantic Compositionality Over a Sentiment Treebank*, EMNLP, 2013. [Original paper](https://nlp.stanford.edu/~socherr/EMNLP2013_RNTN.pdf), [website](https://nlp.stanford.edu/sentiment/).
- <a name="stab">**[Stab et al., 2014]**</a>: Christian Stab, Iryna Gurevych, *Identifying Argumentative Discourse Structures in Persuasive Essay*, EMNLP, 2014. [Original paper](https://www.aclweb.org/anthology/D14-1006.pdf).
- <a name="salem">**Town of Salem**</a>: [Official website](https://www.blankmediagames.com/), [Wikipedia](https://en.wikipedia.org/wiki/Town_of_Salem), [Fandom](https://town-of-salem.fandom.com/wiki/Town_of_Salem_Wiki).
- <a name="hitler">**Secret Hitler**</a>: [Official website](https://www.secrethitler.com/), [Wikipedia](https://en.wikipedia.org/wiki/Secret_Hitler).
- <a name="amongus">**Among Us**</a>: [Official website](http://www.innersloth.com/gameAmongUs.php), [Wikipedia](https://en.wikipedia.org/wiki/Among_Us).
- <a name="mafia">**Werewolf/Mafia**</a>: [Wikipedia](https://en.wikipedia.org/wiki/Mafia_(party_game)), [Telegram game official website](https://www.tgwerewolf.com/).
- <a name="convkit">**ConvKit**</a>: Cornell Conversational Analysis Toolkit. [Website](https://convokit.cornell.edu/).
- <a name="nlpstanford">**Stanford NLP Group**</a>: [Website](https://nlp.stanford.edu/).
