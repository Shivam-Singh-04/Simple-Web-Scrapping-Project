# Simple-Web-Scrapping-Project

EXTRACTING DATA USING BEAUTIFUL SOUP:


Steps for extracting the data:
1) Send an HTTP request to the web page using the requests library.
2) Parse the HTML content of the web page using BeautifulSoup.
3) Identify the HTML tags that contain the data you want to extract.
4) Use BeautifulSoup methods to extract the data from the HTML tags.
5) Print the extracted data

Step 1: Send an HTTP request to the web page:

You will use the request library for sending an HTTP request to the web page.
url="your url"

The requests.get() method takes a URL as its first argument, which specifies the location of the resource to be retrieved.
In this case, the value of the url variable is passed as the argument to the requests.get() method, because you will store a web page URL in a url variable.

You use the .text method for extracting the HTML content as a string in order to make it readable.

data  = requests.get(url).text
print(data)

Step 2: Parse the HTML content:

What is parsing?
In simple words, parsing refers to the process of analyzing a string of text or a data structure, usually following a set of rules or grammar,
to understand its structure and meaning. Parsing involves breaking down a piece of text or data into its individual components or elements, and then
analyzing those components to extract the desired information or to understand their relationships and meanings.

Next you will take the raw HTML content of a web page or a string of HTML code which needs to be parsed and transformed into a structured, hierarchical
format that can be more easily analyzed and manipulated in Python. This can be done using a Python library called Beautiful Soup.

Parsing the data using the BeautifulSoup library:

Create a new BeautifulSoup object.

Note: To create a BeautifulSoup object in Python, you need to pass two arguments to its constructor:
1) The HTML or XML content that you want to parse as a string.
2) The name of the parser that you want to use to parse the HTML or XML content. This argument is optional, and if you don't specify a parser, BeautifulSoup
will use the default HTML parser included with the library. here in this lab we are using "html5lib" parser.

soup = BeautifulSoup(data, 'html5lib')

Step 3: Identify the HTML tags:

As stated above, the web page consists of a table so, we will scrape the content of the HTML web page and convert the table into a data frame.

You will create an empty data frame using the pd.DataFrame() function with the following columns:

• "Date"
• "Open"
• "High"
• "Low"
• "Close"
• "Volume"

data = pd.DataFrame(columns=["Date", "Open", "High", "Low", "Close", "Volume"])

Working on HTML table:

These are the following tags which are used while creating HTML tables:

• <table>: This tag is a root tag used to define the start and end of the table. All the content of the table is enclosed within these tags.

• <tr>: This tag is used to define a table row. Each row of the table is defined within this tag.

• <td>: This tag is used to define a table cell. Each cell of the table is defined within this tag. You can specify the content of the cell between the opening and closing tags.

• <th>: This tag is used to define a header cell in the table. The header cell is used to describe the contents of a column or row. By default, the text inside a tag is bold and centered.

• <tbody>: This is the main content of the table, which is defined using the tag. It contains one or more rows of elements.

Step 4: Use a BeautifulSoup method for extracting data:

We will use find() and find_all() methods of the BeautifulSoup object to locate the table body and table row respectively in the HTML.

• The find() method will return particular tag content.
• The find_all() method returns a list of all matching tags in the HTML.

# First we isolate the body of the table which contains all the information
# Then we loop through each row and find all the column values for each row
for row in soup.find("tbody").find_all('tr'):
    col = row.find_all("td")
    date = col[0].text
    Open = col[1].text
    high = col[2].text
    low = col[3].text
    close = col[4].text
    adj_close = col[5].text
    volume = col[6].text
    
# Finally we append the data of each row to the table
data = netflix_data.append({"Date":date, "Open":Open, "High":high, "Low":low, "Close":close, "Adj Close":adj_close, "Volume":volume}, ignore_index=True)

Step 5: Print the extracted data:

We can now print out the data frame using the head() or tail() function.

netflix_data.head()



EXTRACTING DATA USING PANDAS LIBRARY:

We can also use the pandas read_html function from the pandas library and use the URL for extracting data.

What is read_html in pandas library?

pd.read_html(url) is a function provided by the pandas library in Python that is used to extract tables from HTML web pages. It takes in a URL as input 
and returns a list of all the tables found on the web page.

read_html_pandas_data = pd.read_html(url)

Or you can convert the BeautifulSoup object to a string.

read_html_pandas_data = pd.read_html(str(soup))

Because there is only one table on the page, just take the first table in the returned list.

dataframe = read_html_pandas_data[0]

dataframe.head()
