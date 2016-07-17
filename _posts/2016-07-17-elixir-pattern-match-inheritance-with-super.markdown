---
published: true
title: elixir pattern match inheritance with super
layout: post
---
How to inherit function from parent module, and override some specific cases?

```elixir
defmodule Parent do
  defmacro __using__(_) do
    quote do
      import unquote(__MODULE__)

      def action(param), do:
        inner_handler(param)

      defp inner_handler(:error), do:
        IO.inspect "some error passed"

      defp inner_handler(param), do:
        IO.inspect "some param passed"

      defoverridable [inner_handler: 1]
    end
  end
end

defmodule Child do
  use Parent

  defp inner_handler(:ok), do:
    IO.inspect "ok passed"

  # This is where magic happens
  defp inner_handler(param), do:
    super(param)
end
```

Note that pattern match for **:error** and **"another"** parameter are defined **in Parent** module and only **:ok** is pattern matched **in Child** module


```elixir
Child.action(:ok) # outputs "ok passed"
Child.action(:error) # "some error passed"
Child.action("another") # "some param passed"
```

Thanks to [Qqwy](https://elixirforum.com/t/using-base-module-function-as-fallback/1099/2)