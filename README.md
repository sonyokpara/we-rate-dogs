# WeRateDogs Data Wrangling  
 

## Introduction 

In this project my focus was on wrangling (and analyzing and visualizing) the tweet archive of Twitter user [@dog_rates](https://twitter.com/dog_rates) also known as WeRateDogs. [WeRateDogs](https://en.wikipedia.org/wiki/WeRateDogs) is a Twitter account that rates people's dogs with a humorous comment about the dog.  


## Wrangling Efforts 
 
### Gather 

I began by importing all the required packages for this project. Packages I used include: 

+ Pandas 
+ NumPy 
+ Requests Library
+ Tweepy API 
+ JSON 
+ Matplotlib  
+ Timer  

I gathered data from 3 different sources. First is the twitter_archive_enhanced.csv file which was already provided by Udacity. Second is the image_predictions.tsv file which I download programmatically using python’s Request Library. Lastly I used Twitter API to programmatically download additional data with Tweepy Library and saved as tweet_json.txt. Next I loaded the 3 dataframes using pandas’ read_csv() method.  

### Assess 

I explored the datasets in detail to gain full intuition into its structure and content using both visual and programmatic assessments. I used pandas to display the dataframes individually as well as Google Docs. 
Methods such as info(), describe(), sample() were used.  
I resolved 8 quality and 2 tidiness issues. 

#### Quality Issues  

+ Wrong data type for timestamp and tweet_id.   
+ Text column contains links which can be extracted into a new column.  
+ Source values recorded as hyperlinks instead of actual source like iPhone, Vine, Twitter, etc. 
+ Mistakes in dog ratings.   
+ Inaccurate and arbitrary dog names such as a*, *an, by, his, etc.   
+ Text column contains html entity `&amp; used instead of & and also `\n` for new line.   
+ tweet_id data type should be string instead of int64.   
+ Values for p1, p2, p3 are not case-consistent i.e. mixed uppercase and lowercase values. 

#### Tidiness Issues  
+ doggo, loofer, pupper, and puppo columns were grouped into one dog_stage column. 
+ Drop redundant columns in twitter_archived, drop all null values and merge the 3 tables. 

### Cleaning  

I made a copy of each dataset before cleaning. Using the DCT (Define, Code, and Test) framework, we take turns to clean the data.  

`Quality`

**Issue #1**:  Wrong data type for timestamp and tweet_id. 

**Solution**: I changed the data type of timestamp from string to datetime and tweet_id from int64 to string/object.  

**Issue #2**: Text column contains links which can be extracted into a new column. 

**Solution**: Using regular expressions, I extracted the URLs in the tweet text and saved them in a new column I called tweet_url.  

**Issue #3**: Source values recorded as hyperlinks instead of actual source like iPhone, Vine, Twitter, etc. 

**Solution**: I replaced all the html link tags with the actual content i.e. iPhone, Vine, Twitter, etc.  

**Issue 4#**: Wrong dog ratings apparently due to wrong interpretation of figurative expressions such as 24/7, 9/11, etc. as valid dog ratings. 

**Solution**: I mapped all erroneous ratings with text from which they were extracted. Using methods such as contains and extractall I sanitized the ratings. 

**Issue 5#**: Inaccurate and arbitrary dog names such as a, an, by, his, etc. 

**Solution**: I replaced all arbitrary names such as a, an, by, etc. with numpy.nan.  
And so on till all issues were cleaned.  
 
`Tidiness`  

**Issue 9#**: doggo, floofer, pupper, and puppo columns should be grouped into one dog_stage column. 

**Solution**: Replace all none values with empty string in doggo, floofer, pupper, puppo columns. I concatenated doggo, floofer, pupper and puppo into a single dog. And finally dropped, floofer, pupper and puppo columns. 

**Issue 10#**: Drop redundant columns in twitter_archived, drop all null values and merge the 3 tables. 

**Solution**: I dropped all redundant columns i.e. `in_reply_to_status_id`, `in_reply_to_user_id`, `retweet_status_id`, `retweeted_status_user_id`, `retweeted_status_timestamp`. 

Finally I merged all the cleaned datasets and save it as `twitter_archive_master.csv`.  
 
 
