# Pagerank Project

Name: Seungho (Samuel) Lee\
Date: 9/13/2020

This project involves creating a simple search engine, using the PageRank alogrithm with Power Iteration method, for a following website: `https://www.lawfareblog.com`.

The above website provides legal analysis on the U.S. national security issues.

Hence, completed tasks are listed below:
1. **Task 1: the power method**
   1. Part 1 - Complete
   1. Part 2 - Complete (Updated with Word2Vec Implementation)
   1. Part 3 - Complete (Updated with Word2Vec Implementation)
   1. Part 4 - Complete (Updated with Word2Vec Implementation)
1. **Task 2: the personalization vector**
   1. Part 1 - Complete (Updated with Word2Vec Implementation)
   1. Part 2 - Complete (Updated with Word2Vec Implementation)
   1. Part 3 - Complete (Updated with Word2Vec Implementation)

## Task 1: the power method
Implement the `WebGraph.power_method` function in `pagerank.py` for computing the pagerank vector.

**Part 1:**
For initial assessment of my algorithm, I ran `pagerank.py` on the `small.csv.gz` graph, which yielded the following results:

```
In [1]: run pagerank.py --data=./small.csv.gz --verbose                      
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=6.0257e-01 url=4
INFO:root:rank=1 pagerank=4.6414e-01 url=6
INFO:root:rank=2 pagerank=3.4544e-01 url=5
INFO:root:rank=3 pagerank=1.9498e-01 url=2
INFO:root:rank=4 pagerank=9.9210e-02 url=3
INFO:root:rank=5 pagerank=8.9347e-02 url=1
```

**Part 2:**
As expected, the `pagerank.py` file execution, along with an option `--search_query`, resulted in a similar output, with few different links. 

The following is my output:

