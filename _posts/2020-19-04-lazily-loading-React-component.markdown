---
layout: post
title:  Suspense - A Lazily Loading React Component
date:   2020-04-19 09:57:36 +0530
categories: React
---

React has been a trending choice within the frontend community amongst the various JS frameworks and libraries today. “React is a (Frontend) Javascript library for building user interfaces” - it’s what the official website says and it is what it has always been. The UI needs to be in sync with the data being presented to the user.
<i>Dan Abramov</i> (Creator of Redux), at JSConf 2018 announced - 

<b>“We’ve built a generic way to ensure that high-priority updates like user input don’t get blocked by rendering low-priority updates.” </b>

If you have ever learnt or worked with React, you know new features are being added to React persistently which obviously sounds exciting.

A question has always been haunting me for quite a while. What do I make my application UI do while it goes to a data fetching phase? Probably not go for a drink!

Most developers, especially the FRONTEND kind would shout-out saying “Spinner” and to which I totally accede. Now, this reminds me that we need to create a local state which would be a simple boolean.

```
state = {
	isLoading: false	 // true when the component is in data fetching state
} 
```


The state would now be responsible to show the component or hide it.

React 16 has added an experimental feature and is not available in the stable release. And its <b>Suspense</b> and yes, they named it knowing that an API call may return donkey even if you request for a horse. Well, that was a joke, maybe not a good one!

### Let’s dig in and see what <b>Suspense</b> actually does!

The Official React Documentation states that <i>Suspense</i> lets you “wait” for some code to load and declaratively specify a loading state (like a spinner) while we’re waiting. Let's say we have a component Component which is lazy-loaded.

```
const Component = React.lazy(() => import('./Component')); // Lazy-loaded 🐨

// Show a spinner while the Component is loading
<Suspense fallback={<Spinner />}>
  <Component />
</Suspense>
```

Suspense takes “fallback” as a prop. This prop can be JSX or another component which would render every time an API call is made. It suspends rendering for the component unless some condition(s) are met and shows the fallback instead. 

Suspense is not a data fetching library. It’s a mechanism for data fetching libraries to communicate to React that the data the component is reading is not ready yet.

What <i>Suspense</i> is not :
<ul>
<li>A data fetching implementation which means it doesn’t doesn’t assume you use REST, GraphQL etc. </li>
<li>A replacement for fetch.</li>
<li>A coupling for network logic.</li>
</ul>

What <Suspense> actually does is
<ul>
<li>Integrates with data fetching libraries for a more natural feel.</li>
<li>orchestrates designed loading states intentionally.</li>
<li>Handles asynchronous code which can be error-prone.</li>
</ul>


Due to incorrect assumptions about the order in which the code may run, race conditions are encountered. A solution for that is not to wait until the data is set to the state but set the state and start rendering immediately after the request is fired.

Suspense doesn’t completely rely on async rendering. Working synchronously can also be achieved too with a shortcoming where the nested components are triggered immediately without a delay.

Another use case of React’s Suspense is <b>Code Splitting</b>. Code splitting is a concept in improving performance wherein you break down your application into various parts so that the entire app does not need to load right away. Suspense works well with it.

With Suspense, you get the ability to suspend a component from render will some async call/task is being performed. Until the data is ready, you can pause any state updates and work in loading data down to the component tree. And Voila! You get an instantaneous and fluid UI for faster networks and for the slower network an intentionally crafted loading state. This is still in experimental mode and not available in stable releases. Still, you can have fun using it. <strong> Happy Coding!!</strong>✌🏼

