---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/featured/?sushi,japanese,cooking
# some information about your slides (markdown enabled)
title: How to Roll Your React Components Like a Good Inside-Out Sushi
info: |
  ## Inside-Out React Components: The useImperativeHandle Hook
  A presentation for ReactNext about using imperative handles in a declarative world.
  
  Just like inside-out sushi reveals its beautiful ingredients while keeping its structure,
  useImperativeHandle reveals select component APIs while maintaining React's composition model.
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
highlighter: shiki
lineNumbers: false
---

# How to Roll Your React Components Like a Good Inside-Out Sushi 🍣

## Mastering useImperativeHandle in React

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #f85a3e 10%, #fa8453 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---
layout: center
class: text-center
---

# About Me 👋

<div class="flex justify-center">
  <img src="https://via.placeholder.com/200" class="rounded-full h-40 w-40 object-cover mx-auto my-4" />
</div>

* FullStack Developer @ Your Company
* React enthusiast since 2016
* Coffee lover ☕
* Twitter: @YourHandle
* Github: @YourGithub

---

# 🍣 What We'll Learn Today

<div class="flex">
<div class="mr-5">
<img src="https://em-content.zobj.net/source/microsoft-teams/363/sushi_1f363.png" class="h-50 opacity-80" />
</div>
<div class="flex-1">

<v-clicks>

- The ingredients: What is useImperativeHandle?
- The rice base: React's declarative paradigm
- The knife technique: Simple implementation examples
- The rolling technique: Creating clean component APIs
- The seaweed wrap: Working with forwardRef
- Master chef showcase: Real-world examples
- Perfect plating: Tips and best practices

</v-clicks>
</div>
</div>

---

# 🧐 The Problem: When Regular Rolls Aren't Enough

<div grid="~ cols-2 gap-4">
<div>

<img src="https://em-content.zobj.net/source/microsoft-teams/363/sushi_1f363.png" class="h-25 mb-4" />

React is **declarative** (regular maki roll):

- We define **what** we want to see (ingredients)
- React handles making the DOM changes (rolling)

This works great most of the time! 🎉

</div>
<div>

But sometimes you need inside-out rolls...

<v-clicks>

<img src="https://www.pngall.com/wp-content/uploads/5/California-Sushi-Roll-PNG-Free-Image.png" class="h-25 mb-4" />

There are cases where we need:
- Direct access to functionality inside a component
- Trigger imperative actions on a component
- Control DOM elements from outside

</v-clicks>

</div>
</div>

---

# 🍙 React Programming Paradigms: Maki vs. Uramaki

<div grid="~ cols-2 gap-4">
<div>

### Declarative (Traditional Maki)
```jsx
<Button 
  color="primary"
  onClick={handleClick}
  disabled={isLoading}
>
  Login
</Button>
```

<div class="text-sm mt-2 italic">The seaweed wraps the rice (UI wraps behavior)</div>

</div>
<div>

### Imperative (Inside-Out Uramaki)
```jsx
// Using a ref to access methods
const btnRef = useRef();

// Later in code
btnRef.current.click();
btnRef.current.focus();
btnRef.current.setDisabled(true);
```

<div class="text-sm mt-2 italic">The rice wraps the seaweed (behavior controls UI)</div>

</div>
</div>

---

# 🤔 Why Inside-Out? The useImperativeHandle Story

<div grid="~ cols-2 gap-4">
<div>

<v-clicks>

### The Chef's Challenge:
- Regular refs give you the whole roll (DOM node)
- But we have special fillings inside the component
- We want a curated tasting experience (clean API)
- Need to control what diners can access

</v-clicks>

</div>
<div>

<v-clicks>

### The Sushi Solution:
- With `useImperativeHandle` we can:
  - Create a perfect tasting menu (custom API)
  - Highlight select ingredients (internal methods)
  - Hide preparation techniques (complex functionality)
  - Present only our signature items (controlled exposure)

</v-clicks>

</div>
</div>

---

# 🧪 Basic Recipe: Your First Inside-Out Component

```jsx{all|2|3|4-8|11}
function MyInput(props, ref) {
  // Internal rice (private refs to DOM elements)
  const inputRef = useRef();
  
  // Turn it inside-out with useImperativeHandle
  useImperativeHandle(ref, () => ({
    focus: () => inputRef.current.focus(),
    clear: () => inputRef.current.value = ""
  }));

  return <input ref={inputRef} {...props} />;
}

// The nori wrapper that holds it all together
export default React.forwardRef(MyInput);
```

---

# 🎬 Serving Your Inside-Out Creation

```jsx
function Form() {
  // Get your chopsticks ready (create a ref)
  const inputRef = useRef(null);
  
  const handleSubmit = (e) => {
    e.preventDefault();
    // Pick up just the wasabi (only access exposed methods)
    inputRef.current.clear();
  };
  
  const focusInput = () => {
    // Dip into the soy sauce (call another exposed method)
    inputRef.current.focus();
  };

  return (
    <form onSubmit={handleSubmit}>
      <MyInput ref={inputRef} />
      <button type="button" onClick={focusInput}>Focus</button>
      <button type="submit">Submit</button>
    </form>
  );
}
```

