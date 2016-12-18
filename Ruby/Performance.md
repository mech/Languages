# Ruby Performance

* [Rails Speed](https://www.railsspeed.com/)
* [Symbol is the bad part of Ruby](https://www.amberbit.com/blog/2014/9/9/ruby-the-bad-parts/)

```
derailed bundle:mem
```

Use copy-on-write. Use Puma, Unicorn or Passenger with preloading.

https://github.com/puma/puma/issues/342

## Use minitest/hell

To discover thread-safe bugs.

## Videos

* [Halve Your Memory Usage With These 12 Weird Tricks](https://www.youtube.com/watch?v=kZcqyuPeDao)