# JavaScript Event Loop

## Call Stack

- The call stack is responsible for keeping track of all the operations in line to be executed. Whenever a function is finished, it is popped from the stack.

## Event Queue

- JavaScript can do only one thing at a time.
- The rest are queued to the event queue waiting to be executed.
- The task will be pushed to the stack where thay can be executed.
- The event queue is responsible for sending new functions to the stack for processing. It follows the queue data structure to maintain the correct sequence in which all operations should be sent for execution.

## Asynchronous Callback

- Sometines the JavaScript code can take a lot of time and it can block the page re render.
- JavaScript has asynchronous callbacks for non blocking behavior.

## Event Loop

- JavaScript has a runtime model based on an event loop, which is responsible for executing the code, collecting an dprocessing events, and executing queued sub-tasks.
- The event loop pushes the tasks from the task queue to the call stack.

## Features of Event Loop:

- Event loop is an endless loop, which waits for tasks, executes them and then sleeps until it receives more tasks.
- The event loop executes tasks from the event queue only when the call stack is empty i.e. there is no ongoing task.
- The event loop allows us to use callbacks and promises.
- The event loop executes the tasks starting from the oldest first.
