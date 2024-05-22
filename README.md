## Overall Idea

My goal here was to finetune GPT-2 on pitchfork music reviews with an aim to gain cohesive commentary given a music genre. For example, if a user were to input "Hip Hop:" the model would be able to
fill the rest of the sentence with a cohesive review that pertains to a Hip Hop Album. 


## Data preparation

18k Pitch fork reviews were used. Each review has about 1200 words. In order to structure the data in a way that our model would understand, I appended the genre of music before every review. For example: "This album was good"
would become "Hip Hop: This album was good" (assuming the album was hip hop). 

In addition to this, the NLTK package was used to clean the reviews themselves. This includes lower casing all the words, removing unessary whitespace etc. Most importantly. After every review, I added a "|endoftext|" token which indicated the end of a given review. 

Note up until this point, the data was stored in a dataframe. In order to more easily tokenize this data, I converted it from a dataframe of reviews into a list of reviews. 


## Tokenization

Luckily this step was quite easy. Using hugginface, I loaded up the GPT-2 Tokenizer and fed the list of reviews to it. Note, due to the limited RAM available, I needed to truncate my token representations to have a max length of 120 which had a 
significant negative impact on the model (since the average review had about 5000 characters). As a result, the model is forced to make predictions with very little information.



## Training

- About ~14k rows to the training set, and 4k to the Validation set.
- Finetuning, and so we freeze the base layers and leave the top one unfrozen (38597376 trainable parameters).
- 10 epochs.

## Results
- Average training loss: 2.7999
- Average validation loss: 3.9745

## Example generations
- Generated Text 1: experimental: the first time i heard mouse on mars' debut the end of an hour was in may 2011, when they released a 12" live album called bukkumma. it was recorded at the carrack modern college in boston, where they self-released their 7" tape as part of 2007's microsound series. with that disc plus endicillin’s radium girls and vibrating waves, endicillin surprised me more
- Generated Text 2: hip hop: there's a name for the album, courtesy of dirty projectors. it follows four years of quirky pop-savantia that resulted in one record from six people creating completely different songs with no regard to who was making them-- which is sorta odd given how dorky and brooding downhearted hipness often seem on an idea level at best.  but instead holy fuck! take la roux; you're gonna miss me here anyway. so let's get this out
- Generated Text 3: rock: if you're in the mood for a full-length, get ready for some of the most exciting new material from veteran musician/multiinstrumentalist daniel lopatin.  he's spun rainbow guitar with his band as nathan williams and brian wilson played keyboards with him on "leaving lights". last year, they tidied up their lineup to include dan balisby, sam cooke (now chelon jennifer)ldon, and matthew
- Generated Text 4: hip hop: the houston-born rapper has spent most of his career as a member of local free energy and hip hop groups. in 2013, he released an ep called "dog days". at that point, though, there was little evidence to suggest anything personal changed for him—polished spoken word messages visible on ragged production values favored by gangsta rap outfit xibalba; muscle emphasized over rage against masculinity issues like getting punched during.? um riotous shows (deaf buck 3000's
- Generated Text 5: hip hop: if you're a hip-hop fan, chances are that the album title might as well ring loosely around "hitch hike".  it's not hard to see why. when hitch hike involves doing something different than another person standing still on an indoor fog bank in central park-- leaning and showing up for requests or letting loose with some other people who can't really connect fully without further contemplation (unless they actually have anything sleepwalking about). but listening back over six hours of music

## Potential improvements
The biggest potential improvement would just be increasing the token length, again the truncation currently is too much to capture enough information for the whole review and that is why some of these generated sentences are not as coherent as they could be!


## Big Picture takeaway
The model gets pretty good at associating artists to their given genre. For example, "mouse on mars" does refer to experimental music projects, while Brian wilson is a rock artist. This could be useful in the future for Genre - music tagging products. Where we can use an LLM to make these connections!









