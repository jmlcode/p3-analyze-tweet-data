# Analyze Tweet Data
Wrangling and analysis of Tweets from [WeRateDogs (@dogrates)](https://twitter.com/dog_rates) and visualization of insights with Python in Jupyter Notebook. Project is motivated by and thus focuses on the data wrangling process that covers gathering, assessing and cleaning data. Various methods including programmatic approaches such as querying Twitter API with Python's Tweepy package were used to collect Tweets and relevant metadata.

## Software Requirements
* conda 4.6.3 or similar versions
* python 3.7.2 (or python 3)
* Packages
  - pandas
  - requests
  - os
  - tweepy 3.7.0
  - timeit.default_timer
  - json
  - numpy
  - copy
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
### Gathering Data
1. Enhanced Twitter Archive
    * Udacity was provided with [WeRateDogs](https://twitter.com/dog_rates) Twitter Archive which contains basic tweet data for all 5,000+ tweets.
    * Udacity _enhanced_ this original dataset by extracting dog ratings (numerator and denominator), dog names, and dog "stage" (i.e. doggo, floofer, pupper, and puppo) from the tweets' text data.
    * This enhanced version contains 2,356 rows of data, which were filtered from the 5,000+ tweets for only the tweets with ratings.
    * The enhanced Twitter archive was made available as `twitter_archive_enhanced.csv` for manual download and is assigned to the object `df_archive`.
2. Image Predictions
    * Udacity ran the images included in the tweets from the enhanced Twitter archive through a [neural network](https://www.youtube.com/watch?v=2-Ol7ZB0MmU) and made top three predictions of each dog's breed.
    * The predictions data stored in `image-predictions.tsv` contains the following columns of data.
        - tweet_id: last portion of the tweet URL after _status/_
        - jpg_url: image URL
        - img_num: image number ranging from 1 to 4 (a tweet can have up to four images)
        - p1, p2, p3: first, second, and third best predictions of the dog's breed
        - p1_conf, p2_conf, p3_conf: confidence of the algorithm in its first, second, and third predictions
        - p1_dog, p2_dog, p3_dog: whether the first, second, and third predictions are a breed of dog
    * The `image-predictions.tsv` file hosted in Udacity's server was programmatically downloaded by using the [Requests](http://docs.python-requests.org/en/master/) library to submit a request to the [URL](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv) and was assigned to the object `df_image`.
3. Additional Tweet Data
    * Additional tweet data including the counts of re-tweets and favorites which were omitted during the process of _enhancing_ the twitter archive were gathered by using Python's [Tweepy](http://www.tweepy.org/) library to query Twitter's API for each tweet's JSON data.
    * The JSON data of each tweet was written in its own line in the `tweet_json.txt` file which is assigned to the object `df_json`.

### Assessing Data
* Each of the three datasets gathered above were assessed for quality and tidiness issues.
* Only these observations from reviewing the datasets, which render cleaning necessary in the next section, were documented.

### Cleaning Data
* Three sequential steps listed below were used to address each assessment from the __Assessing Data__ section.
  1. _Define_: translate the assessment to an actionable plan for cleaning the data
  2. _Code_: programmatically clean the data based on the definition
  3. _Test_: check if the cleaned data reflect the desired outcome

## Part 2: Exploratory Data Analysis and Data Visualization

## Author
Jong Min (Jay) Lee [jmlee5629@gmail.com]

## Acknowledgement
* This project was completed as a mandatory requirement for the _Data Wrangling_ unit from the __Data Analyst Nanodegree__ program at [Udacity](https://www.udacity.com/).
* Step-by-step guidance from the [Get Started](https://developer.twitter.com/en/account/get-started) page in __Twitter Developers__ site was referenced to create an App, generate keys and tokens, and query Twitter API.
* [Tweepy Documentation](http://docs.tweepy.org/en/3.7.0/) was referenced to search for and understand the methods from the Tweepy package and their specifications and arguments which were applicable to querying Twitter API and gathering JSON data.
* Assessment and cleaning of untidy data were motivated by the framework for tidying data detailed in Hadley Wickham's _Tidy Data_.
  Wickham, H. (2014). Tidy Data. _Journal of Statistical Software, 59_(10). doi:10.18637/jss.v059.i10
