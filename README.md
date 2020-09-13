# Pagerank Project

Name: Seungho (Samuel) Lee\
Date: 9/13/2020

This project involves creating a simple search engine, using the PageRank alogrithm with Power Iteration method, for a following website: `https://www.lawfareblog.com`.

The above website provides legal analysis on the U.S. national security issues.

Hence, completed tasks are listed below:
1. **Task 1: the power method**
   1. Part 1 - Complete
   1. Part 2 - Complete
   1. Part 3 - Complete
   1. Part 4 - Complete
1. **Task 2: the personalization vector**
   1. Part 1 - Complete
   1. Part 2 - Complete
   1. Part 3 - Complete

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
In [2]: run pagerank.py --data=./lawfareblog.csv.gz --search_query='corona'
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=4.5861e-03 url=www.lawfareblog.com/lawfare-podcast-united-nations-and-coronavirus-crisis
INFO:root:rank=1 pagerank=4.0460e-03 url=www.lawfareblog.com/house-oversight-committee-holds-day-two-hearing-government-coronavirus-response
INFO:root:rank=2 pagerank=2.6116e-03 url=www.lawfareblog.com/britains-coronavirus-response
INFO:root:rank=3 pagerank=2.5390e-03 url=www.lawfareblog.com/prosecuting-purposeful-coronavirus-exposure-terrorism
INFO:root:rank=4 pagerank=2.3557e-03 url=www.lawfareblog.com/israeli-emergency-regulations-location-tracking-coronavirus-carriers
INFO:root:rank=5 pagerank=2.2895e-03 url=www.lawfareblog.com/why-congress-conducting-business-usual-face-coronavirus
INFO:root:rank=6 pagerank=2.2727e-03 url=www.lawfareblog.com/livestream-house-oversight-committee-holds-hearing-government-coronavirus-response
INFO:root:rank=7 pagerank=2.2520e-03 url=www.lawfareblog.com/congressional-homeland-security-committees-seek-ways-support-state-federal-responses-coronavirus
INFO:root:rank=8 pagerank=2.1878e-03 url=www.lawfareblog.com/paper-hearing-experts-debate-digital-contact-tracing-and-coronavirus-privacy-concerns
INFO:root:rank=9 pagerank=2.0339e-03 url=www.lawfareblog.com/cyberlaw-podcast-how-israel-fighting-coronavirus

In [3]: run pagerank.py --data=./lawfareblog.csv.gz --search_query='trump'
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=6.6254e-02 url=www.lawfareblog.com/donald-trump-and-politically-weaponized-executive-branch
INFO:root:rank=1 pagerank=6.0194e-02 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=2 pagerank=3.4969e-02 url=www.lawfareblog.com/trump-administrations-worrying-new-policy-israeli-settlements
INFO:root:rank=3 pagerank=3.2193e-02 url=www.lawfareblog.com/document-trump-revokes-obama-executive-order-counterterrorism-strike-casualty-reporting
INFO:root:rank=4 pagerank=3.0971e-02 url=www.lawfareblog.com/dc-circuit-overrules-district-courts-due-process-ruling-qasim-v-trump
INFO:root:rank=5 pagerank=2.8460e-02 url=www.lawfareblog.com/how-trumps-approach-middle-east-ignores-past-future-and-human-condition
INFO:root:rank=6 pagerank=2.5252e-02 url=www.lawfareblog.com/why-trump-cant-buy-greenland
INFO:root:rank=7 pagerank=2.2457e-02 url=www.lawfareblog.com/oral-argument-summary-qassim-v-trump
INFO:root:rank=8 pagerank=2.1463e-02 url=www.lawfareblog.com/dc-circuit-court-denies-trump-rehearing-mazars-case
INFO:root:rank=9 pagerank=2.1103e-02 url=www.lawfareblog.com/second-circuit-rules-mazars-must-hand-over-trump-tax-returns-new-york-prosecutors

