# CropCircle

CropCircle is a modern, minimal, hackable image cropping widget with minimal dependences (just jQuery) that tries to provide a cropping interface that's manageable on small touch devices as well as desktops.

[Live Demo](http://avocadocorp.github.io/CropCircle/cropcircletest.html)

## Using

CropCircle is built to be loaded by your favorite AMD-compliant tool. If you don't want to pull one of those in, see cropcircletest.html for an example of hacking around that. Once the code is loaded, initialization is very simple:

```javascript
    /* The first constructor parameter (the "parent box") is a box element that
       will contain the cropping area and content to be cropped. It will need 
       to have overflow:hidden set. */
    var cropper = new CropCircle($("#testBox"),  {

        /* Required. The number of handles to display. Must be either 4 or 8. */
        handles: 8, 
        
        /* Optional. Aspect ratio to constrain the crop area to. 
           If absent, aspect ratio is not constrained. */
        forceAspect: 1,

        /* Optional. If true, a short help blurb explaining how to use the
           widget on a touchscreen will be shown when CropCircle detects that 
           it's running on a touch device. */
        showHelp: true,

        /* Optional. Callback to call when the cropping area is moved. */
        onFrameChanged: function(frame) {
            /* Parameter 'frame' contains the position of the cropping area 
               relative to the box element passed above, in pixels of offset 
               from the parent edges as with CSS top/left/right/bottom properties.
               Pixel width and height of the crop area are also supplied. */
            console.log(frame);
        },

        /* Optional. If true, the crop area will be rendered as an ellipse
           instead of a rectangle. */
        circle: true,

        /* Optional. The actual element (<img>, etc) whose content is being 
           croped. If provided, the cropping area's movement will be 
           constrained to stay within the bounds of this element, but it will
           be possible on touch devices to use the complete area of the box 
           element passed in the first constructor parameter to move the crop
           area. This makes it possible to provide an extra "handle" area on
           mobile devices beyond the bounds of the actual content being cropped, 
           eliminating the "fat thumbs" issue. */
        image: $('#preview'),

        /* Optional. If true, indicates that the dimensions of the image and
           parent box elements are invalid at the time the CropCircle instance
           is constructed. Layout of the initial crop area position will be 
           delayed until the first resize event or first mutation of the parent
           box or image element's attributes.
           Additionally, if a forceAspect ratio is provided and no initial 
           dimensions are set, the crop area will be set to the maximum size 
           possible that still maintains the requested aspect ratio and 
           centered within any resulting excess space. */
        noInitialBounds: false,

        /* Optional. Initial position of the cropping area in CSS-style pixel
           offsets computed relative to the parent box. */
        top: 100,
        left: 100,
        bottom: 100,
        right: 100
    });
```

There is also a <code>remove()</code> method available on the created CropCircle object which will remove any elements or event handlers added to your page by CropCircle.

You will also need some CSS. This is left as an exercise to the reader because everyone has different styles and maybe you're using LESS or SASS. Here is some example CSS to get you started:

```css
    /* The actual cropping frame overlay. The border is what you actually
        see covering the cropped content.
        border-width gets set to an appropriate (large) value in code. */
    .crop-circle-crop-frame {
        border: 40px solid rgba(0, 0, 0, 0.8);
    }

    /* What the handles should look like. */
    .crop-circle-handle {
        width: 10px;
        height: 10px;
        background-color: white;
        box-shadow: 0 0 5px black;
    }

    /* On touch devices, the parent box gets the class crop-circle-touch added.
       Here we're using this to have no handles on touch devices because
       they're only useful if there's a mouse. */
    .crop-circle-touch .crop-circle-handle {
        display: none;
    }

    /* How to style the help blurb that shows on touch devices. Note the
       z-index, it's necessary to put the help blurb above the crop frame. */
    .crop-circle-help {
        color: white;
        text-shadow: 2px 2px 2px black;
        font-size: 20px;
        position: absolute;
        z-index: 1000;
        top: 10px;
        left: 10px;
    }
```

## Requirements
A modern flavor of jQuery. Probably something like 1.8.x. Built and tested with 1.11.1.
  
## License
CropCircle is freely distributable under the MIT license. See LICENSE.txt for full license.
