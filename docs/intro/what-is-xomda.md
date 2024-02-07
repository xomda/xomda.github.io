---
outline: deep
---

# What is XOMDA?

XOMDA stands for E**x**tensible **O**bject **M**odel **D**ata **A**bstraction.
It's a way of defining your data models, and generate code out of them.

It allows to define a centralised object model, out of which code can be generated. This can go from beans, to
database definitions, documentation, dialogs, ...

It's just all in your own hands.

## Why?

During the lifecycle of application development, your models change.
Attributes are added, removed or renamed, new entities are added and so on.

While these changes are only minimal within the model itself, they can become pretty extensive
when it comes to adapting all code accordingly.
By generating this code automatically, changes become predictable and will become effective throughout your codebase.

## How?

The model is defined in a simple format, which is then parsed into an object model. This object model is then presented to the template engine, which generates the code and assets that you configured it to do so.

The parsing and generation is integrated automagically within your build system.
