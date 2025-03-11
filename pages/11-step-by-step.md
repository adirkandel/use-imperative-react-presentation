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