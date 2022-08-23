# Todo_Web_App_using_Django_with_Chrome_extension

This ToDo app makes use of [AdminLTE](https://adminlte.io/) template also implemnts a chrome extension to easly access webapp if you are hosting. If you Add To Home screen in phones can be used like an app. 
## Screenshot
![Screenshot from 2021-09-22 18-37-31](https://user-images.githubusercontent.com/33574841/134349244-5a7bee02-37af-4fde-9a75-6bcec63f46cc.png)

![ezgif com-gif-maker (2)](https://user-images.githubusercontent.com/33574841/134348975-9076c27e-c7a9-4b6b-8194-cc901e239ebc.gif) ![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/33574841/134348784-f5690d78-b860-4824-9b5f-aa7054609d61.gif)


## How to use

Can be used in local host or deploy using heroku it's also free.

You need to install **Python** and **pip** 

  ### For Local usage
  
    ```
    git clone https://github.com/Asif404/Todo_Web_App_using_Django_with_Chrome_extension
    cd Todo_Web_App_using_Django_with_Chrome_extension
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
cd Todo_Web_App_using_Django_with_Chrome_extension
pip install -r requirements.txt
heroku login
heroku create yourappname
```
THis will generate a URL for you take a copy of it.Now we some adjustments in **settings.py**
```python
ALLOWED_HOSTS = ["yourappname.herokuapp.com","127.0.0.1"]
```

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
## Chrome Extension

Before uploading extension first navigate to Extension/background.js and change your_url to your heroku app url
```javascript
chrome.action.onClicked.addListener(function(){
    chrome.tabs.create({ url: "your_url" });
  });
  
```
Goto Chrome [Extension](chrome://extensions/) page 

Enebale **Developer mode** at top right.
Click _Load Unpacked_ Open **Extension** folder 
and thats it....

##Mobile view

This will work in mobile browser since its using Bootstrap but we can make it look like an Mobile App by _Add to Home screen_(pic 1) option. It will add icon to homescreen (pic 2) and also Shows _splash Screen_ when opening(pic 3).<br><br>
<img src='https://user-images.githubusercontent.com/33574841/134354219-1ffbd9d3-6adb-47bc-9695-89fbe7b20064.png' height=350> <img src='https://user-images.githubusercontent.com/33574841/134359477-0a8c714d-0475-452c-9b80-30b7ff3a3af4.png' height=350> <img src='https://user-images.githubusercontent.com/33574841/134359470-4038d872-4008-45f1-9227-cb95cc76f479.png' height=350>


