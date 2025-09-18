```python
import os
import pandas as pd

def collector(LOCAL_DIR):
	folder_path = LOCAL_DIR
	guts_togo = []
	name_togo = []
	lo_togo = []
	for root, dirs, files in os.walk(folder_path):
		for filename in files:
			try:
				if full_fpath.startswith(('.csv', '.DS_Store')) or filename.startswith(('.git', '.DS_Store')):
					print(f"{filename}\'s spoofed.")
				else:
					full_fpath = os.path.join(root, filename)
					with open (full_fpath, 'r', encoding='utf-8') as f:
						guts = f.read()
						guts_togo.append(guts)

					lo_togo.append(full_fpath)
					name_togo.append(filename)
			except UnicodeDecodeError:
				print(f"Encoding error with {filename}.")

	return guts_togo, name_togo, lo_togo

def container(guts_togo, name_togo, lo_togo):
	guts_glory = pd.DataFrame({
		'note_tl': name_togo,
		'note_lo': lo_togo,
		'note': guts_togo
		})
	guts = guts_glory.to_records()
	return guts

LOCAL_DIR = '/home/tom/vault'
collected = collector(LOCAL_DIR)
res = container(*collected) # unpack the collected, then contain
print(res)
```

.gitignore's spoofed.
Encoding error with index.
Encoding error with pack-62dbfc1fa734f4bb30d5eb48d5eaef8b2b877047.rev.
Encoding error with pack-62dbfc1fa734f4bb30d5eb48d5eaef8b2b877047.idx.
Encoding error with pack-62dbfc1fa734f4bb30d5eb48d5eaef8b2b877047.pack.
[(  0, 'README.md', '/home/tom/vault/README.md', "INTRODUCTION & OVERVIEW\nWelcome to the Data Science & Analytics Vault! This is an open-source repository of notes on Python, SQL, Machine Learning, Statistics, Probability, and more. The goal of this repository is to create and maintain a living resource for all things data.\n\nABOUT & PURPOSE\nThis repository started as I gained interest in the behind-the-scenes of Machine Learning. Specifically, Ollama has always intrigued me as such a capable and dynamic technology 