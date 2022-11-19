Python decorators are used to modify the behaviour of functions.

### Example

~~~ python

def the_dec(func):

    def func_wrapper():

# before code behaviour
        func()
        # after code behaviour
        return func_wrapper

@the_dec

def print_message():

	print("Hello there.")


~~~

  
### TLDR;
When the 'print_message' function is called, the decorator funtion applies the before and after code.
The decorator function extends the functionality of the original function.
The decorator function can be used to decorate other functions as well.