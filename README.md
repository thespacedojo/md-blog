xolvio:md-blog
==============

This is the blog package currently used on The Meteor Testing Manual. It will give you a
markdown powered blog on your site.

 * WYSIWYG Markdown support with in-place editing
 * Syntax highlighting using [highlight.js](https://highlightjs.org/)
 * Customizable styling with the ability to add your own classes to elements!
 * Publish / Unpublish / Archive / Unarchive workflows

[Try the demo site](http://md-blog.meteor.com)

[See the demo site code](https://github.com/xolvio/md-blog)

##Installation

`> meteor add xolvio:md-blog`

##Getting Started

There are a couple of steps to carry out before you can start using this package. Don't worry
it's very easy!

### 1. Define Layouts
First you need to define two templates that the blog in your app that look like this:

```html
<template name="blogListLayout">
  {{> yield}}
</template>

<template name="blogPostLayout">
  {{> yield}}
</template>
```

These are iron-router layouts that you be available at `<your site>/blog` and `<your site>/blog/:_id/:slug`.

You may want to customize these template further like adding disqus for instance:

```html
<template name="blogPostLayout">
  {{> yield}}
  {{> disqus}}
</template>
```

### 2. Setup Accounts & Roles
You need to ensure you are using a Meteor accounts package like accounts-password, and that the
user you are logged has 'roles' array with the element `mdblog-author`. Here's an example of a
user object:

```json
{
  "_id": "ixoreoJY5wzmNYMcY",
  "emails": [ {
    "address" : "sam@xolv.io",
    "verified" : true
  } ],
  "profile": { "name" : "Sam Hatoum" },
  "roles": [ "mdblog-author" ]
}
```

You can also the above pragmatically by calling
`Roles.addUsersToRoles(user._id, ['mdblog-author']);`

For more information about roles, have a look at the
[alanning:roles](https://github.com/alanning/meteor-roles) package.


You're ready to go!

### 3. Customize

This blog is designed to be fully customizable and as unopinionated as possible. Here are some of
the ways you can configure it.

####Styling

To style the blog list and posts, apply css
[just like in the demo app](https://github.com/xolvio/md-blog/blob/master/app/client/blog/blog.less).

For syntax highlighting style, you need to add the hljs css file of your choice.
[Pick a css template from here](https://highlightjs.org/static/demo/). You can see this in the
demo app,
[there is a file named hljs.css](https://github.com/xolvio/md-blog/tree/master/app/client/blog).

####Custom Classes
You can also add classes to any element of your choice! For this you need to use the settings.json
file. Have a look at the settings.json file below. You can see there's a field named
`element-classes`. The example above is adding the class
`pure-img` to all `img` elements. This is very powerful as it allows you to use your CSS
framework of your choice.

####Sorting
By default, the blog sorts your posts by date. You can change this by modifying the `sortBy`
field in the settings file.

####Settings File Example
```json
{
  "public": {
    "blog": {
      "name": "The Xolv.io md-blog",
      "Description": "Get verbal on your websites.",
      "prettify": {
        "syntax-highlighting": true,
        "element-classes": [
          {
            "locator": "img",
            "classes": ["pure-img"]
          },
          {
            "locator": "button",
            "classes": ["pure-button"]
          }
        ]
      },
      "sortBy": {"date": -1}
    }
  }
}
```

##Additional Info

###URL Format
The URL format of your blog will look lik this:

`www.your-site.com/blog`

`www.your-site.com/blog/7yh22/your-latest-blog-post`

The format is `/:_id/:slug`

The `:slug` is the title of the blog post with all the spaces replaced with dashes. It's believed
this is good for SEO purposes.

The `:_id` is a truncated version of the mongo id for the blog entry. This allows you to have
multiple posts with the same title over time.

When you archive blog posts, currently they are removed from the main view but they are still
accessible by search engines and external links. To see your archived blog entries, go to:

`www.your-site.com/archive`

##Contribution
Yes please!

Todo list:
 * [ ] Your idea!
 * [ ] Image Uploads
 * [ ] Date Picker
 * [ ] Author Picker
 * [ ] Pagination
 * [ ] Auto draft saving + history