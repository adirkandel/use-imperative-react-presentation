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