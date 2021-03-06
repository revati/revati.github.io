---
published: true
title: elixir struct constructor within the same module
layout: post
categories: [elixir]
---
Trying to create something like constructor, but using struct within the same model does not work :(

```elixir
defmodule App.News.Event.NewsItemAdded do
  defstruct id: nil, title: nil, contents: nil, featuredImageId: nil, gallery: nil

  alias App.News.Command.AddNewsItem

  def make(id, command = %AddNewsItem{}), do:
    %NewsItemAdded{
      id: id,
      title: command.title,
      contents: command.contents,
      featuredImageId: command.featuredImageId,
      gallery: command.gallery}
end
```
Code will produce compile error:

`(CompileError) web/domain/news/events/news_item_added.ex:7: NewsItemAdded.__struct__/1 is undefined, cannot expand struct NewsItemAdded`

But [ExConstructor](https://github.com/appcues/exconstructor) somehow managed to make it work. A little bit of digging into source code and i found `__MODULE__`. So i changed make function to fallowing and now it works :)

```elixir
  def make(id, command = %AddNewsItem{}), do:
    %__MODULE__{
      id: id,
      title: command.title,
      contents: command.contents,
      featuredImageId: command.featuredImageId,
      gallery: command.gallery}
```
