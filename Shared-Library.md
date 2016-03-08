With **Shared library** module you can define your own variables and functions, which you can use in a **Transformation** of any **Microservice**.


In the **Shared Library** code you can use all the features described in the **[Transformation](https://github.com/c-534/documentation/wiki/4.-Transformation)** section.

## Usage example

The **Shared Library** code:
```Python
def my_own_function(a, b):
    return a + b
```

The **Transformation** code:
```Python
out_dict = sharedlib.my_own_function(4, 5)
```

The result of **Microservice** run:
```Python
out_dict = 9
```