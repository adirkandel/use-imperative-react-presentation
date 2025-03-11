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