Install Web-PDB into your working Python environment:

### pip install web-pdb

```python
x = 1
import web_pdb; web_pdb.set_trace()
x = 2
x = 3
```
Insert the following line into your Python program at the point where you want to start debugging:

### import web_pdb; web_pdb.set_trace()

connect localhost:5555

# TIP

Globals and Locals boxes show local and global variables in the current scope. Special variables that start and end with double underscores __ are excluded (you can always view them using PDB commands).
Human-readable Unicode literals for Python 2.
Command history that stores up to 10 last unique PDB commands (accessed by arrow UP/DOWN keys).
