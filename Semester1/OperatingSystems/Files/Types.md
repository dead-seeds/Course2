
- `size_t` is an `unsigned integer` type capable of storing values in the range [0, SIZE_MAX]. `size_t` can store the maximum size of a theoretically possible object of any type (including array). **SIZE_MAX = 18 446 744 073 709 551 615 (64 bits)**.

But if we check [[ISO_C.pdf]] (2018 year), which says in section 6.5.3.4 (page 65 in PDF):
> The value of the result of both operators is implementation-defined, and its type (an `unsigned integer` type) is `size_t`, defined in `<stddef.h>` (and other headers).

So, the size of `size_t` is not specified, only that it has to be an `unsigned integer` type. However, an interesting specification can be found in chapter 7.20.3 of the standard (page 216 in PDF):
> — limit of size_t 
> SIZE_MAX 65535

Size of `size_t` doesn't matter, **the allowed value range is from 0-65535**, the rest is implementation dependent.


- `ssize_t` is used for a count of bytes or an error indication. It is a `signed integer` type capable of storing values at least in the range [-1, SSIZE_MAX]. **SSIZE_MAX = 2147483647 (same as INT_MAX)**
- `off_t` is used for describing file sizes. It is a `signed integer` type.
- `off64_t` is a 64-bit version of the type, used in `glibc`.
- `loff_t` is a 64-bit version of the type, introduced by the Linux [[Kernel]].