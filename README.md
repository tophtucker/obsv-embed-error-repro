# Errors from using different copies of the Runtime

Here are two notebook embeds. Notebook Embed 1 was downloaded to a local folder,
and uses that local copy of the runtime. Notebook Embed 2 is hotlinked to the
module served by the API, and uses the CDN's copy of the runtime.

The first time, it loads fine. The second time (presumably cached), we get
“spectralDecompositionsAll = RuntimeError: invalid module” in Notebook Embed
1.

This can be fixed by changing either notebook embed to use the same copy of the
runtime — either one of the following two lines:

~~~js
import {Runtime, Inspector} from "https://cdn.jsdelivr.net/npm/@observablehq/runtime@4/dist/runtime.js";
import {Runtime, Inspector} from "./spectral-decompositions-of-natural-images/runtime.js";
~~~

The same problem occurs if you're using two different local copies of the
runtime.

It does seem to depend somewhat on the contents of the cells you're embedding; I
haven't been able to reconstruct the failure with fresh minimal notebooks yet.