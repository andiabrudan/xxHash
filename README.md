# xxHash
A constexpr implementation of xxHash written in C++

> If you thought the C version was fast, you ain't seen nothing yet

## What is this?
This is a header-only constexpr implementation of the popular hashing algorithm `xxHash`.  
You can find the original implementation in C at [Cyan4973 / xxHash](https://github.com/Cyan4973/xxHash)

### Is the code here compatible with the original xxHash?
Yes. I tested against the hashes produced by the original code and I'll try to stick to that standard.  

## Why does this exist?
I adapted the original C code to a modern C++ standard to take advantage of C++17's `constexpr` functions.  
The main reason for doing so was to be able to `switch-case` on strings, without the overhead of computing the hashes for constants every single time (or store computed hashes somewhere).

## How to use it
```C++
int function(const char* str)
{
    using namespace xxh;
    const size_t str_size = strlen(str); // null character not included
    const uint64_t str_hash = xxHash64(str, str_size);

    switch (str_hash)
    {
        case "a"_h:
            return 1;
        case "abcdefgh very long string"_h:
            return 2;
    }
}
```

## Limitations
 - At the moment, the header only implements the 64 bit version of xxHash.  
 - Furthermore, the function can hash a string of up to 128 bytes.  
 (I thought that would be enough for my use case)  
 - Lastly, no support for seeds or custom secrets.

## Contribute
If you want to submit a PR, I'd be happy to review it.

## License
Feel free to do whatever you want with this code.  
I don't know how licensing works, and I don't want to find out.
