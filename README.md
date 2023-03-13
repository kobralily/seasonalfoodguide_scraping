# scraping_project
 
The goal of this project is to scrape each state's growing season for each fruit on seasonalfoodguide.org

This would mean scraping thousands of pages like https://www.seasonalfoodguide.org/veg/apples/alabama for the fruit name and growing season.

The code itself was fairly simple and straightforward, since the site was well made and doesn't use any tricky html.

## Steps:
1. Get a list of the states
    - The function get_list_states() was created (not necessary to be a function) and takes a string argument of the homepage url
    - Get the home page html with Selenium 
    - Comb through that html with BeautifulSoup to get all the state names on the page from the drop down menu list
    - Put those states in a list variable and save it for later

2. Create a function that gets all the fruit links using a single state's name
    - This function get_state_links() takes a string argument of a state's name
    - The function appends that state to a url that will lead to that state's page
    - Selenium goes to that link and gets the html
    - BeautifulSoup grabs all the links on that page which correspond to a fruit
    - The list of links are returned
    
3. Create a function that gets all the info off a fruit page using one fruit page link
    - The function get_seasonality() takes a string argument url of a fruit's page
    - Selenium gets all the html off that page
    - BeautifulSoup goes into the html to collect the state name, fruit name, and seasonality
    - Those values are put into a list and returned

4. Write it all together in a CSV
    - The function write_csv() takes the argument states_list, which is the list of states created in step 1
    - The function creates and opens a file named fruit_stats.csv in write mode to add the data
    - A headings row is added
    - A for loop is created to send each state name to the function created in step 2, get_state_links()
    - Inside that loop, another loop runs using the list of links returned by the get_state_links() function. This loop sends each link to the function created in step 3, get_seasonality()
    - The returned data from get_seasonality() is written directly to the fruit_stats.csv
    - This function ultimately results in a loop that enters each state's page, then goes to each fruit, gets the info on that fruit, then throws that info in the csv until there are no more states and no more fruits

The biggest issue I encountered was not the code itself, which only took about 4 hours to finish, but getting my computer to get through the entirety of the site. 

The scraping, when I finally got it to work, ended up taking about 15 hours or so. What would happen was whenever my computer went to sleep after being idle, the program would stop running and I would get an error and have a half-finished csv. It took a while to figure out that it was my computer's sleep that was the issue, and not something with my code or the site blocking my scraping attempts.

In truth, I still had to do the entire scraping in two parts because I had my internet conntection drop for a split second halfway through, so I finished off the CSV by splicing the states_list to only run the second half of the list of states, which ran overnight.