# WordCloud From Wikipedia Using Python

This code can be used to create word cloud for any topic present on wikipedia. 

The code prompts user to enter:
- The 'Topic' for which wordcloud needs to be generated
- The number of words to be included in the WordCloud
- The name of WordCloud file to be generated

So, this code can be used to generate a WordCloud for any topic from the wikipedia website.

![alt text](https://github.com/deepankarkotnala/WordCloud_From_Wikipedia_Using_Python/blob/master/images/data_science_wordcloud.png)
### Here is the Code: 

```Python
import wikipedia
import numpy as np
import matplotlib as plt
from PIL import Image
from wordcloud import WordCloud, STOPWORDS
import os
```

```Python
currdir = os.path.dirname(__file__)  # keeping the track of current directory

title = input("Enter the title for WordCloud: ")
num_of_words = int(input("How many words do you wish to include in the WordCloud? "))
name_of_file = input("Please enter the name of the WordCloud file to be saved?")
```

```Python
def get_wiki(query):
	title = wikipedia.search(query)[0]
	page = wikipedia.page(title)
	return page.content
```

```Python
def create_wordcloud(text):

	mask=np.array(Image.open(os.path.join(currdir, "cloud1.png")))

	stopwords = set(STOPWORDS)
	new_stopwords=stopwords.union(os.path.join(currdir, "new_words.txt"))
	wc = WordCloud(background_color="white",
				   mask=mask,
				   max_words=num_of_words,
				   stopwords=new_stopwords)

	wc.generate(text)

	wc.to_file(os.path.join(currdir, "{}.png".format(name_of_file)))

	print("WordCloud created at the following location: {}".format(os.path.join(currdir, "{}.png".format(name_of_file))))
```

#### Calling the function to create the WordCloud
```Python
create_wordcloud(get_wiki(title))
```
![alt text](https://github.com/deepankarkotnala/WordCloud_From_Wikipedia_Using_Python/blob/master/images/Prompt.JPG)


