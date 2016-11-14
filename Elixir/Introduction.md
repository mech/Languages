# Elixir

* [Thoughtbot love Elixir](https://robots.thoughtbot.com/tags/elixir)

---

* Actor Model - Erlang, Scala's Akka
* CSP - Golang's goroutines channel

## Asynchronous

When you think asynchronous, the general Rails pattern is to think message queue and a worker in a Sidekiq/DelayedJob. This is totally unnecessary in Elixir which is designed for concurrency. Typically you can just wrap a function in a `Task.async` to create your own OTP application.

## Umbrella Project

## Companies moving to Elixir from Ruby

* [Amberbit](https://www.amberbit.com/blog)
* [Thoughtbot](https://robots.thoughtbot.com)