<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-SZCFBH2LZ7"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-SZCFBH2LZ7');
</script>

## Metaprogramming in Javascript

## Key Concept in Metaprogramming

1. Introspection:Introspection is the ability of code to analyse internal information about itself. An example of this would be the `Object.entries()` method which returns array of key-value pairs of an object.

2. Self Modification: Beyond just analysing it's internal, self-modification is a metaprogramming concept that enables a piece of code to alter itself during execution. This is not to be confused with control statement, where alternate branches are taken based on some conditionals. Self modification involves the actual mutation to the content of a piece of the code. Before we proceed, I want to drop here the Self-Modification is a DANGEROUS practice and is generally avoided unless you fully understand what you are doing. With that out of the way, here is a contrived example using the `eval` statement:

```js
let sayHi = () => console.log("hi");

sayHi();
let sayHiString = sayHi.toString();
sayHiString = sayHiString.replace("console.log", "alert");

eval(`sayHi=${sayHiString}`);

sayHi();
```

Yuhp, you guessed right. That is pretty bad code up there. However, the purpose is to show you what is possible with self modifying code.

3. Intercession: This is actually a rather interesting and pretty useful aspect of metaprogramming. It enables you define custom behaivour the wraps around the intrinsic behaviour of an object. For instance, it's possible to attach custom logic to be executed when you access or set the property of an object. We won't take an example here, as we are going to explore this further in the next section.

## Metaprogramming with the Proxy API

The Proxy API helps to create an object that can customize the behaivour of a given target object. That way, the exposed object (which is a proxy) can be interacted with directly while triggering custom logic that is executed behind-the-scenes. The Proxy API was introduced in ES6 and is being used internally by frameworks such as [Vuejs (version 3)]().

To take an example we are defining a Proxy object

```js
const obj = new Proxy(
  {},
  {
    set(target, name, value) {
      console.log(name, value);
      target[name] = value;
    },
  }
);
```

In our example, we define a Proxy with the `Proxy` constructor with an empty object, and our handler which consists of traps. Our `set` trap implementation which is called antytime a property is being assigned, logs the name of the property and its value.

There are alot of traps such as:

1. `has()`
2. `getPropertyOf()`
3. `get`

A full list can be found [here]()
