---
Title: '.Thread()'
Description: 'Creates a new thread that runs a target function with optional arguments.'
Subjects:
  - 'Computer Science'
  - 'Data Science'
Tags:
  - 'Async Await'
  - 'Functions'
  - 'Thread'
CatalogContent:
  - 'learn-python-3'
  - 'paths/computer-science'
---

The **`.Thread()`** constructor from Python's [**threading**](https://www.codecademy.com/resources/docs/python/threading) module creates a thread object that can run a specified function with optional arguments.

## Syntax

```pseudo
threading.Thread(target=callable, args=())
```

[Functions](https://www.codecademy.com/resources/docs/python/functions) are commonly passed as the `target` argument, but without parentheses. If any items are listed in the `args` tuple, they are passed as positional arguments to the `target`.

## Example: Basic Thread Creation

The object that returns from the `.Thread()` constructor can be assigned to its own variable, as shown in the example below:

```py
import threading

thread_1 = threading.Thread()
thread_2 = threading.Thread()

print(thread_1)
print(thread_2)
```

Every thread object has a `name` attribute that, unless otherwise specified, defaults to `Thread-x`:

```shell
<Thread(Thread-1, initial)>
<Thread(Thread-2, initial)>
```

## Codebyte Example 1: Simple Greeting Thread

In the example below, a thread, `hello_thread`, targets the `say_hello()` function with supplied arguments. After the thread is created, the targeted `say_hello()` function is executed when the [`.start()`](https://www.codecademy.com/resources/docs/python/threading/start) method is run:

```codebyte/python
import threading

def say_hello(subject):
  print(f'Hello, {subject}!')
  # Output: Hello, World!

hello_thread = threading.Thread(target=say_hello, args=("World",))

hello_thread.start()
```

## Codebyte Example 2: Concurrent File Downloads

In the example below, two threads, `thread_1` and `thread_2`, target the `download_file()` function with supplied arguments. Each thread simulates downloading a file concurrently by running the `download_file()` function in the background. After the threads are created, the targeted `download_file()` functions are executed when the `.start()` method is run:

```codebyte/python
import threading
import time

def download_file(filename, duration):
  print(f"Starting download: {filename}")
  time.sleep(duration)
  print(f"Finished downloading: {filename}")

# Creating two threads to simulate downloading two files simultaneously
thread_1 = threading.Thread(target=download_file, args=("file1.txt", 2))
thread_2 = threading.Thread(target=download_file, args=("file2.txt", 4))

# Starting the threads, both downloads begin concurrently
thread_1.start()
thread_2.start()

# Ensuring the main program waits for both threads to finish
thread_1.join()
thread_2.join()

print("Both downloads completed!")
```

## Codebyte Example 3: Parallel Task Execution

In the example below, two threads, `coffee_thread` and `toast_thread`, target the `make_coffee()` and `toast_bread()` functions, respectively. Each thread simulates the preparation of coffee and toast concurrently. After the threads are created, the targeted functions are executed when the [`.start()`](https://www.codecademy.com/resources/docs/python/threading/start) method is run:

```codebyte/python
import threading
import time

def make_coffee():
  print("Making coffee...")
  time.sleep(3)  # Simulating the time taken to make coffee
  print("Coffee is ready!")

def toast_bread():
  print("Toasting bread...")
  time.sleep(2)  # Simulating the time taken to toast bread
  print("Bread is toasted!")

# Creating threads for making coffee and toasting bread
coffee_thread = threading.Thread(target=make_coffee)
toast_thread = threading.Thread(target=toast_bread)

# Starting both threads to make coffee and toast bread concurrently
coffee_thread.start()
toast_thread.start()

# Ensuring the main program waits for both threads to finish
coffee_thread.join()
toast_thread.join()

print("Breakfast is ready!")
```

## Frequently Asked Questions

### 1. How to sleep a thread in Python?

To sleep a thread in Python, use the [`time.sleep()`](https://www.codecademy.com/resources/docs/python/time-module/sleep) function. Import the [`time`](https://www.codecademy.com/resources/docs/python/time-module) module and call `time.sleep(seconds)` where `seconds` is the number of seconds to pause the thread. This is useful for adding delays, simulating wait times, or creating periodic tasks in Python's threading.

### 2. Is Pandas single-threaded?

[Pandas](https://www.codecademy.com/resources/docs/pandas) is primarily single-threaded by default. However, some functions (like [`read_csv()`](https://www.codecademy.com/resources/docs/pandas/built-in-functions/read-csv) with `engine='pyarrow'`) can use multi-threading or multi-processing for performance.

### 3. Is Node.js single-threaded?

[Node.js](https://www.codecademy.com/resources/blog/what-is-nodejs/) operates on a single-threaded event loop model but handles concurrent operations through asynchronous callbacks. For true parallelism in Node.js, you can use the Worker Threads API or the cluster module.
