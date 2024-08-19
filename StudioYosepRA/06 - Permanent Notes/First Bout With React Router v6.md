
*Monday, August 19, 2024 - 17:17*

Status:

Tags: [[blog]] [[software engineering]]

---

The fact that it takes me this long before I can write another blog post is the reality that I haven't rebuilt my habit of writing blog post every day. However, from here on, I'm dedicating 30 minutes a day in the evening to write about what I'm doing for the day. Though hopefully, the content should've been around my work every day, and not my rants about life, haha. But I will keep doing my best to do that.

So today, I continue to work on StudioYosepRA v3. Which at this time of writing this post, it is still not finished yet. But on the bright side, I would hope that by the time it is finished, I would have a stash of posts that I could just send to my CMS later and fill out the blog page with enough posts right from the website's release.

Working on StudioYosepRA also signifies my journey and effort to go back into web development, and computer science in general. As anyone would've expected, everything that I do have come up rusty. I would forget the coding patterns that I would use previously as I try to retrace my memory. Although, it hasn't gone so bad that I forget how to write JavaScript and use React, the libraries have evolved to its new versions while I'm away. And one of them is [React Router](https://reactrouter.com/).

The last time I build an app, I used Next.js as my framework. Therefore, it actually has been a lot longer for me since I last touched React Router because Next.js have their own routing approach. I can still remember roughly how to use React Router on top of my head because of the lasting impression it had when I first tried using it. I mean, having a new page rendered instantly instead of going back to the server was mind-blowing for me at the time where I rely on a more traditional approach of asking HTML, CSS, and JavaScript whenever I need to enter a new page.

Although I have made a short head start for StudioYosepRA, as in I have set my dev environment up, update and audit the packages, and whatnot, I have come to a point where I need to setup my client-side routing. And that is when I realize that I need to go to React Router as my solution.

I go to the React Router website. As expected, everything is new. What the heck that it's already v6? Has time gone that quickly? I can't recall exactly when I last use React Router, but I do recall that I've used the late v4 and early v5. I don't know how long it has been since, but I reckon it hasn't been much longer than a year.

Despite everything that is new, the essence of client-side routing remain the same. I went through the feature overview of their documentation, and I only read a few new patterns that is not too difficult to understand once I understand enough of the previous versions. In short, it's only a matter of doing the same thing, yet with a slightly different approach. 

For example. the last time I would implement a nested routing, as in I want to have a specific section of the page to load different content on each route, yet what is outside of that section remain the same. For that, I would previously use something like a nested `<Switch>` on a certain part of the page component, and determine the routing for that specific section to render each of the necessary components.

In React Router v6, there is a stark difference that I no longer need to define `<Switch>` on different pages. But rather, the router configuration is now put in one place only. Such as:

```js
const router = createBrowserRouter([
	{
		path: '/',
		element: <Root />,
		children: [
			{
				path: 'blog',
				element: <Blog />,
			}
		],
	},
	{
		path: '/about',
		element: <About />,
	},
])
```

That one is just the simplest example I could provide in this post, but this router can get more comprehensive as it also determines the structure of the app. Although it needs some readjustment from me, but I like it that the route configurations are put into one space now. Therefore, I don't need to jump between files to see and configure its routing, or even comprehend the app structure if I'm reading someone else's code.

This is just one example of changes in React Router compared to the one that I use before. But it is all part of the game, and I'm in for it. I reckon I won't need longer than 2 days to make myself comfortable enough to understand the fundamentals and use it in StudioYosepRA. But I would still linger around their documentation for the time being.

---
## References