```
In [1]: run pagerank.py --data=./lawfareblog.csv.gz --search_query='corona'                     
INFO:gensim.models.keyedvectors:precomputing L2-norms of word weight vectors
INFO:root:rank=0 pagerank=0.001003776676952839 url=www.lawfareblog.com/lawfare-podcast-united-nations-and-coronavirus-crisis
INFO:root:rank=1 pagerank=0.0008922395063564181 url=www.lawfareblog.com/house-oversight-committee-holds-day-two-hearing-government-coronavirus-response
INFO:root:rank=2 pagerank=0.0007039029151201248 url=www.lawfareblog.com/britains-coronavirus-response
INFO:root:rank=3 pagerank=0.0006915341946296394 url=www.lawfareblog.com/prosecuting-purposeful-coronavirus-exposure-terrorism
INFO:root:rank=4 pagerank=0.000670412031468004 url=www.lawfareblog.com/israeli-emergency-regulations-location-tracking-coronavirus-carriers
INFO:root:rank=5 pagerank=0.0006625585374422371 url=www.lawfareblog.com/why-congress-conducting-business-usual-face-coronavirus
INFO:root:rank=6 pagerank=0.0006504578050225973 url=www.lawfareblog.com/congressional-homeland-security-committees-seek-ways-support-state-federal-responses-coronavirus
INFO:root:rank=7 pagerank=0.0006361958803609014 url=www.lawfareblog.com/paper-hearing-experts-debate-digital-contact-tracing-and-coronavirus-privacy-concerns
INFO:root:rank=8 pagerank=0.000612482544966042 url=www.lawfareblog.com/house-subcommittee-voices-concerns-over-us-management-coronavirus
INFO:root:rank=9 pagerank=0.0006018723943270743 url=www.lawfareblog.com/livestream-house-oversight-committee-holds-hearing-government-coronavirus-response

In [2]: run pagerank.py --data=./lawfareblog.csv.gz --search_query='trump'                      
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.keyedvectors:precomputing L2-norms of word weight vectors
INFO:root:rank=0 pagerank=0.005782557651400566 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=0.005233839154243469 url=www.lawfareblog.com/document-trump-revokes-obama-executive-order-counterterrorism-strike-casualty-reporting
INFO:root:rank=2 pagerank=0.005129670724272728 url=www.lawfareblog.com/trump-administrations-worrying-new-policy-israeli-settlements
INFO:root:rank=3 pagerank=0.004659898113459349 url=www.lawfareblog.com/dc-circuit-overrules-district-courts-due-process-ruling-qasim-v-trump
INFO:root:rank=4 pagerank=0.004593398422002792 url=www.lawfareblog.com/donald-trump-and-politically-weaponized-executive-branch
INFO:root:rank=5 pagerank=0.004307133611291647 url=www.lawfareblog.com/how-trumps-approach-middle-east-ignores-past-future-and-human-condition
INFO:root:rank=6 pagerank=0.0040934765711426735 url=www.lawfareblog.com/why-trump-cant-buy-greenland
INFO:root:rank=7 pagerank=0.0037590833380818367 url=www.lawfareblog.com/oral-argument-summary-qassim-v-trump
INFO:root:rank=8 pagerank=0.003450872143730521 url=www.lawfareblog.com/dc-circuit-court-denies-trump-rehearing-mazars-case
INFO:root:rank=9 pagerank=0.0034484383650124073 url=www.lawfareblog.com/second-circuit-rules-mazars-must-hand-over-trump-tax-returns-new-york-prosecutors

In [3]: run pagerank.py --data=./lawfareblog.csv.gz --search_query='iran'                       
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.keyedvectors:precomputing L2-norms of word weight vectors
INFO:root:rank=0 pagerank=0.005129670724272728 url=www.lawfareblog.com/trump-administrations-worrying-new-policy-israeli-settlements
INFO:root:rank=1 pagerank=0.005016769748181105 url=www.lawfareblog.com/update-military-commissions-continued-health-issues-recusal-motion-and-new-cell-al-iraqi
INFO:root:rank=2 pagerank=0.004574609454721212 url=www.lawfareblog.com/praise-presidents-iran-tweets
INFO:root:rank=3 pagerank=0.004417411983013153 url=www.lawfareblog.com/how-us-iran-tensions-could-disrupt-iraqs-fragile-peace
INFO:root:rank=4 pagerank=0.0034236714709550142 url=www.lawfareblog.com/france-makes-play-try-foreign-fighters-iraq
INFO:root:rank=5 pagerank=0.0026927897706627846 url=www.lawfareblog.com/cyber-command-operational-update-clarifying-june-2019-iran-operation
INFO:root:rank=6 pagerank=0.002256679581478238 url=www.lawfareblog.com/document-sens-kaine-and-young-introduce-bill-revoke-iraq-force-authorizations
INFO:root:rank=7 pagerank=0.0019391420064494014 url=www.lawfareblog.com/aborted-iran-strike-fine-line-between-necessity-and-revenge
INFO:root:rank=8 pagerank=0.0018262730445712805 url=www.lawfareblog.com/its-not-only-iraq-and-syria
INFO:root:rank=9 pagerank=0.001733092125505209 url=www.lawfareblog.com/assessing-aclu-habeas-petition-behalf-unnamed-us-citizen-held-enemy-combatant-iraq
```

**Part 3:**
The following is an output of the pages with the largest pagerank within the webgraph of `lawfareblog.com`:

```
In [4]: run pagerank.py --data=./lawfareblog.csv.gz                                             
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:root:rank=0 pagerank=0.2874051630496979 url=www.lawfareblog.com/about-lawfare-brief-history-term-and-site
INFO:root:rank=1 pagerank=0.2874051630496979 url=www.lawfareblog.com/lawfare-job-board
INFO:root:rank=2 pagerank=0.2874051630496979 url=www.lawfareblog.com/masthead
INFO:root:rank=3 pagerank=0.2874051630496979 url=www.lawfareblog.com/litigation-documents-resources-related-travel-ban
INFO:root:rank=4 pagerank=0.2874051630496979 url=www.lawfareblog.com/subscribe-lawfare
INFO:root:rank=5 pagerank=0.2874051630496979 url=www.lawfareblog.com/litigation-documents-related-appointment-matthew-whitaker-acting-attorney-general
INFO:root:rank=6 pagerank=0.2874051630496979 url=www.lawfareblog.com/documents-related-mueller-investigation
INFO:root:rank=7 pagerank=0.2874051630496979 url=www.lawfareblog.com/our-comments-policy
INFO:root:rank=8 pagerank=0.2874051630496979 url=www.lawfareblog.com/upcoming-events
INFO:root:rank=9 pagerank=0.2874051630496979 url=www.lawfareblog.com/topics
```

