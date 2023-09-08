====
Blog
====

**Odoo Blog** allows you to create and manage blog posts on your website to engage your audience and
build a community.

You can activate the Blog module from your website by clicking :guilabel:`+New`,
:guilabel:`Blog Post`, and :guilabel:`Save` it.

.. seealso::
   :doc:`Website documentation <website>`

Creating a blog
===============

To create or edit a blog, go to :menuselection:`Website --> Configuration --> Blogs: Blogs`. Click
:guilabel:`New` and fill in the required information: add a :guilabel:`Blog Name` and a
:guilabel:`Blog Subtitle` that appears in the top banner under your blog's name.

Your blog appears in the sub-menu bar of your website.

Writing a blog post
===================

Go to your website and click :guilabel:`+New` in the top-right corner and select
:guilabel:`Blog Post`. In the pop-up, **Select the blog** where the post should appear and write the
post's :guilabel:`Title`.

Write your blog post and customize your page’s content using the website builder.

.. tip::
   - Illustrate your articles with copyright-free images from :doc:`Unsplash <website/configuration/unsplash>`.
   - Type `/` in the text editor to format and add elements to your text.

.. important::
   Don't forget to toggle the :guilabel:`Unpublished` switch in the upper-right corner to publish
   your article.

Using tags
==========

Tags are visible by default at the end of each blog post, and can also be shown on the blog's main
page to help you organize your blog posts and facilitate searching them. To show tags on your blog
main page, click :menuselection:`Edit --> Customize` and enable the :guilabel:`Sidebar`. Do not
disable the :guilabel:`Tags List`.

To create a tag, go to :menuselection:`Website --> Configuration --> Blogs: Tags` and click
:guilabel:`New`. Fill in the required information:

- :guilabel:`Name`;
- :guilabel:`Category`: the :ref:`category <blog/tag-categories>` your tag belongs to, if any;
- :guilabel:`Used in`: to apply your tag to existing blog posts, click :guilabel:`Add a line`,
  select your posts, and click :guilabel:`Select`.

You can also create a tag from a blog post by clicking :menuselection:`Edit --> Customize`. If not
yet done, enable the :guilabel:`Sidebar`, go to the :guilabel:`Blog Post Cover` section, click
:guilabel:`Choose a record`, and :guilabel:`Create`.

.. image:: blog/create-tag.png
   :alt: create a tag

.. _blog/tag-categories:

Tag categories
--------------

You can organize your tags in different categories visible on your blog main page when the
:guilabel:`Sidebar` is enabled.

To create a tag category, click :menuselection:`Website --> Configuration --> Blogs: Tag Categories
--> New`. You can add a tag to your category by going to :menuselection:`Website --> Configuration
--> Blogs: Tags`, open a tag, and fill in the :guilabel:`Category` field.

Customizing content
===================

Customizing the blog main page
------------------------------

You can customize your blog's main page by going to :menuselection:`Edit --> Customize`.

.. note::
   Changes applied to a blog's main page apply to all blog's main pages.

:guilabel:`Top Banner`: select :guilabel:`Name/Latest Post` to display the title of the latest post
on the top banner, or :guilabel:`Drop Zone for Building Blocks` to hide the top banner.

:guilabel:`Layout`: select to display blog posts on the main page as :guilabel:`Grid` or
:guilabel:`List`.

- :guilabel:`Cards`: to display your posts as cards;
- :guilabel:`Increase Readability`: to change the way the text is displayed.

:guilabel:`Sidebar`: to display a column an :guilabel:`About us` section and, if enabled, additional
sections:

- :guilabel:`Archives`: a search bar allows to search posts by creation date;
- :guilabel:`Follow Us`: add links to your social media networks if previously configured in a
  Social Media building block;
- :guilabel:`Tags List`: shows all existing tags related to your posts. Users can click on a tag
  to access all related posts.

:guilabel:`Posts List`: select :guilabel:`Cover` to show the image related to your posts, or
:guilabel:`No Cover` to hide it.

- :guilabel:`Author`: to display the author of the post;
- :guilabel:`Comments/View Stats`: to display the number of comments and views on your post;
- :guilabel:`Teaser & Tags`: to display the first sentences of your article and tags below your
  post's image and title.

Customizing your blog post
--------------------------

You can customize your blog posts by going to :menuselection:`Edit --> Customize`.

.. note::
   Changes applied to a blog post apply to all posts.

:guilabel:`Layout`: select :guilabel:`Title Inside Cover` to display the title inside the cover
image or :guilabel:`Title above Cover` to display the title above the cover image.

- :guilabel:`Increase Readability`: to increase the font weight and decrease the text zone width.

:guilabel:`Sidebar`: to display the :guilabel:`Sidebar` and additional options:

- :guilabel:`Archive`: a search bar allows to search posts by creation date;
- :guilabel:`Author`: to mention the author on the post;
- :guilabel:`Blog List`: to show the list of your blogs;
- :guilabel:`Share Links`: to allow users to share your posts on social media;
- :guilabel:`Tags`: to display the tags of the post.

:guilabel:`Breadcrumb`: to show the path to the post and the user's location within the website.

:guilabel:`Bottom`: click :guilabel:`Next Article` to display the article below your post, or click
:guilabel:`Comments` to allow visitors to comment on your post.

:guilabel:`Select To Tweet`: to enable the tweet of part of the text when selected.

.. tip::
   Use :ref:`Plausible <website/analytics/plausible>` to keep track of the traffic on your blog.
