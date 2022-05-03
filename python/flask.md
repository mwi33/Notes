# Flask setup and use

  ## Flask package and import
  
Create and start a virtual environment


From within the virtual environment install flask

~~~ python

pip install flask

~~~

## test install

~~~ python

python -c "import flask; print(flask.__version__)"

~~~
# configure flask

~~~ python

set FLASK_APP=my_app.py

$env:FLASK_APP = "my_app.py"

flask run

~~~