As shown in the above, the query includes both articles and non-article pages. To address the issue, I used `--filter_ratio` at 0.2 to filter out non-article nodes. 

The filtered query produced the following results:

```
In [5]: run pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2                          
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:root:rank=0 pagerank=0.3469613492488861 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=0.29521211981773376 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=2 pagerank=0.29039666056632996 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=3 pagerank=0.15178653597831726 url=www.lawfareblog.com/lawfare-podcast-ben-nimmo-whack-mole-game-disinformation
INFO:root:rank=4 pagerank=0.15098513662815094 url=www.lawfareblog.com/todays-headlines-and-commentary-1964
INFO:root:rank=5 pagerank=0.15098513662815094 url=www.lawfareblog.com/todays-headlines-and-commentary-1963
INFO:root:rank=6 pagerank=0.15071173012256622 url=www.lawfareblog.com/lawfare-podcast-week-was-impeachment
INFO:root:rank=7 pagerank=0.14956679940223694 url=www.lawfareblog.com/todays-headlines-and-commentary-1962
INFO:root:rank=8 pagerank=0.14366623759269714 url=www.lawfareblog.com/cyberlaw-podcast-mistrusting-google
INFO:root:rank=9 pagerank=0.14239734411239624 url=www.lawfareblog.com/lawfare-podcast-bonus-edition-gordon-sondland-vs-committee-no-bull
```

**Part 4:**
In this section, I ran the following 4 commands:

1. `run pagerank.py --data=./lawfareblog.csv.gz --verbose`
1. `run pagerank.py --data=./lawfareblog.csv.gz --verbose --alpha=0.99999`
1. `run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2`
1. `run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2 --alpha=0.99999`

