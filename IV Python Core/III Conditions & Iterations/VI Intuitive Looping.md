if we want 0,1,2; we could bind x to [0,1,2], or...
```python
x=[0,1,2] # for len to count
len(x) # == 3
for n in range(len(x)): # range(3) = range(0, 3, 1)
	print(x[n])
```
{{ outputs: 0, 1, 2 }}
	{{ requires indexing for outputs to be used }}