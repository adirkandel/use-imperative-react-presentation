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