```
In [6]: run pagerank.py --data=./lawfareblog.csv.gz --verbose                                   
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:root:rank=0 pagerank=0.2874051630496979 url=www.lawfareblog.com/about-lawfare-brief-history-term-and-site
INFO:root:rank=1 pagerank=0.2874051630496979 url=www.lawfareblog.com/lawfare-job-board
INFO:root:rank=2 pagerank=0.2874051630496979 url=www.lawfareblog.com/masthead
INFO:root:rank=3 pagerank=0.2874051630496979 url=www.lawfareblog.com/litigation-documents-resources-related-travel-ban
INFO:root:rank=4 pagerank=0.2874051630496979 url=www.lawfareblog.com/subscribe-lawfare
INFO:root:rank=5 pagerank=0.2874051630496979 url=www.lawfareblog.com/litigation-documents-related-appointment-matthew-whitaker-acting-attorney-general
INFO:root:rank=6 pagerank=0.2874051630496979 url=www.lawfareblog.com/documents-related-mueller-investigation
INFO:root:rank=7 pagerank=0.2874051630496979 url=www.lawfareblog.com/our-comments-policy
INFO:root:rank=8 pagerank=0.2874051630496979 url=www.lawfareblog.com/upcoming-events
INFO:root:rank=9 pagerank=0.2874051630496979 url=www.lawfareblog.com/topics 

In [7]: run pagerank.py --data=./lawfareblog.csv.gz --verbose --alpha=0.99999                   
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:root:rank=0 pagerank=0.28859302401542664 url=www.lawfareblog.com/snowden-revelations
INFO:root:rank=1 pagerank=0.28859302401542664 url=www.lawfareblog.com/lawfare-job-board
INFO:root:rank=2 pagerank=0.28859302401542664 url=www.lawfareblog.com/documents-related-mueller-investigation
INFO:root:rank=3 pagerank=0.28859302401542664 url=www.lawfareblog.com/litigation-documents-resources-related-travel-ban
INFO:root:rank=4 pagerank=0.28859302401542664 url=www.lawfareblog.com/subscribe-lawfare
INFO:root:rank=5 pagerank=0.28859302401542664 url=www.lawfareblog.com/topics
INFO:root:rank=6 pagerank=0.28859302401542664 url=www.lawfareblog.com/masthead
INFO:root:rank=7 pagerank=0.28859302401542664 url=www.lawfareblog.com/our-comments-policy
INFO:root:rank=8 pagerank=0.28859302401542664 url=www.lawfareblog.com/upcoming-events
INFO:root:rank=9 pagerank=0.28859302401542664 url=www.lawfareblog.com/litigation-documents-related-appointment-matthew-whitaker-acting-attorney-general

In [8]: run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2                
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:root:rank=0 pagerank=0.3469613492488861 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=0.29521211981773376 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=2 pagerank=0.29039666056632996 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=3 pagerank=0.15178653597831726 url=www.lawfareblog.com/lawfare-podcast-ben-nimmo-whack-mole-game-disinformation
INFO:root:rank=4 pagerank=0.15098513662815094 url=www.lawfareblog.com/todays-headlines-and-commentary-1964
INFO:root:rank=5 pagerank=0.15098513662815094 url=www.lawfareblog.com/todays-headlines-and-commentary-1963
INFO:root:rank=6 pagerank=0.15071173012256622 url=www.lawfareblog.com/lawfare-podcast-week-was-impeachment
INFO:root:rank=7 pagerank=0.14956679940223694 url=www.lawfareblog.com/todays-headlines-and-commentary-1962
INFO:root:rank=8 pagerank=0.14366623759269714 url=www.lawfareblog.com/cyberlaw-podcast-mistrusting-google
INFO:root:rank=9 pagerank=0.14239734411239624 url=www.lawfareblog.com/lawfare-podcast-bonus-edition-gordon-sondland-vs-committee-no-bull

In [9]: run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2 --alpha=0.99999
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:root:rank=0 pagerank=0.7014895677566528 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=1 pagerank=0.7014873623847961 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
INFO:root:rank=2 pagerank=0.10551629960536957 url=www.lawfareblog.com/cost-using-zero-days
INFO:root:rank=3 pagerank=0.03175504133105278 url=www.lawfareblog.com/lawfare-podcast-former-congressman-brian-baird-and-daniel-schuman-how-congress-can-continue-function
INFO:root:rank=4 pagerank=0.022039713338017464 url=www.lawfareblog.com/events
INFO:root:rank=5 pagerank=0.01602667197585106 url=www.lawfareblog.com/water-wars-increased-us-focus-indo-pacific
INFO:root:rank=6 pagerank=0.016025930643081665 url=www.lawfareblog.com/water-wars-drill-maybe-drill
INFO:root:rank=7 pagerank=0.016022762283682823 url=www.lawfareblog.com/water-wars-disjointed-operations-south-china-sea
INFO:root:rank=8 pagerank=0.016019931063055992 url=www.lawfareblog.com/water-wars-song-oil-and-fire
INFO:root:rank=9 pagerank=0.016019923612475395 url=www.lawfareblog.com/water-wars-sinking-feeling-philippine-china-relations
```

It is important to note that the last command took significantly more iterations. While the original P graph of `www.lawfareblog.com` has a large eigengap, which makes it fast to compute with any alpha values, the filtered graph does not have a large eigengap, requiring a lower alpha value for a faster convergence.

There is a trade-off between quality of results and speed of execution, depending on which alpha value is utilized. Changing alpha values produced following results:

```
In [10]: run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2               
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:root:rank=0 pagerank=0.3469613492488861 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=0.29521211981773376 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=2 pagerank=0.29039666056632996 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=3 pagerank=0.15178653597831726 url=www.lawfareblog.com/lawfare-podcast-ben-nimmo-whack-mole-game-disinformation
INFO:root:rank=4 pagerank=0.15098513662815094 url=www.lawfareblog.com/todays-headlines-and-commentary-1964
INFO:root:rank=5 pagerank=0.15098513662815094 url=www.lawfareblog.com/todays-headlines-and-commentary-1963
INFO:root:rank=6 pagerank=0.15071173012256622 url=www.lawfareblog.com/lawfare-podcast-week-was-impeachment
INFO:root:rank=7 pagerank=0.14956679940223694 url=www.lawfareblog.com/todays-headlines-and-commentary-1962
INFO:root:rank=8 pagerank=0.14366623759269714 url=www.lawfareblog.com/cyberlaw-podcast-mistrusting-google
INFO:root:rank=9 pagerank=0.14239734411239624 url=www.lawfareblog.com/lawfare-podcast-bonus-edition-gordon-sondland-vs-committee-no-bull

In [11]: run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2 --alpha=0.99999
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:root:rank=0 pagerank=0.7014895677566528 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=1 pagerank=0.7014873623847961 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
INFO:root:rank=2 pagerank=0.10551629960536957 url=www.lawfareblog.com/cost-using-zero-days
INFO:root:rank=3 pagerank=0.03175504133105278 url=www.lawfareblog.com/lawfare-podcast-former-congressman-brian-baird-and-daniel-schuman-how-congress-can-continue-function
INFO:root:rank=4 pagerank=0.022039713338017464 url=www.lawfareblog.com/events
INFO:root:rank=5 pagerank=0.01602667197585106 url=www.lawfareblog.com/water-wars-increased-us-focus-indo-pacific
INFO:root:rank=6 pagerank=0.016025930643081665 url=www.lawfareblog.com/water-wars-drill-maybe-drill
INFO:root:rank=7 pagerank=0.016022762283682823 url=www.lawfareblog.com/water-wars-disjointed-operations-south-china-sea
INFO:root:rank=8 pagerank=0.016019931063055992 url=www.lawfareblog.com/water-wars-song-oil-and-fire
INFO:root:rank=9 pagerank=0.016019923612475395 url=www.lawfareblog.com/water-wars-sinking-feeling-philippine-china-relations
```

