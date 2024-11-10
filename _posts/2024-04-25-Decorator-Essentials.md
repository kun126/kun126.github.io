---
layout: distill
title: Decorator Essentials
description: 
tags: python
giscus_comments: false
date: 2024-04-25
featured: true

authors:
  - name: Kun Chen
    url: "https://kun126.github.io"
    affiliations:
      name: World Food Programme, Rome

bibliography: 

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: What is Decorator and why it matters?
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: Syntax
  - name: Common use cases and practical information
  - name: Reference


# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
# _styles: >
#   .fake-img {
#     background: #bbb;
#     border: 1px solid rgba(0, 0, 0, 0.1);
#     box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
#     margin-bottom: 12px;
#   }
#   .fake-img p {
#     font-family: monospace;
#     color: white;
#     text-align: left;
#     margin: 12px 0;
#     text-align: center;
#     font-size: 16px;
#   }
---

## What is Decorator and why it matters?
In simple terms, a decorator is a function that enhances the behavior of another function without changing its code directly. It's like adding a special twist to your functions without complicating their core logic. 

Below is a simplified example to show how it works. In this example, `my_decorator` is a decorator function that takes a function `func` as its argument and returns a new function `wrapper`. The wrapper function adds behavior after calling `func`. By decorating our target function with `@my_decorator`, we effectively create `decorated_function` with the wrapped version provided by the decorator. When `decorated_function` is called, it executes the additional logic defined in the decorator alongside its original functionality.

{% highlight python %}
# Without decorator
def my_decorator(func):
	def wrapper():
		func()
		print("We just called the input function.")
	return wrapper

def func():
	print('This is the function to be applied.')

my_decorator(func)()
{% endhighlight %}

{% highlight python %}
# With decorator
@my_decorator
def decorated_function():
	print('This is the function to be applied.')
	
decorated_function()
{% endhighlight %}
Think of decorators as a way to neatly wrap up your functions or methods with extra features without cluttering them up. Normally, if you want to add something to a function, you tack it on after the function's code. But when your functions start getting big, this can make it hard to understand what's going on. Decorators address this by providing a cleaner way to add functionality to functions or methods. They essentially allow you to wrap your original function with additional behavior without altering its core implementation. This separation of concerns enhances readability and maintainability by keeping the main function's logic distinct from the added features.

---

## Syntax
### Multiple decorators
Python accepts multiple decorators, which are executed from bottom to top. This means that the decorator closest to the function declaration will be applied first, followed by the next decorator, and so on. For example:

{% highlight python %}
@d2
@d1
def func():
	pass

func()
{% endhighlight %}
is equivalent to:
{% highlight python %}
d2(d1(func))()
{% endhighlight %}
In both cases, the function `func` is decorated first with `d1` and then with `d2`, and finally, the decorated function is called. Here's an important point to note: `d2` is not applied directly to `func`, but rather to the `d1-wrapped` version of `func`. This demonstrates the concept of decorators being nested within each other.

### Decorator as a function output
You can also use a decorator as the output of a function. This allows for more dynamic behavior when decorating functions. Here's how it works:
{% highlight python %}
def decorator_func(arg1,arg2, ...):
	def decorator(func):
		def wrapper(*args, **kwargs):
			return func(*args, **kwargs)
		return wrapper
	return decorator	

@decorator_func(arg1, arg2, ...)
def func(argA, argB, ...):
	pass

func(argA, argB, ...)		
{% endhighlight %}
is equivalent to:
{% highlight python %}
decorator_func(arg1,arg2, ...)(func)(argA, argB, ...)
{% endhighlight %}
in order to add parameters `arg1,arg2, ...` to the `decorator_func`, we define the `decorator` function which wraps the original function `func` with additional behavior, and return this `decorator`. This technique allows for greater flexibility in creating decorators with varying behaviors based on arguments passed to the `decorator_func`. 

---

## Common use cases and practical information
Python decorators find application in various scenarios such as logging, caching, and authentication. They are also useful for enforcing access control and permission checks, validating function arguments, and implementing memoization to enhance caching efficiency. 

