# Software Paradigms
The three common software paradigms and their benefits/disadvantages

# Paragigms
1. [Object Oriented](#object-oriented)
1. [Functional](#functional)
1. [Procedural](#procedural)

## Object Oriented
Object oriented is a paradigm style where components are their own object, and each object contains methods that modify its internal state.

## Functional
Functional 

### Pure Functions
Pure functions are akin to mathematical functions where the output of a function are consistent to the inputs, and that multiple calls to the function does not change the function's actions.

A pure function must satisfy the following:
- There must be no observable side effects - the function must not modify an observable global state
- A set of inputs will always produce the same consistent output(s). Future or previous calls to the function will not alter the result of the output(s). 
- Two or more threads can simultaneously call the function at any point of the function's lifetime without any race condition, alter the result, or result in any issue or undefined behavior. If a call to this function occurs while another thread is simultaneously in the middle of this function, the behavior of the function will be so that to the perspective of each thread, the function should behave as if there are no other threads other than itself is running in the system.

#### Example
``` C++
double hypotenus(double a, double b) {

    static std::atomic<int> counter = 0;    # this is still a pure function, because counter does not affect the return value or modify a global state

    ++counter;

    return std::sqrt(a * a, b * b);
}
```

## Procedural
A paradigm where the program changes state by performing a set of procedures. A procedure can be a function that changes a global state in the system. In this paradigm, a series of "linear" like steps is performed.

#### Example
``` C++

using wait_f = bool (*)();

void wait_for(time_s wait, wait_f condition)
{
    while (!condition()) {
        sleep(wait);
    }
}

int main()
{
    collect_ingredients();

    if (!have_all_ingredients()) {
        return 1;
    }

    static constexpr bool preHeat = true;
    set_oven_temperature(375.0, preHeat);

    mix_all_ingredients();
    put_ingredients_into_cake_pan();

    wait_for(30, []() -> bool {
        return oven_ready();
    });

    put_cake_pan_into_oven();

    wait_for(60, ()[] -> bool {
        cake_is_done();
    });

    take_cake_pan_out_from_oven();
    
    return 0;
}
```
