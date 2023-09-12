
- `size_t` is an unsigned integer type capable of storing values in the range [0, SIZE_MAX].
- `ssize_t` is used for a count of bytes or an error indication. It is a signed integer type capable of storing values al least in the range [-1, SSIZE_MAX].
- `off_t` is used for describing file sizes. It is a signed integer type.
- `off64_t` is a 64-bit version of the type, used in glibc.
- `loff_t` is a 64-bit version of the type, introduced by the Linux kernel.