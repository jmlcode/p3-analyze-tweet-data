# Analyze Tweet Data
Wrangling and analysis of Tweets from [WeRateDogs (@dogrates)](https://twitter.com/dog_rates) and visualization of insights with Python in Jupyter Notebook. Project was motivated by and thus focuses on the data wrangling process that covers gathering, assessing and cleaning data. Various methods including programmatic approaches such as querying Twitter API with Python's Tweepy package were used to collect Tweets and relevant metadata.

## Software Requirements
* conda 4.6.3 or similar versions
* python 3.7.2 (or python 3)
* Packages
  - pandas
  - requests
  - os
  - tweepy 3.7.0
    ```bash
    git clone git://github.com/tweepy/tweepy.git
    cd tweepy
    python setup.py install
    ```
  - timeit.default_timer
  - json
  - numpy
  - copy
  - datetime
  - matplotlib.pyplot
  - seaborn
  - statsmodels.api
  - TextBlob
    ```bash
    pip install -U textblob
    python -m textblob.download_corpora
    ```
* `twitter_api.py` file
  - The file returns Twitter API Wrapper for querying Twitter's API in _Section 3_ of __Gathering Data__ with the Tweet IDs obtained from the first dataset in _Section 1_ of __Gathering Data__.
  - The file was imported to the notebook and was not tracked in the repository in order to prevent disclosure of private keys and tokens.
  ```python
    import tweepy

    def twitter_api():

      # Keys and Tokens
      consumer_key = 'CONSUMER KEY'
      consumer_secret = 'CONSUMER SECRET'
      access_token = 'ACCESS TOKEN'
      access_secret = 'ACCESS SECRET'

      # OAuthHandler instance equipped with an access token for OAuth Authentication
      auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
      auth.set_access_token(access_token, access_secret)

      # twitter API wrapper
      return tweepy.API(auth_handler = auth, wait_on_rate_limit = True, wait_on_rate_limit_notify = True)
  ```

## Part 1: Data Wrangling
* Content of the first part of the project including all code blocks for data wrangling is documented in the Jupyter Notebook file, `analyze_tweet_1_wrangle.ipynb`. The HTML file `analyze_tweet_part1_wrangle.html` was published from this notebook file.
* Three raw datasets gathered in the first step of data wrangling and the clean version of the master dataset obtained after the last step of data wrangling are all available in the `\data` directory.
    * Raw Datasets
      - `twitter_archive_enhanced.csv`
      - `image-predictions.tsv`
      - `tweet_json.txt`
    * Merged Dataset: `twitter_archive_master.csv`

### Gathering Data
1. Enhanced Twitter Archive
    * Udacity was provided with [WeRateDogs](https://twitter.com/dog_rates) Twitter Archive which contains basic tweet data for all 5,000+ tweets.
    * Udacity _enhanced_ this original dataset by extracting dog ratings, dog names, and dog "stage" from the tweets' text data.
    * The enhanced Twitter archive was made available as `twitter_archive_enhanced.csv` for manual download and is assigned to the object `df_archive`.
2. Image Predictions
    * Udacity ran the images included in the tweets from the enhanced Twitter archive through a [neural network](https://www.youtube.com/watch?v=2-Ol7ZB0MmU) and made top three predictions of each dog's breed.
    * The `image-predictions.tsv` file hosted in Udacity's server was programmatically downloaded by using the [Requests](http://docs.python-requests.org/en/master/) library to submit a request to the [URL](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv) and was assigned to the object `df_image`.
3. Additional Tweet Data
    * Additional tweet data which were omitted during the process of _enhancing_ the twitter archive were gathered by using Python's [Tweepy](http://www.tweepy.org/) library to query Twitter's API.
    * The JSON data of each tweet was dumped in the `tweet_json.txt` file.
    * Only the re-tweet and favorite counts for each tweet was extracted and assigned to the object `df_json`.

### Assessing Data
* Each of the three datasets gathered above were assessed for quality and tidiness issues.
* Only these observations from reviewing the datasets, which render cleaning necessary in the next section, were documented.

### Cleaning Data
* Each assessment from the __Assessing Data__ section was addressed in three sequential steps: define, code, and test.
* The clean versions of the three datasets were merged to create `df_archive_master`, which was stored as a separate `.csv` file, `twitter_archive_master.csv`.

## Part 2: Exploratory Data Analysis and Data Visualization
1. Time of the Day when _WeRateDogs (@dogrates)_ Shows Most Activity
    * Each day of the week was divided into 24-hour increments.
    * Tweet activity was quantified by the percentage of tweets in each increment for a given day.
    * Bar plots, box plots and statistics (mean, standard deviation, quartiles) of the 24 percentages for each day are presented.
2. Correlation between Favorite Counts and Retweet Counts
    * Data points with favorite count of 0 were defined as outliers.
    * For both sets of favorite counts and retweet counts pairs, one including and another excluding outliers,
      - Two scatter plots were created.
      - Two linear regressions were performed.
      - Correlation Coefficients and R-squared values are presented.
3. Comparison of Dog Ratings and Sentiment of Tweets
    * Numeric dog ratings were categorized into _low_, _medium_, and _high_ ratings.
    * Polarity scores of the text data of original tweets were gathered from sentiment analysis.
    * Three histograms of the polarity scores, one for each category of dog ratings, are presented.
4. Accuracy and Precision of Predicting Dog's Breeds from Images
    * The performance of the neural network in recognizing images and predicting each dog's breed was assessed with both statistics and visualizations.
      - Mean proportion of predictions with dog breeds for each level of prediction
      - Histogram for the distribution of confidence levels for each level of prediction and its center (median)

## Author
Jong Min (Jay) Lee [jmlee5629@gmail.com]

## Acknowledgement
* This project was completed as a mandatory requirement for the _Data Wrangling_ unit from the __Data Analyst Nanodegree__ program at [Udacity](https://www.udacity.com/).
* Step-by-step guidance from the [Get Started](https://developer.twitter.com/en/account/get-started) page in __Twitter Developers__ site was referenced to create an App, generate keys and tokens, and query Twitter API.
* [Tweepy](http://docs.tweepy.org/en/3.7.0/) documentation was referenced to search for and understand the methods from the Tweepy package and their specifications and arguments which were applicable to querying Twitter API and gathering JSON data.
* Assessment and cleaning of untidy data were motivated by the extensive nature this process in data analysis (Dasu and Johnson 2003) and the framework for tidying data (Wickham 2014).
  - Dasu T, Johnson T (2003). _Exploratory Data Mining and Data Cleaning._ John Wiley & Sons.
  - Wickham, H. (2014). Tidy Data. _Journal of Statistical Software, 59_(10). doi:10.18637/jss.v059.i10
* [TextBlob](https://textblob.readthedocs.io/en/dev/quickstart.html#sentiment-analysis) documentation was referenced to create a `TextBlob` with text data and obtain _polarity_ score from the `sentiment` property.
