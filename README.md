# spaCy

spaCy is a free, open-source library for advanced Natural Language Processing (NLP) in Python.

#The nlp object
At the center of spaCy is the object containing the processing pipeline. We usually call this variable "nlp".

For example, to create an English nlp object, you can import spacy and use the spacy.blank method to create a blank English pipeline. You can use the nlp object like a function to analyze text.

```
# Import spaCy
import spacy

# Create a blank English nlp object
nlp = spacy.blank("en")
```

#The Doc object
When you process a text with the nlp object, spaCy creates a Doc object – short for "document". The Doc lets you access information about the text in a structured way, and no information is lost.
```
# Created by processing a string of text with the nlp object
doc = nlp("Hello world!")

# Iterate over tokens in a Doc
for token in doc:
    print(token.text)
```
```
Output: Hello
world
!
```

#The Token object
Token objects represent the tokens in a document – for example, a word or a punctuation character.
To get a token at a specific position, you can index into the doc.
Token objects also provide various attributes that let you access more information about the tokens. For example, the .text attribute returns the verbatim token text.

```
doc = nlp("Hello world!")

# Index into the Doc to get a single Token
token = doc[1]

# Get the token text via the .text attribute
print(token.text)
```
```
Output: world
```

#The Span object
A Span object is a slice of the document consisting of one or more tokens. It's only a view of the Doc and doesn't contain any data itself.

To create a span, you can use Python's slice notation. For example, 1:3 will create a slice starting from the token at position 1, up to – but not including! – the token at position 3.
```
doc = nlp("Hello world!")

# A slice from the Doc is a Span object
span = doc[1:3]

# Get the span text via the .text attribute
print(span.text)
```

#Lexical Attributes
Here you can see some of the available token attributes:
i is the index of the token within the parent document.
text returns the token text.

is_alpha, is_punct and like_num return boolean values indicating whether the token consists of alphabetic characters, whether it's punctuation or whether it resembles a number. For example, a token "10" – one, zero – or the word "ten" – T, E, N.

These attributes are also called lexical attributes: they refer to the entry in the vocabulary and don't depend on the token's context.
```
doc = nlp("It costs $5.")
```
```
print("Index:   ", [token.i for token in doc])
print("Text:    ", [token.text for token in doc])

print("is_alpha:", [token.is_alpha for token in doc])
print("is_punct:", [token.is_punct for token in doc])
print("like_num:", [token.like_num for token in doc])
```
```
Output: 
Index:    [0, 1, 2, 3, 4]
Text:     ['It', 'costs', '$', '5', '.']

is_alpha: [True, True, False, False, False]
is_punct: [False, False, False, False, True]
like_num: [False, False, False, True, False]
```

