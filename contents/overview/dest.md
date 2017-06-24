# Destinations

There are a few different ways to use the `.dest()` function
in hopp to define the output of the task chain.

 1. `.dest(directory)`: by default, hopp assumes that the
 destination provided is a directory that all source files must
 end up in after compilation.
 2. `.dest(file)`: **if you use any bundling plugins** in your task
 chain, hopp will assume that the path given as the destination
 is not a directory but rather **is a file**.
 3. `.dest()`: if no output destination is provided, hopp switches
 to in-place mode and the output will completely replace the original
 source files.