
**create and activate a python env**

python -m venv namE
source namE/bin/activate # in macos
/namE/Scripts/activate # in windows

**script for git but much more useful**
```python
import sys # allows interactions with the Python system
import subprocess # allows terminal command from Python

def git_backup(message):
	subprocess.run(["git","add","."])

	subprocess.run(["git","commit","-m",message])

	subprocess.run(["git","push"])

	print('all done, boss')

if __name__ == "__main__":
	commit_message = input("learned a little more")

	git_backup(commit_message)