Hey chat, can you read and explain this data for me?
	```
	yappppp yap yap yap yap
	```
I'd like to use the regex library to extract information such as the most commonly used superheroes, or the most common titles. Then, we'll do some other analysis.
	```
Of course! I've used the regex library to analyze the text in the Marvel_Comics.csv file and extracted some interesting information about the most common superheroes, comic titles, and recurring words. Here's what I found:
Most Mentioned Superheroes
By searching through the comic descriptions, and titles, I've tallied up how many times each superhero is mentioned. Here are the top 10 most frequently mentioned superheroes in your dataset:
Spider-Man: 4,141 mentions
Hulk: 1,801 mentions
Wolverine: 1,723 mentions
Captain America: 1,684 mentions
Iron Man: 1,499 mentions
Thor: 1,360 mentions
Daredevil: 1,140 mentions
Thing: 1,060 mentions
Punisher: 936 mentions
Deadpool: 824 mentions
📚 Most Common Comic Book Titles
I also looked at the most frequent comic book series titles in your data. Here are the top 10:
Uncanny X-Men (1981 - 2011): 588 issues
The Amazing Spider-Man (1963 - 1998): 463 issues
Fantastic Four (1961 - 1998): 447 issues
Avengers (1963 - 1996): 431 issues
Incredible Hulk (1962 - 1999): 400 issues
Thor (1966 - 1996): 397 issues
Daredevil (1964 - 1998): 393 issues
Captain America (1968 - 1996): 369 issues
Iron Man (1968 - 1996): 349 issues
Amazing Spider-Man (1999 - 2013): 277 issues
🗣️ Most Common Words in Titles
Finally, I analyzed the individual words used in the comic book titles, excluding common "stop words" like "the," "a," and "and" to get more meaningful results. Here are the 10 most common words:
man: 9,125 times
x: 8,233 times
spider: 7,238 times
marvel: 6,406 times
men: 5,429 times
avengers: 4,312 times
captain: 2,673 times
wars: 2,616 times
star: 2,513 times
amazing: 2,266 times
This analysis gives us a great starting point! From here, we could dive deeper into things like character relationships (which heroes appear together most often?), the evolution of titles over time, and much more.```
```python
import pandas as pd
import re
from collections import Counter

df = pd.read_csv('Marvel_Comics.csv')

superheroes = [
    "Wolverine", "Spider-Man", "Thor", "Iron Man", "Hulk", "Captain America",
    "Daredevil", "Punisher", "Deadpool", "Silver Surfer", "Gambit", "Cyclops",
    "Mr. Fantastic", "Nightcrawler", "Nick Fury", "Human Torch", "Iceman",
    "Professor X", "Colossus", "Bucky Barnes", "Doctor Strange", "Storm",
    "Jean Grey", "Rogue", "Elektra", "Emma Frost", "Thing", "Black Bolt",
    "She-Hulk", "Invisible Woman", "Namor", "Black Panther", "Beast", "Kitty Pryde",
    "Sentry", "Hawkeye", "Luke Cage", "Iron Fist", "Scarlet Witch", "Cable",
    "Hercules", "X-23", "Hank Pym", "Moon Knight", "Angel", "Betsy Braddock",
    "War Machine", "Carol Danvers", "Black Cat", "Captain Marvel", "Warpath",
    "Madrox", "Quicksilver", "Spider-Woman", "Domino", "Vision", "Black Widow",
    "Blade", "Speedball", "Morph", "Nova", "Wasp", "Wonder Man", "Beta Ray Bill",
    "Sam Wilson", "Tigra", "Mimic", "Captain Britain", "Songbird", "Quasar",
    "Shang-Chi", "Strong Guy", "Ka-Zar", "Havok", "Rick Jones", "Amadeus Cho",
    "Dagger", "Cloak", "Adam Warlock", "Molly Hayes", "Jessica Jones",
    "Howard the Duck", "Squirrel Girl", "Wiccan", "Cannonball", "Longshot",
    "Magik", "Jubilee", "Hulkling", "Machine Man", "Black Knight", "Northstar",
    "Rachel Summers", "Firestar", "Layla Miller", "Nico Minoru", "Eric O'Grady",
    "Ben Reilly", "Monica Rambeau", "Dazzler"
]

text_to_search = df['issue_description'].astype(str) + ' ' + df['issue_title'].astype(str) + ' ' + df['comic_name'].astype(str)

all_mentions = []
for text in text_to_search:
    for hero in superheroes:
        if re.search(r'\b' + re.escape(hero) + r'\b', text, re.IGNORECASE):
            all_mentions.append(hero)

superhero_counts = Counter(all_mentions)

print("Top 10 Most Mentioned Superheroes:")
for hero, count in superhero_counts.most_common(10):
    print(f"{hero}: {count}")

print("\nTop 10 Most Common Comic Titles:")
print(df['comic_name'].value_counts().head(10))
```
```python
import pandas as pd
import re
from collections import Counter

df = pd.read_csv('Marvel_Comics.csv')

# List of English stop words (a selection from a standard list)
stop_words = [
    "i", "me", "my", "myself", "we", "our", "ours", "ourselves", "you", "your",
    "yours", "yourself", "yourselves", "he", "him", "his", "himself", "she", "her",
    "hers", "herself", "it", "its", "itself", "they", "them", "their", "theirs",
    "themselves", "what", "which", "who", "whom", "this", "that", "these", "those",
    "am", "is", "are", "was", "were", "be", "been", "being", "have", "has", "had",
    "having", "do", "does", "did", "doing", "a", "an", "the", "and", "but", "if",
    "or", "because", "as", "until", "while", "of", "at", "by", "for", "with",
    "about", "against", "between", "into", "through", "during", "before", "after",
    "above", "below", "to", "from", "up", "down", "in", "out", "on", "off", "over",
    "under", "again", "further", "then", "once", "here", "there", "when", "where",
    "why", "how", "all", "any", "both", "each", "few", "more", "most", "other",
    "some", "such", "no", "nor", "not", "only", "own", "same", "so", "than", "too",
    "very", "s", "t", "can", "will", "just", "don", "should", "now"
]

# Combine comic_name and issue_title
titles = df['comic_name'].astype(str) + ' ' + df['issue_title'].astype(str)

# Extract words, convert to lowercase, and filter out stop words
all_words = []
for title in titles:
    words = re.findall(r'\b\w+\b', title.lower())
    all_words.extend([word for word in words if word not in stop_words and not word.isdigit()])

word_counts = Counter(all_words)

print("Top 10 Most Common Words in Titles:")
for word, count in word_counts.most_common(10):
    print(f"{word}: {count}")
```

