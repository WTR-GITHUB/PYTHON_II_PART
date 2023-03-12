# Logging

We have already seen how we do some logging in python code in the previous lectures. But the introduction that we had gave us only a glance on how the logging could be implemented, today we will see how to introduce logging a bit more gracefully in the context of the bigger project than just one file. and how to handle logger.

## What we have seen so far

We have already seen how to implement different stream handlers:

```python
import logging

# create logger
logger = logging.getLogger('simple_example')
logger.setLevel(logging.DEBUG)

# create console handler and set level to debug
ch = logging.StreamHandler()
ch.setLevel(logging.DEBUG)

# create formatter
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# add formatter to ch
ch.setFormatter(formatter)

# add ch to logger
logger.addHandler(ch)

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warning('warn message')
logger.error('error message')
logger.critical('critical message')
```

Here we can see a lot of boiler plate for in order to setup the logger configurations, format, various handlers that can be seen [here](https://docs.python.org/3/library/logging.handlers.html)  
Ideally we do not want to be adding this boiler plate code in each and every file and today we will see how to do this.

## Configuration file

Logging can be done with the help of configuration file that can be reused throughout the project and like this we exercise DRY principles.
configuration example:

```config
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
format=%(asctime)s - %(name)s - %(levelname)s - %(message)s
datefmt=%Y-%m-%d %H:%M:%S

[formatter_consoleFormatter]
format=%(levelname)s - %(message)s
datefmt=%Y-%m-%d %H:%M:%S
```

in order to use this configuration we can execute the code:

```python
import logging
import logging.config

logging.config.fileConfig('logging.conf')

# create logger
logger = logging.getLogger('simpleExample')

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warning('warn message')
logger.error('error message')
logger.critical('critical message')
```

