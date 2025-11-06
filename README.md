# Ajax

> 🧩 Lightweight vanilla JS library for adding HTMX-like AJAX behavior using simple `data-ajax-*` attributes.

---

## 💡 Example Usage

### Basic example

```html
<!-- Basic example -->
<button
  data-ajax-get="/demo"
  data-ajax-trigger="click"
  data-ajax-target="#result"
>
  Load content
</button>

<div id="result">Initial content</div>
```

When the button is clicked:
- A GET request is sent to `/demo`
- The response HTML replaces the inner content of `#result`

---

### Example with POST and events

```html
<form
  data-ajax-post="/submit"
  data-ajax-trigger="submit"
  data-ajax-target="#response"
  data-ajax-event-success="console.log('Success!')"
  data-ajax-event-error="console.error('Error!')"
>
  <input name="username" required>
  <button type="submit">Send</button>
</form>

<div id="response"></div>
```

---

## 🔧 Installation

You can include it manually or through your build system.

### Option 1 – Direct script include

```html
<script type="module" src="/path/to/ajax.js"></script>
```

### Option 2 – ES6 import

```js
import Ajax from './ajax.js';
new Ajax();
```

---

## 🧩 Initialization

You only need to instantiate it once:

```js
import Ajax from './ajax.js';
new Ajax();
```

This automatically scans the DOM for `data-ajax-trigger` attributes and sets up delegated event listeners.

---

## ⚡ How it works

1. **Event delegation** — All elements using `data-ajax-trigger` are automatically handled, even if added dynamically.
2. **Context creation** — The script reads relevant `data-ajax-*` attributes to build the request.
3. **Request handling** — The `fetch()` API sends data as GET or POST depending on attributes.
4. **Response update** — The target element is updated according to `data-ajax-target` and `data-ajax-swap`.

---

## 🧰 Custom Events

| Event name | When it fires |
|-------------|---------------|
| `data-ajax:before-request` | Before sending the request |
| `data-ajax:on-success` | After a successful response |
| `data-ajax:on-error` | When a network or server error occurs |
| `data-ajax:after-request` | Always fires after request completion |

You can listen to these events using standard JavaScript:

```js
document.addEventListener('data-ajax:on-success', (e) => {
  console.log('AJAX success:', e.detail);
});
```

---

## 🧪 Browser Support

✅ Works in all modern browsers (Chrome, Firefox, Edge, Safari).  
⚠️ For older browsers, you may need a polyfill for `fetch()` or `FormData`.

---

## 📜 License

MIT License © Laurent Lassallette
