# Debugging Python code

There are a lot of ways one can Debug Python code. You could be using an IDE extensions allowing to do that in you IDE GUI, or you can do that a bit more tedious way with print statements or additional libraries.


## Good old print() statements

Of course by now we have used print plenty enough, some people also like to use print() for debugging or logging as well:

![IMG](https://github.com/CodeAcademy-Online/python-new-material-level2/blob/master/images/debug4.png)

This is not great and not terrible during the developing period of your application, but once it is live - you should not be doing such things. So let's discuss other options.

P.S. If you got this far in course you know how print() works, so no examples here.

## pdb library:

Another a little bit more sophisticated way of debugging is using pdb library:

```python
...
import pdb
pdb.set_trace()
...
``` 

Once this line is reached you will get a shell where you can look around in computers memory and see what variables you have, their state etc.

Of course it is indeed a bit tedious to debug the code by writing more code... So let's look how we can do this with the help of the VSCode. 

So let's create main.py file and write some code:

```python
my_list = [1, 2, 3]

for item in my_list:
    something = item + 1
    print(something + 1)
```


So this is rather simple and straightforward but how do we inspect what is _something_ during the runtime? So let's at first one the left handside of the code window add red bubble simply by clicking with our cursor:

![IMG](https://github.com/CodeAcademy-Online/python-new-material-level2/blob/master/images/debug1.jpg)

now we are ready for debugging. Hit the button with a play button and a bug:

![IMG](https://github.com/CodeAcademy-Online/python-new-material-level2/blob/master/images/debug2.jpg)

For now simply choose _Python File: Debug the currently active Python file_ and this is it in a matter of seconds you will see something like this:

![IMG](https://github.com/CodeAcademy-Online/python-new-material-level2/blob/master/images/debug3.jpg)


As you can see on the left hand side you can see all of the variables currently loaded into computers memory and you can inspect manually what is what. It is a bit less tedious approach cause now you have an UI where you can see things conveniently. What is more you have this play menu where you also have a few choices what to do.

Please have a go of your own. Write different code, try debugging it. Is everything clear? Discuss.

# Logging

So for now we have seen how to investigate issues once you are developing your application - you run some examples, investigate what is going on and solve the issues along the way. But what happens if the issues occur during once the application is in the production environment, how do we know what caused it, and how to we recreate those situations in safe environment? Answer is in the Subject - Logging!
With logging you can pickup the logs and review what happened in your system, what were the actions that led it to unwanted state or made it do things it was not supposed to.

We have already seen the [logging](https://github.com/CodeAcademy-Online/python-new-material/wiki/Lesson-14:-Logging) in the beginning of the course, let's look into it a bit deeper.

What we yet have not seen is how to elegantly create logging config. So let's try doing it ourselves.

create a file called _logging.conf_ 
Add the following information

```conf
[loggers]
keys=root,sLogger

[handlers]
keys=consoleHandler,fileHandler

[formatters]
keys=fileFormatter,consoleFormatter

[logger_root]
level=DEBUG
handlers=consoleHandler

[logger_sLogger]
level=DEBUG
handlers=consoleHandler,fileHandler
qualname=sLogger
propagate=0

[handler_consoleHandler]
class=StreamHandler
level=WARNING
formatter=consoleFormatter
args=(sys.stdout,)

[handler_fileHandler]
class=FileHandler
level=DEBUG
formatter=fileFormatter
args=('logfile.log',)

[formatter_fileFormatter]
format=%(asctime)s - %(name)s - %(module)s - %(levelname)s - %(message)s
datefmt=%Y-%m-%d %H:%M:%S

[formatter_consoleFormatter]
format=%(levelname)s - %(message)s
datefmt=%Y-%m-%d %H:%M:%S
```

Now create python file called _main.py_ with contents:

```python
import logging, logging.config

# set up logging
logging.config.fileConfig("logging.conf")
logger = logging.getLogger("sLogger")

# log something
logger.debug("debug message")
logger.info("info message")
logger.warning("warn message")
logger.error("error message")
logger.critical("critical message")

```

Now without any hassle you can recreate this logging in any of the other files and reuse it, having only one place where to change the configuration of your logging or adding additional handlers etc.

Try adding functionality for logger to write into the file. Can you do it via configuration file? Give it a try and discuss findings.


## Logging for errors

What is more it is also quite important to log out what actually happened, what errors caused the application to break. Usually we could be expecting some errors, but at the same time it could be something else but we could also log those errors as well. It could be done like this:

```python
try:
    with open(filepath,'rb') as f:
        ...
    logger.info('File successfully read')
except Exception as e:
    logger.error('Failed to open: '+ str(e))
```

And now you will definitely see if anything goes wrong here in the logs. Here we could even do print instead of logger.error except that print will only be visible in terminal where the application is being run.

# Last commit approach

It could be that suddenly the bug is introduced into your code. This is not a new scenario believe me... What we could do:
1. Analyze entire codebase.
2. Try finding out when this bug appeared.

If we choose the latter we can try going through GitHub commit history. and try checking out to the previous commits, run code and see what happens.

If you want to checkout to the certain commit, you can simply do:



`git checkout <commit_hash>`

You will immediately get notified by git that the HEAD is now detached. I believe we have seen this one before. **NOTE ** This situation only allows you to look around at certain point in time. You cannot go back in time and change the Future, this is not some movie from 80s... But you can always branch out and carry on working from certain commit. So it kind of works.


So if you checked out to previous commit and it still does not work as expected, you can always go one step back again and try it one more time. If it works - analyze what was changed. This sometimes could be a big time saver.

# Comment out until it works

Sometimes Errors are not that clear to understand, especially when you are doing something with databases or some third party libraries. So you might choose the commenting out approach. Simply try commenting out lines to see if at some point code stops breaking. Then it is easy to understand what is going wrong.

# Rubber duck debugging

The idea is that when a programmer needs to debug their code, they should explain the program line-by-line to a rubber duck. Often, the act of explaining the problem step by step will cause the solution to present itself.

The concept of Rubber Duck Debugging need not be confined to programming

# 🔍 Just Google it

Sometimes when things don't work (That of course happens more often than we would like it to) programmers just google things. This is one of those professions where new things/ frameworks come and go, and you gotta learn complex things on the fly. So what separates good programmer from great one? Yes, the way people Google. It seems like a nobrainer, but it definitely is the art of asking your questions correctly. Most likely the answer is already out there, it must have been asked by someone else before us. Unless we are in an extremely niche topic. 

**PRO TIP** ✔️ It is also possible to use some tricks when googling. For example if you want to get answers specifically from stackoverflow.com `site:stackoverflow.com <your_question>` this will lead to results coming from only stack overflow. 

So how do we ask questions correctly? We will try looking into this along the way. But in general you should be asking questions very specifically yet abstracting out elements as well. I.E let's say you have dictionary:

```python
information = {"name": "Gandalf"}
```

And you wanted to change the name, but did now know the syntax. You would not go asking around: _how to change name in dictionary_ or something like that. Here you are simply changing what? A value for a certain key. so we should google something like: _python changing dictionary value_ . 

**PRO TIP** ✔️ It is also quite useful to state the language you are working on since most of the things are similar through the programming language. For example, strings are string everywhere, like integers, lists/ arrays or other things like that, so take shortcuts whenever you can - work smart not hard. 


Not having the same dictionary how would you google to get the answer of how to change _name _to _character_?

## Exercises: 


* **Task Nr.1**:

Find some coding examples from before, and try applying debugging/ logging examples seen in the lecture today. Try using try/ except blogs somewhere and add logging to them. Try breaking them on purpose to see what error messages can you get in the log file.

# 🌐 Extra reading:

* [Logging](https://realpython.com/python-logging/#classes-and-functions)

* [More google tricks](https://www.lifehack.org/articles/technology/20-tips-use-google-search-efficiently.html)






