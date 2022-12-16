## Gesture Interaction UI

I'm starting a series where I write about advanced UI patterns that takes intuitive user interaction to the next level. This is the first part of this series, if you want to receive notification when a new article drops, please subscribe to my newsletter.

So in this first series, we are going to look a gesture based interaction that is common in mobile applications like Gmail [more examples etc]. Basically, what we are building is going to look like this;

[Simple gesture based interaction](image-picture)

## Mental Model

To make our article more interesting, here we talk about the mental model for builinding this UI pattern before we begin implementing it.

## Installing our Dependencies

- React setting up
- Framer-motion

## Index file

```js
// App.js
```

So, our `App.js` contains the setup for our demo application. Here we've imported the MenuItem Component and used it to generate the view by populating it with a mock `json` data in the itemsMock file, The next section dives deeper into the contents of the `Item` component. We also make use of `zusctand` to store our global data in order to make it available to other components without worrying about `zusctand`. The choice for `zucstand` is completely arbitrary, and any state management tool will suffice.

## Item Component

```js
// Item.js
```

So, based on our initial decision, we want each item to exhibit the following behaivour:

1. When slided to the right, it reveals controls for starring and archiving.
2. When slided to the left, it reveals controls for editing and deleting
3. When slided all the way to right, it stars
4. When slided all the way to the left, it deletes.

To achieve this, we decided to create our actions component after which we overlayed the content over the actions component. The styling for this looks like:

```css

```

## The Actions Rearrangement

So in our last section, we are now concerned with how to rearrange the content of the actions component. With the awesome drag interaction functonality in framer-motion, impleneting a draggable and rearrangement content is quite easy

The menu options

```js
// Menu.js
```
