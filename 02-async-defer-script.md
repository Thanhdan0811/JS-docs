- When the browser loads HTML and comes across a <script>...</script> tag, It can't continue building the DOM.
- The same happens for external scripts <script src=""></script>.
- The browser must wait for the script to download, execute the downloaded script, and only then can it process the rest of the page.
- That leads to two issues : Scripts can't see DOM elements below them.
- If there's a bulky script at the top of the page , it "blocks the page".
  
# defer script.
- The _defer_ script tells the browser not to wait for the script.
- The browser will continue to process the HTML, build DOM.
- So : _defer_ never block page and always execute when the DOM is ready (but before DOMContentLoaded event.)

```
<p>...content before scripts...</p>

<script>
  document.addEventListener('DOMContentLoaded', () => alert("DOM ready after defer!"));
</script>

<script defer src="https://javascript.info/article/script-async-defer/long.js?speed=1"></script>

<p>...content after scripts...</p>

=> The page content shows up immediately.
   DOMContentLoaded waits for the deferred script. Only triggers when the script is downloaded and executed.
```

- Deferred scripts keesp their relative order, just like regular scripts.
- _NOTE_ The defer attribute is only for external scripts : ignore if the <script> tag has no src.

# async script.
- The async attribute means that a script is completely independent.
  + The browser doesn't block on _async_ script
  + Other scripts don't wait for _async_ script and _async_ script don't wait for them.
  + DOMContentLoaded and _async_ scripts don't wait for each other.
 
```
<p>...content before scripts...</p>

<script>
  document.addEventListener('DOMContentLoaded', () => alert("DOM ready!"));
</script>

<script async src="https://javascript.info/article/script-async-defer/long.js"></script>
<script async src="https://javascript.info/article/script-async-defer/small.js"></script>

<p>...content after scripts...</p>

=> the page content shows up immediately ; async doesn't block it.
DOMContentLoaded , small.js, long.js not sure which will be executed first.

```

- Async is great when we integrate an independent third-party script into the page.
- Like _defer_ script, _async_ script is only for externals scripts.


# Dynamic scripts.

```
let script = document.createElement('script');
script.src = "/article/script-async-defer/long.js";
document.body.append(script); // (*)
```

- The script starts loading as soon as it's appended to the document.
- Dynamic scripts behave as "async" by default : Don't wait for anything, and Vice versa.; load first run first.
- This can be changed if we explicitly set _script.async = false_

```
function loadScript(src) {
  let script = document.createElement('script');
  script.src = src;
  script.async = false;
  document.body.append(script);
}

// long.js runs first because of async=false
loadScript("/article/script-async-defer/long.js");
loadScript("/article/script-async-defer/small.js");

```

- 
