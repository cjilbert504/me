---
title: "Strictly Business"
permalink: /strictly-business
---

One thing that kept coming up when I was first digging into a lot of resources about learning ruby on rails was the idea of business logic.

Now from reading older resources about rails it seems as though at some point in time a lot of business logic was placed within controller files and then a shift happened. The new shift was to have all of the business logic moved out of the controller layer and into the model layer. This, as of current times, still seems to be the normal approach of structuring rails applications.

So what is considered "business logic"? Let's walk through a very basic example and try to build our understanding by doing.

The starting point is a simple movie statistics application, where movies are a model in the application and have the attributes of title, description, total gross and rating.

On the show page for an individual movie, what we would like to do is that if the movie grossed over a certain amount we would like to show the total gross attribute. If it didn't make over a certain amount then we want to have the page state that the movie was a flop. 

Since we are trying to have this happen in a view and since we also want to try to limit how much ruby code we embed in the view templates, a helper method sounds like a great starting point.

```ruby
module MoviesHelper
  def format_total_gross(movie)
    if movie.total_gross < 100000000
      content_tag(:strong, "Flop!")
    else
      number_to_currency(movie.total_gross)
    end
  end
end
```

Here we have a helper that conditionally renders content based on a comparison of a movies total gross and the number 100,000,000. And within that comparison lies the piece of business logic. Should a view helper be responsible for comparing a movies total gross to the target amount of 100,000,000? 

It is probably more in line with convention that we make a method at the model layer that does this comparison for us and then this helper can simply decide what content to render based up the result of calling the method we write in the model layer for movies.

Let's start with what we wish we could have:

```ruby
module MoviesHelper
  def format_total_gross(movie)
    if movie.flop?
      content_tag(:strong, "Flop!")
    else
      number_to_currency(movie.total_gross)
    end
  end
end
```

If we were to try to run this code now in the application we would get an error about an undefined method for "flop?". So let's go to the movie model and define that method:

```ruby
class Movie < ApplicationRecord
  def flop?
    total_gross < 100000000
  end
end
```

Now we have the method defined and our responsibilities aligned by having this piece of code that does some action with the data from the database at the appropriate layer, the layer which is responsible for interacting with the database, the model.

Most businesses that provide software solutions rely on the data in their database tables as the valuable asset of the company or business. The code that we just wrote is a bit of logic (the comparison) that operates on the data that the business values, which is what is known as "business logic".

Happy Rubying!