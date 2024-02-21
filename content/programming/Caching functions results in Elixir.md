---
date: 2024-02-20
tags:
  - "#Elixir"
---
A few weeks ago I started a course [at Polytech](https://www.polytech.umontpellier.fr/formation/cycle-ingenieur/devops/en-quelques-mots-do) about [[Dynamic Programming]], one of the main points of dynamic programming is the use of memoisation (as known as. caching, proxies and so-on).

We had to apply this method in our favorite programming language on the Fibonacci suite, ideally with decorators, and turns out that elixir is the language I just got in love with recently.

## Why would you cache function calls ? 

As mentioned in the [[Dynamic Programming]] page caching redundant function calls will allow us to spare computational power and save us many amounts of time and memory. 

[The Fibonacci suite](https://en.wikipedia.org/wiki/Fibonacci_sequence) is the prime example of this, let's take at the usual implementation of it: 

```elixir
def fibonacci(n) do 
  case n do 
    _ when n < 2 -> n
    _ -> fibonacci(n - 1) + fibonacci(n - 2)
end
```

When you decompose the calls of this function, here is the calling tree you get: 

![[fib.png|center]]

Don't you see something shocking ? Besides the number of calls that have been made for such a small input, the quantity of redundant function calls you do is insanely high.

By caching the results of ``fibonacci(n)`` we would cut down the calling tree like this: 

![[fib_cached.png|center]]

And as you can imagine, you greatly reduce the resourced used by the function.

> [!NOTE]
> What we effectively have here is a recursive function that itself two times for each input $n$, giving it effectively a exponential complexity of $\mathcal{O}(2^n)$ 
> Now with caching we simplified our tree by trimming one of the two recursive calls bringing down it's complexity to $\mathcal{O}(n)$

## Writing the actual caching decorator

We will write our caching mechanism with a [decorator](https://refactoring.guru/design-patterns/decorator) as it will allow a function to be cached without it's body being changed.

Our decorator will be placed on top of functions, with a cache name and default cache, being a map having a list of arguments as keys and the expected return value as it's value.

```elixir
#                         v fibonacci(0) = 0 & fibonacci(1) = 1
@decorate mem(:fibonacci, %{[0] => 0, [1] => 1})
def fibonacci(n) do
  fibonacci(n - 1) + fibonacci(n - 2)
end
```

### The decorator

Unfortunately in elixir there is no easy and native solution to do decorators unlike typescript, however there is a library named [decorators](https://hex.pm/packages/decorator) that provides macros to do so. 

Add it to your project dependencies in the ``mix.exs`` file:

```elixir
defp deps do
  [
  # ...
    {:decorator, "~> 1.4"}
  ]
end
```

Now create the decorator's module: 

```elixir
defmodule ProgDyn.Mem do
  use Decorator.Define, [mem: 2] 

  alias Agent

  @spec mem(atom() | {:global, any()} | {:via, atom(), any()}, map(), any(), any()) :: any()
  def mem(table_name, init_values, body, context) do
    quote do 
    end
  end
end
```

On line two we use the macro from the `decorator` library, to define the decorator `mem/2`, now create a function having the same name and the same arity `+2`, the first extra is the decorated function, and the second one is a context about said function (`name`, `arity`, `module`, `kind` and `args` ).

> [!QUESTION]- What are Agents? 
> Elixir agents are one of the few ways to maintain a mutable state between Erlang process or within a single at different points in time. In our case we will use these to keep track of the cache between our function calls.

First, we check if the agent exists, if not we create it, providing it with the default cache:

```elixir
@spec mem(atom() | {:global, any()} | {:via, atom(), any()}, map(), any(), any()) :: any()
def mem(table_name, init_values, body, context) do
  quote do 
    id = case Agent.start_link(fn -> Map.new(unquote(init_values)) end, [name: unquote(table_name)]) do
      {:ok, pid} -> pid
      {:error, {:already_started, pid}} -> pid
    end
  end
end
```

Then we proceed to implement both our cache hitting and updating 

```elixir
@spec mem(atom() | {:global, any()} | {:via, atom(), any()}, map(), any(), any()) :: any()
def mem(table_name, init_values, body, context) do
  quote do 
    id = case Agent.start_link(fn -> Map.new(unquote(init_values)) end, [name: unquote(table_name)]) do
      {:ok, pid} -> pid
      {:error, {:already_started, pid}} -> pid
    end
    
     case Agent.get(id, fn state -> Map.get(state, unquote(context.args)) end) do
        nil ->
          result = unquote(body)
          Agent.update(id, fn state -> Map.put(state, unquote(context.args), result) end)
          result

        result ->result
      end
  end
end
```

### See it in action! 

Now what we have a handsome decorator, now is about time to use it! 
For doing so let's so call it's module `use` clause in our main file: 

```elixir
defmodule ProgDyn.Main do
  use ProgDyn.Mem
  use PrintDecorator

  use Application

  @decorate mem(:fibonacci, %{})
  def fibonacci(num) do
    case num do
      _ when num < 2 -> num
      _ -> fibonacci(num - 1) + fibonacci(num - 2)
    end
  end

  def start(_type, _args) do
    IO.puts fibonacci(150)
    {:ok, self()}
  end
end
```

Now we can use the decorator by using `@decorate <our decorator function>` before defining the function. 

You can now feel free to use `mix run` to the program with and without the decorator to see the difference by yourself 😉. You can find the source [code right here](https://github.com/WoodenMaiden/elixir_cache_decorator).