# 1.Regex_NLP_Tutorial
NLP Tutorial: Regular Expressions
## Regular expressions (regex) are a fundamental tool in Natural Language Processing (NLP) and are primarily used for pattern matching and text manipulation. While information extraction is a key application, regex functions in NLP can be broadly categorised into two main areas:


## Information Extraction:
This involves identifying and extracting specific pieces of information from unstructured text based on defined patterns. Examples include:
Extracting dates, phone numbers, email addresses, or monetary amounts.
Identifying named entities like people, organizations, or locations.
Parsing structured data from semi-structured text, such as log files or web pages.


## Text Preprocessing and Transformation:
This encompasses a range of tasks aimed at cleaning, normalizing, or transforming text data for further NLP analysis. Examples include:
Removing or replacing specific characters, such as punctuation or special symbols.
Standardizing text by converting to lowercase or uppercase.
Removing extra spaces or line breaks.
Tokenization (splitting text into words or sub-word units) and lemmatization/stemming (reducing words to their base form), though these often involve more sophisticated algorithms than just regex.






(1) Regex in customer support
Retrieve order number
```
import re

chat1='codebasics: Hello, I am having an issue with my order # 412889912'

pattern = 'order[^\d]*(\d*)'
matches = re.findall(pattern, chat1)
matches
['412889912']
chat2='codebasics: I have a problem with my order number 412889912'
pattern = 'order[^\d]*(\d*)'
matches = re.findall(pattern, chat2)
matches
['412889912']
chat3='codebasics: My order 412889912 is having an issue, I was charged 300$ when online it says 280$'
pattern = 'order[^\d]*(\d*)'
matches = re.findall(pattern, chat3)
matches
['412889912']
```
```
def get_pattern_match(pattern, text):
    matches = re.findall(pattern, text)
    if matches:
        return matches[0]
get_pattern_match('order[^\d]*(\d*)', chat1)
'412889912'
Retrieve email id and phone
chat1 = 'codebasics: you ask lot of questions 😠  1235678912, abc@xyz.com'
chat2 = 'codebasics: here it is: (123)-567-8912, abc@xyz.com'
chat3 = 'codebasics: yes, phone: 1235678912 email: abc@xyz.com'
-----Email id-----

get_pattern_match('[a-zA-Z0-9_]*@[a-z]*\.[a-zA-Z0-9]*',chat1)
'abc@xyz.com'
get_pattern_match('[a-zA-Z0-9_]*@[a-z]*\.[a-zA-Z0-9]*',chat2)
'abc@xyz.com'
get_pattern_match('[a-zA-Z0-9_]*@[a-z]*\.[a-zA-Z0-9]*',chat3)
'abc@xyz.com'
-----Phone number-----
```
```
get_pattern_match('(\d{10})|(\(\d{3}\)-\d{3}-\d{4})',chat1)
'1235678912'
get_pattern_match('(\d{10})|(\(\d{3}\)-\d{3}-\d{4})', chat2)
('', '(123)-567-8912')
get_pattern_match('(\d{10})|(\(\d{3}\)-\d{3}-\d{4})', chat3)
('1235678912', '')
```
(2) Regex for Information Extraction
```
text='''
Born	Elon Reeve Musk
June 28, 1971 (age 50)
Pretoria, Transvaal, South Africa
Citizenship	
South Africa (1971–present)
Canada (1971–present)
United States (2002–present)
Education	University of Pennsylvania (BS, BA)
Title	
Founder, CEO and Chief Engineer of SpaceX
CEO and product architect of Tesla, Inc.
Founder of The Boring Company and X.com (now part of PayPal)
Co-founder of Neuralink, OpenAI, and Zip2
Spouse(s)	
Justine Wilson
​
​(m. 2000; div. 2008)​
Talulah Riley
​
​(m. 2010; div. 2012)​
​
​(m. 2013; div. 2016)
'''
```
```
get_pattern_match(r'age (\d+)', text)
'50'
get_pattern_match(r'Born(.*)\n', text).strip()
'Elon Reeve Musk'
get_pattern_match(r'Born.*\n(.*)\(age', text).strip()
'June 28, 1971'
get_pattern_match(r'\(age.*\n(.*)', text)
'Pretoria, Transvaal, South Africa'
def extract_personal_information(text):
    age = get_pattern_match('age (\d+)', text)
    full_name = get_pattern_match('Born(.*)\n', text)
    birth_date = get_pattern_match('Born.*\n(.*)\(age', text)
    birth_place = get_pattern_match('\(age.*\n(.*)', text)
    return {
        'age': int(age),
        'name': full_name.strip(),
        'birth_date': birth_date.strip(),
        'birth_place': birth_place.strip()
    }
extract_personal_information(text)
{'age': 50,
 'name': 'Elon Reeve Musk',
 'birth_date': 'June 28, 1971',
 'birth_place': 'Pretoria, Transvaal, South Africa'}
```
```
text = '''
Born	Mukesh Dhirubhai Ambani
19 April 1957 (age 64)
Aden, Colony of Aden
(present-day Yemen)[1][2]
Nationality	Indian
Alma mater	
St. Xavier's College, Mumbai
Institute of Chemical Technology (B.E.)
Stanford University (drop-out)
Occupation	Chairman and MD, Reliance Industries
Spouse(s)	Nita Ambani ​(m. 1985)​[3]
Children	3
Parent(s)	
Dhirubhai Ambani (father)
Kokilaben Ambani (mother)
Relatives	Anil Ambani (brother)
Tina Ambani (sister-in-law)
'''
```
```
extract_personal_information(text)
{'age': 64,
 'name': 'Mukesh Dhirubhai Ambani',
 'birth_date': '19 April 1957',
 'birth_place': 'Aden, Colony of Aden'}
```
