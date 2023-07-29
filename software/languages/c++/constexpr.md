# constexpr

# Special and Edge Cases
## Floating Point
A constexpr floating point value may result in a non-equivalent value compared to a floating point created during runtime.

The compiler, and thus the standard, cannot reliably determine how the target hardware and/or the operating system (and in general, the platform) handle floating point arithmetic and operation. Thus, the floating point value derived by the compiler during compile time may be non-equivalent to the same floating point value derived at runtime.
