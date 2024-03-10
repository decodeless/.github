# decodeless

`decodeless` (previously no-decode) is a collection of utility libraries for
conveniently reading and writing large binary files via memory mapping. The data
could be whatever you want, but there are performance benefits to writing raw
C++ structures that can be read without any decoding/deserialization/parsing -
hence the name "decodeless".

- [`offset_ptr`](https://github.com/decodeless/offset_ptr) provides convenient
  relational pointers that are implicitly valid within the file's address space
- [`writer`](https://github.com/decodeless/writer) combines:
  - [`allocator`](https://github.com/decodeless/allocator) handles packing and
    aligning data when writing files and interfaces with...
  - [`mappedfile`](https://github.com/decodeless/mappedfile), a small cross
    platform memory mapping library that can also grow files so you don't need
    to compute the total size up front

  This is particularly convenient for writing files because you can populate
  relational structures after allocating them and the data they point to.

- [`header`](https://github.com/decodeless/header) is a completely optional
  extensible file header (using `offset_ptr`) that also includes a unique ID,
  versioning and binary compatibility features

Component repositories can be used individually or combined. They do not include
each other as git submodules.

Typical usage is combining [`writer`](https://github.com/decodeless/writer) and
[`header`](https://github.com/decodeless/header) to quickly write structured
binary data to disk. Then using
[`mappedfile`](https://github.com/decodeless/mappedfile) to read them.
