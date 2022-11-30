---
title: Callbacks And Closure
published: true
---

Callbacks, closure and other things I wish to get out of life... but I digress. In programming, a callback is a function that gets passed into another function. In Java, this would look like;

```java
public class A {

    public void B (DoSomethingCallback callback) {
        // Does something ....
        // Something is done
        // Calls callback
        callback.onSomethingDone(...)
        // Maybe does something else ...
    }

    interface DoSomethingCallback {
        // Callback method
        void onSomethingDone();
    }
}
```

While I am not new to the concept, I have recently been working with it a lot in Java async code and it's a fascinating paradigm.

In the best case, the callback is simple and straightforward like the snippet above shows. However, in some cases, it can get pretty complicated to understand what exactly is going on aka [Callback Hell](https://www.geeksforgeeks.org/what-is-callback-hell-in-node-js/#:~:text=This%20is%20a%20big%20issue,result%20of%20the%20previous%20callbacks.).

A closure on the other hand is a function defined inside of another function. In python this would look like;

```python
def foo_operator(x, y):
    # Outer function
    def add():
        # Nested inner function (closure)
        print(x)
        print(y)
    # return inner function (closure)   
    return add 
```

This is a very common paradigm in python and is used a lot by python [decorators](https://www.programiz.com/python-programming/decorator). 

With closures, the inner function, can have access to the outer functions variables  (In the above example it's possible to access x & y from the add() method). This is a distinction from the callback paradigm since callbacks are unable to access variables without being passed. 

I think it's useful being familiar with these two paradigms as it makes code much easier to read and understand, since they occur quite frequently. 
