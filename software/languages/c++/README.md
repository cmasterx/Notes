# C++
C++ notes collected over time

# Object Lifetime
[Stack Overflow Link](https://stackoverflow.com/questions/6403055/object-destruction-in-c)

**Note to self**: Actually read the link above and bring the notes down here

# Object Initialization
## Static Initialization Order Fiasco
If multiple static global objects exists across multiple translation units, no guarantees exists to determine the order of initialization of static global objects.

This is problematic in scenarios when a static global object depends on a static global object from a different translation unit. Per language spec, the langauge has no means of enforcing initialization order of static global objects. Thus, static global objects depending on another static global object from a different translation unit is **undefined behaviour**.
