# Todo_Web_App_using_Django_with_Chrome_extension

This ToDo app makes use of [AdminLTE](https://adminlte.io/themes/dev/AdminLTE/index.html) template also implemnts a chrome extension to easly access webapp if you are hosting. If you Add To Home screen in phones can be used like an app. 

## How to use

can be used in local host or deploy using heroku it's also free.

You need to install python and pip 

  ### For Local usage
  
    ```
    git clone https://github.com/Asif404/Todo_Web_App_using_Django_with_Chrome_extension
    cd todoapp
    pip install -r requirements.txt
    python manage.py makemigrations
    python manage.py migrate
    python manage.py runserver
    ```
Vola...server starts running
 
  ### For heroku
 
First you need to make [Heroku](heroku.com) account ,then download and install [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)
 
```bash
git clone https://github.com/Asif404/Todo_Web_App_using_Django_with_Chrome_extension
cd todoapp
pip install -r requirements.txt
heroku login
heroku create yourappname
```
THis will generate a URL for you take a copy of it.Now we some adjustments in **settings.py**
```python
ALLOWED_HOSTS = ["yourappname.herokuapp.com","127.0.0.1"]
```
![Screenshot from 2021-09-22 15-26-12](https://user-images.githubusercontent.com/33574841/134327500-0222192a-6d9c-44f0-99a8-901ac20a342c.png)

```python
STATIC_ROOT=os.path.join(BASE_DIR,"static")
STATICFILES_STORAGE='whitenoise.storage.CompressedManifestStaticFilesStorage'

prod_db=dj_database_url.config(conn_max_age=500)
DATABASES['default'].update(prod_db)
```` 

All this are diabled initially to work in localhost but should be enabled while deploying to heroku, also

```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'whitenoise.middleware.WhiteNoiseMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```
Now goto **static/manifest.webmanifest** and change start_url": "your_url"
This makes Phone view better thats coming later in tutorial.
Next,
```bash
git init
heroku git:remote your_app_name
git add .
git commit -m "initial commit"
heroku config:set DISABLE_COLLECTSTATIC=1
git push heroku master
heroku run python manage.py migrate
#You can make superuser with
heroku run python manage.py createsuperuser 
```
We are done now open URL (yourappname.heroku.com) to see your app 