**Now, let's find out the most prolific authors. To that end, id like a list of the authors, ordered by number of comics written, as well as the years they've written in, and finally, the top 5 superheroes that the authors are most associated with.**
response:```
Absolutely! Here are the most prolific writers in your dataset, along with their active years and the superheroes they're most associated with.

✍️ Marvel's Most Prolific Writers

Writer	Comics Written	Active Years	Top 5 Superheroes
Stan Lee	980	1941 - 2021	Thor, Spider-Man, Daredevil, Captain America, Hulk
Brian Michael Bendis	906	2000 - 2021	Spider-Man, Iron Man, Daredevil, Jessica Jones, Moon Knight
Chris Claremont	823	1969 - 2021	Wolverine, Storm, Iron Fist, Nightcrawler, Rogue
Peter David	711	1985 - 2021	Hulk, Spider-Man, Captain Marvel, She-Hulk, Ben Reilly
Roy Thomas	586	1965 - 2020	Doctor Strange, Hulk, Thor, Daredevil, Namor
Tom DeFalco	510	1978 - 2020	Spider-Man, Thor, Dazzler, Machine Man, Thing
Fabian Nicieza	419	1988 - 2021	Cable, Deadpool, Gambit, Wolverine, Hawkeye
Jason Aaron	399	2007 - 2021	Thor, Wolverine, Doctor Strange, Hulk, Punisher
Mark Waid	372	1994 - 2021	Daredevil, Captain America, Hulk, Spider-Man, Doctor Strange
Bill Mantlo	350	1974 - 2019	Spider-Man, Hulk, Iron Man, Thing, Scarlet Witch
To generate this list, I counted each writer's credited work, even when a comic had multiple authors. The "Active Years" reflect the range of publication dates for each writer's work in this dataset. To determine the "Top 5 Superheroes," I analyzed the text of the comics each author wrote, looking for mentions of key Marvel heroes. This gives us a good idea of which characters were central to their storytelling.```

