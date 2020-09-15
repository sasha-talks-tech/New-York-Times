# Women Through the Lens of The New York Times: Data Journalism Project. 
*****************************************************************************************************************************************************************
The **goal** of this project is to investigate womens' representation in The New York Times though the sentiment analysis, frequent term visualization and topic modeling.

For this investigation I scraped The New York Times data through the [Archive API](https://developer.nytimes.com/docs/archive-product/1/overview) of The New York Times Developer Portal. First, you have to obtain the API key [here](https://developer.nytimes.com/). It's free! The NYT just likes the concept of the regulated flood gate. Since this type of the API is good for the bulk data collection, it doesn't allow for effective prior filtering. Please follow the instructions in the notebooks if you wish to re-create the experiment.
*****************************************************************************************************************************************************************
*****************************************************************************************************************************************************************
**data_collection_topics** is the very first notebook in the series. I broke down the data collection into smaller increments in order not to overload the API as well as the internet connection. The helper function scrapes the data for the specified time period and saves it into the **headlines.csv** file: one file for each corresponding month for each year requested, which you can further concatenate into one dataframe for further analysis and filtering.

I decided to run the generic topic modeling first in order to make sure that the topic of my research goes along the lines of The New York Times mission statement, and that I'm not misrepresenting their journalisn style.

In this notebook we run topic modeling using the Latent Dirichlet Allocation (LDA) and gensim. 
Prevalent **topics** discovered: COVID-19, police brutality, politics and social policies, election, climate crisis and natural disasters, race and gender representation. Even though all the topics are equally important and serious, I went with the gender representation.
*****************************************************************************************************************************************************************
*****************************************************************************************************************************************************************
**project5_data_gather** is the next notebook in our series. Since we chose a large timeframe - 70 years, the code needs to be run in chunks. A decade seems like an optimal timeframe for each round. As the result, we will have the articles' headline and keywords for the range 1950-2020.
The *helper functions* allow for automated the data collection: <br>
* *send_request* prepares the request into the archive for a given date, and returns a response.<br>
* *is_valid* checks whether the article falls into the requested timeframe, confirms whether the headline is present, thus insuring the article's validity, and returns a binary result of is_in_range and has_headline. <br>
* *parse_response* turns the json response into a dataframe. data here is a dictionary where we specify what we want our columns to be. If everything is valid, it appends to the dictionary and returns a dataframe. <br>
* *get_data* uses send_request and parse_response as well as the dates specified by user, and then saves the headlines and other info to csv files corresponding to each month within the range. <br>

Result: 11,472,902 articles collected.
*****************************************************************************************************************************************************************
*****************************************************************************************************************************************************************
**project5_data_analysis** is the 3rd notebook of The New York Times project series. In the previous notebook we collected the data from 1950 - present through the Archive API. In this notebook we will clean and organize the obtained dataframe and filter the relevant data.
This notebook contains **several dataframes**. Here are the df's that are important for our analysis along with the summary of their contents:<br>
****************************************************************************************************************
* **df** (also known as the **frame_all.pickle**): <br>
contains all the data between 1950 and the present day (11+ million rows). It was acquired through the [Archive API](https://developer.nytimes.com/docs/archive-product/1/overview) of The New York Times. The Archive API allows for efficient bulk data collection for extensive periods of time, but it doesn't allow any kind of querying. This is why all the filtering is performed on the dataframe directly.
****************************************************************************************************************
* **project_df**: <br>
contains data filtered from the big **df** based on the presence of certain keywords in the article titles as well *keywords column.* Our target keywords used for filtering include, but aren't limited to, activism, suffragist movement, science, technology, professonal growth, entrepreneurship, feminism, business and politics.
****************************************************************************************************************
* **persons**: <br>
dataframe that I obtained by searching for certain names mentioned in the headlines, e.g. Serena Williams, Harriet Tubman and Malala Yousafzai.

**Note**: The term "strong women" is used subjectively according to the criteria defined by me for the purpose of this exercise, e.g women in politics, entrepreneurship, civil rights movement, social activism etc. It's by no means meant to exclude anyone from this group. I will appreciate any advice and guidance for expanding and enriching this dataset.

Further comments, storyline and visualizations can be found in the slidedeck attached. If you have any questions, please don't hesitate to reach out!
