Wagner
======

Effects composer for three.js

This is a WIP version of a new proposal for an effect composer for three.js

There's a demo with the latest-ish version of the code here [demo](http://www.clicktorelease.com/tmp/wagner). Here's a snapshot to give you an idea of what it can achieve:

![Image](./assets/snapshot.jpg)

Please use it only for review and test purposes. Don't hesitate to add issues or open a conversation about design decisions.


telime says:
----------

This is a personal maintenance project.

You can use the WAGNER composer on the browser just by reading the file(Wagner.js and Wagner.base.js).
If you can use Transpiler [superguigui/Wagner](http://github.com/superguigui/Wagner) or "THREE.EffectComposer" is recommended


Basic usage
----------

```js
/*
Include the libs
<script src="Wagner.js"></script>
*/

var composer = new WAGNER.Composer( renderer );
composer.setSize( window.innerWidth, window.innerHeight ); // or whatever resolution

var zoomBlurPass = new WAGNER.ZoomBlurPass();
var multiPassBloomPass = new WAGNER.MultiPassBloomPass();

renderer.autoClearColor = true;
composer.reset();
composer.render( scene, camera );
composer.pass( multiPassBloomPass );
composer.pass( zoomBlurPass );
composer.toScreen();
```

What works
----------

- Passes are by default RGBA
- Ping-pong buffers when chaining passes
- ShaderLoader is being replaced, but you can use it to load .glsl files. It hides all the XHR stuff
- Composing with Wagner for effects that run chained with the same resolution (e.g. full-screen effects)
- Basic effects implemented in the new WAGNER.Pass class:
    - Blend pass: all single pass. Current blend modes implemented: normal, darken, multiply, lighten, screen, overlay, soft light, hard light
    - Invert: single pass, inverts colours
    - Box Blur: single pass, blur in one direction specified in vec2 delta uniform
    - Full Box Blur: multipass, 2 box blur in two directions
    - Zoom Blur: single pass
    - Sepia, Noise, Denoise, Vignette, edge detection
    - Multi Pass Bloom: multipass, applies blur and blends with Screen mode
    - DOF (simple)
    - SSAO (simple)
- uniform reflection from GLSL source is working enough to be usable for most cases
- settings different path for shader loading

Credits
-------

Composer following the work of alteredq's [THREE.EffectComposer](https://github.com/mrdoob/three.js/blob/master/examples/js/postprocessing/EffectComposer.js)

Most of the shaders are from [https://github.com/evanw/glfx.js](https://github.com/evanw/glfx.js). Others are from different sources and forums, papers, or my own.

License
=======

MIT licensed

Copyright (C) 2014 Jaume Sanchez Elias - All shaders are copyright of their respective authors.

I'm trying to trace the original source for some of the common shaders. If your code is featured in the shaders folders, and wish to be correctly credited, or the code removed, please open an issue.

http://www.clicktorelease.com