# === Deploy to Heroku ===


##################
# PostgreSQL URI #
##################
# go to the main folder that holds both the website folder and the virtual/
sudo heroku login
# create an app
sudo heroku create <app_name>
# destroy an app
heroku apps:destroy --app <app_name>
https://datapostgresql.herokuapp.com/ 
# create postgresql, this dev version allows to have up to 10K rows
# also, note that Heroku counts a database as an app
sudo heroku addons:create heroku-postgresql:hobby-dev
heroku addons:attach my-originating-app::DATABASE --app datacollectoremaildownload
# fetch the URI of the database
sudo heroku config --app <app_name>
postgres://qlalxkvvxnhmms:eba6fc081936b05bf7576299e0e4ea49ccfe54b9b8644e4689d45b931528d106@ec2-54-83-33-213.compute-1.amazonaws.com:5432/d6fpophj3nior5
# paste this into your code and add at the end 
?sslmode=require # this will allow you to access the db via ssh
# create a file .gitignore and add virtual/ and __pycache__ and also the .whl file to it

##################
# Remote Session #
##################
# python shell
sudo heroku run python
# bash shell
sudo heroku bash
# postgresql shell
sudo heroku pg:psql --app <app_name> # you might need to all the path to the psql executable on local machine..

##############
# Simple App #
##############
cd plot_webapp/ # the website files are inside it
sudo -H virtual/bin/pip install gunicorn # this is http server for Heroku
virtual/bin/pip freeze > requirements.txt 
# in the above, make sure to remove the line that says certifi==2018.4.16
# also if it complains about some package like pkg-resources==0.0.0 
# then try to remove it from the requirements.txt
vim Procfile
web: gunicorn script1.py:app
vim runtime.txt # check the runtimes available on Heroku
python-3.5.1 # latest stable and supported is python-3.6.6
sudo heroku login
sudo heroku apps
sudo heroku create <app_name> # sudo heroku create <gtmcandlestickplot>

git init
git add .
git commit -m "first commit"
# connect your session to an app
heroku info # if no app specified do the following:
sudo heroku git:remote --app <app_name>
sudo heroku info # https://gtmcandlestickplot.herokuapp.com/
sudo git push heroku master
# ...wait...
sudo heroku open


########
# Logs #
########
sudo heroku logs -n 1500
