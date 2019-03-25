# Analyze Tweet Data

## Software Requirements
* conda 4.6.3 or similar versions
* python 3.7.2 (or python 3)
* Packages
  - pandas
  - requests
  - os
  - tweepy
  - timeit.default_timer
  - json

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

### Cleaning Data

## Part 2: Exploratory Data Analysis and Data Visualization

## Author
Jong Min (Jay) Lee [jmlee5629@gmail.com]

## Acknowledgement
* This project was completed as a mandatory requirement for the _Data Wrangling_ unit from the __Data Analyst Nanodegree__ program at [Udacity](https://www.udacity.com/).
