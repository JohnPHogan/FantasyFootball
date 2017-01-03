# FantasyFootball  #
Scripts to create CSV files from footballdb.com data and then perform analysis on them
## Python source file
GetPlayerData.ipynb

## Web Source  ##
http://www.footballdb.com

### Dependencies  ###

The program depends on the existence of CSV based files for each position you wish to evaluate.  qb.csv, rb.csv and wr.csv already exist.  These files consist of two columns:  NAME and PAGE.  The name needs to be the first and last name of the player separated by a space and the second column must be the numeric counter that the website uses to manage players whose names are similar enough to cause a naming collision.  The number, as far as i can tell, increments for each occurrance.  Here are a couple examples:

NAME,PAGE
Aaron Brown,4
Adrian Peterson,2
Ahmad Bradshaw,1
Ahmard Hall,1

### Code  ###

The first script of the Jupyter Notebook, labled Player Yearly Total, will take the values from from the file mentioned above and create the appropriate URL to get the yearly data for each player.    

The base url for footballdb.com is:

http://www.footballdb.com/players/

To get the summary data for a player you need to add take the first and last name and create a new string where they are separated by a hyphen, and then append another hyphe.  Then the first 5 charaters of the player's last name and the first two characters of their first name together.  Any sort of punctuation in the player's name (appostrophe's or periods, for example) must be stripped prior to creating this string. A.J, Green because aj-green-greenaj  After that, the numeric value needs to be appended as a 2 digit value.  

http://www.footballdb.com/players/aj-green-greenaj02

The output from this script will be rows of data for each player with the year that player was in the NFL, the accumulating count of what year that represents in their career, and the basic stats for that position.  This data will be written out to the <position>_yearly.csv file.  

The second script, Player Game Totals, uses the files created from the first script and uses it to traverse each game's data for each year the player has played to date.  It starts from the base URL listed above, adds the name string created in the first script and then appends '/gamelogs/' and the year it gathered from the first page.  An example is:

http://www.footballdb.com/players/aj-green-greenaj02/gamelogs/2011

At this level, there can be multiple tables of data for each player.  Quarterback passing data will be of key importance, but also running data will be availble if the quiarterback runs in any game during a specific year.  The data is stored in two different tables on the web page, but grouped together into a single row in the output.  The headings in the columns are amended to mark if they are Passing, Rushing, or Receiving data.
.   
