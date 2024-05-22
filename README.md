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
- Generated Text 1: hip hop: i hate you, bitch.  "i won't stop" is a lyric that usually means the absence of desire or jealousy-- and it's true; after all this time spent making music for people who never really cared about what they heard in public school radio mulatu vibes were like watching an old acquaintance straddle with his deadringer before he died while listening to sped-up rap songs on one end (to get pissed off at how fun some adults are getting when kids
- Generated Text 2: hip hop: there's a name for the album, courtesy of dirty projectors. it follows four years of quirky pop-savantia that resulted in one record from six people creating completely different songs with no regard to who was making them-- which is sorta odd given how dorky and brooding downhearted hipness often seem on an idea level at best.  but instead holy fuck! take la roux; you're gonna miss me here anyway. so let's get this out
- Generated Text 3: hip hop: so i can't really count it, but this is the only song that stands out for me.  let's just call 'em "baba o'riley", okay? and their melody matched what could've been a lo-fi garage rock number echoing nicely around tim hecker's telephone calls from drella to hollywood sci-fi romance ("i'm eating dog shit") with enough other token of charm coupled together (just by stretching them into one continuous street). those
- Generated Text 4: hip hop: the houston-born rapper has spent most of his career as a member of local free energy and hip hop groups. in 2013, he released an ep called "dog days". at that point, though, there was little evidence to suggest anything personal changed for him—polished spoken word messages visible on ragged production values favored by gangsta rap outfit xibalba; muscle emphasized over rage against masculinity issues like getting punched during.? um riotous shows (deaf buck 3000's
- Generated Text 5: hip hop: if you're a hip-hop fan, chances are that the album title might as well ring loosely around "hitch hike".  it's not hard to see why. when hitch hike involves doing something different than another person standing still on an indoor fog bank in central park-- leaning and showing up for requests or letting loose with some other people who can't really connect fully without further contemplation (unless they actually have anything sleepwalking about). but listening back over six hours of music

## Potential improvements
The biggest potential improvement would just be increasing the token length, again the truncation currently is too much to capture enough information for the whole review and that is why some of these generated sentences are not as coherent as they could be!








