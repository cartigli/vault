INTRODUCTION & OVERVIEW
Welcome to the Data Science & Analytics Vault! This is an open-source repository of notes on Python, SQL, Machine Learning, Statistics, Probability, and more. The goal of this repository is to create and maintain a living resource for all things data.

ABOUT & PURPOSE
This repository started as I gained interest in the behind-the-scenes of Machine Learning. Specifically, Ollama has always intrigued me as such a capable and dynamic technology available world-wide offline. As I continue to learn about Large Language Models, Neural Networks, Back Propagation, etc., it becomes overwhelmingly important organized documentation is. As I started classes on the programming back-end of these models and the intuition behind their architecture. I decided I needed thorough notes on not only M.L. design & architecture but Python, SQL, their nuances, novelties, tricks, features, etc., to properly keep track of and build from as a knowledge base. As I did so, it also became apparent how useful this could be for others & how useful others could be for this.

I tried to be clear in showing the meaning behind the code and methods applied throughout the notes in this vault, and even more so to be accurate. I am also aware of the fact that the libraries and versions used in the classes were slightly outdated in some cases, and although I think I have I found and repaired them all, there's likely items I missed, misleading notation, or plain incorrect notes at some points in this vault. I would love to hear about them!

This notebook was written and read entirely in Obsidian. To render certain symbols, formulas, and matrices, I chose to use Latex commands throughout the vault for various purposes. For diagrams and charts, I chose Tikz's library which came in handy for more complex representations. To render Tikz in Obsidian, the community plugin 'TikZJax' is needed. To simplify the user's required configuration, I did not include the .obsidian specification within the .gitignore. The goal is cloning the repository allows one to open the vault with the configuration preset with the Tikz plugin. There is also an Execute Code plugin which makes it much easier to run and compare outputs of Python scripts while taking notes on them, in my opinion. If you do not want to install or run these plugins, use the branch no_obsidian where the .obsidian folder is ignored, leaving only .md files.

STRUCTURE
This repository is organized into three main categories: Statistics, Python, and MySQL
- I Stats
	- I Probabilities - Mathematical Foundations and Distributions
	- II Statistics - Application of Statistical Methods
- II Python
	- I Intro - Basic Python Formatting & Syntax
	- II Core - More Basic { Architecture of } Functions and Methodology
	- III Stats - Application of Statistical Methods with Python using NumPy, Pandas, Sci-Kit Learn, StatsModels, & more
	- IV M.L. - Advanced Statistical Methods & Machine Learning
	- V Extraneous - Additional Notes or Functions
- III MySQL - contains less files but longer notes on MySQL functions like creating databases, tables, triggers, window functions, & more fundamentals

CONTRIBUTING
Contributions are welcome! If you have an additional example, a found error with a correction, or a new topic, please:
- Fork the repository
- Create a new branch for your changes
- Submit a pull request with a  clear description of your contribution[s]
For complex contributions or corrections, please include thorough explanation of logic and provide & test code snippets if possible. Try to be clear with what you want to introduce or the error you are identifying and correcting.

AREAS FOR CONTRIBUTION
- Error corrections
- Additional examples
- Improved explanations / definitions
- Updated best practices
- Other if reasoning is well supported

GETTING STARTED & RENDERING
```
# Get the repository on your machine:
git clone https://github.com/cartigli/vault.git

# Navigate to the vault
cd vault

# For the python & ML libraries
pip install pandas numpy scikit-learn matplotlib seaborn
# Tensorflow is needed in this section but is large enough to wait for installation if you so desire
pip install tensorflow

# If on macos, I recomend using a venv with python3:
python3 -m venv venv_name
source /venv_name/bin/activate

# Now your shell should show (venv_name) at the begining 
# This means your venv is activated; proceed w/ installing dependencies
pip install pandas numpy scikit-learn matplotlib seaborn tensorflow
# Sometimes pip3 is needed, but usually once inside a virtual environment the installation is fairly smooth
```

This notebook was written and read entirely in Obsidian. To render certain symbols, formulas, and matrices, I chose to use Latex commands throughout the vault for various purposes. Additionally, for diagrams and charts, I chose Tikz's library which came in handy often for more complex representations. To render Tikz in Obsidian, the community plugin 'TikZJax' is needed. To run code within the Obsidian application, I installed the Execute Code Plugin community plugin which allows one to execute code blocks when in read mode. 

To simplify the user's required setup, I did not include '.obsidian' within the .gitignore. I did specify one workspace.json file for Windows/MacOS compatibility, but the goal is cloning the repository allows one to open the vault with the configuration preset with the Tikz and Execute Code plugins. If you do not want to install or run these plugins, use the branch [ xxx ] which ignores the .obsidian folder, leaving only .md files. If you would like this feature and/or don't care, ignore this section.

ABOUT ME
I am a data science practitioner with a B.S. in Business Administration, Management, & Marketing, bringing a focused perspective to data analytics. I am excited about what I have learned so far and hope to continue to gain knowledge and experience with data management and information sciences. 

LICENSE
This project is open source and available under the MIT License.

---
*This vault is a work in progress; your contributions and feedback make it a better resource for anyone learning data science. Happy Learning!*