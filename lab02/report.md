# Lab 02 Report — Web Scraping, Feature Engineering and EDA

## Task 2.1 — NumPy vs Manual Loop Timing

Summing 10,000,000 random floats:

| Method | Time (sec) |
|---|---|
| NumPy vectorised sum | 0.01006 |
| Manual Python loop | 1.36312 |

Both methods agree on the result (4999374.17), but NumPy was roughly **135x faster**.
This is because NumPy runs the operation as a single compiled instruction over the
whole array, while the manual loop pays Python's interpreter overhead on every one
of the 10 million iterations.

## Task 2.2/2.3 — Scraping and Feature Engineering

Five articles were scraped from techncruncher.blogspot.com and enriched with
spaCy-derived linguistic features (token count, sentence count, named entity
count, noun count) and TextBlob sentiment scores (polarity, subjectivity).

## Task 2.4 — Exploratory Data Analysis

- **Title length distribution:** shown in `figures/01_title_length_dist.png`.
- **Sentiment polarity distribution:** shown in `figures/02_sentiment_polarity_dist.png`.
  Articles skewed mildly positive overall, consistent with promotional blog content.
- **Pair plot of derived features:** shown in `figures/03_pairplot.png`. With only
  five articles, any apparent correlations are indicative rather than conclusive.

## TF–IDF Interpretation

The top TF-IDF terms across the original five articles (stopwords removed) were
dominated by content-specific vocabulary such as "content", "ai", "tool", "limewire",
"creators", and "features" — shown in `figures/04_tfidf_terms.png`.

**Exercise 4 (with vs without stopwords):** re-running TF-IDF with `stop_words=None`
pulled common English function words (e.g. "the", "and", "a") into the top-20 list,
crowding out some of the more topic-specific terms that appeared when stopwords
were removed. This confirms that stopword removal is necessary for TF-IDF to
surface genuinely *characteristic* vocabulary rather than just frequent words.

## Exercise 1 — Extended URL Test

Testing 7 URLs (5 original + 2 added) against the original Blogger selectors
(`h3.post-title`, `div.post-body.entry-content`) showed that several of the
newer/different pages failed to parse, because their HTML structure didn't match
those specific tag/class combinations — confirming that scraper selectors are
site-template-specific and don't generalize across different blogs without
adjustment.

## Exercise 2 — Extended Features

Added `num_verbs` and `avg_sentence_length` to the feature set. Pair plot shown
in `figures/06_extended_features_pairplot.png`.

## Exercise 3 — KDE on Five Points

With a sample size of n = 5, a kernel density estimate is not a reliable estimate
of the population distribution — it is highly sensitive to the exact values of
individual data points, and should be read as a rough visual smoothing aid rather
than evidence of any true underlying distribution shape.

## Home Assignment — Two-Source Comparison

20 articles were scraped: 10 from **techncruncher.blogspot.com** and 10 from
**matrixdigests.blogspot.com**. Comparison chart: `figures/05_source_comparison.png`.

| Source | Mean Polarity | Mean Noun Density |
|---|---|---|
| techncruncher | 0.2179 | 0.2313 |
| matrixdigests | 0.1279 | 0.2301 |

- **Polarity difference:** −0.0900 (techncruncher scored notably more positive)
- **Noun density difference:** −0.0012 (essentially no difference)

**Interpretation:** With only 10 articles per source, techncruncher's higher mean
polarity (0.218 vs 0.128) is a difference worth noting, but with this sample size
it could easily reflect a handful of unusually upbeat or neutral posts rather than
a true stylistic difference between the two blogs. Noun density was nearly
identical between sources, suggesting no meaningful difference in how noun-heavy
their writing is. To treat the polarity gap as a real, reliable pattern rather
than sampling noise, a larger sample per source and a statistical test (e.g. an
independent-samples t-test) would be needed to confirm the difference exceeds
what random variation between articles would produce on its own.