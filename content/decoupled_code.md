+++
title = 'Decoupling Code'
date = 2024-04-12T11:52:57-07:00
draft = false
weight = 5
+++

### Separate concerns

Components should be compartmentalized as much as possible:

- A function should do only one thing and should be as small as possible. If a function is more than a full screen (40 lines by 80 columns), it should be separated further in some fashion. 
- A module should include functions that all work towards a single product.
- A class should modify its own members rather than other objects.

### Side effects

Deterministic, stateless functions are best as they are simple and robust.

1. Inputs come from arguments.
2. Outputs are returned with the `return` statement.

When you deviate from these structures, you end up with side effects which are anything that happens behind the scenes outside of the pure data flow function such as:

- **Modifying a global or static local variable**
- **Modifying an argument**: If the input variable is then modified at the end of the function. The state of the argument will be dependent on how many times the function is called. A better method is to create a new variable for the output.
- **Any kind of IO** including:
    - Printing to the console.
    - Drawing on screen.
    - Calling a remote server.

Use classes to encapsulate state in that only the class has access to specific variables. The convention is to add an underscore prefix to private variables that shouldn't be modified from the outside. The example `self._x` refers to a class member that should be managed by the class itself.
