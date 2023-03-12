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
format=%(asctime)s - %(name)s - %(module)s - %(levelname)s - %(message)s
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

You can see that from the code perspective this is way more elegant, as now if you want to reuse this logging logic you only have to instantiate the logger telling where the configuration file is. You can see that the config file approach has a few advantages over the Python code approach, mainly separation of configuration and code and the ability of noncoders to easily modify the logging properties.

Let's now go through the entire configuration file.

### loggers

```ini
[loggers]
keys=root,sLogger

[handlers]
keys=consoleHandler,fileHandler

[formatters]
keys=fileFormatter,consoleFormatter
```
The loggers section defines the names of the loggers that will be used in this configuration. The keys attribute lists the names of the loggers. In this case, there are two loggers named root and sLogger.

The handlers section defines the names of the handlers that will be used in this configuration. The keys attribute lists the names of the handlers. In this case, there are two handlers named consoleHandler and fileHandler.

The formatters section defines the names of the formatters that will be used in this configuration. The keys attribute lists the names of the formatters. In this case, there are two formatters named fileFormatter and consoleFormatter.

```ini
[logger_root]
level=DEBUG
handlers=consoleHandler
```

The logger_root section defines the configuration for the root logger. The level attribute sets the minimum level of severity for log messages to be logged by this logger. In this case, messages with a severity of DEBUG or higher will be logged. The handlers attribute lists the handlers that will be used by this logger. In this case, only the consoleHandler handler will be used.

```ini
[logger_sLogger]
level=DEBUG
handlers=consoleHandler,fileHandler
qualname=sLogger
propagate=0
```

The logger_sLogger section defines the configuration for the sLogger logger. The level attribute sets the minimum level of severity for log messages to be logged by this logger. In this case, messages with a severity of DEBUG or higher will be logged. The handlers attribute lists the handlers that will be used by this logger. In this case, both the consoleHandler and fileHandler handlers will be used. The qualname attribute sets the fully qualified name of this logger. The propagate attribute determines whether this logger will propagate its messages to its parent logger. In this case, propagation is turned off.


```ini
[handler_consoleHandler]
class=StreamHandler
level=WARNING
formatter=consoleFormatter
args=(sys.stdout,)
```


The handler_consoleHandler section defines the configuration for the consoleHandler handler. The class attribute specifies the type of handler to use. In this case, a StreamHandler is used to send log messages to the console. The level attribute sets the minimum level of severity for log messages to be handled by this handler. In this case, messages with a severity of WARNING or higher will be handled. The formatter attribute specifies the formatter to use for log messages. In this case, the consoleFormatter formatter will be used. The args attribute specifies any additional arguments that the handler needs. In this case, the sys.stdout argument tells the handler to send log messages to standard output.

```ini
[handler_fileHandler]
class=FileHandler
level=DEBUG
formatter=fileFormatter
args=('logfile.log',)
```

The handler_fileHandler section defines the configuration for the fileHandler handler. The class attribute specifies the type of handler to use. In this case, a FileHandler is used to send log messages to a file. The level attribute sets the minimum level of severity for log messages to be handled by this handler. In this case, messages with a severity of DEBUG or higher will.

Task for everyone in the class: try changing the arguments in the config file, experiment with different handlers.



