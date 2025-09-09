Regular Expressions:
Python for Preprocessing, cleaning, analyzing
find patters ; manipulate test ; add / remove text based off patterns 

Marvel Comics DB
contains: comic names, active years, publish date, issue description, penciler, writer, cover artist, imprint, format, rating, and price
Marvel Comics.zip [Marvel_Comics.csv] - comic_names column is messy and needs cleaning, then we'll find trends like who's the most prolific writer, the most popular, the most profitable, etc.,

{ with Marvel_Comics.csv } **Hey chat, can you read and explain this data for me?**
response:```
Got it ✅ — here’s what your Marvel_Comics.csv file looks like:
Size: 34,992 rows (each row = one comic issue)
Columns (12 total):
comic_name → Name of the comic series (e.g., A Year of Marvels: April Infinite Comic)
active_years → Year(s) the series was active
issue_title → Title of the specific issue (with number if applicable)
publish_date → When it was published
...
📈 Trends (comics published over time, price changes, etc.)
👉 What would you like me to break down first?```
	**I'd like to use the regex library to extract information such as the most commonly used superheroes, or the most common titles. Then, we'll do some other analysis**
response:```
Perfect! Using regex here makes sense because a lot of superhero names will show up in comic_name, issue_title, and issue_description.
Here’s the game plan:
Regex extraction:
Build regex patterns to detect common hero names (e.g., Spider-Man, Iron Man, Hulk, Thor, etc.).
Apply them across text-heavy columns like comic_name and issue_description.
Frequency analysis:
Count which names show up most often.
Identify the most common titles (e.g., "Avengers," "X-Men").
Prepare for other analysis:
Once we know which heroes/titles dominate, we can dive into trends (by year, by price, etc.).
Before I write the regex, a quick clarification:
 Do you want me to focus only on specific superheroes (like the Marvel “big names”), or should I try to pull out any capitalized word that looks like a character/title and then rank them?```
	 **Let's start with any capital word that looks like a character/title and rank them, and if it fails, we'll try something new.**
response:```
The regex extraction worked 🎉 — but it also picked up some false positives like The, But, None, And, It, What, and Rated.
Here are the top real superhero/title terms it surfaced so far:
Man → 9,686 (too generic, often appears as part of Spider-Man, Iron Man, etc.)
Men → 7,537 (likely X-Men)
Spider → 6,089 (mostly Spider-Man)
Avengers → 3,560
Captain America → 2,858
Wolverine → 2,732
Thor → 2,605
Iron Man → 2,385
Fantastic Four → 2,331
Star Wars → 2,307
Daredevil → 2,288
Hulk → 2,127
Next Step (Cleanup Idea 🧹)
We can refine this by:
Filtering out stopwords (e.g., The, And, It, But, None, Rated).
Merging related terms (e.g., Spider + Man → Spider-Man, Men → X-Men).
Ranking again after cleanup to get a truer picture of superhero frequency.
👉 Want me to clean and merge these terms automatically so we get a more accurate “Top Heroes/Titles” list?```
	**Let's try this. Treat words with a hyphen between them as one word. Ignore stopwords; i.e., The, And, But, Or, None, Rated, If, etc., then, after cleaning is complete, apply a ranking.**
response:```
Much better! 🚀 With hyphen handling and stopwords removed, the ranking now highlights real heroes and teams.
Here are the top characters/titles in your Marvel dataset:
X-Men (shows up as “Men”) → 7,484
Spider-Man → 4,285
Avengers → 3,559
Marvel (company or branding) → 2,886
Captain America → 2,857
Wolverine → 2,732
Thor → 2,601
Iron Man → 2,383
Fantastic Four → 2,331
Star Wars → 2,307
Daredevil → 2,288
Deadpool → 1,850
Hulk → 1,555
Peter Parker → 1,380
Marvel Universe → 1,368
⚠️ A few extras still sneak in (Earth, Plus, Uncanny, In, Who), but most of the list is now true superheroes/teams.
👉 Do you want me to refine this further (e.g., merge “Men” into “X-Men” automatically, drop non-character terms like Earth/Uncanny/Plus) so you get a pure hero ranking?```
	**Hit the context limit here**