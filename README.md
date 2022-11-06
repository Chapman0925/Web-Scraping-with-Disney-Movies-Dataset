# Web-Scraping-Project-with-Disney-Movies-Dataset

In this Project, I scraped the Disney Movie dataset from the WikiPedia website and display the finalized dataset in dataframe format as well as exporting it as csv file utilizing different Python Libraries such as BeautifulSoup, Requests, RegEx and Pandas.

1. Scrapping the infobox on the Toy Story 3  Wiki Page

Explaination of the code:
- the get_text(' ',strip=True) =  be able to seperate strings that are combined by accident and strip out all the whitespace from beginning and end of text. 
- replace('\xa0',' ') = replace uncessary wording to be replaced by space 
- using enumberate function to be able to label each number with index number 
- index 0 is usually the title of info box and index 1 is always the image

2. Scrapping All the Movies'infobox from Wiki Diney Movies List

Explaination of the code:
- '.wikitable.sortable i' as CSS Selector (.class1 .class2) , a['href'] will get us -->'the link'.  
- Function(clear_tag(links)) is for removing the refernce link such as [1],[2] as the right corner of the content (decomposing the sup. Removing dulplicated date by decomposing the  span .  
- Realizing Some of the name within the info box are combined and became a "LONG STRINGS" after digging into the coding part of html. Realizing some of the code its used with  br  instead of li , thus added "return [text for text in x.stripped_strings]" to generate List of Names.  
-  Some Rows do not consist of th, thus it generates error when adding them to list, thus adding the line of ( if header:) so if header exists, we will run the followiing quote.

3. Data Cleaning

- Cleaning the reference link and duplicated date (Fixed in Step2)
- Fixing the name tags(long strings) (Fixed in Step2)
- Looking into the error that were generated via creation of the movielist (Fixed in Step2), rest of errors persist as some of the movie are in series and some of them doesnt have infobox.
- Taking the numeric value only from the Running Time Col (1)
- Converting the budget and box office amount to proper numberic values  (2)
- Converting the Date to Datetime (3)

Explaination of the code:

(1)
- Converting th running time with numeric values only as its better to look at it within the dataframe
- isinstance(x,list) indicates that if x is a list then we will proceed the following
- Eg.18 mins, we apply 'int(entry.split(' ')[0]' we will convert this string to int and we split it into '18 and  'mins' and [0] indicates we taking the first one of the list.
- (x.get('Running time','N/A')) will allow u to get the value of the KEY(runningtime) in the Dict x. if value is none, will display as N/A.

(2)

Utilizing RegEx to develop the Syntax and Patterns in order to convert number value from word .

- def word_to_value(word) --> for converting words from input to digits.
- def main_method(x) --> re.search(pattern, inputvalue) allow us to generate output based on the input with the instruction of the pattern requirement. and group() indicates returns the part of the string where there was a match. Giving an example if value is 15Thousand, the function will first look into the number  and replace comma with period as comma cant be processed. and function will look into the word 'Thousand', flags=re.I allow function to run without being case sensitive and letting on total = 15*1000= 15000
- def method2(x) --> Simply just convert to digit
- def value_conversion(money)  -- > if input consists of word we go through the main method and if it doesnt then we go through method2


(3)

- We splitting the date data into a list and only taking the first date before '(' and converting data to datetime format 


4. Attaching Review Scores(Rotten Tomatoes, Metascore, IMDB) with move database api

Explaination of the code:

- Utilizing A Movie Dataset API website to import review scores into the dataset.
- Utilize Window enviromental variable to hide my personal API KEY
- rotten tomato are in seperate function as score from rotten tomato is within the Rating List of api site



5. Converting the Dictionary into dataframe and export it as csv

Explaination of the code:

- applying panda library to make it into df
- export as CSV file


Little Note

Json Allows us to save the data without the datatype(datetime) 

Pickle allow us to store datetime but we cant transfer pickle to other

Duplicated the movie Datalist by using (movie_lists_copy=[x.copy() for x in movie_lists]) as it is dict and .copy() wont work.

HelpFul Website for this Projects:

https://en.wikipedia.org/wiki/List_of_Walt_Disney_Pictures_films

https://en.wikipedia.org/wiki/Toy_Story_3

https://www.crummy.com/software/BeautifulSoup/bs4/doc/

https://www.w3schools.com/csSref/css_selectors.php

https://www.w3schools.com/python/python_regex.asp


