# Rendering Collections

## Objectives

1. Use the `collection` keyword with partials
2. Pass a collection to the render method
3. Handle empty collections

## Overview

Up until now our only way to render collections was somewhat manually. We could
iterate over an array and render the partial for each object in the array. Let's
see how Rails can abstract this into a nicer syntax.

## Lesson

Make sure you run `bin/rails db:migrate` and `bin/rails db:seed` before testing the app in your browser. This lesson focuses on using the `collection` keyword with partials. The connection between authors and posts is hard-coded. In the posts controller create action, the newly created post is linked with the first author in the database.

Currently, the `posts#index` view manually renders the partial in a loop:

```erb
<% @posts.each do |post| %>
  <%= render partial: "post", locals: { post: post } %>
<% end %>
```erb

Rails provides a cleaner way to render a collection using a partial:

```erb
<%= render partial: "post", collection: @posts %>
```

This approach is more concise and clear. You can also pass an array directly to the render method:

```erb
<%= render @posts %>
```

This approach is a bit more abstract. Under the hood Rails uses the convention
that you will have a partial with the name of the models in the collection.
Rails will even render a collection of heterogeneous models
([customer, order, customer]) calling the correct partial for each one.

### Empty Collections

What happens if the collection you pass to your render call is empty? If you
don't handle this exception the render method will return nil and nothing will
appear on the screen. A useful trick is to use the `||` operator to print
something to the screen to alert the user to this.

```erb
<%= render(@posts) || "There are no blog posts!" %>
```

**Note:** When dealing with an empty collection, you'll _need to use `()` to
wrap that collection_.

## Conclusion

As always, Rails has tried to abstract commonly used functionality into more
terse and implicit code. Experiment with these tricks in the upcoming lab.
