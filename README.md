# Custom JS Web API

Here I am exploring how to create a custom Web API just like how Javascript browser-built-in Web APIs.

> **INFO**
> 
> One thing to note is that it will be limited to your JavaScript environment and won’t be exactly like the built-in JavaScript **Web APIs** (e.g., `fetch`, `localStorage`, etc.).
>
> You can, however, create custom APIs that provide specific functionality for your web application by leveraging **JavaScript classes**, **modules**, and **event-driven programming**.
> 
> You can’t add new global Web APIs to the browser environment like those built into JavaScript, but you can absolutely create custom JavaScript APIs for your applications. By leveraging classes, modules, and event-driven programming, you can mimic the behavior of native Web APIs and create reusable, modular pieces of functionality tailored to your needs.
>
> Creating native Web APIs just like `localStorage` and `fetch` requires you to modify the Javascript runtime which is essentially a browser.

### Steps to Create Your Own Web API

Here’s how you can create a custom API that mimics the behavior of built-in Web APIs:

### 1. **Encapsulate Your API in a Class**
You can create a JavaScript class to encapsulate the logic of your API. This will make your API feel like it is part of the browser's environment.

#### Example: A Custom Timer API

```javascript
class TimerAPI {
  constructor() {
    this.timerId = null;
  }

  // Start a timer and execute a callback after a specified time
  startTimer(callback, duration) {
    this.timerId = setTimeout(() => {
      callback();
      console.log('Timer finished');
    }, duration);
  }

  // Cancel the timer
  cancelTimer() {
    if (this.timerId) {
      clearTimeout(this.timerId);
      console.log('Timer cancelled');
    }
  }
}

// Using the TimerAPI
const myTimer = new TimerAPI();
myTimer.startTimer(() => {
  console.log('Time’s up!');
}, 2000);

// To cancel the timer before it finishes
// myTimer.cancelTimer();
```

### 2. **Use Events and Callbacks for Asynchronous Behavior**
If you want your API to handle asynchronous events (like how the `fetch` API works), you can use **Promises** or **callbacks** to manage asynchronous behavior.

#### Example: A Custom Storage API

```javascript
class MyStorageAPI {
  constructor() {
    this.storage = {};
  }

  // Store data asynchronously
  async setItem(key, value) {
    return new Promise((resolve) => {
      setTimeout(() => {
        this.storage[key] = value;
        resolve('Item stored successfully');
      }, 1000);
    });
  }

  // Retrieve data asynchronously
  async getItem(key) {
    return new Promise((resolve) => {
      setTimeout(() => {
        resolve(this.storage[key]);
      }, 500);
    });
  }
}

// Using the MyStorageAPI
const storageAPI = new MyStorageAPI();

storageAPI.setItem('name', 'John Doe').then((message) => {
  console.log(message);
  storageAPI.getItem('name').then((value) => {
    console.log('Stored value:', value);
  });
});
```

### 3. **Extend Native JavaScript APIs (Optional)**
You can also create your own API by extending native browser APIs. For example, you can extend the `Storage` API or `EventTarget` to create a custom API that behaves similarly to native ones.

#### Example: Extending `EventTarget` for Custom Events

```javascript
class MyEventAPI extends EventTarget {
  triggerCustomEvent() {
    const event = new Event('customEvent');
    this.dispatchEvent(event);
  }
}

const myAPI = new MyEventAPI();
myAPI.addEventListener('customEvent', () => {
  console.log('Custom event triggered!');
});

myAPI.triggerCustomEvent();  // Output: "Custom event triggered!"
```

### 4. **Make Your API Modular**
If you’re using **ES6 modules**, you can create reusable components that feel like they belong to a larger API framework.

#### Example: Exporting a Custom API

```javascript
// myAPI.js
export class MyAPI {
  doSomething() {
    console.log('API doing something...');
  }
}

// main.js
import { MyAPI } from './myAPI.js';

const api = new MyAPI();
api.doSomething();  // Output: "API doing something..."
```

### 5. **Document Your API (Optional but Encouraged)**
Just like official Web APIs, it’s a good practice to document how to use your API. Provide descriptions of the methods, parameters, and usage examples.

### Important Considerations
- **Security**: Custom APIs can only run in the browser where they are defined. They don’t have system-level privileges like native Web APIs.
- **Browser Limitations**: Your custom Web API will only exist in the context of your application. It won’t be available globally across the browser or to other websites.
- **Performance**: Be mindful of performance and memory usage, especially if your API involves timers, event listeners, or heavy computations.

