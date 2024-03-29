# Environmental variables

For now we have heard what is the virtual environment. But what are those Environmental variables and what problems do they solve?

To put simply, we can use them as a form of configuration or storing sensitive data: IPs, credentials, anything else that we do not have exposed in our git project for others to see. We could also use predefine some Environmental variables in GitHub, GitLab, etc. for automated pipelines. 

## Local environmental variables


### Simple approach
In this section we will review how can the environmental variables can help us run our application locally. So imagine a situation where you have to connect to some external API to fetch some data. [Example](https://polygon.io/) this API has couple of tiers allowing us to do certain things. But if we paid for it,  would we want others to use it on our behalf? If the API is charged based on amount of requests - probably not. So how do we make sure that application still works, and we don't break anything along the way? 


what we could do is introduce some environmental variables simply using terminal:

```bash
export USER=USERNAME
export TOKEN=12345
```


What is more now from the terminal we can also access those variables:

```bash
echo $USER
echo $TOKEN
```

**PRO TIP** 🧠 Remember that these variables are only available on the terminal that you are working on. Once you open up new terminal they are "forgotten".

Now how do we reach them once python code is running? - Simple!

```python3
import os


USER = os.getenv("USER")
TOKEN = os.getenv("TOKEN")
...
```


What is more, at the same time we can also be setting env variables using python as well:

```python
import os
os.environ["password"] = "you_will_never_find_out"
```

Another useful feature, maybe we do not have the variable set, but would like to give user a default value?

```python
import os
USER = os.environ.get("USER", "Not Set")
...
```



Try this out yourself. How can you check if this works? What others things would you like to hide from others in your repo? Discuss.

Of course if you have codebase like that it is mandatory to warn your possible users/ colleagues that these variables have to be exported before launching the application, otherwise you will be asked about this too many times.


### Pydantic approach
There are also ways of setting there variables in separate configuration files, that have to be pre created manually, another option is to use some 3rd party library. One of such examples is the library that along with FastAPI gets a lot of love as well - [pydantic](https://docs.pydantic.dev/) . Please check it out, here we will just show a simple example with environmental variables, but the library goes far beyond that - It's main purpose is to validate data structures, mostly json, but it is really amazing.

So getting back to our topic, how do we use thing great tool for env variables? We start by cutting out importing of os module and adding pydantic:



```python
from typing import Optional


from pydantic import BaseSettings

class Settings(BaseSettings):
    API_V1_STR: str = "/api/v1"
    MONGODB_URL: str
    GF_API_URL: Optional[str] = None
    TOKEN_SECRET_KEY: str = (
        "fj0823t8y3t9shoidn9184h13iudhaslidfuh3190841-00=52394hfu"
    )
settings = Settings()

print(settings.API_V1_STR)
```

What is happening here?
1. We import BaseSettings class from pydantic which is then inherited for Settings class. This enhanced our class quite a lot as now we are able to use it as a bundle of environmental variables required for our application.
1. For the Settings class we define certain class variables some of which are mandatory, some are Optional, and pay attention also that there are some default variables as well. 
1. To simply start using the class we have to initiate it without any parameters.
1. If something is not right - pydantic will let you know.

Try running the code. Does it work? Try fixing it. IS everything clear here? Discussion time.

### dotenv approach

One last way of getting it done would be to use library called [python-dotenv](https://pypi.org/project/python-dotenv/) It is also rather straight forward way of doing it, and you do no track this file with git as well, so remember adding it to .gitignore . 

so let's create **.env** file:
```
DOMAIN=example.org
ADMIN_EMAIL=admin@${DOMAIN}
ROOT_URL=${DOMAIN}/app
```

You can immediately notice that the syntax in this file is similar to bash. Now how to access these variables in the code?


```python
from dotenv import dotenv_values

config = dotenv_values(".env")  # config = {'DOMAIN': 'example.org', 'ADMIN_EMAIL': 'admin@example.org', 'ROOT_URL': 'example.org/app'}
```

And now we are able to access them in our code as well. Try it out yourselves.

## Environmental variables non local

So what is this this non local place? Your application will have to eventually be launched somewhere right? According to the best practices it should be done in an automated fashion using CI/CD principles and we do now want to be doing this manually each and every time, imagine how many mistakes that could generate...

### GitHub actions

Today we will look into GitHub actions, to add those, we do not need to do `export` command as before we simply need to navigate the UI of the project and add those variables ourselves:


![IMG](https://github.com/CodeAcademy-Online/python-new-material-level2/blob/master/images/github_secrets.jpg)


Here we can make use of those variables in any of the later logic when deployging the application to another server/ machine. 

# TODO: Maybe add CI CD topic in here? But we do not have the application we can deploy yet, and where to deploy it? It could be the FAST API DEMO that is using some env variable or something like that. Or we can make it locally.


* **Task Nr.1**:

Create `.env` file with environmental variables:
1. username
1. password

Write an application asking user to enter `username` and `password`. Check if user entered the same credentials as in your .env file. If so print "ACCESS GRANTED" Otherwise print "WRONG CREDENTIALS" until user enters correct details.

# 🌐 Extra reading:

* [more on env variables](https://developer.vonage.com/blog/21/10/01/python-environment-variables-a-primer#:~:text=What%20Are%20Environment%20Variables%3F,it%20connects%20to%20the%20API.)

