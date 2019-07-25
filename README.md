# EgoShell
Shell script based command line interface for overture-stack/EGO

Version 0.1 

# What is it?

It's a series of shell scripts that let you administer an [EGO] (http://overture/products/ego) authorization service. 

# Why is it good?

It gives you a quick and easy way to grab the ego authentication token that you need to do anything else with Ego's rest API, and it gives you some utility scripts that you can run that communicate with ego. 

# How do I get it set up?

(1) **Set up OAuth 2.0 Authentication with Google**

Go to https://console.developers.google.com/apis/

Log in with your google email and password.

Go to *Credentials*, then *Create OAuth client ID*. 

Select **application type** *web application*.

Enter *http://localhost:1235* under **Authorized redirect URLs**.
 
Google will then generate a **client_id** and **client_secret** for you that you can use to let someone log in to your Ego server google email password.
     
(2) Set up your Ego server, and configure it with the *client id* that you just got.

(3) Edit the file called **config** and set the correct values in the variables **CLIENT_ID** and **CLIENT_SECRET**, and
the **EGO_URL** to the url of your Ego server.

(4) If you're not running on a Mac, change the **BROWSER_COMMAND** setting from "open" to whatever command you use to run your web browser from the command line

# What other programs do I need have installed?
- ego (of course!)
- curl
- jq
- nc
- sh
- cut 
- sleep

You might need to install **jq** -- most UNIX systems already have the other programs installed. 

# How do I run it?
(1) Run **./google.login**, and wait for a browser window to open up, with google
Oauth login page.  

(2) In your web browser, log in with your google email and password. 

(3) You'll see a small page that says "ok" at the top if the login was successful.

(4) Back in your shell window, google.login will display ego authorization
token, then launch a new shell with your authorization token set to the
environment variable **AUTH**. 

(5) Now you can run a series of shell scripts that interact with your ego
server. Most of them assume that you are running as an Ego user of type ADMIN.

From there, you have several commands that you can run to interact with Ego.

Examples:

```
% ./create_permission <policy_name>.[READ|WRITE|DENY] <group_name>
```

Creates a group permission setting that authorizes access to the resource controlled by <policy_name> with the given policy mask (READ, WRITE, or DENY) to all members of group <group_name> groups and policies are created if they don't already exist.

Other things to try:

```
% ./list policies
% ./list users
% ./list groups
% ./list_permissions <policy_name>
% ./find_id <name> [policies|users|groups|permissions] 
% ./get <name> [policies|users|groups]
% ./delete <name> [policies|users|groups]
% ./add_user <group_name> <user_name> 
```

# What files do these programs create?

- google.html (contains the Google login page )
- results ( temporary file )
- tokens ( temporary file )

# What other files do these programs rely on?
- msg ( HTTP reply message for our browser  )

# How long did you spend writing and testing this?

I wrote it all late last night. There are probably bugs and edge cases to solve. It's still very much a work in progress -- but it works well enough that I find it useful. Perhaps you will, too! 


