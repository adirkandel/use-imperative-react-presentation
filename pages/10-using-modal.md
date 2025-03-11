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