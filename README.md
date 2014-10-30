## How to use the Dropbox API as a storage center for your file uploads when using the 'Paperclip' gem.


A simple 10 step process to get you up and running. This tutorial will go over how to use the Dropbox API to store your files/images while using paperclip to upload them in your app. This tutorial assumes you are using the paperclip gem and have it set up already. This is a great solution to store image uploads for your deployed applications.

### 1st : 
##### Head on over to Dropbox.com and go through the motions to sign yourself up for an account. You will need one of these to use their API. Don't worry, it's free and they are an awesome company.

### 2nd : 
##### Find your way to Dropbox.com/developers . Here is will you will be creating an app and registering it with Dropbox. Click on 'App Console' and then 'Create App'. Choose the 'Dropbox API app' selection and then choose 'Files and datastores'. The next part is up to you. I generally limit my app to only its own folder. Now, name it!

### 3rd : 
##### On the next page you will find you 'App Key' and 'App Secret'. These wil be crucial in getting things fully setup.

### 4th : 
##### Head over to your Gemfile and include this guy and then bundle install:

```
gem "paperclip-dropbox", ">= 1.1.7"
```

### 5th : 
##### This part will be up to you. It depends on what version of Rails you are using and what you are comfortable with. For this example I will be using the gem 'Figaro'. Some of you may prefer to just use your secrets.yml file. All up to you! Head over to https://github.com/laserlemon/figaro for instructions on how to set 'Figaro". I like 'Figaro' to store all my secrets and key that I might be using in my app because it automatically adds these to your .gitignore file via the application.yml file. Don't upload your secrets to Github!

### 6th : 
##### Now we are going to want to create a 'dropbox.yml' file in our 'config' folder.

### 7th : 
##### This will be the code we put in the 'dropbox.yml' file if we are using 'Figaro':

```
app_key: ENV['APP_KEY']
app_secret: ENV['APP_SECRET']
access_token: ENV['ACCESS_TOKEN']
access_token_secret: ENV['ACCESS_TOKEN_SECRET']
user_id: ENV['USER_ID']
access_type: 'app_folder'
```

### 8th : 
##### We now want to add some code to which ever model we are using 'Paperclip' on for uploads. This will be what the code looks like:

```
has_attached_file :image,
    :storage => :dropbox,
    :dropbox_credentials => { app_key: ENV['APP_KEY'],
                              app_secret: ENV['APP_SECRET'],
                              access_token: ENV['ACCESS_TOKEN'],
                              access_token_secret: ENV['ACCESS_TOKEN_SECRET'],
                              user_id: ENV['USER_ID'],
                              access_type: 'app_folder'}
```

### 9th : 
##### Now in the terminal we will want to run this code :

```

rake dropbox:authorize APP_KEY="your_app_key" APP_SECRET="your_app_secret" ACCESS_TYPE=app_folder
```

It will respond with a URL. Visit this URL and allow your app persmission to your Dropbox. After doing so it will give you the remaining puzzle peices that we need. These will be in the form of an 'access token' and 'access token secret'. Use these to fill in the remaining fields in your application.yml/secrets.yml .

### 10th : 
##### Last but not least... restart your app and start uploading! your uploads will no begin being saved to your Dropbox account. You can verify this by logging into Dropbox and checking out your apps folder to see all the uploads.

Hope this helps you with storing your uploads for your deployed application.

I always enjoy feedback!

Big thanks to [Nick Bucciarelli] (https://github.com/nbucciarelli) for originally giving me the knowledge to accomplish such things and to both the [paperclip gem] (https://github.com/thoughtbot/paperclip) and the [paperclip_dropbox gem] (https://github.com/janko-m/paperclip-dropbox).












