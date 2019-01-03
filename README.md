# Gutenberg API for paragraph generation

### Preparations

In order to use this API you should get files "books_data.pkl", "books_shelves.pkl", "paragraph_metadata.pkl" and "paragraph_data.pkl" in directory "data/".


### API

use API methods such as get_books, get_paragraphs and get_bookshelves to get data. 

GutenbergBook is a class supporting books and Paragraph supporting paragraphs. GutenbergBook contains metadata of each book and Paragraph contain both text and metadata. Metadata of books contains:
* title
* authors
* language 
* bookshelves: the booshelves that the book belong to.

Paragraph contains book_id, next_id \(next paragraph id\), prev_id, and some tags which illustrate some syntatic properties of paragraph.


### get_paragraphs

In order to get a list of paragraphs you should call get_paragraphs:
```python
pars = API.get_paragraphs(books=books, tags=tags, num_sequential=n)
```

* If books is not None, then the returned paragraphs will only belong to that list. books is a list of integers \(books id\) or GutenbergBook.
* If tags are specified then only the paragraphs which include those tags will be returned. It is recommended to specify that parameter because there are a lot of paragraphs that are not litteraly paragraphs. \( like dialogue, titles, and ...\). Tags are integer numbers and class Tags in HP specify identify each number. For instance HP.Tags.WITHOUT_DIALOGUE (which is 4) identify the paragraphs without any dialogue.
The format of tags are a list of integers or lists. which the second lists are dedicated to "or", which means at least one of tags should exist in the paragraph tags. for instant tags=\[1, 2, \[3, 4\]\] means that output paragraphs have tags 1, 2 and at least one of 3 and 4.
* If num_sequential > 1, the output will be a list of tuples, triples or ... that are sequential paragraphs each one have the properties given to method. \( being sequential means paragraphs are sequential in a book\) 

Note that you can get paragraphs by paragraph id:

```python
pars = API.get_paragraphs(paragrap_id=ids)
```

if you have memory limit, you can use paragraph_object = False to return only paragrap sentences instead of Paragraph object.

```python
pars = API.get_paragraphs(Paragraph_Object=False, lowercase=<True/False>)
```

### Paragraph
Paragraph is a class for working with paragraph easily. it contains, some id (id, next_id, prev_id, book_id) if they exist, tags and text. in order to get text you can call text() method in the class:
```python
text = par.text(format=<"sentences"/"words"/"text">, lowercase=<True/False>)
```

* format = "sentences" return a list of sentences which each sentence is a list of words.
* format = "words" return a list of words.
* format = "text" return a string.


