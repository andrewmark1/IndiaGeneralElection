# IndiaGeneralElection 

## OBJECTIVE: 
  Create database of parties and candidates from the 2014 Indian Election

## DEVELOPERS: 
  andrewmark1 and gaurav14111

## TOOLS: 
  Python (Pandas, BeautifulSoup, SQLAlchemy, Google.cloud.language, Selenium)

## RESOURCES:
### IndiaVotes: http://www.indiavotes.com/pc/party_list/0/16
    Data on all parties from the 2014 election including:
     * Total Contestants
     * Number Won
     * Number Runner-up
     * Number 2nd Runner-up
     * Total votes

### Google News: https://www.google.com/search?source=lnms&tbm=nws
    Retrieve top news articles for party and major candidate
    Used for sentiment analysis data

### Google Trends: Using Python library called PyTrends
    Filtering first 9 top parties based on the votes they received
    Searching for 9 party leaders
    Pulling Data from google trends about party
    Pulling Data from google trends about party leaders

### Wikipedia: https://www.wikipedia.org/
    Retrieve information on each party including:
      Party Abbreviation
      President
      Year Founded
      Headquarters
      Student/Youth/Women’s Wing
      Seats in Lok Sabha

## FILES:
### IndiaVotesCollection.ipynb
 * **Extract**: Using Selenium, pulls html data from IndiaVotes website
 * **Transform**: Filter out unnecessary tables and columns. Set Index to Party
 * **Load**: Output to PartySummary.csv

### NewsScraping.ipynb
 * **Extract**: Using BeautifulSoup, pulls headlines for the top 9 parties (as determined by PartySummary.csv)
 * **Transform**: Grab only the headline text and store as dictionary (key: party name, value: headline). Use Google Language Service Client   to compute sentiment score for each headline and add to a dictionary. Create dataframe with produced dictionary. Run statistics on       dataframe. Transform database so that code is the axis.
 * **Load**: Output to SentimentScores.csv

### WkipediaScraping
 * **Extract**: Using BeautifulSoup pull descriptive table from Wikipedia for the top 9 parties.
 * **Transform**: Rename columns to be more descriptive. Remove footnotes from values. Set index to Properties. Joined together all 9 tables   (outer join).Transpose data so that Code is the axis. Set ‘Shiv Sena’ abbreviation to be SHS.
 * **Load**: Output to PartyProperties.csv

### IndianGeneralElection2014.ipynb
 * **Extract**: Using Pandas Data frame loaded .csv file, Google Trends for top 9 parties, Google Trends for top 9 party leaders
 * **Transform**: Created a column called Code and using map function created code for each party. Transformed Party name to party code in     google trend output. Created code in Google trends data frame. Used Code column as index. Removed date column. Transposed Google Trend   data
 * **Load**: IndianGeneralElectionData.csv, Party_Leader_Ratings_googleTrends.csv, Party_Rating_googleTrends.csv

### SqlDatabase.ipynb
 * **Extract**: Pull PartySummary.csv, SentimentScores.csv, PartyProperties.csv, IndiaGeneralElection.csv, PartyLeaderRatings.csv,             PartyRatings.csv
 * **Transform**: Tables to dataframes and loaded into a sqlite database
 * **Load**: Output IndiaElectionDB.sql which contains 6 tables
