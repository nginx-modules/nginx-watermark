# Nginx image module (ngx_http_image_filter_module) with watermark support

## Usage
```
image_filter watermark;
image_filter_watermark /path/to/watermark.png;
image_filter_watermark_position bottom-right;
image_filter_watermark_margin 0;
image_filter_watermark_alpha 100;
image_filter_upscale on;
```
## Documentation
```
Syntax:  image_filter watermark [<path> [ <position> ]];
Default: none
Context: location
```
Applies watermark to images. Watermark can be combined with other image filters and is applied after `crop/resize/rotate` and `sharpen`, but before `interlace` (see original docs).
___
```
Syntax:  image_filter_watermark <path>;
Default: none
Context: http, server, location
```
Sets path to watermark. Watermark must be in PNG format.
___
```
Syntax:  image_filter_watermark_position bottom-right | top-left | top-right | bottom-left | center;
Default: image_filter_watermark_position bottom-right;
Context: http, server, location
```
Sets position of watermark.
___
```
Syntax:  image_filter_watermark_margin <margin>;
Default: image_filter_watermark_margin 10;
Context: http, server, location
```
Sets watermark margin.
___
```
Syntax:  image_filter_watermark_alpha <alpha>;
Default: image_filter_watermark_alpha 75;
Context: http, server, location
```
Sets watermark transparency. Must be between 0 and 100.
___
```
Syntax:  image_filter_upscale on | off;
Default: image_filter_upscale off;
Context: http, server, location
```
Defines whether image upscaling during resize/crop should be allowed. Note that `gdImageCopyResampled()` is used for image manipulation, and libgd docs say the following:
>If the source and destination area differ in size, the area will be resized using bilinear interpolation for truecolor images, and nearest-neighbor interpolation for palette images.

## Differences from original patch
Original patch: https://github.com/vdvm/nginx-watermark
* bumped nginx source version to 1.12.0 (WebP support was added)
* image upscaling in crop/resize mode is allowed (disallowed in upstream)
* added watermark margin customization (10px by default)
* added watermark transparency customization (75 by default)
* watermark is added after crop/resize, not instead of

## Original docs
http://nginx.org/en/docs/http/ngx_http_image_filter_module.html#image_filter

## Tested with
* nginx 1.12.0
