# About This Project

The project included connecting to a YouTube API via Python, retrieving video statistics for a YouTuber and storing this data in a Pandas DataFrame. The DataFrame will later be used for data analysis and visualisation to analyse how the YouTuber has grown over time.

# Libraries 

The main libraries of concern were Python's Requests and Pandas. 

# Simplified Methodology 

- Create Google Developer account
- Create project and enable YouTube API
- Retrieve API key
- Setup environment: this project was conducted in Jupyter Labs
- Obtain YouTuber channel ID
- Thoroughly understand YouTube API documentation to make requests to the correct endpoints
- Create separate functions: 1) Obtain all videos for a YouTube channel 2) Obtain statistics for each video 3) Cycles between endpoint pages using the nextPageToken

# API requests

## Quotas
The YouTube API documentation is very comprehensive and outlines how to access different endpoints concisely. It has a default quota of **10,000** and the search results were constrained to 500 results (see below):

"Note: Search results are constrained to a maximum of 500 videos if your request specifies a value for the channelId parameter and sets the type parameter value to video , but it does not also set one of the forContentOwner , forDeveloper , or forMine filters." - [YouTube API](https://developers.google.com/youtube/v3/docs/search/list#:~:text=Note%3A%20Search%20results%20are%20constrained,%2C%20forDeveloper%20%2C%20or%20forMine%20filters.)

## Obtaining Video Statistics (like, comment and view count)
The data regarding the videos was stored in the **items** key of the JSON response. The items key had a value equal to a list which contained multiple dictionaries. Each dictionary references a video. Within each dictionary follow the **id key and then the videoId key** to obtain the videoId value. The videoId value is inputted into a separate endpoint as a query parameter to retrieve statistics such as like count, comment count and view count.

## Page Tokens
Since the JSON results were large they were loaded onto several pages and each JSON response included a **nextPageToken or a prevPageToken** or both to enable users to gain access to all results. Therefore, to access all the results, or at least the 500 results allowed since a channelId was specified, consecutive API calls were made including a value for the pageToken query parameter in the endpoint. The final page of results does not contain a nextPageToken key in it's JSON response, however it does contain a prevPageToken key. Therefore, the final results page was identified by checking if the nextPageToken key was not in the keys of the JSON response.

# Notes 

The project was intended to be carried out using best practices in software engineering such as DRY (Don't Repeat Your) code. Therefore, where possible chunks of code were made into functions.

I do believe my retrieve_pages() function can be simplified or even reduced into the video_list function - future attempts will be made to consolidate and optimise the efficiency of the code.