## Task 2: the personalization vector
The most interesting applications of pagerank involve the personalization vector.

**Part 1:**
The following output involves a usage of `WebGraph.make_personalization_vector` function. It involves filtered query on the personalization vector and ranks highly if other webpages with a specified topic also think that the page is important:

```
In [12]: run pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='corona'
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.keyedvectors:precomputing L2-norms of word weight vectors
INFO:root:rank=0 pagerank=0.6320855617523193 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=1 pagerank=0.6320620179176331 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
INFO:root:rank=2 pagerank=0.15656693279743195 url=www.lawfareblog.com/chinatalk-how-party-takes-its-propaganda-global
INFO:root:rank=3 pagerank=0.12040437757968903 url=www.lawfareblog.com/rational-security-my-corona-edition
INFO:root:rank=4 pagerank=0.12040437757968903 url=www.lawfareblog.com/brexit-not-immune-coronavirus
INFO:root:rank=5 pagerank=0.09199091792106628 url=www.lawfareblog.com/trump-cant-reopen-country-over-state-objections
INFO:root:rank=6 pagerank=0.08998079597949982 url=www.lawfareblog.com/prosecuting-purposeful-coronavirus-exposure-terrorism
INFO:root:rank=7 pagerank=0.08998079597949982 url=www.lawfareblog.com/britains-coronavirus-response
INFO:root:rank=8 pagerank=0.07601435482501984 url=www.lawfareblog.com/lawfare-podcast-united-nations-and-coronavirus-crisis
INFO:root:rank=9 pagerank=0.0717419981956482 url=www.lawfareblog.com/house-oversight-committee-holds-day-two-hearing-government-coronavirus-response
```

On the contrary, `--search_query` ranks in regards to any other pages. Hence, utilizing the option produced the following results:

```
In [13]: run pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --search_query='corona' 
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.keyedvectors:precomputing L2-norms of word weight vectors
INFO:root:rank=0 pagerank=0.008131962269544601 url=www.lawfareblog.com/house-oversight-committee-holds-day-two-hearing-government-coronavirus-response
INFO:root:rank=1 pagerank=0.007790825795382261 url=www.lawfareblog.com/lawfare-podcast-united-nations-and-coronavirus-crisis
INFO:root:rank=2 pagerank=0.005226220469921827 url=www.lawfareblog.com/livestream-house-oversight-committee-holds-hearing-government-coronavirus-response
INFO:root:rank=3 pagerank=0.0039583845064044 url=www.lawfareblog.com/britains-coronavirus-response
INFO:root:rank=4 pagerank=0.003811446251347661 url=www.lawfareblog.com/prosecuting-purposeful-coronavirus-exposure-terrorism
INFO:root:rank=5 pagerank=0.003397284774109721 url=www.lawfareblog.com/paper-hearing-experts-debate-digital-contact-tracing-and-coronavirus-privacy-concerns
INFO:root:rank=6 pagerank=0.0033633282873779535 url=www.lawfareblog.com/cyberlaw-podcast-how-israel-fighting-coronavirus
INFO:root:rank=7 pagerank=0.0033556800335645676 url=www.lawfareblog.com/israeli-emergency-regulations-location-tracking-coronavirus-carriers
INFO:root:rank=8 pagerank=0.0032159897964447737 url=www.lawfareblog.com/congress-needs-coronavirus-failsafe-its-too-late
INFO:root:rank=9 pagerank=0.0031036492437124252 url=www.lawfareblog.com/why-congress-conducting-business-usual-face-coronavirus
```

