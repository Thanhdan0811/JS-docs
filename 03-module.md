- A module is just a file. One script is one module.
- As modules support special keywords and features, we must tell the browser that a script should be treated as a module.
- _<script type="moduel">_
- _NOTE_ : modules work only via HTTP(s), not locally.

# Core module features.
- these features will valid both for browser and server-side Javascript.

- Modules always work in _strict mode_.
- _Module-level scope_ : Each module has its own top-level scope, top-level variables and functions from a module are not seen in other scripts.
- Modules should export what they want to be accessible from outside.
- _NOTE_ : window object can make a variable window-level and can be accesses in module script.
- _A module code is evaluated only the first time when imported_
  + If the same module is imported into multiple other modules, its code is executed only once, upon the first import.
 
```
// 📁 alert.js
alert("Module is evaluated!");

// Import the same module from different files
// 📁 1.js
import `./alert.js`; // Module is evaluated!

// 📁 2.js
import `./alert.js`; // (shows nothing)

```

- Such behavior is actually very convenient, because it allows us to configure modules.

# Import.meta 
- The object _import.meta_ contains the information about the current module.
- its content depends on the environment,
- In the browser , it contains the URL of the script or a current webpage URL if inside HTML.

```
<script type="module">
  alert(import.meta.url); // script URL
  // for an inline script - the URL of the current HTML-page
</script>
```

# In a module, "this" is undefined.
- In a module, top-level _this_ is undefined.


# Browser-specific features 
- There are several browser-specific differences of script module.

## Module scripts are deffered
- Module scripts are _always_ deferred, same effect as _defer_ attribute script.

## Async works on inline scripts.

```
<!-- all dependencies are fetched (analytics.js), and the script runs -->
<!-- doesn't wait for the document or other <script> tags -->
<script async type="module">
  import {counter} from './analytics.js';

  counter.count();
</script>

```

- this script doesn't wait for anything.

## External scripts
- External scripts with the same _src_ run only once.
```
<!-- the script my.js is fetched and executed only once -->
<script type="module" src="my.js"></script>
<script type="module" src="my.js"></script>
```

- External scripts that are fetched from another origin (e.g another site) require CORS headers,
- if a module script is fetched from another origin , the remote server must supply a header _Access-Control-Allow-Origin_
```
<!-- another-site.com must supply Access-Control-Allow-Origin -->
<!-- otherwise, the script won't execute -->
<script type="module" src="http://another-site.com/their.js"></script>
```

- NO "bare" modules allowed :
```
import {sayHi} from 'sayHi'; // Error, "bare" module => no relative or absolute , called bare module.
// the module must have a path, e.g. './sayHi.js' or wherever the module is
```

- Compatibility, "nonmodule"
- Old browsers do not understand type="module". Scripts of an unknown type are just ignored. For them, it’s possible to provide a fallback using the nomodule attribute:
```
<script type="module">
  alert("Runs in modern browsers");
</script>

<script nomodule>
  alert("Modern browsers know both type=module and nomodule, so skip this")
  alert("Old browsers ignore script with unknown type=module, but execute this.");
</script>
```