However, it's important to note that using several decorators may affect code readability, as determining their order without examining their inner workings can be challenging. Additionally, decorators can sometimes modify the function signature, potentially leading to bad practices when invoking the function.

In the following sections, we delve into two sets of popular decorators and their applications within Python.

### Python descriptors
Decorators such as @property, @staticmethod, and @classmethod are powerful tools for enhancing the functionality and clarity of class definitions.

#### @property
The @property decorator is used to create computed attributes and implement controlled access to class attributes. Essentially, it allows you to define methods that can be accessed like regular attributes, providing a cleaner interface for attribute manipulation. 
#### @staticmethod
The @staticmethod decorator defines a method that is associated with a class rather than with instances of the class. Unlike regular methods, static methods don't have access to instance-specific data (accessed via `self`). They are typically used for utility functions that are related to the class but don't depend on specific instance data.
#### @classmethod
The @classmethod decorator is used to define methods that operate on the class. When you define a class method, the first parameter is typically named `cls`, which refers to the class itself. Unlike static methods, class methods have access to the class and can modify class-level variables.

[Here](https://pandas.pydata.org/docs/development/extending.html#registering-custom-accessors) is an example of `@property` and `@staticmethod` when registering custom accessors with Pandas.

### Numba decorators
Numba is a Just-In-Time (JIT) compiler for Python that translates Python functions to optimized machine code at runtime. It's primarily used for numerical computing and scientific computing tasks where performance is critical. 

#### @jit and @njit
Numba's main feature is `@jit`, which stands for just-in-time compilation, making computations faster. It has two modes: "object mode" and "no-Python mode." Setting `forceobj=True` puts you in object mode, while `nopython=True` boosts performance by avoiding Python C API. To make things simpler, Numba offers `@njit` as a shortcut for `@jit(nopython=True)`, making optimization easier.

#### @vectorize and @guvectorize
While `@jit` is great for optimizing array-based computations, Numba offers a higher-level abstraction through universal functions, `@vectorize` decorator. Instead of dealing with whole arrays at once, you write functions that work on individual elements. Numba then does the heavy lifting, making sure your functions run fast by efficiently looping over the arrays. Plus, `@vectorize` gives you access to advanced features like reduction, accumulation, and broadcasting. For more flexibility, there's `@guvectorize`, which allows you create functions that can handle arbitrary number of elements of input arrays, and take and return arrays of differing dimensions. 

Here is an example of harmonic regression with `@guvectorize`, comparing the second harmonic's amplitude to that of the first harmonic.
{% highlight python %}
@guvectorize(
    "(float64[:], int64, boolean, float64[:])",
    "(n), (), () -> ()",
    nopython=True,
)
def amp_reg_1d(y, period, res):
    """
    1D implementation of amplitude ratio.
    """
    # Initialise the default value and dimension of res
    res[0] = np.nan
   
    # Create the input array X 
    t = np.arange(1, n + 1)
    X = np.column_stack(
        (
            np.ones_like(y),
            np.cos(2 * np.pi / period * t),
            np.sin(2 * np.pi / period * t),
            np.cos(4 * np.pi / period * t),
            np.sin(4 * np.pi / period * t),
        )
    )

    # Compute the coefficients
    coefficients = np.square(np.linalg.lstsq(X, y)[0])

    # Place the ratio at the pre-registered location, res[0]
    res[0] = (np.sqrt(coefficients[3] + coefficients[4]) + 1e-20) / (
        np.sqrt(coefficients[1] + coefficients[2]) + 1e-20
    )
{% endhighlight %}

#### Tips and recommendations
- focus on small piece of performance-critical code
- use nopython mode instead of object mode
- use `Parallel=True` when the code logic is parallelisable 

---

## Reference
https://peps.python.org/pep-0318/
https://docs.python.org/3.13/howto/descriptor.html#properties
https://pandas.pydata.org/docs/development/extending.html
https://pandas.pydata.org/docs/user_guide/enhancingperf.html
https://numba.readthedocs.io/en/stable/index.html

