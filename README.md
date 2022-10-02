# Typescript Note

#### useRef "Object is possibly null" error in React
- The exclamation mark is called the non-null assertion operator in TypeScript. 
- It is used to remove null and undefined from a type without doing any explicit type checking.

```js
import {useEffect, useRef} from 'react';

export default function App() {
  const inputRef = useRef<HTMLInputElement>(null); //Some commonly used types are: HTMLInputElement, HTMLButtonElement, HTMLAnchorElement, HTMLImageElement , HTMLTextAreaElement, HTMLDivElement etc.

  useEffect(() => {
    // 👉️ ref could be null here
    if (inputRef.current != null) {
      // 👉️ TypeScript knows that ref is not null here
      inputRef.current.focus();
    }
  }, []);
  
  useEffect(() => {
    // 👇️ optional chaining (?.) => if the current property on the ref stores a null value, the operator would short-circuit returning undefined instead of try to call the focus() method on an undefined value and cause a runtime error.
    inputRef.current?.focus();
  }, []);
  
  useEffect(() => {
    // 👇️ using non-null (!) assertion => the current property on the ref object does not store a null or an undefined value so TypeScript doesn't perform any checks to make sure the property is not nullish.
    inputRef.current!.focus();
  }, []);

  return (
    <div>
      <input ref={inputRef} type="text" id="message" />
      <button>Click</button>
    </div>
  );
}
```
