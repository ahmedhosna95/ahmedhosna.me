---
order: 2
title: "Conservation Legacy 3"
team: "Mighty in the Midwest"
summary: "Led the development of a platform of websites for Conservation Legacy, an organization that supports local conservation services across the US."
year: "2017"
roles:
  - "Front-end development"
  - "CraftCMS development"
tech:
  - "CraftCMS"
  - "Webpack"
link: "https://conservationlegacy.org"
banner: "conservation-legacy.png"
primaryColor: "#C46C27"
category: js
tags:
  - js
---
Conservation Legacy is the third largest non-profit conservation corps program in the country. With eight seperate programs, Conservation Legacy needed a new website platform to showcase the work they do and move people to join their programs.

I worked closely with our team lead to define and lead the development of the platform based on work we had previously done for [Herman Miller certified dealers](http://mightyinthemidwest.com/work/herman-miller-dealer-platform).

## Flexible templating and navigation

One of the biggest issues the team was experiencing with their previous website was the inability to create and manage content easily. We worked with the team to define a set of "modules" they could use to build out pages using [matrix fields](https://www.youtube.com/watch?v=VSXglzqJ2Z4).


Each programs needs were different in terms of pages needed. We built a fully customizable navigation setup that allowed each program to add, remove, and reorder pages as needed.

## Themeing

{% Figure {
  src: '/assets/images/conservation-legacy-azcorps.jpg',
  ratio: '1000/367',
  alt: 'Photo of Alex Carpenter',
  caption: '[Arizona Conservation Corps](https://azcorps.org) call to action',
  lazyload: true
} %}

Each site needed to be easily themeable. Choosing to stick to two color variable options, we created a Sass file for each program and defined the primary and secondary color variables before importing the master Sass file.

```scss
/* src/styles/conservation-legacy.scss */

$primary-color: #4f4c08;
$secondary-color: #918c10;

@import 'main.scss';
```

This allowed us to output only the CSS needed for each program, keeping things performant. This also allowed us to easily add a new program to the platform with little configuration needed.

We made heavy use of SVGs to create the torn edges look which allowed us to be able to change the background color based on the variables as well.
