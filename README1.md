# GETTING STARTED

Let’s get started and try out spaCy! In this exercise, you’ll be able to try out some of the 60+ available languages.

Part 1: English
Use spacy.blank to create a blank English ("en") nlp object.
Create a doc and print its text.
```
# Import **spaCy**
import spacy

# Create the English nlp object
nlp = spacy.blank("en")

# Process a text
doc = nlp("This is a sentence.")

# Print the document text
print(doc.text)
```

# DOCUMENTS, SPAN AND TOKENS

When you call nlp on a string, spaCy first tokenizes the text and creates a document object. In this exercise, you’ll learn more about the Doc, as well as its views Token and Span.

Step 1
Use spacy.blank to create the English nlp object.
Process the text and instantiate a Doc object in the variable doc.
Select the first token of the Doc and print its text.
```
# Import spaCy and create the English nlp object
import spacy

nlp = spacy.blank("en")

# Process the text
doc = nlp("I like tree kangaroos and narwhals.")

# Select the first token
first_token = doc[0]

# Print the first token's text
print(first_token.text)
```

# TRAINED PIPELINES

What are trained pipelines?
Models that enable spaCy to predict linguistic attributes in context
Part-of-speech tags
Syntactic dependencies
Named entities
Trained on labeled example texts
Can be updated with more examples to fine-tune predictions

spaCy provides a number of trained pipeline packages you can download using the spacy download command. For example, the "en_core_web_sm" package is a small English pipeline that supports all core capabilities and is trained on web text.
The spacy.load method loads a pipeline package by name and returns an nlp object.
The package provides the binary weights that enable spaCy to make predictions.
```
$ python -m spacy download en_core_web_sm
import spacy

nlp = spacy.load("en_core_web_sm")
```

## Predicting Part-of-speech Tags
Let's take a look at the model's predictions. In this example, we're using spaCy to predict part-of-speech tags, the word types in context.
First, we load the small English pipeline and receive an nlp object.
Next, we're processing the text "She ate the pizza".
For each token in the doc, we can print the text and the .pos_ attribute, the predicted part-of-speech tag.
In spaCy, attributes that return strings usually end with an underscore – attributes without the underscore return an integer ID value.
Here, the model correctly predicted "ate" as a verb and "pizza" as a noun.

```
import spacy

# Load the small English pipeline
nlp = spacy.load("en_core_web_sm")

# Process a text
doc = nlp("She ate the pizza")

# Iterate over the tokens
for token in doc:
    # Print the text and the predicted part-of-speech tag
    print(token.text, token.pos_)
```
```
OUTPUT:
She PRON
ate VERB
the DET
pizza NOUN
```

## Predicting Syntactic Dependencies

In addition to the part-of-speech tags, we can also predict how the words are related. For example, whether a word is the subject of the sentence or an object.
The .dep_ attribute returns the predicted dependency label.
The .head attribute returns the syntactic head token. You can also think of it as the parent token this word is attached to.

```
for token in doc:
    print(token.text, token.pos_, token.dep_, token.head.text)
```
```
OUTPUT: 
She PRON nsubj ate
ate VERB ROOT ate
the DET det pizza
pizza NOUN dobj ate
```
![nsubject](https://user-images.githubusercontent.com/79436509/169543311-593c660b-3bb9-455d-8956-bf1e24b36a58.PNG)


## Predicting Named Entities

Named entities are "real world objects" that are assigned a name – for example, a person, an organization or a country.
The doc.ents property lets you access the named entities predicted by the named entity recognition model.
It returns an iterator of Span objects, so we can print the entity text and the entity label using the .label_ attribute.
In this case, the model is correctly predicting "Apple" as an organization, "U.K." as a geopolitical entity and "$1 billion" as money.
```
# Process a text
doc = nlp("Apple is looking at buying U.K. startup for $1 billion")

# Iterate over the predicted entities
for ent in doc.ents:
    # Print the entity text and its label
    print(ent.text, ent.label_)
```
```
OUTPUT: Apple ORG
U.K. GPE
$1 billion MONEY
```

# LOADING PIPELINES

Use **spacy.load** to load the small English pipeline **"en_core_web_sm"**.
Process the text and print the document text.

```
import spacy

# Load the "en_core_web_sm" pipeline
nlp = spacy.load("en_core_web_sm")

text = "It’s official: Apple is the first U.S. public company to reach a $1 trillion market value"

# Process the text
doc = nlp(text)

# Print the document text
print(doc.text)
```

# PREDICTING NAME ENTITIES IN CONTEXT

Models are statistical and not always right. Whether their predictions are correct depends on the training data and the text you’re processing. Let’s take a look at an example.

Process the text with the nlp object.
Iterate over the entities and print the entity text and label.
Looks like the model didn’t predict “iPhone X”. Create a span for those tokens manually.

```
import spacy

nlp = spacy.load("en_core_web_sm")

text = "Upcoming iPhone X release date leaked as Apple reveals pre-orders"

# Process the text
doc = nlp(text)

# Iterate over the entities
for ent in doc.ents:
    # Print the entity text and label
    print(ent.text, ent.label)

# Get the span for "iPhone X"
iphone_x = doc[1:3]

# Print the span text
print("Missing entity:", iphone_x.text)
```
```
Apple 383
Missing entity: iPhone X
```





