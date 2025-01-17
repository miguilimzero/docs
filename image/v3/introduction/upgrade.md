# Upgrade Guide
## Upgrade from Intervention Image 2.x to 3.x

[TOC]

## New Features

Intervention Image 3 has been rewritten from the ground up with very little code carried
over from the previous version. This means a more modern and sophisticated
architecture and API that takes advantage of the modern features of PHP 8+.
There are a few key features that further improve the library.

- [Support of animated GIF with GD and Imagick drivers](/v3/basics/instantiation#creating-animations)
- [Support for colorspaces](/v3/basics/meta-information)
- [Support for line height in font system](/v3/modifying/text-fonts)
- [Object for encoded images](/v3/basics/image-output#handling-of-encoded-image-data)

## API Changes

- [canvas()](/v2/api/canvas) is now handled by [create()](/v3/basics/instantiation#creating-new-images)
- [circle()](/v2/api/circle) is now handled by [drawCircle()](/v3/modifying/drawing#drawing-a-circle)
- [crop()](/v2/api/crop) still exists but has a new [signature](/v3/modifying/resizing#crop-image)
- [ellipse()](/v2/api/ellipse) is now handled by [drawEllipse()](/v3/modifying/drawing#drawing-ellipses)
- [encode()](/v2/api/encode) is now handled by [toJpeg()](https://image.intervention.io/v3/basics/image-output#encoding-jpeg-format), [toWebp()](https://image.intervention.io/v3/basics/image-output#encoding-webp-format), [toPng()](/v3/basics/image-output#encoding-png-format), [toGif()](/v3/basics/image-output#encoding-gif-format), [toBitmap()](/v3/basics/image-output#encoding-windows-bitmap-format) and [toAvif()](/v3/basics/image-output#encoding-av1-image-file-format-avif)
- [exif()](/v2/api/exif) is now handled by [exif()](/v3/basics/meta-information#exif-information) with a different signature
- [fill()](/v3/modifying/effects#fill-image-with-color) currently only supports color values
- [filter()](/v2/api/filter) is now handled by [modify()](/v3/modifying/custom-modifiers)
- The resizing methods [resize()](/v2/api/resize), [fit()](/v2/api/fit), [widen()](/v2/api/widen) and [heighten()](/v2/api/heighten) have been completely rebuild and are now handled by [resize()](/v3/modifying/resizing), [resizeDown](/v3/modifying/resizing), [scale()](/v3/modifying/resizing), [scaleDown()](/v3/modifying/resizing), [cover()](/v3/modifying/resizing), [coverDown()](/v3/modifying/resizing), [pad()](/v3/modifying/resizing) and [contain()](/v3/modifying/resizing)
- [flip()](/v2/api/flip) still exists but has a new signature and is handled by [flip()](/v3/modifying/effects#mirror-image-horizontally) and [flop()](/v3/modifying/effects#mirror-image-vertically)
- [insert()](/v2/api/insert) has been replaced by [place()](/v3/modifying/inserting)
- [line()](/v2/api/line) has been replaced by [drawLine()](/v3/modifying/drawing#drawing-a-line)
- [make()](/v2/api/make) has been replaced by [read()](/v3/basics/instantiation#reading-image-sources)
- [mime()](/v2/api/make) is now handled by an [encoded image](/v3/basics/image-output#handling-of-encoded-image-data) only
- [pickColor()](/v2/api/pick-color) has a different signature without format which is handled by the [color class](/v3/basics/meta-information#reading-colors-of-certain-pixels)
- [pixel()](/v2/api/pixel) is handled by [drawPixel()](/v3/modifying/drawing#drawing-a-pixel)
- [polygon()](/v2/api/polygon) is handled by [drawPolygon()](/v3/modifying/drawing#drawing-a-polygon)
- [rectangle()](/v2/api/rectangle) is handled by [drawRectangle()](/v3/modifying/drawing#drawing-a-rectangle)
- [text()](/v2/api/text) still exists but has a new [signature](/v3/modifying/text-fonts)
- [resizeCanvas()](/v2/api/resize-canvas) still exists but has a new [signature](/v3/modifying/resizing)
- [limitColors()](/v2/api/limit-colors) is handled by [reduceColors](/v3/modifying/effects)

## Removed Features

- [trim()](/v2/api/trim) no longer exists
- [colorize()](/v2/api/colorize) no longer exists
- [interlace()](/v2/api/interlace) no longer exists
- [backup()](/v2/api/backup) no longer exists
- [basepath()](/v2/api/base-path) no longer exists
- [cache()](/v2/api/cache) no longer exists
- [filesize()](/v2/api/filesize) no longer exists
- [getCore()](/v2/api/get-core) no longer exists
- [iptc()](/v2/api/iptc) no longer exists
- [mask()](/v2/api/mask) no longer exists
- [opacity()](/v2/api/opacity) no longer exists
- [orientate()](/v2/api/orientate) no longer exists and is handled automatically
- [psrResponse()](/v2/api/psr-response) no longer exists
- [reset()](/v2/api/reset) no longer exists
- [response()](/v2/api/response) no longer exists
- [stream()](/v2/api/stream) no longer exists but you may use [toFilePointer()](/v3/basics/image-output#transform-encoded-image-to-file-pointer)

## Other Changes

- The [caching library](https://packagist.org/packages/intervention/imagecache)
  of Intervention Image 2 is not supported by the new version. 

- The service providers for the Laravel were removed to avoid a dependency to
  the framework and to highlight Intervention Image rather framework agnostic,
  which it always was. However, there is an [official package for Laravel integration](https://github.com/Intervention/image-laravel)

- It is no longer possible to create images from an URI directly. The data must
  first be loaded by a dedicated HTTP client and then passed to the image
  library. Intervention Image is not responsible for HTTP client operations.

- It is no longer possible to pass color values as array.