---
layout: two-cols
---

# 🍱 Advanced Recipe: Temaki Hand Roll Modal

::right::

```jsx
function Modal(props, ref) {
  // Our secret filling (component state)
  const [isOpen, setIsOpen] = useState(false);
  
  // Wrap it with rice on the outside (expose API)
  useImperativeHandle(ref, () => ({
    open: () => setIsOpen(true),
    close: () => setIsOpen(false)
  }));
  
  if (!isOpen) return null;
  
  return (
    <div className="modal">
      {props.children}
      <button onClick={() => setIsOpen(false)}>
        Close
      </button>
    </div>
  );
}

// Don't forget the seaweed wrapper
const ImperativeModal = forwardRef(Modal);
```

---

# 🥢 Enjoying Your Hand Roll

```jsx
function App() {
  // Your chopsticks to pick up the roll
  const modalRef = useRef(null);
  
  return (
    <div>
      <button onClick={() => modalRef.current.open()}>
        Taste the Roll
      </button>
      
      <ImperativeModal ref={modalRef}>
        <h2>Delicious Modal!</h2>
        <p>Savor the imperative flavor...</p>
      </ImperativeModal>
    </div>
  );
}
```

---

# 🍱 Sushi Master Class: The Inside-Out Technique

<div class="flex">
<div class="flex-auto">
<v-clicks>

1. **Place seaweed on the bamboo mat (`forwardRef`)**
   ```jsx
   const MyComponent = forwardRef((props, ref) => { ... });
   ```

2. **Prepare your rice and fillings (refs for DOM elements)**
   ```jsx
   const someElementRef = useRef();
   ```

3. **Flip and expose the rice outside (`useImperativeHandle`)**
   ```jsx
   useImperativeHandle(ref, () => ({
     doSomething: () => { /* your ingredients */ },
     someValue: 42
   }));
   ```

4. **Pick it up with chopsticks (parent component's refs)**
   ```jsx
   componentRef.current.doSomething();
   ```

</v-clicks>
</div>

<div class="flex-none pl-4">
<img src="https://em-content.zobj.net/source/microsoft-teams/363/sushi_1f363.png" class="h-50 opacity-80" />
</div>
</div>

---

# 💪 Sushi Grade Type Safety

```tsx
// Define your menu items with precision
interface MyComponentHandle {
  focus: () => void;
  reset: () => void;
}

const MyComponent = forwardRef<MyComponentHandle, MyComponentProps>(
  (props, ref) => {
    // Premium grade ingredients
    const inputRef = useRef<HTMLInputElement>(null);
    
    // Present only certified fresh methods
    useImperativeHandle(ref, () => ({
      focus: () => inputRef.current?.focus(),
      reset: () => {
        if (inputRef.current) {
          inputRef.current.value = '';
        }
      }
    }));
    
    return <input ref={inputRef} {...props} />;
  }
);
```

---

# ⚠️ Sushi Chef Wisdom: Handle with Care

<div class="flex">
<div class="flex-auto">
<v-clicks>

- **Use sparingly** - Not every roll needs to be inside-out
  
- **Respect traditional techniques** - Manage state with props when possible

- **Keep the menu simple** - Only expose what your customers need

- **Inside-out = complex preparation** - Can lead to harder debugging

- **Mind the freshness** - Be aware of re-renders and stale values

- **Label your specials** - Use TypeScript for clear documentation

</v-clicks>
</div>

<div class="flex-none pl-4">
<img src="https://em-content.zobj.net/source/skype/289/warning_26a0-fe0f.png" class="h-40 opacity-90" />
</div>
</div>

---

# 🍣 Specialty Rolls: Advanced Techniques

<div class="flex">
<div class="flex-auto">
<v-clicks>

- **Complex Nigiri** - Rich text editors, time sliders, precision inputs
  
- **Fusion Cuisine** - Working with third-party libraries that have their own APIs

- **Artistic Plating** - Controlling animations and transitions with precision

- **Omakase Experience** - Clean wrappers around external services 

- **Chef's Special Menu** - Complex coordinated interactions between components

</v-clicks>
</div>

<div class="flex-none pl-4">
<img src="https://em-content.zobj.net/source/microsoft-teams/363/takeout-box_1f961.png" class="h-50 opacity-80" />
</div>
</div>

---
layout: center
class: text-center
---

# 🙏 Arigato Gozaimasu!

<div class="flex justify-center items-center h-60">
  <div class="text-center">
    <img src="https://em-content.zobj.net/source/microsoft-teams/363/sushi_1f363.png" class="h-25 inline-block mx-4" />
    <img src="https://em-content.zobj.net/source/microsoft-teams/363/chopsticks_1f962.png" class="h-25 inline-block mx-4" />

  <p class="mt-4">Hungry for more examples or have questions?</p>

  <div class="mt-8">
    <h3 class="text-xl mb-2">Find me at the sushi bar:</h3>
    <div class="grid grid-cols-2 gap-2">
      <div>
        * Twitter: @YourHandle
        * Github: @YourGithub
      </div>
      <div>
        * Blog: yourblog.dev
        * Email: your@email.com
      </div>
    </div>
  </div>
  </div>
</div>
