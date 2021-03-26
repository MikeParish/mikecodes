---
layout: post
title:  "PHP for Sharing Navbars, Footers, and Other Repeated Elements Across a Website"
category: webdev
---

One thing I was thinking about when writing the [424 Recording Vue App](https://mikeparish.github.io/mikecodes/webdev/2021/03/23/424-recording-vue-app.html) post a couple days ago was implementing a navbar and footer across [424recording.com](https://424recording.com), the static website on which the Vue app is based. 

I wanted to do this without copying the HTML for these elements from page to page, which becomes a headache anytime the site is updated and/or as the number of pages on the site grows.

As I mentioned in the previous post, I violated the DRY (Don't Repeat Yourself) Principle with repeating HTML for two reasons:
1. Lack of knowledge at the time of the site's creation four years ago
2. The site's origin as a two page website consisting of a landing page and a contact page (where copying over the navbar was a simple solution to get the site up and running, but which was then carried over as a bad habit into future iterations of the site)

Over time, while learning about web development and working on other projects, it became clear that there was a better solution, one that would involve either the use of PHP or JavaScript/jQuery to display repeated HTML across different pages of the site.

## Let's Use PHP 

The main reasons I used PHP came down to speed, GoDaddy's cPanel/Linux server (where the site is hosted) already being equipped with a PHP interpreter, and (perhaps an edge-case but) if a user doesn't have JavaScript enabled in their browser, the navigational elements of the site would not be displayed, making the site unnavigable.

The PHP solution is easy, too. I also have more experience using PHP from two classes that I've taken, Cloud Computing and E-Business Systems. I also like that PHP scripts run server-side, and there's just something I find enjoyable about working with the language.

## But Why Do We Need a Scripting Language For This Task?

We need to use PHP, JavaScript, or some other scripting language to display the repeated HTML because HTML itself is not a programming language. 

To quote Ben Romy [in this article about HTML](https://ischool.syr.edu/why-html-is-not-a-programming-language/), 
> HTML is used for structural purposes on a web page, not functional ones.

HTML is a markup language. This means it tells the browser how information should be formatted or displayed. And that's it.

## The Solution

The first thing we need is a file that contains the navbar HTML we want to display on each page. The same goes for any element we want to display multiple times across different pages (footer, sidebar, etc.)

I wound up having four files: `navbar.php`, `footer.php`, `left-sidebar.php`, and `right-sidebar.php`. 

([The site](https://424recording.com/dawless-setup) has a three column layout: one central main bar which is flanked by sidebars on either side.)

The PHP for these files is the same (but with the HTML specific to each element inside of the `echo` statement where the comment is below):
~~~~
<?php
    echo '<!--insert HTML here-->';
?>
~~~~
The `echo` statement allows us to output strings and can contain HTML/markup. (You can read more about `echo` in the [PHP docs](https://www.php.net/manual/en/function.echo).)

I'd recommend using single quotes for the `echo` statement, as you will most likely have double quotes for an `id`, `class`, or `style` in your HTML, and if any strings contain a single quote (like a contraction) make sure to use a backslash (for instance, `that's` becomes `that\'s`).

Once you have these files added to the server, you can then use PHP to add them on each HTML page. 

There's two things left to do:

~~~~
<div class="hero-head" style="background-color: #0099FF;">
    <?php include 'navbar.php';?>
</div>
~~~~

1. Find the location in each file where you want to display the element and add it to the file using the `include` keyword (as in the above example)
2. Change the extension of files that contain PHP from `filename.html` to `filename.php`.

## Why Is This Better?
There's a couple reasons I prefer this (and why I would assume most people would):
1. Each file is cleaner and easier to scan when changing or adding code
2. It's easier to distinguish between the files based on their content if you have multiple files open at once
3. Since the navbar, footer, and sidebars are all repeated on most pages, you use these elements and PHP files almost like you would use components in Vue.js (or maybe it's the other way around)
4. There's one central file for each element, and as updates are needed, the links or information can be updated in one place, rather than by needing to edit every page of the site where an element appears (which is bad form, tedious, and increases the chances of making an error)
5. In some files, where all of these elements appear, 50-150 lines of code have been replaced by 12 lines

Overall, it took longer to write this blog post than it did to refactor the HTML and add PHP to the files!
## Further Reading

If anything on this page is unclear, here's a few resources that should help out if you get stuck:
* [PHP Include Files (W3Schools)](https://www.w3schools.com/PhP/php_includes.asp)
* [PHP Documentation (php.net)](https://www.php.net/manual/en/intro-whatis.php)
* [View or Change PHP Version (GoDaddy)](https://www.godaddy.com/help/view-or-change-the-php-version-for-my-linux-hosting-16090)

Thanks for reading and happy coding!