In [4]: run pagerank.py --data=./lawfareblog.csv.gz --search_query='iran'
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=6.6142e-02 url=www.lawfareblog.com/praise-presidents-iran-tweets
INFO:root:rank=1 pagerank=2.9199e-02 url=www.lawfareblog.com/how-us-iran-tensions-could-disrupt-iraqs-fragile-peace
INFO:root:rank=2 pagerank=1.7709e-02 url=www.lawfareblog.com/cyber-command-operational-update-clarifying-june-2019-iran-operation
INFO:root:rank=3 pagerank=1.4604e-02 url=www.lawfareblog.com/aborted-iran-strike-fine-line-between-necessity-and-revenge
INFO:root:rank=4 pagerank=8.4512e-03 url=www.lawfareblog.com/iranian-hostage-crisis-and-its-effect-american-politics
INFO:root:rank=5 pagerank=8.3989e-03 url=www.lawfareblog.com/parsing-state-departments-letter-use-force-against-iran
INFO:root:rank=6 pagerank=8.2581e-03 url=www.lawfareblog.com/announcing-united-states-and-use-force-against-iran-new-lawfare-e-book
INFO:root:rank=7 pagerank=8.0561e-03 url=www.lawfareblog.com/trump-moves-cut-irans-oil-revenues-whats-his-endgame
INFO:root:rank=8 pagerank=7.1939e-03 url=www.lawfareblog.com/us-names-iranian-revolutionary-guard-terrorist-organization-and-sanctions-international-criminal
INFO:root:rank=9 pagerank=5.9405e-03 url=www.lawfareblog.com/iran-shoots-down-us-drone-domestic-and-international-legal-implications
```

**Part 3:**
The following is an output of the pages with the largest pagerank within the webgraph of `lawfareblog.com`:

```
In [5]: run pagerank.py --data=./lawfareblog.csv.gz
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=8.4183e+00 url=www.lawfareblog.com/litigation-documents-related-appointment-matthew-whitaker-acting-attorney-general
INFO:root:rank=1 pagerank=8.4183e+00 url=www.lawfareblog.com/lawfare-job-board
INFO:root:rank=2 pagerank=8.4183e+00 url=www.lawfareblog.com/documents-related-mueller-investigation
INFO:root:rank=3 pagerank=8.4183e+00 url=www.lawfareblog.com/litigation-documents-resources-related-travel-ban
INFO:root:rank=4 pagerank=8.4183e+00 url=www.lawfareblog.com/subscribe-lawfare
INFO:root:rank=5 pagerank=8.4183e+00 url=www.lawfareblog.com/masthead
INFO:root:rank=6 pagerank=8.4183e+00 url=www.lawfareblog.com/topics
INFO:root:rank=7 pagerank=8.4183e+00 url=www.lawfareblog.com/our-comments-policy
INFO:root:rank=8 pagerank=8.4183e+00 url=www.lawfareblog.com/upcoming-events
INFO:root:rank=9 pagerank=8.4183e+00 url=www.lawfareblog.com/about-lawfare-brief-history-term-and-site
```

As shown in the above, the query includes both articles and non-article pages. To address the issue, I used `--filter_ratio` at 0.2 to filter out non-article nodes. 

The filtered query produced the following results:

```
In [6]: run pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=4.2773e+00 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=2.7717e+00 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=2 pagerank=2.7533e+00 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=3 pagerank=1.8720e+00 url=www.lawfareblog.com/senate-examines-threats-homeland
INFO:root:rank=4 pagerank=1.7417e+00 url=www.lawfareblog.com/what-make-first-day-impeachment-hearings
INFO:root:rank=5 pagerank=1.7411e+00 url=www.lawfareblog.com/livestream-house-armed-services-committee-hearing-f-35-program
INFO:root:rank=6 pagerank=1.7347e+00 url=www.lawfareblog.com/whats-house-resolution-impeachment
INFO:root:rank=7 pagerank=1.6384e+00 url=www.lawfareblog.com/congress-us-policy-toward-syria-and-turkey-overview-recent-hearings
INFO:root:rank=8 pagerank=1.5597e+00 url=www.lawfareblog.com/summary-david-holmess-deposition-testimony
INFO:root:rank=9 pagerank=9.1265e-01 url=www.lawfareblog.com/events
```

**Part 4:**
In this section, I ran the following 4 commands:

1. `run pagerank.py --data=./lawfareblog.csv.gz --verbose`
1. `run pagerank.py --data=./lawfareblog.csv.gz --verbose --alpha=0.99999`
1. `run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2`
1. `run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2 --alpha=0.99999`

```
In [7]: run pagerank.py --data=./lawfareblog.csv.gz --verbose
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=8.4183e+00 url=www.lawfareblog.com/litigation-documents-related-appointment-matthew-whitaker-acting-attorney-general
INFO:root:rank=1 pagerank=8.4183e+00 url=www.lawfareblog.com/lawfare-job-board
INFO:root:rank=2 pagerank=8.4183e+00 url=www.lawfareblog.com/documents-related-mueller-investigation
INFO:root:rank=3 pagerank=8.4183e+00 url=www.lawfareblog.com/litigation-documents-resources-related-travel-ban
INFO:root:rank=4 pagerank=8.4183e+00 url=www.lawfareblog.com/subscribe-lawfare
INFO:root:rank=5 pagerank=8.4183e+00 url=www.lawfareblog.com/masthead
INFO:root:rank=6 pagerank=8.4183e+00 url=www.lawfareblog.com/topics
INFO:root:rank=7 pagerank=8.4183e+00 url=www.lawfareblog.com/our-comments-policy
INFO:root:rank=8 pagerank=8.4183e+00 url=www.lawfareblog.com/upcoming-events
INFO:root:rank=9 pagerank=8.4183e+00 url=www.lawfareblog.com/about-lawfare-brief-history-term-and-site 