**Part 2:**
Another use of the `--personalization_vector_query` option is to find pages related to a specified keyword but do not directly contain it.

For example, the following query ranks all webpages by their `corona` importance, but removes webpages mentioning `corona` from the results:

```
In [14]: run pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='corona' --search_query='-corona'
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.keyedvectors:precomputing L2-norms of word weight vectors
INFO:root:rank=0 pagerank=0.6320855617523193 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=1 pagerank=0.6320620179176331 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
INFO:root:rank=2 pagerank=0.15656693279743195 url=www.lawfareblog.com/chinatalk-how-party-takes-its-propaganda-global
INFO:root:rank=3 pagerank=0.09199091792106628 url=www.lawfareblog.com/trump-cant-reopen-country-over-state-objections
INFO:root:rank=4 pagerank=0.06943929940462112 url=www.lawfareblog.com/lawfare-podcast-mom-and-dad-talk-clinical-trials-pandemic
INFO:root:rank=5 pagerank=0.06895698606967926 url=www.lawfareblog.com/fault-lines-foreign-policy-quarantined
INFO:root:rank=6 pagerank=0.06389345228672028 url=www.lawfareblog.com/limits-world-health-organization
INFO:root:rank=7 pagerank=0.05843931436538696 url=www.lawfareblog.com/chinatalk-dispatches-shanghai-beijing-and-hong-kong
INFO:root:rank=8 pagerank=0.0507182851433754 url=www.lawfareblog.com/us-moves-dismiss-case-against-company-linked-ira-troll-farm
INFO:root:rank=9 pagerank=0.05071817338466644 url=www.lawfareblog.com/livestream-house-armed-services-holds-hearing-national-security-challenges-north-and-south-america
```

From the execution, I was able to find articles related to the COVID-19 pandemic that are implicative. 

**Part 3:**
While interpreting `china` related results would be interesting, I proceeded to look for topics related to `korea`. I ran the `pagerank.py` file with `--filter_ratio=0.2` and `--personalization_vector_query='korea'` options.

```
In [15]: run pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='korea' --search_query='-korea'
INFO:gensim.models.utils_any2vec:loading projection weights from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.utils_any2vec:loaded (1193514, 200) matrix from /Users/slee19/gensim-data/glove-twitter-200/glove-twitter-200.gz
INFO:gensim.models.keyedvectors:precomputing L2-norms of word weight vectors
INFO:root:rank=0 pagerank=0.2753930985927582 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=0.24798652529716492 url=www.lawfareblog.com/whats-point-charging-foreign-state-linked-hackers
INFO:root:rank=2 pagerank=0.21604172885417938 url=www.lawfareblog.com/defense-helsinki-conference-asia-response-sam-roggeveen
INFO:root:rank=3 pagerank=0.21363480389118195 url=www.lawfareblog.com/document-joint-statement-president-trump-and-kim-jong-un
INFO:root:rank=4 pagerank=0.1699959933757782 url=www.lawfareblog.com/water-wars-disjointed-operations-south-china-sea
INFO:root:rank=5 pagerank=0.16543012857437134 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=6 pagerank=0.16543012857437134 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=7 pagerank=0.1545444130897522 url=www.lawfareblog.com/water-wars-increased-us-focus-indo-pacific
INFO:root:rank=8 pagerank=0.1543947160243988 url=www.lawfareblog.com/water-wars-drill-maybe-drill
INFO:root:rank=9 pagerank=0.15345491468906403 url=www.lawfareblog.com/senate-examines-threats-homeland
```

The PageRank algorithm outputs inform us what types of activities (North) Korea is associated with. For instance, there are numerous links that are related to `hack` and `wars`, suggesting that North Korea conveys negative sentiment on the U.S. national security. Also, as the query includes broader national security issues, such as `china` and `impeachment`, the results imply that `korea` is highly related to others national security topics, making it an important matter in politics.