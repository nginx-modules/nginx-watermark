# Nginx HttpImageFilterModule with watermark support

## Usage:

```
image_filter watermark /path/to/watermark.png [ bottom-right (default) | top-left | top-right | bottom-left | center ];
```

Differences from original patch (https://github.com/vdvm/nginx-watermark):
* bumped source version to 1.12.0 (WebP support was added)
* image upscaling in crop/resize mode is allowed (disallowed in upstream)

Tested with nginx 1.12.0

See also original docs: http://nginx.org/en/docs/http/ngx_http_image_filter_module.html#image_filter
