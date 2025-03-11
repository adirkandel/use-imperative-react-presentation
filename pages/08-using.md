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