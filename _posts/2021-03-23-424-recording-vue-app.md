---
layout: post
title:  "424 Recording Vue App"
category: webdev
---

Here's the readme for the Vue.js app I completed and launched on GitHub Pages this week. 

I have some future development ideas for this project I'll detail at some point soon.

I was also thinking it might be useful to write a simple tutorial on how to host Vue applications on GitHub Pages since these apps will not run natively in that environment out of the box. I wound up using a combination of two separate tutorials in order to get the app to run and I'm sure a walkthrough on how to do it would be helpful to others.

Check out the app on GitHub Pages here: [424 Recording Vue App](https://mikeparish.github.io/424-vue-app/).

Here's the contents of the readme for this project (which can also be found at the [project repo](https://github.com/MikeParish/424-vue-app)):

---

## What is this project?

One of my main interests and hobbies is music recording. 

Over the past four years, I've been creating online video content and a community for home recording enthusiasts. 

This project is a Vue.js web application based on an earlier version of the website [424recording.com](https://424recording.com). This website hosts affiliate links for helping support the production of the videos, recording gear recommendations, and social media links and contact information for the community.

One thing I wanted to explore with this project was creating a single-page application of the site. I've hosted [424recording.com](https://424recording.com) on GoDaddy for the length of the project, and I've made various versions of the site, adding needed features along the way. As I learned about JS frameworks in the Master's program at SUNY New Paltz, I wondered whether or not it would make sense to convert a site like this into a single-page web app using Vue.js.

## Pros and Cons: Static vs. Dynamic

### Pros

The original site is a static site that is hardcoded using HTML, [Bulma (a CSS framework)](https://bulma.io), and JS. One benefit of using a JS framework like Vue is the use of reusuable components: rather than rewriting the same code to display each gear review like on the static site, I created a 'gearcard' component which can be reused and dynamically displayed depending on the information on fake JSON servers that are setup on GitHub. (I'm using [My JSON Server](https://my-json-server.typicode.com/), which I discovered through Jeremy at [Vue Mastery](https://vuemastery.com), both of which are outstanding resources if you're looking to create something similar). The app then uses Axios to make calls to the JSON servers.

Similarly, another pro to using Vue is reusing the header, footer, sidebars, etc. While the static site is rudimentary, with the header, footer, and sidebars copied over to each new page created, with Vue, these components are coded once and then loaded to each .vue file as needed. 

(Since writing this post, I implemented reusable PHP templates for the header, footer, and sidebars on the static site which you can read about [here](https://mikeparish.github.io/mikecodes/webdev/2021/03/24/php-for-sharing-navbars-footers-and-other-repeated-elements-across-a-website.html).) 

The reason the static site was built like this was due to my inexperience creating static websites a few years ago, and goes to show that simple sites can become unneccessarily complex if you don't plan for the long term! Originally, the site was also meant to be a landing page for a mailing list and contact information (the first version was actually one .html file) so it was perfect for what was needed. Presently, it would probably make sense to refactor the site and utilize PHP or JS to display a header, footer, and sidebars sitewide.

### Cons

Another consideration as to whether to replace the static site with a dynamic web app is how often the site is updated. The time between updates is every four months or more. This site is a 'set it and forget it' type of site. I think this idea illustrates an important question to consider when it comes to web design: what is the best solution for the project at hand?

Other considerations in favor of a static site are how fast the site loads and SEO. One thing that I need to do more research on is how would replacing the current site with a single-page web app affect the present and future SEO of the site? That's one thing that's important from a discovery standpoint and also for ensuring a high ranking on Google. Hardcoding the site also guarantees that it will be fast loading, which is important given the reasons that visitors from around the world decide to visit the site.

## Conclusion

In its current form and for its current purpose, the static site is the best solution, despite the advantages gained by using Vue. Since the site is static and not meant to have much reactivity, and the fact that the site gets updated 3-4 times per year, a fully-fledged web app is probably overkill and more costly. But it's good practice and that's the purpose of this project: become acclimated to new web technologies, test a real-world use case, fetch data from JSON objects, and learn how to launch a Vue app on GitHub Pages (and eventually, the cloud).

Thanks for reading and happy coding!