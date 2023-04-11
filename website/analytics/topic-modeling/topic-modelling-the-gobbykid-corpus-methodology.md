# Topic modelling the Gobbykid corpus: methodology

We based or methodology on the process described by [Jockers (2013)](broken-reference), who topic modeled a large corpus of XIX century English language novels.

## The software

For topic modelling our dataset we used a well-known and robust implementation of the [Latent Dirchlet Allocation](https://en.wikipedia.org/wiki/Latent\_Dirichlet\_allocation) (LDA) model: [MALLET](https://mimno.github.io/Mallet/).

Since Mallet is written in Java, we used a Mallet wrapper for Python: [Little Mallet Wrapper](https://pypi.org/project/little-mallet-wrapper/), developed by Maria Antoniak.&#x20;

## Pre-processing our corpus

In order to topic model our corpus, we first need to pre-process the texts in it, to later feed them to the training algorithm.&#x20;

#### Stopwords

At first, we used the default pre-processing functions provided by the software, but we realized that most of the words in the topics carried little meaning. We then decided to extend the list of stopwords to remove by adding to it the characters names and other grammatical or very common words that had appeared to be too present in the results of the training phase, making them difficult to interpret.&#x20;

#### Retaining only nouns

Since, after this modification, the topics still included "useless" words (adverbs, indefinite pronouns, etc.), we determined to retain, in the text to feed to the model, only the nouns (following Jocker's strategy), on the assumption that the themes present in the corpus were best represented by this part-of-speech. Of course, for other types of analysis, it would have been best to include a wider range of word categories (e.g. verbs or adjectives), but since we were interested in identifying the themes present in the books, this selection seemed fit enough.&#x20;

#### Chunking the texts into sections

As we have said, the LDA model calculates the similarity between each word in the corpus vocabulary based on the frequency with which it co-occurs together with the other words _in the document_, where a document is taken as a bag of words. Following again Jocker's workflow, we therefore decided to limit the context of each word to a size reasonable within a novel, on the assumption that the meaning of a word would be likely to be correctly identifiable by considering the words co-occurring in the _part_ of the book where the word is, rather than all of the words in the whole book. We chunked each book into 1000 words-long sections, making each of these sections a document for the training phase.

#### Summary

In the final workflow for pre-processing the documents, each text in the corpus has undergone the following steps:

1. Sentence-level segementation of the text
2. Word-level tokenization of the sentence
3. POS tagging for every word in each sentence
4. Creating book **chunks**, each of a maximum size of 1000 words, where each word in each chunk must match all the following conditions:
   1. &#x20;must have been pos tagged as noun
   2. must not be included in the stopwords list (including characters' names)
   3. must contain only [ASCII](https://en.wikipedia.org/wiki/ASCII) characters
   4. must not be a number
5. Adding each book chunk in the training dataset

## Training the model

Once we have pre-processed our dataset, we have to feed it to the training algorithm, which will output the model on the dataset of 2544 book chunks.&#x20;

#### Setting the number of topics to extract

As Jockers mentions (2013: 128) "there is neither consensus nor conventional wisdom regarding a perfect **number of topics to extract**, but it can be said that the “sweet spot” is largely dependent upon and determined by the scope of the corpus, the diversity of the corpus, and the level of granularity one is seeking in terms of topic interpretability and coherence. \[...] Setting the number of topics too high may result in topics lacking enough contextual markers to provide a clear sense of how the topic is being expressed in the text; setting the number too low may result in topics of such a general nature that they tend to occur throughout the entire corpus." Moreover it should be taken in consideration that "though the machine does a very good job in identifying the topics latent in a corpus, the machine does a comparatively poor job when it comes to auto-identifying which of the harvested topics are the most interpretable by human beings", possibly making it ineffective to choose the number of topics based on a coherence value automatically calculated by an algorithm.

Given the above, we followed Jockers in adopting a trial-and-error approach, and trained our model over the same documents multiple times, each time with a different value for the $$k$$ number of topics to extract. We tried the following $$k$$​ values: 20, 30, 40, 45, 50, 80, 100. The most coherent model, i.e. the one for which we have considered the topics -after having having analysed them - more easily interpretable, was given with $$k=45$$**.**

### Applying the model over the corpus of whole documents &#x20;

After having extracted the 45 topics present in the dataset composed by book _chunks_, we want to apply this model to a dataset where each document is a _whole book_, to be able to see the distribution of each topic over each _book_, rather than over each book _chunk_ (which we are not interested in for the purpose of this work).&#x20;

The content and the global size of the two dataset is exactly the same (a whole book is pre-processed in the same way as its chunks, i.e. a book basically consists of the juxtaposition of all its chunks), what changes are the units over which to calculate the probability distribution of each topic (the book _chunks_ in the training phase, the _whole books_ in the phase where we infer the previously trained model).

As a result of the inferring phase, we have the probability distribution of each of the 45 topics extracted earlier over the corpus composed by whole books, i.e. the **probability of each topic in each book**.&#x20;

## Analysing the results

### Interpreting the topics

We try and intepret what each topic is about from the words it contains.&#x20;

#### The 45 topics in the corpus (unlabelled)

{% file src="../../.gitbook/assets/45_topic_keys.csv" %}

| Topic index | Words in topic                                                                                                                                                               |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0           | face, look, voice, something, word, mind, bit, sort, eye, right, road, business, back, song, side, you, breath, arm, gentleman, book                                         |
| 1           | men, oxford, town, rooms, year, life, work, river, university, porter, sort, fellow, play, stage, side, set, hero, rate, crew, gentlemen                                     |
| 2           | horses, road, day, whip, men, gentleman, course, saddle, tail, legs, groom, mare, picture, children, jackanapes, tails, cab, grimes, reins, deal                             |
| 3           | child, day, face, children, heart, life, tears, years, arms, kind, voice, wife, days, dear, story, nothing, care, room, husband, side                                        |
| 4           | board, men, guns, ships, vessel, shot, crew, boats, officers, deck, craft, gun, officer, vessels, pirates, frigate, shore, course, side, bay                                 |
| 5           | school, term, house, fellows, door, right, study, meeting, side, chap, course, cheers, room, fellow, everybody, question, d'arcy, heroes, grandcourt, day                    |
| 6           | yer, money, street, shop, purse, face, door, bit, streets, night, policeman, court, pocket, ma'am, morning, please, wot, thief, chapter, police                              |
| 7           | church, men, books, sunday, soul, minister, service, book, sin, prayer, oxford, life, chapel, day, friends, work, earth, truth, sermon, others                               |
| 8           | boys, school, study, form, room, fellows, fellow, work, day, book, desk, holidays, class, morning, lesson, books, rest, others, house, half                                  |
| 9           | night, door, nothing, house, something, anything, bed, wall, feet, window, day, moon, morning, work, side, moment, floor, sun, back, stones                                  |
| 10          | gun, raft, fish, side, island, shore, new, course, yards, nothing, anything, oak, sun, minute, surface, ground, something, grass, hut, sand                                  |
| 11          | men, spaniard, day, heaven, maiden, gentlemen, soul, galleon, spain, years, night, honor, bideford, marshall, ireland, none, ships, land, stove, company                     |
| 12          | boys, day, christmas, gentleman, hair, tea, children, box, kitchen, money, clothes, nursery, legs, bread, window, doll, story, shop, kind, pocket                            |
| 13          | course, anything, nothing, something, sort, friend, day, moment, part, friends, face, mind, fact, matter, voice, deal, look, manner, everything, word                        |
| 14          | friend, men, smile, look, surprise, pipe, youth, ice, friends, scene, countenance, consul, laugh, expression, work, mind, course, comrade, guide, feelings                   |
| 15          | hero, fifth, paper, sixth, gentleman, match, service, equality, guinea-pigs, goal, dominican, watch, fellow, midshipmen, fourth, examination, rod, bat, events, form         |
| 16          | shore, men, island, board, vessel, boats, night, cabin, beach, sail, rocks, crew, day, oars, waves, side, fish, land, tide, work                                             |
| 17          | room, house, door, window, bed, night, morning, face, chair, moment, hour, rooms, carriage, floor, windows, stairs, servants, ladies, dinner, steps                          |
| 18          | children, mrs, child, morning, basket, dear, bit, boys, garden, house, please, milk, lessons, nothing, picnic, dinner, heir, side, face, birthday                            |
| 19          | garden, trees, birds, day, sun, grass, summer, air, leaves, fairies, wings, nothing, earth, branches, morning, sky, ground, spring, feet, side                               |
| 20          | indians, men, river, lake, night, ice, camp, bear, village, trail, canoe, moonlight, feet, prairie, day, hunting, wolves, tribe, deer, friends                               |
| 21          | face, moment, night, heart, voice, nothing, life, word, something, lips, hour, fear, mind, look, air, strength, part, danger, silence, rest                                  |
| 22          | turkey, kirsty, face, kind, country, lad, day, side, laddie, house, heather, ranald, folk, rod, pipes, part, allister, scotland, weel, sun                                   |
| 23          | work, pride, children, genius, pleasure, model, book, paper, type, bazaar, necklace, mamma, tabernacle, manchuri, town, poetry, poem, curtains, ladder, art                  |
| 24          | mind, manner, subject, care, nothing, pleasure, character, feelings, heart, life, person, opinion, sense, evening, tears, truth, doubt, years, happiness, feeling            |
| 25          | tutor, lordship, rocket, blandford, dorincourt, house, study, liverpool, turkey, lawyer, gentlemen, heir, shanklin, court, eye, goin, tertius, prefects, grandfather, sefton |
| 26          | duchess, orphan, doctor-in-law, flute, dolor, thyra, fish, sep, court, town, rhymester, beggar, ladies, godmother, esq, guests, friends, bashaw, cockatrice, portugal        |
| 27          | england, country, men, years, story, life, land, slaves, days, year, town, nation, wife, tale, children, lives, friends, cloth, savage, chiefs                               |
| 28          | mrs, dear, wife, ladies, lake, drawing-room, husband, dress, shop, cheap, town, deal, bonnet, painter, mill, carriage, schoolmaster, school, ma'am, windmiller               |
| 29          | party, horses, day, animals, rifle, cattle, distance, animal, morning, country, gun, elephant, night, side, dogs, ground, waggons, others, intendant, house                  |
| 30          | mamma, children, course, anything, something, kind, day, dear, grandmother, sort, lessons, face, girls, morning, afternoon, nothing, everything, moment, voice, days         |
| 31          | men, enemy, soldiers, troops, camp, attack, guns, position, town, river, day, party, officers, army, officer, ground, news, night, order, country                            |
| 32          | house, work, village, houses, men, street, children, day, road, cart, wife, plague, streets, bridge, town, country, folk, trade, farm, mill                                  |
| 33          | deck, schooner, craft, brig, men, cabin, crew, canvas, sail, breeze, board, weather, aft, mate, moment, boats, watch, quarter, course, hour                                  |
| 34          | length, fact, course, party, feet, matter, moment, means, day, case, passage, spot, minutes, appearance, work, difficulty, opportunity, hour, result, position               |
| 35          | prisoners, prison, prisoner, men, door, friend, honour, officer, cell, escape, friends, guard, soldiers, pistol, crowd, news, murder, road, brigands, blood                  |
| 36          | children, course, others, anything, carpet, something, book, door, denny, right, girls, ring, gentleman, kind, sort, day, h.o, books, police, paper                          |
| 37          | men, house, day, face, days, life, peril, hast, art, nay, brothers, methinks, forth, youth, heart, none, walls, matter, wife, news                                           |
| 38          | moment, men, feet, side, fellow, body, minutes, back, arms, sight, chance, ground, eye, line, arm, blood, lad, right, blow, shoulder                                         |
| 39          | battle, france, arms, day, england, army, soldiers, court, side, cause, knights, country, walls, brothers, victory, part, nobles, tent, foe, band                            |
| 40          | men, work, mine, flames, lad, smoke, lads, shaft, coal, engine, boys, years, air, hour, life, explosion, fireman, fires, gas, miners                                         |
| 41          | cuckoo, penn, louisiana, benet, tabitha, thar, dory, dollars, fer, thet, fog, violin, auction, here, fish, clock, persis, new, butterflies, wildermann                       |
| 42          | girls, school, room, course, dear, sort, face, money, anything, house, dress, heart, life, morning, bit, moment, child, day, tea, minute                                     |
| 43          | day, letter, money, nothing, friend, days, business, morning, gentleman, week, course, years, life, mind, house, something, anything, matter, letters, months                |
| 44          | river, trees, birds, hut, ground, savages, day, island, spot, canoe, distance, feet, sun, village, natives, rocks, food, bushes, journey, savage                             |

#### Labelling the topics

From the 45 topics, we were able to interpret and label 18 of them, listed in the table below along with their assigned labelled.

{% file src="../../.gitbook/assets/labelled_topics.csv" %}



| Topic index | Label                                                 | Words in topic                                                                                                                                                               |
| ----------- | ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2           | Topic 2: Horses                                       | horses, road, day, whip, men, gentleman, course, saddle, tail, legs, groom, mare, picture, children, jackanapes, tails, cab, grimes, reins, deal                             |
| 4           | Topic 4: Navy and pirates                             | board, men, guns, ships, vessel, shot, crew, boats, officers, deck, craft, gun, officer, vessels, pirates, frigate, shore, course, side, bay                                 |
| 6           | Topic 6: Street life                                  | yer, money, street, shop, purse, face, door, bit, streets, night, policeman, court, pocket, ma'am, morning, please, wot, thief, chapter, police                              |
| 7           | Topic 7: Church and religion                          | church, men, books, sunday, soul, minister, service, book, sin, prayer, oxford, life, chapel, day, friends, work, earth, truth, sermon, others                               |
| 8           | Topic 8: School and studying                          | boys, school, study, form, room, fellows, fellow, work, day, book, desk, holidays, class, morning, lesson, books, rest, others, house, half                                  |
| 9           | Topic 9: Night and sleeping                           | night, door, nothing, house, something, anything, bed, wall, feet, window, day, moon, morning, work, side, moment, floor, sun, back, stones                                  |
| 16          | Topic 16: Sea and navigation                          | shore, men, island, board, vessel, boats, night, cabin, beach, sail, rocks, crew, day, oars, waves, side, fish, land, tide, work                                             |
| 17          | Topic 17: House and interior                          | room, house, door, window, bed, night, morning, face, chair, moment, hour, rooms, carriage, floor, windows, stairs, servants, ladies, dinner, steps                          |
| 19          | Topic 19: Open air                                    | garden, trees, birds, day, sun, grass, summer, air, leaves, fairies, wings, nothing, earth, branches, morning, sky, ground, spring, feet, side                               |
| 20          | Topic 20: Indian Americans and life in the wilderness | indians, men, river, lake, night, ice, camp, bear, village, trail, canoe, moonlight, feet, prairie, day, hunting, wolves, tribe, deer, friends                               |
| 25          | Topic 25: Feelings and sentiments                     | tutor, lordship, rocket, blandford, dorincourt, house, study, liverpool, turkey, lawyer, gentlemen, heir, shanklin, court, eye, goin, tertius, prefects, grandfather, sefton |
| 27          | Topic 27: Nation                                      | england, country, men, years, story, life, land, slaves, days, year, town, nation, wife, tale, children, lives, friends, cloth, savage, chiefs                               |
| 31          | Topic 31: Armed conflict                              | men, enemy, soldiers, troops, camp, attack, guns, position, town, river, day, party, officers, army, officer, ground, news, night, order, country                            |
| 31          | Topic 32: Landscape: village                          | house, work, village, houses, men, street, children, day, road, cart, wife, plague, streets, bridge, town, country, folk, trade, farm, mill                                  |
| 35          | Topic 35: Prison and criminality                      | prisoners, prison, prisoner, men, door, friend, honour, officer, cell, escape, friends, guard, soldiers, pistol, crowd, news, murder, road, brigands, blood                  |
| 39          | Topic 39: Battles and Nations                         | battle, france, arms, day, england, army, soldiers, court, side, cause, knights, country, walls, brothers, victory, part, nobles, tent, foe, band                            |
| 40          | Topic 40: Coal mines and fire                         | men, work, mine, flames, lad, smoke, lads, shaft, coal, engine, boys, years, air, hour, life, explosion, fireman, fires, gas, miners                                         |
| 44          | Topic 44: Nature and native People                    | river, trees, birds, hut, ground, savages, day, island, spot, canoe, distance, feet, sun, village, natives, rocks, food, bushes, journey, savage                             |
