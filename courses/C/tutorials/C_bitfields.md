# Bit Fields
``bit fields`` are another C concept in which we can optimize our memory usage, just like ``union``s.

What's a ``bit field``? A ``bit field`` is a **limit** on the size of a member within a ``struct`` or ``union``.

Suppose we're creating a game. Let's say it's a Pokemon game! We want to define a Pokemon like so:
```c
struct Pokemon {
    char* name;
    unsigned int id;
    unsigned int level;
    // etc...
}
```
This is a good structure so far. But there's an issue. The issue is that we **know** our ``level`` data will **never** be above 100. But, an ``int`` takes up **4 bytes**, which can hold data up to the **billions**.

So the issue is we have bits that are not necessary in representing the Pokemon's level. So what we can do is tell C to "shave" the bits that we will never need. And we do this using ``bit fields``:
```c
struct Pokemon {
    char* name;
    unsigned int id;
    unsigned int level: 7;
    // etc...
}
```
If we know how ``bit``s work, we know that we can represent ``128`` values using only ``7`` bits. So we've limited our ``level`` data to only use 7 bits, as opposed to the whopping ``32`` that the ``int`` uses.

Now, we didn't have to use an ``int`` here. We could have just used an ``unsigned char`` here, which is essentially a ``byte``:
```c
struct Pokemon {
    char* name;
    unsigned int id;
    unsigned char level: 7;
    // etc...
}
```
But even though it's now an ``unsigned char``, you'd still have ``1`` bit leftover that isn't being used at all (we don't need Pokemon with levels up to 256!). Therefore, we should still use only the first 7 bits.

## The Catch
Because we are working intimately with bits, there's a small catch. The catch is that we can not create and manipulate ``pointer``s to bit field members of ``struct``s or ``union``s.

The reason is because ``pointer``s work on a byte-by-byte basis. Therefore, using a ``pointer`` on bit field members may make our ``bit field`` limitation pointless.

In other words, a ``pointer`` to a ``unsigned char`` member with ``7`` bits would point to all ``8`` bits, therefore making our ``bit field`` redundant. Additionally, it would also be dangerous to do, since that 8th bit may be used for something else. So C saves us from making this mistake by simply preventing it from happening in the first place.

### What about ``: 0;``?
This is an interesting behavior of ``bit field``s to consider. When you do ``: 0;`` on a member of a ``struct`` specifically (not a ``union``), you can force the ``struct`` to undergo **struct alignment**. This concept is somewhat advanced, so it'll be covered in a later tutorial.

For now, just know that doing ``: 0;`` to a member of a ``struct`` **DOES** have a purpose. Just don't worry about that purpose quite yet!

[![Discord](https://img.shields.io/discord/609993365832073217?color=7289da&label=discord)](https://discord.gg/Sw3npy4)

[Home](https://bvanseg.github.io)