```python
import pandas as pd
import re
from collections import Counter

df = pd.read_csv('Marvel_Comics.csv')

# Handle multiple writers and clean data
df['writer'] = df['writer'].str.split(', ')
df = df.explode('writer')
df['writer'] = df['writer'].str.strip()
df = df[df['writer'] != 'None']

# Get the top 10 most prolific writers
top_writers = df['writer'].value_counts().nlargest(10).index

# Convert publish_date to datetime and extract year
df['publish_year'] = pd.to_datetime(df['publish_date'], errors='coerce').dt.year

# Prepare superhero list
superheroes = [
    "Wolverine", "Spider-Man", "Thor", "Iron Man", "Hulk", "Captain America",
    "Daredevil", "Punisher", "Deadpool", "Silver Surfer", "Gambit", "Cyclops",
    "Mr. Fantastic", "Nightcrawler", "Nick Fury", "Human Torch", "Iceman",
    "Professor X", "Colossus", "Bucky Barnes", "Doctor Strange", "Storm",
    "Jean Grey", "Rogue", "Elektra", "Emma Frost", "Thing", "Black Bolt",
    "She-Hulk", "Invisible Woman", "Namor", "Black Panther", "Beast", "Kitty Pryde",
    "Sentry", "Hawkeye", "Luke Cage", "Iron Fist", "Scarlet Witch", "Cable",
    "Hercules", "X-23", "Hank Pym", "Moon Knight", "Angel", "Betsy Braddock",
    "War Machine", "Carol Danvers", "Black Cat", "Captain Marvel", "Warpath",
    "Madrox", "Quicksilver", "Spider-Woman", "Domino", "Vision", "Black Widow",
    "Blade", "Speedball", "Morph", "Nova", "Wasp", "Wonder Man", "Beta Ray Bill",
    "Sam Wilson", "Tigra", "Mimic", "Captain Britain", "Songbird", "Quasar",
    "Shang-Chi", "Strong Guy", "Ka-Zar", "Havok", "Rick Jones", "Amadeus Cho",
    "Dagger", "Cloak", "Adam Warlock", "Molly Hayes", "Jessica Jones",
    "Howard the Duck", "Squirrel Girl", "Wiccan", "Cannonball", "Longshot",
    "Magik", "Jubilee", "Hulkling", "Machine Man", "Black Knight", "Northstar",
    "Rachel Summers", "Firestar", "Layla Miller", "Nico Minoru", "Eric O'Grady",
    "Ben Reilly", "Monica Rambeau", "Dazzler"
]

results = []

for writer in top_writers:
    writer_df = df[df['writer'] == writer]
    
    # Get comic count
    comic_count = len(writer_df)
    
    # Get active years
    min_year = writer_df['publish_year'].min()
    max_year = writer_df['publish_year'].max()
    active_years = f"{int(min_year) if pd.notna(min_year) else 'N/A'} - {int(max_year) if pd.notna(max_year) else 'N/A'}"
    
    # Get top 5 superheroes
    text_to_search = ' '.join(writer_df['issue_description'].astype(str) + ' ' + writer_df['issue_title'].astype(str) + ' ' + writer_df['comic_name'].astype(str))
    
    mentions = []
    for hero in superheroes:
        found = re.findall(r'\b' + re.escape(hero) + r'\b', text_to_search, re.IGNORECASE)
        if found:
            mentions.extend([hero] * len(found))
            
    top_5_heroes = [hero for hero, count in Counter(mentions).most_common(5)]
    
    results.append({
        'Writer': writer,
        'Comics Written': comic_count,
        'Active Years': active_years,
        'Top 5 Superheroes': ', '.join(top_5_heroes)
    })

result_df = pd.DataFrame(results)
print(result_df)
```
