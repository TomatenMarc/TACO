# :taco: TACO -- Twitter Arguments from COnversations

In this folder, you can find the annotation framework and information about the data used in the resource paper: "TACO - Twitter Arguments from 
Conversations".

## Sensitive Data

The contents of this folder comprise all data that can be shared with the public. This includes reduced versions of tweets that only contain their
tweet_id. Additionally, we offer the [dataset_statistics.ipynb](../notebooks/dataset_statistics.ipynb) file, which we utilized to generate our ground
truth data and gain preliminary insights. Since we cannot release all data, such as the text of tweets,
the [dataset_statistics.ipynb](../notebooks/dataset_statistics.ipynb) file is only provided for comparison purposes. Accessing it would
necessitate the use of the following files:

1. [data/unify.py](./import/unify.py): Used to build our ground truth data as specified in section 2.2 of the paper.
2. [data/import](./import): Conversations and expert decisions were brought in from external sources (*).
3. [data/backup_tweets.csv](./backup_tweets.csv): Containing the clear text of all tweets (*).
4. [data/url_dict.json](./url_dict.json): The resolved tiny URLs in order to trace the original URLs (*).

| (*): The sensitive user data contained in these files should not be made public. Please [contact](#contact) for additional information. For rehydrating tweets or for obtaining own conversations we recommend to use our [tool](https://pypi.org/project/twitter-conversation/). |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

## About conversations

To construct Twitter conversations, we have included the [conversations.csv](./conversations.csv) file, which contains all conversations. This
file comprises the following columns:

1. **tweet_id**: The unique identifier of a tweet in Twitter's database.
2. **conversation_id**: The **tweet_id** of the very first (top-level) tweet in the conversation.
3. **parent_id**: The **tweet_id** of the parent tweet that the current tweet is replying to (*).
4. **topic**: The conversation's topic that was assigned for sampling purposes.

| (*): There are tweets with a tweet_id that is the same as their parent_id but with a different conversation_id. These tweets are dead-end tweets that have their parent deleted but are not top-level tweets. |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

## About the ground truth

To create the ground truth labels, we used the individual decisions of our six experts, which are stored
in [worker_decisions.csv](./worker_decisions.csv), and obtained the majority vote by hard coding the results
in [majority_votes.csv](./majority_votes.csv). The [worker_decisions.csv](./worker_decisions.csv) file includes the following columns:

1. **tweet_id**: The unique identifier of a tweet in Twitter's database.
2. **information**: A binary value indicating the presence (1) or absence (0) of information in the tweet.
3. **inference**: A binary value indicating the presence (1) or absence (0) of inference in the tweet.
4. **confidence**: A value indicating the annotator's task confidence, ranging from easy (1) to hard (3).
5. **worker**: The identifier of the annotator (A and E both belong to the author Marc Feger)).
6. **topic**: The conversation's topic that was assigned for sampling purposes.
7. **phase**: The phase in which the tweet was annotated.

### Annotation Phases

Our six experts provided individual decisions from different annotation phases. During the initial annotation stage, experts A, B, C, and D annotated
600 conversation-starting tweets. This first annotation step comprised two phases:

1. **training_1 - 2**: Two successive training phases, each involving 100 tweets, were conducted for the annotators. These were followed by a
   debriefing session.
2. **extension_1 - 4**: The first through fourth extensions, each comprising 100 tweets, were conducted after the annotators had completed their
   training.

In the second annotation step, three additional annotators, namely A (E), F, and G, annotated the tweets in 200 conversations. To this end, 100
conversation-starting tweets from the first step were selected for training the new annotators on the tweets and their subsequent conversations. This
was followed by another 100 conversations. In total, the second annotation step comprised the following phases:

1. **training_3 - 4**: Two training phases involving 100 conversation-starting tweets from the first annotation step (conducted with 100%
   agreement among annotators A, B, C, and D) along with their entire conversations.
2. **extension_5 - 8**: The subsequent four annotation steps covered 25 new conversations each.

The individual annotation phases are detailed in [dataset_statistics.ipynb](../notebooks/dataset_statistics.ipynb).

### Majority Votes

Once the annotation phases were complete, the ground truth labels were assigned using a hard majority vote. The resulting ground truth data
is saved in [majority_votes.csv](./majority_votes.csv), which contains the following columns:

1. **tweet_id**: A unique identifier for each tweet in Twitter's database.
2. **topic**: The topic of the conversation that was assigned for sampling purposes.
3. **category**: The category assigned to each tweet based on the majority vote of the annotators, as specified
   in [annotation_framework.pdf](./annotation_framework.pdf).
4. **confidence**: The proportion of annotators who voted for the final category. For example, if A, B, and C all voted for the same category, the
   confidence value would be 3/4.

## Contact

Please contact [marc.feger@uni-duesseldorf.de](marc.feger@uni-duesseldorf.de) or [stefan.dietze@gesis.org](stefan.dietze@gesis.org).

## Acknowledgements

We thank Aylin Martin, Tillmann Junk, Andreas Burbach, Talha Caliskan, and Aaron Schneider for their contributions to the
annotation process in this paper.