# Regular Expressions

In the following, you will parse information from text-based files with the command line and Unix tools and Python in the next step. Please note that even though the files are provided as structured csv files you are not supposed to simply read out the columns, but you should use regular expressions instead.

## Parsing contact information from the command line

In this directory, you will find a txt-file called `csv/contacts.csv`. Use regular expressions to extract the following information from it.

Remember that you can use different tools like `grep`, `awk`, or `sed` to use regular expressions from the command line. Pipes might also be helpful. 

You can add your command line in- and outputs directly to this README file. Alternatively, you can write a bash script with all commands and commit it to this directory.

1. Extract all email addresses from the text.
``` 
$ grep -oP '[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}' contacts.csv

john.doe@example.com
jane.smith@gmail.com
mjohnson@yahoo.com
lharris@hotmail.com
rbrown@company.com
alice.white@domain.org
dgreen@domain.net
eblack@webmail.com
cblue@provider.com
ssilver@university.edu

``` 
2. Extract all phone numbers from the text.
``` 
$ grep -oP '\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}' contacts.csv

(555) 123-4567
(555) 987-6543
(555) 555-5555
(555) 321-6789
(555) 876-5432
(555) 432-5678
(555) 246-1357
(555) 531-2468
(555) 864-9753
(555) 975-8642

``` 
3. Extract all names that start with the letter ‘J’.
``` 
grep -oP '\bJ[a-zA-Z]*\b' contacts.csv

John
Jane
Johnson

``` 
4. Extract all street names that contain the word 'St'.
``` 
$ grep -oP '\b\w+\s*St\w*\b' contacts.csv

Main St
Oak St
Cedar St
Elm St
Birch St
Walnut St
Chestnut St

``` 
5. Extract all addresses in ‘USA’.
``` 
$ grep -oP '.*\bUSA\b' contacts.csv | sed 's/,\s*USA.*//'

John Doe, 123 Main St, Anytown
Jane Smith, 456 Oak St, Sometown
Mike Johnson, 789 Pine Rd, Othertown
Linda Harris, 321 Maple Dr, Newcity
Robert Brown, 654 Cedar St, Oldtown
Alice White, 987 Elm St, Smalltown
David Green, 246 Birch St, Uptown
Emily Black, 135 Walnut St, Middletown
Chris Blue, 864 Chestnut St, Metropolis
Susan Silver, 975 Cypress Ave, Bigcity

``` 
6. Extract the last names of all people.
``` 
$ grep -oP '^\S+\s(\S+)' contacts.csv | awk '{print $2}'

Doe,
Smith,
Johnson,
Harris,
Brown,
White,
Green,
Black,
Blue,
Silver,

``` 
7. Extract all email domains (part after the @ sign).
``` 
$ grep -oP '@\K[\w.-]+' contacts.csv

example.com
gmail.com
yahoo.com
hotmail.com
company.com
domain.org
domain.net
webmail.com
provider.com
university.edu

``` 
8.	Extract all instances of the first name ‘David’ along with their full address (street and city).
``` 
$ grep -oP 'David\s+\S+\s*,\s*[^,]+,\s*[A-Za-z\s]+' contacts.csv

David Green, 246 Birch St, Uptown

``` 
9.	Find all entries where the phone number ends with ‘7’.
``` 
$ grep -P '.*\d{1,}7\b.*' contacts.csv

John Doe, 123 Main St, Anytown, USA, john.doe@example.com, (555) 123-4567
Jane Smith, 456 Oak St, Sometown, USA, jane.smith@gmail.com, (555) 987-6543
Alice White, 987 Elm St, Smalltown, USA, alice.white@domain.org, (555) 432-5678
David Green, 246 Birch St, Uptown, USA, dgreen@domain.net, (555) 246-1357

``` 
10.	Extract all instances of first names that end with the letter 'e'.
``` 
$ grep -oP '^\b[A-Za-z]+e\b' contacts.csv

Jane
Mike
Alice

``` 

## Parsing product orders with Python

In this directory, you will find another file called `csv/orders.csv` and also a short Python script that reads the file and parses all numbers with a regular expression. Please extend the script such that it also print the following extracted text pieces.

1.	Extract all order numbers from the text. 
2.	Extract all product names.
3.	Extract all prices.
4.	Extract all order dates.
5.	Find all orders for products priced over $500. (You are allowed to use Python to filter the list.)
6.	Change the date format to DD/MM/YYYY. (Note the re.sub() method)
7.	Extract product names that have more than 6 characters.
8.	Count the occurrence of each product in the text. (You may want to use the Counter class from the collections package.)
9.	Extract the orders with prices ending in .99.
10.	Find the cheapest product. (You may want to use Python's min() method.)