In [8]: run pagerank.py --data=./lawfareblog.csv.gz --verbose --alpha=0.99999
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=1.0624e+01 url=www.lawfareblog.com/snowden-revelations
INFO:root:rank=1 pagerank=1.0624e+01 url=www.lawfareblog.com/lawfare-job-board
INFO:root:rank=2 pagerank=1.0624e+01 url=www.lawfareblog.com/masthead
INFO:root:rank=3 pagerank=1.0624e+01 url=www.lawfareblog.com/litigation-documents-resources-related-travel-ban
INFO:root:rank=4 pagerank=1.0624e+01 url=www.lawfareblog.com/subscribe-lawfare
INFO:root:rank=5 pagerank=1.0624e+01 url=www.lawfareblog.com/litigation-documents-related-appointment-matthew-whitaker-acting-attorney-general
INFO:root:rank=6 pagerank=1.0624e+01 url=www.lawfareblog.com/documents-related-mueller-investigation
INFO:root:rank=7 pagerank=1.0624e+01 url=www.lawfareblog.com/our-comments-policy
INFO:root:rank=8 pagerank=1.0624e+01 url=www.lawfareblog.com/upcoming-events
INFO:root:rank=9 pagerank=1.0624e+01 url=www.lawfareblog.com/topics

In [9]: run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=4.2773e+00 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=2.7717e+00 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=2 pagerank=2.7533e+00 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=3 pagerank=1.8720e+00 url=www.lawfareblog.com/senate-examines-threats-homeland
INFO:root:rank=4 pagerank=1.7417e+00 url=www.lawfareblog.com/what-make-first-day-impeachment-hearings
INFO:root:rank=5 pagerank=1.7411e+00 url=www.lawfareblog.com/livestream-house-armed-services-committee-hearing-f-35-program
INFO:root:rank=6 pagerank=1.7347e+00 url=www.lawfareblog.com/whats-house-resolution-impeachment
INFO:root:rank=7 pagerank=1.6384e+00 url=www.lawfareblog.com/congress-us-policy-toward-syria-and-turkey-overview-recent-hearings
INFO:root:rank=8 pagerank=1.5597e+00 url=www.lawfareblog.com/summary-david-holmess-deposition-testimony
INFO:root:rank=9 pagerank=9.1265e-01 url=www.lawfareblog.com/events

In [10]: run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2 --alpha=0.99999
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=4.7947e+01 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=1 pagerank=4.7947e+01 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
INFO:root:rank=2 pagerank=7.2709e+00 url=www.lawfareblog.com/cost-using-zero-days
INFO:root:rank=3 pagerank=2.1691e+00 url=www.lawfareblog.com/lawfare-podcast-former-congressman-brian-baird-and-daniel-schuman-how-congress-can-continue-function
INFO:root:rank=4 pagerank=1.4214e+00 url=www.lawfareblog.com/events
INFO:root:rank=5 pagerank=1.0863e+00 url=www.lawfareblog.com/water-wars-increased-us-focus-indo-pacific
INFO:root:rank=6 pagerank=1.0863e+00 url=www.lawfareblog.com/water-wars-drill-maybe-drill
INFO:root:rank=7 pagerank=1.0863e+00 url=www.lawfareblog.com/water-wars-disjointed-operations-south-china-sea
INFO:root:rank=8 pagerank=1.0863e+00 url=www.lawfareblog.com/water-wars-us-china-divide-shangri-la
INFO:root:rank=9 pagerank=1.0863e+00 url=www.lawfareblog.com/water-wars-sinking-feeling-philippine-china-relations
```

It is important to note that the last command took significantly more iterations. While the original P graph of `www.lawfareblog.com` has a large eigengap, which makes it fast to compute with any alpha values, the filtered graph does not have a large eigengap, requiring a lower alpha value for a faster convergence.

There is a trade-off between quality of results and speed of execution, depending on which alpha value is utilized. Changing alpha values produced following results:

```
In [11]: run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=4.2773e+00 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=2.7717e+00 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=2 pagerank=2.7533e+00 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=3 pagerank=1.8720e+00 url=www.lawfareblog.com/senate-examines-threats-homeland
INFO:root:rank=4 pagerank=1.7417e+00 url=www.lawfareblog.com/what-make-first-day-impeachment-hearings
INFO:root:rank=5 pagerank=1.7411e+00 url=www.lawfareblog.com/livestream-house-armed-services-committee-hearing-f-35-program
INFO:root:rank=6 pagerank=1.7347e+00 url=www.lawfareblog.com/whats-house-resolution-impeachment
INFO:root:rank=7 pagerank=1.6384e+00 url=www.lawfareblog.com/congress-us-policy-toward-syria-and-turkey-overview-recent-hearings
INFO:root:rank=8 pagerank=1.5597e+00 url=www.lawfareblog.com/summary-david-holmess-deposition-testimony
INFO:root:rank=9 pagerank=9.1265e-01 url=www.lawfareblog.com/events

