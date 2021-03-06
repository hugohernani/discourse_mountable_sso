# Discourse Mountable Sso

Discourse Mountable Sso is a mountable engine made to handle [Discourse](https://github.com/discourse/discourse/) single sign on technique.

##Getting started

Discourse mountable sso 0.0.2 works with Rails >= 3.2 . You can add it to your Gemfile with:

```ruby
gem 'discourse_mountable_sso'
```

Run the bundle command to install it.

After you install Discourse mountable sso and add it to your Gemfile, you need to create a file in config/initializers in your application filled with the below data :


```ruby
#config/initializers/discourse_config.rb
DiscourseMountableSso.configuration.secret = <secret>
DiscourseMountableSso.configuration.discourse_url = <DISCOURSE_URL>	
DiscourseMountableSso.configuration.login_path = <LOGIN_PATH>
DiscourseMountableSso.configuration.discourse_data_method = <DISCOURSE_DATA_METHOD>
DiscourseMountableSso.configuration.logged_in_check_method = <CHECK_LOGIN_METHOD>
DiscourseMountableSso.configuration.store_return_to_url_method = <RETURN_TO_URL_METHOD>
```
##Configuration description

* secret : Is the the secret you configured in your discourse admin panel
* discourse_url : Is the URL of your discourse application.
* login_path : Is the login path of your own app as www.example.com/login then your login path will be "/login"
* discourse_data_method : Is a method returns the user data for discourse in this format:
    * ``` {:avatar_url=>"http://www.example.com/avatar1.jpg", :email=>"lorem@ipsum.com", :name=>"lorem", :username=>"lorem", :external_id=>1}```
* logged_in_check_method : Is a method to check if the user is logged in or not and returns true or false.
* store_return_to_url_method : Is a method to store the return_to path as after the user log-in in your app it'll be redirected back to discourse server.

##Notes: 
  * Add this route to your routes.rb file  
  
   ```ruby
   mount DiscourseMountableSso::Engine => "/discourse_mountable_sso"
   ```
  * We use a session named ```[:discourse_mountable_sso][:query_string]```
  * Adjust your login method to check if you stored a return_to using ``` store_return_to_url_method ``` to redirect to this url.

   

