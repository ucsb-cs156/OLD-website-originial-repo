---
topic: "OAuth: Google Setup"
desc: "Setting up a Google OAuth App to obtain client id and client secret"
category_prefix: "OAuth: "
indent: true
---


# How to set up Google OAuth

1. Navigate to <https://developers.google.com/identity/sign-in/web/sign-in> to create a Google OAuth Application.
    - If you are asked "Where are you calling from", select "Web Server"

    - Set the *Authorized Redirect URI* to: `http://localhost:8080/login/oauth2/code/google`
2. Add the following items to your `localhost.json` file, filling out the `client-id` and `client-secret` with the values from 
your Google OAuth application:
```
"spring.security.oauth2.client.registration.google.client-id":"ENTER-GOOGLE-ID",
"spring.security.oauth2.client.registration.google.client-secret":"ENTER-GOOGLE-SECRET"
```
    - **NOTE**: If you want Heroku to also support Google OAuth, you'll need to do the same in `heroku.json`, hopefully with a set of production credentials from a production Google OAuth app.
3. Run `source env.sh` to update your environment.
4. Run `mvn -P localhost spring-boot:run` and see that your application is now configured to support Google OAuth!.

# Configuring the OAuth Consent Screen

The first time you create a new OAuth application, you'll be asked to configure the OAuth Consent Screen.

**What is the OAuth Consent Screen?** The idea is that when your application authenticates using Google OAuth OAuth, it will share certain information/permissions with the application; at a minimum, your name and Google email address.  Before Google allows this, it wants to be sure that you give your permission.   For this reason, you need to configure what will be shown to the user when this happens.

**What information am I asked for when configuring the OAuth Consent Screen?**  Here is a screen shot that shows what I filled in for a sample application running on Heroku called `demo-spring-react-example-s22`:

<img width="687" alt="image" src="https://user-images.githubusercontent.com/1119017/159813247-16ff80dc-cc56-42fa-8f10-42dcda021327.png">
<img width="676" alt="image" src="https://user-images.githubusercontent.com/1119017/159813299-1122efe4-8940-4aa7-9878-fcfcb9d17d6f.png">
<img width="606" alt="image" src="https://user-images.githubusercontent.com/1119017/159813319-cbf35953-b7eb-489a-84c2-69a85934515a.png">
