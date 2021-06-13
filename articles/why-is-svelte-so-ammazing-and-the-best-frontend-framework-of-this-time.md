# **Why is Svelte so great, and the best front-end 'framework' of this time**

Despite the fact that svelte is almost celebrating its 5th anniversary, it is still one of the most underrated JavaScript frameworks or libraries of the moment. It is currently still snowed under by the big three: React, Vue & Angular.

Where the GitHub repository of React has 170k stars, Vue 184k & Angular 73.9k at the time of writing, Svelte only has 47.7k. Despite being the least popular at the moment, it is one of the fastest growing.

Despite I use the term framework, it is better not to see Svelte as a framework. Svelte uses a technology that compiles the code into a small, vanilla JS file. This makes the speed of these applications particularly fast.

## **How does it works?**

### **Easy to understand**

The syntax of a svelte file is very simple. By using a script, styles and html tag, you have already written a component.

```html
<script>
  let count = 1;

  function handleClick() {
    count += 1;
  }
</script>

<button on:click="{handleClick}">Count: {count}</button>

<p>{count}</p>
```

Compared to other front-end methods, which often require a more complex structure, Svelte is quite easy to understand. It is also very nice to see that Svelte uses HTML, CSS & JavaScript. Because Svelte has this easy approach, the legibility of a component is very good. It's easy to see what's happening inside a component, because of its beginner-friendly structure.

### **Less is more**

As can be seen in the example above, little code is required when writing a Svelte component Just like the famous saying 'Less is more' by Ludwig Mies van der Rohe used to be, so is the thinking behind Svelte.

Rich Harris, the founder of Svelte, has made several comparisons of a component written in Svelte, compared to other major platforms such as React & Vue, in his article [Write less code](https://svelte.dev/blog/write-less-code). The example shows how a Svelte component is written in only six lines, while in React it is about 200% more lines.

### **Reactivity with statements**

Within Svelte it is quite easy to update a variable, these are also called reactive statements. Using a reactive decleration: `$:`, the value can be easily updated with a simple click of the button.

```html
<script>
  let count = 1;

  $: doubled = count * 2; // the `$:` means 're-run whenever these values change'

  function handleClick() {
    count += 1;
  }
</script>

<button on:click="{handleClick}">Count: {count}</button>

<p>{count} * 2 = {doubled}</p>
```

In the example above it can be seen that every time the button is clicked, the value is increased by 1, the variable double recognizes that count has been updated, so that it immediately updates its own value.

### **Global State manager**

### **Styling inside a component**

You don't need to mess around with external styling sheets, packages, or other weird methods to style your components inside Svelte. In fact, you can indicate your preference within a style tag in which language you want to style. Of course the default method is vanilla CSS, but SCSS/SASS/LESS is also an option, or styling libraries like TailwindCSS that work perfectly with Svelte.

The default styling will look like this, if you choose to use SCSS for example, you need to add `lang='scss'` to the style tag, after you've installed the package ofcourse. After that you can nest the code on the SCSS way.

```html
<style>
  p {
    color: purple;
    font-family: 'Comic Sans MS', cursive;
    font-size: 2em;
  }
</style>

<section>
  <p>This is a paragraph.</p>
</section>
```

### **JavaScript blocks**

In plain HTML you don't have an option to have conditional rendering, loops or await blocks. Inside Svelte it's quite easy to implement it. It is therefore very similar to the handlebars template engine in terms of syntax.

#### **If / else**

For conditional rendering it is possible to use an if block. When there must be a fallback (else statement), you can combine it with each other. The code will then appear as shown below. When the user is logged in, he will see the log-out button, if this is not the case, the user will be given the option to log in.

```html
{#if user.loggedIn}
<button on:click="{toggle}">Log out</button>
{:else}
<button on:click="{toggle}">Log in</button>
{/if}
```

#### **Each loops**

When you need to loop over an array of data, for example to render all blog posts, you can use an each block. You give as array the data you want to use within the loop, and as argument what you want to use as an individual element.

```html
{#each cats as cat, i}
<li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}"> {i + 1}: {cat.name} </a></li>
{/each}
```

#### **Await blocks**

If you want to retrieve data with, for example, a fetch method, you can use an asynchronous block. Svelte ensures that the data is waited for, and when this is successfully processed, the user can start working with the data. All states of the data fetch are captured here, and shown to the user.

```html
{#await promise}
<p>...waiting</p>
{:then number}
<p>The number is {number}</p>
{:catch error}
<p style="color: red">{error.message}</p>
{/await}
```

## **Conclusion: Svelte is awesome!**

If you like writing clean HTML, CSS & JavaScript, small bundle sizes, and great performance on your applications, Svelte is the perfect choice for you as a Front-end Developer. Svelte has an accessible tutorial that you can go through to familiarize yourself with the syntax.

Coming soon will be the launch of SvelteKit v1.0, a Server Side Rendered application like Next/Nuxt, the ideal tool for your JAMStack. I'm looking forward to building cool applications with this, and I'm convinced that Svelte will continue to grow and soon settle into the top 3 largest JavaScript frameworks.
