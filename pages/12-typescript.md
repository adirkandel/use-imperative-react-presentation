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