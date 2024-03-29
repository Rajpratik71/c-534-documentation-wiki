**Transformation** is used to convert "**in_dict**" (the data returned by input connector) to "**out_dict**" (target data structure sent by output connector) using Python code. 
Default data type is Python "dictionary". 

Available **Transformation** features:
```Python
# Built-in functions:
__builtins__, strftime, strptime, mktime, utcnow, re, print

# Operators: 
+=, -=, *=, /=, //=, %=, **=, <<=, >>=, &=, ^=, |=,

# Constants: 
in_dict, param_dict

# Variable: 
out_dict

# Alert function: 
alert(msg)

# Interrupt the running microservice in the Transformation code: 
raise MicroserviceInterrupt('Message', alert=False)

# With sending email alert: 
raise MicroserviceInterrupt(u'Any message that you want to appear '
                            u'in the Microservice Logs.', alert=True)
# Without sending email alert: 
raise MicroserviceInterrupt(u'Any message that you want to appear '
                            u'in the log microservice')

# Datetime localizaion function:
get_localized_datetime(timezone, dt_format). 
"""An example of use: 
get_localized_datetime("Australia/Sydney", "%Y-%m-%d %H:%M:%S")
# Result: "2015-06-06 15:00:00"
"""
```

**You can also create your own functions.**

### It only applies to the REST connector, v4.1 and above:
There is a possibility to define the url to which the message is sent by using the **REST Connector, v4.1** or above by adding the "**rest_url**" key in out_dict, after that the data should be placed in key "**rest_data**" of **out_dict**.
Example: 
```Python
out_dict = {'rest_url': 'http://your_url.com', 
            'rest_data': data} # data variable should by a dictionary
```