In [12]: run pagerank.py --data=./lawfareblog.csv.gz --verbose --filter_ratio=0.2 --alpha=0.99999
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=4.7947e+01 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=1 pagerank=4.7947e+01 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
INFO:root:rank=2 pagerank=7.2709e+00 url=www.lawfareblog.com/cost-using-zero-days
INFO:root:rank=3 pagerank=2.1691e+00 url=www.lawfareblog.com/lawfare-podcast-former-congressman-brian-baird-and-daniel-schuman-how-congress-can-continue-function
INFO:root:rank=4 pagerank=1.4214e+00 url=www.lawfareblog.com/events
INFO:root:rank=5 pagerank=1.0863e+00 url=www.lawfareblog.com/water-wars-increased-us-focus-indo-pacific
INFO:root:rank=6 pagerank=1.0863e+00 url=www.lawfareblog.com/water-wars-drill-maybe-drill
INFO:root:rank=7 pagerank=1.0863e+00 url=www.lawfareblog.com/water-wars-disjointed-operations-south-china-sea
INFO:root:rank=8 pagerank=1.0863e+00 url=www.lawfareblog.com/water-wars-us-china-divide-shangri-la
INFO:root:rank=9 pagerank=1.0863e+00 url=www.lawfareblog.com/water-wars-sinking-feeling-philippine-china-relations
```

## Task 2: the personalization vector
The most interesting applications of pagerank involve the personalization vector.

**Part 1:**
The following output involves a usage of `WebGraph.make_personalization_vector` function. It involves filtered query on the personalization vector and ranks highly if other webpages with a specified topic also think that the page is important:

```
In [13]: run pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='corona'
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=8.8870e-01 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=1 pagerank=8.8867e-01 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
INFO:root:rank=2 pagerank=1.8256e-01 url=www.lawfareblog.com/chinatalk-how-party-takes-its-propaganda-global
INFO:root:rank=3 pagerank=1.4907e-01 url=www.lawfareblog.com/rational-security-my-corona-edition
INFO:root:rank=4 pagerank=1.4907e-01 url=www.lawfareblog.com/brexit-not-immune-coronavirus
INFO:root:rank=5 pagerank=1.0729e-01 url=www.lawfareblog.com/trump-cant-reopen-country-over-state-objections
INFO:root:rank=6 pagerank=1.0199e-01 url=www.lawfareblog.com/prosecuting-purposeful-coronavirus-exposure-terrorism
INFO:root:rank=7 pagerank=1.0199e-01 url=www.lawfareblog.com/britains-coronavirus-response
INFO:root:rank=8 pagerank=9.4298e-02 url=www.lawfareblog.com/lawfare-podcast-mom-and-dad-talk-clinical-trials-pandemic
INFO:root:rank=9 pagerank=8.7207e-02 url=www.lawfareblog.com/house-oversight-committee-holds-day-two-hearing-government-coronavirus-response
```

On the contrary, `--search_query` ranks in regards to any other pages. Hence, utilizing the option produced the following results:

```
In [14]: run pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --search_query='corona'
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=1.1602e-01 url=www.lawfareblog.com/congress-needs-coronavirus-failsafe-its-too-late
INFO:root:rank=1 pagerank=5.6374e-02 url=www.lawfareblog.com/house-oversight-committee-holds-day-two-hearing-government-coronavirus-response
INFO:root:rank=2 pagerank=5.0830e-02 url=www.lawfareblog.com/britains-coronavirus-response
INFO:root:rank=3 pagerank=5.0481e-02 url=www.lawfareblog.com/prosecuting-purposeful-coronavirus-exposure-terrorism
INFO:root:rank=4 pagerank=4.8031e-02 url=www.lawfareblog.com/livestream-house-oversight-committee-holds-hearing-government-coronavirus-response
INFO:root:rank=5 pagerank=4.7743e-02 url=www.lawfareblog.com/paper-hearing-experts-debate-digital-contact-tracing-and-coronavirus-privacy-concerns
INFO:root:rank=6 pagerank=4.3727e-02 url=www.lawfareblog.com/why-congress-conducting-business-usual-face-coronavirus
INFO:root:rank=7 pagerank=2.5817e-02 url=www.lawfareblog.com/israeli-emergency-regulations-location-tracking-coronavirus-carriers
INFO:root:rank=8 pagerank=2.5463e-02 url=www.lawfareblog.com/lawfare-podcast-united-nations-and-coronavirus-crisis
INFO:root:rank=9 pagerank=1.9066e-02 url=www.lawfareblog.com/congressional-homeland-security-committees-seek-ways-support-state-federal-responses-coronavirus
```

**Part 2:**
Another use of the `--personalization_vector_query` option is to find pages related to a specified keyword but do not directly contain it.

For example, the following query ranks all webpages by their `corona` importance, but removes webpages mentioning `corona` from the results:

```
In [15]: run pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='corona' --search_query='-corona'
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=8.8870e-01 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=1 pagerank=8.8867e-01 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
INFO:root:rank=2 pagerank=1.8256e-01 url=www.lawfareblog.com/chinatalk-how-party-takes-its-propaganda-global
INFO:root:rank=3 pagerank=1.0729e-01 url=www.lawfareblog.com/trump-cant-reopen-country-over-state-objections
INFO:root:rank=4 pagerank=9.4298e-02 url=www.lawfareblog.com/lawfare-podcast-mom-and-dad-talk-clinical-trials-pandemic
INFO:root:rank=5 pagerank=7.9633e-02 url=www.lawfareblog.com/fault-lines-foreign-policy-quarantined
INFO:root:rank=6 pagerank=7.5307e-02 url=www.lawfareblog.com/limits-world-health-organization
INFO:root:rank=7 pagerank=6.8115e-02 url=www.lawfareblog.com/chinatalk-dispatches-shanghai-beijing-and-hong-kong
INFO:root:rank=8 pagerank=6.4847e-02 url=www.lawfareblog.com/us-moves-dismiss-case-against-company-linked-ira-troll-farm
INFO:root:rank=9 pagerank=6.4847e-02 url=www.lawfareblog.com/livestream-house-armed-services-committee-holds-hearing-priorities-missile-defense
```

From the execution, I was able to find articles related to the COVID-19 pandemic that are implicative. 

**Part 3:**
While interpreting `china` related results would be interesting, I proceeded to look for topics related to `korea`. I ran the `pagerank.py` file with `--filter_ratio=0.2` and `--personalization_vector_query='korea'` options.

```
In [16]: run pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='korea' --search_query='-korea'
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=2.5013e-01 url=www.lawfareblog.com/whats-point-charging-foreign-state-linked-hackers
INFO:root:rank=1 pagerank=2.1854e-01 url=www.lawfareblog.com/defense-helsinki-conference-asia-response-sam-roggeveen
INFO:root:rank=2 pagerank=2.1593e-01 url=www.lawfareblog.com/document-joint-statement-president-trump-and-kim-jong-un
INFO:root:rank=3 pagerank=1.5761e-01 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=4 pagerank=1.1749e-01 url=www.lawfareblog.com/helsinki-asia-response-philip-bobbitt
INFO:root:rank=5 pagerank=1.0632e-01 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=6 pagerank=1.0632e-01 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=7 pagerank=8.2220e-02 url=www.lawfareblog.com/cyber-command-operational-update-clarifying-june-2019-iran-operation
INFO:root:rank=8 pagerank=7.8151e-02 url=www.lawfareblog.com/response-persistent-engagement-and-agreed-competition
INFO:root:rank=9 pagerank=7.5212e-02 url=www.lawfareblog.com/persistent-engagement-chinese-characteristics
```

The PageRank algorithm outputs inform us what types of activities (North) Korea is associated with. For instance, there are numerous links that are related to `hack` and `defense`, suggesting that North Korea conveys negative sentiment on the U.S. national security. Also, as the query includes broader national security issues, such as `china` and `impeachment`, the results imply that `korea` is highly related to others national security topics, making it an important matter in politics.