# Logging

We have already seen how we do some logging in python code in the previous lectures. But the introduction that we had gave us only a glance on how the logging could be implemented, today we will see how to introduce logging a bit more gracefully in the context of the bigger project than just one file. and how to handle logger.

## Configuration

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
Ideally we do not want to be adding this 