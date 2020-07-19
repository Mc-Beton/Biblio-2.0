# **Book Library**
Hi. I am glad to present to You a new program of mine, Library 2.0. Yes, I know it's in a raw state, but it will be upgraded later.
## Getting started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system. 
Just clone or download the files into a folder and it's ready to be used.
## How to use it.
Here You'll find how to turn on the program and a list of available commands You may use.
### Turn it on in CMD
Let's get to its proper directory. Then we should prepare a venv for it and pip the requirements.
First venv:
```
> python -m venv venv
```
If your on Mac/Linux we can activate it by:
```
> source venv/bin/activate
```
Or on windows:
```
> venv\Scripts\activate
```
After that we can pip the requirements:
```
(venv) > pip install -r requirements.txt
```
And know we have everything prepared to start our program. ;)

### Turn on flask shell
Ok. Since we are working on a sql database, it will be easier to use this program from flask shell. Let's turn it on:
```
(venv) > flask shell
Python 3.7.7 (tags/v3.7.7:d7c567b08f, Mar 10 2020, 10:41:24) [MSC v.1900 64 bit (AMD64)] on win32
IPython: 7.16.1
App: app [production]
Instance: D:\xxx\Biblio\instance
In [1]:
```
Now we can start using the program. But first of all what do we have in our database?

### Basic info about our database
Okey. Let's do it!!
We have 3 tables in our database:
- author
- book
- off_shelf

Author takes in:
- name (Authors name and surname)
- info (Anything you like to write about him)

Book take in:
- title (no need to expain)
- description (yep, still clear)
- author_id (hmm... here we pin the book to the proper writer)

And at last off_shelf:
- date (when the bastard was stolen)
- book_id (which book)
- ... (here was supposed to be who took it from you, but maybe later ill migrate more data)
Okey, lets rumbleeeee!!!

### How can i put in some data
Sicne we are in flask shell and the core is built in sqlalchemy we can use some simple combinations:
Add an Author:
```
In[1]: a = Author(name="Stephen King", info="His vision of sex is digusting")
```
That's how we name a variable "a" with a new author. Yet he is still not in our database, sooo:
```
In[2]: db.session.add(a)
In[3]: db.session.commit()
In[4]:
```
Great! We have a first Author in our library database! Go on! Add some more writers. ;)
But how can i add a book? Well, it's quite simple:
```
In[4]: au = Author.query.get(1)
```
Here, if i want to add a Kings book, we need to name him in our shell. We can check quite easily if we have the proper author:
```
In[5]: print(au)
<Author: Stephen King>
```
So, lets give him a book:
```
In[6]: b = Book(title="Dark Tower", description="a badass saga (never could make it to 4th part)", author=au)
In[7]: db.session.add(b)
In[8]: db.session.commit()
```
And there You go!! A writer with a book. Try it out with other writers. ;)

### Other commands you can use
to get a list of authors you need to type in:
```
In[9]: aa = Author.query.all()
In[10]:aa
Out[10]: [<Author 1>, <Author 2>, <Author 3>]
In[11]: for au in aa:
  ...:     print(au)
  ...:
<Author: Remigiusz Mroz>
<Author: Stephen King>
<Author: B.V. Larson>
In[12]:
```
And the as with books. ;)

Hej!!! But what about deleting a book or author?
Well, i do have a sollution for that too pall:
```
In[12]: de = Author.query.get(2)
in[13]: db.session.delete(de)
In[14]: db.session.commit()
In[15]:
```
And there you go. You burnt the book, didn't ya? :P

## Later updates
Well, i guess, since the program is operated by flask i should make it in html. Well... i hope that sooner or later I'll get it running that way, for now You can use it this way.

## Authors
Filip Gabrys - Initial work
With help from his mentor from the Kodilla course.