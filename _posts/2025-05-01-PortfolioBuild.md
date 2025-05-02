---
title: Making my portfolio
date: 2025-05-1 20:00:00 -0400
categories:
  - Dev Log
tags:
  - portfolio
pin: "false"
image: portfolio.webp
media_subpath: /assets/img/portfolio
---
## Why a portfolio?

I was seeing left and right how every software developer, web designer, etc. had a portfolio to showcase everything they've done. So I figured why not do the same. I mean, what better way to track your progress than by showcasing everything that you've worked on?


## The Design

So I decided to build my portfolio. The first thing I needed to do was figure out a design. A while ago, when I was initially inspired by web design and web development, I stumbled upon an interesting portfolio.

![La Playa Studio](laplaya.webp)_La Playa [Studio] Landing Page_

[La Playa [Studio]](https://www.laplaya.studio/) is a boutique design studio that builds most, if not all, of their sites using Squarespace. I loved their unique approach in hiding every site and only showing the image once you hovered your mouse over it. So, I decided to model my own portfolio website after their design. After a few days of building and tweaking, I ended up with this:

![Final Portfolio - Light](l-portfolio.webp)
![Final Portfolio](portfolio.webp)[_Final Design_](https://jorgexag.github.io/portfolio/)

## Roadblocks/Learning Opportunities
### Hiding Images
After building the skeleton on how I wanted things to look like, hiding the images was the first issue that I stumbled upon. My initial thought was to just have a `<div>` cover the image and on `:hover` the opacity would transition from 1 to 0.

While the idea was correct, for some reason, the `div` would not cover the underlying image. It was only after adding the following to the overlay, that the image was covered.
```css
.card-overlay {
	position: absolute;
	top: 0;
	right: 0;
	left: 0;
	bottom: 0;
}
```

Once that was added, this was the result:
![1st Result](old-portfolio.webp)

At this point, I was just happy with the fact that the functionality of the site was working as intended and that I was finally able to figure it out. But something still irked me, **it didn't look good!**

### Grainy-ness

I remember watching a video a while from [Juxtopposed](https://www.youtube.com/@juxtopposed) where they discussed designing and coding with grainy textures. I've added the video below in case anyone is interested.

{% include embed/youtube.html id='_ZFghigBmqo' %}

So I decided to add grainy texture to my portfolio site. While there are numerous resources covering how to add grainy textures to the site, I decided to follow Eamonn Cottrell's freeCodeCamp guide on [How to Create Grainy CSS Backgrounds Using SVG Filters](https://www.freecodecamp.org/news/grainy-css-backgrounds-using-svg-filters/). 

Throughout the article, three methods are covered on how to add grainy textures to your site. I ended up going with the PNG noise image, and just adding it as a background in my CSS file.
```css
body {
	background-image: url("./img/noise-light.png");
}
```

**Nice! Another roadblock down!**
### Light & Dark Mode
With how common it is to see sites have both dark/light mode, I decided to give it a shot. Nothing too crazy here. All I did was create the following Javascript script file to get things working:

```js
document.addEventListener('DOMContentLoaded', () => {
	const sunIcon = document.getElementById('sun');
	const moonIcon = document.getElementById('moon');
	const lImage = document.getElementById('l-image');
	const dImage = document.getElementById('d-image');
	const body = document.body;
	
	// Function to set the theme based on the preference
	const setTheme = (isDarkMode) => {
		if (isDarkMode) {
			body.classList.add('dark-mode');
			body.classList.remove('light-mode');
			sunIcon.style.display = 'block';
			moonIcon.style.display = 'none';
			lImage.style.display = 'none';
			dImage.style.display = 'block';
		} else {
			body.classList.add('light-mode');
			body.classList.remove('dark-mode');
			sunIcon.style.display = 'none';
			moonIcon.style.display = 'block';
			lImage.style.display = 'block';
			dImage.style.display = 'none';
			}
		}; 
	
	// Check the user's preference and set the initial theme
	const prefersDarkScheme = window.matchMedia("(prefers-color-scheme: dark)").matches;
	setTheme(prefersDarkScheme);
	
	// Event listeners for toggling the theme
	sunIcon.addEventListener('click', () => {
	setTheme(false); // Switch to light mode
	});
	  
	moonIcon.addEventListener('click', () => {
	setTheme(true); // Switch to dark mode
	});
});
```

I also ensured that the image for the portfolio card changes depending on the color-scheme.

## Main takeaways
Writing these blog posts allow me to look back at the project and see what I took away from them. For this one in particular, I learnt:
- CSS
	- Grid vs Flex display.
	- Utilizing positions for placement of elements.
	- Working with background images.
- JS
	- Using `window.matchMedia` to gather user preference.
	- Using `eventListener` for user activity.

## What's next?
My next focus will be diving deeper into the *design* aspect of web design. Learning how to properly design, structure, and build service sites.

**Thank you for reading!**