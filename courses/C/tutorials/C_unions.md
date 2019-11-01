# Unions
Back in the old days, memory was a precious resource for a programmer. For computers that had so little memory (we're talking Kilobytes of RAM), it was vital to make every bit count.

The above being said, ``struct``s were a very big memory hog to C developers in those days. Consider the following ``struct``:
```c
struct SomeStruct {
    int integer;
    char letter;
    float decimal;
};
```
When we do ``sizeof(struct SomeStruct)``, we are going to get back a size of ``9`` (int + char + float, aka 4 + 1 + 4 bytes).

A single one of these ``struct``s on its own is only 9 bytes. That's nothing!

But consider if we had millions of these things. That's then a considerable amount of memory. So how can we save space? By using a ``union`` instead of a ``struct``:
```c
union SomeUnion {
    int integer;
    char letter;
    float decimal;
};
```
It's about the same way you would make a ``struct``, except it's called a ``union`` instead of a ``struct``. So what gives? How does changing the type make this more efficient memory-wise?

Well, recall that the ``struct`` mentioned earlier was a size of 9 bytes. A ``union`` of that same data, on the other hand, is **only as big as the largest member within it**. In this case, both ``int`` and ``float`` are the biggest members, so, the overall ``union`` size is 4 bytes.

How is it possible to cram those 3 members into only 4 bytes? The short story is **it isn't**. Data is data, and if those 3 members *could* be defined using only 4 bytes, then they would be a lot smaller individually than they already are.

So what's actually going on is all 3 of those members (``integer``, ``letter``, and ``decimal``) are using the same **starting address** in memory. In other words, they are sharing the same 4 bytes, in the case of ``SomeUnion``.

**"But wait a minute! If they're using the same bytes, wouldn't changing ``integer``'s value ALSO change ``decimal``'s value?!"**
- You are 100% correct. Because they all share the same bytes, changing ``integer`` will cause ``decimal`` and ``letter`` to also change.

**"That's bogus, though. Why would anyone use a ``union`` like ``SomeUnion``? Wouldn't it be better to just use an ``int`` or ``float`` instead?"**
- Well, no. What's useful about a ``union`` is that we can interpret those 4 bytes in however many ways as we have members inside of the ``union``. So not only is a ``union`` good at conserving data, but it's also good at interpreting the same bytes into different types.

The use-cases for ``union``s can be extremely rare, **but**, they do exist. Whenever you're working with register data, working with switching between Linux/Unix systems, switching between raw bytes and a readable structure, etc., *then* a ``union`` can be useful.

As we go further into the course and eventually reach ``file`` handling, we'll see that we can actually use a ``union`` to write raw data (``unsigned char*``) to a file, and then when we read it, we can interpret it as a ``struct``:
```c
/* Since this is a union, raw_data[16] has the same memory address (and therefore bytes) as the struct below it. */
union PersonEntry {
  unsigned char raw_data[16]; // We write this to a file.
  struct // We work with this when reading the individual data segments.
  {
    char name[12];
    short age;
    short height;
  }
}
```

So not only are ``union``s useful for saving data, but, they're also useful for interpreting the same data in different ways.

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)