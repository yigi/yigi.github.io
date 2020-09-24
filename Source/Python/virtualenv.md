### pip install virtualenv

### mkdir ProjectFolder

### virtualenv project1

### source project1/bin/activate

### deactivate

### rm -rf ProjectFolder

___________________________________________________________________

after you install many packages you can save your history in req.txt 

pip freeze --local > req.txt

### then

pip install -r req.txt #in desired virtual environment
