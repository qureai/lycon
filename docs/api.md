# Lycon API

## Core Functions

### `lycon.load(path, mode=Decode.UNCHANGED)`

Loads and returns the image at the given path as a numpy ndarray.


### `lycon.save(path, image, options=None)`

Saves the given image (a numpy ndarray) at the given path.
The image format is inferred from the extension.

The options argument, if provided, should be a dictionary where the keys are constants from the Encode enum and the values are integers.

### `lycon.resize(image, width, height, interpolation=Interpolation.LINEAR, output=None)`

Resize the image to the given dimensions, resampled using the given interpolation method.

If an output ndarray is provided, it must be the same type as the input and have the
dimensions of the resized image.

### `lycon.get_supported_extensions`

Returns a list of supported image extensions.

## Enums

### `Interpolation`:

- `lycon.Interpolation.NEAREST`: Nearest Neighbor interpolation
- `lycon.Interpolation.LINEAR`: Bilinear interpolation
- `lycon.Interpolation.CUBIC`: Bicubic interpolation
- `lycon.Interpolation.AREA`: Resampling using pixel area relation. It may be a preferred method for image decimation, as it gives moire free results. When the image is zoomed, it is similar to nearest neighborhood interpolation.
- `lycon.Interpolation.LANCZOS` Lanczos interpolation over 8x8 neighborhood.

### `Decode`:

- `lycon.Decode.UNCHANGED`: Load either a grayscale or color image (including alpha channel), 8-bit format
- `lycon.Decode.GRAYSCALE`: Load as a grayscale 8-bit image. Color images will be converted to grayscale.
- `lycon.Decode.COLOR`: Load as a three-channeled 8-bit image. Grayscale images will be converted. Any alpha channels will be discarded.
- `lycon.Decode.ANY_DEPTH`: If set, 16-bit and 32-bit images are returned as such. Otherwise, an 8-bit image is returned.

### `Encode`:

See `lycon.save`.

*Keys*:

- `lycon.Encode.JPEG_QUALITY`
- `lycon.Encode.JPEG_PROGRESSIVE`
- `lycon.Encode.JPEG_OPTIMIZE`
- `lycon.Encode.JPEG_RST_INTERVAL`
- `lycon.Encode.JPEG_LUMA_QUALITY`
- `lycon.Encode.JPEG_CHROMA_QUALITY`

*Values*: An integer from 0 to 100 (the higher is the better). The default value is 95.

*Keys:*
    
- PNG_COMPRESSION
- PNG_STRATEGY
- PNG_BILEVEL
- PNG_STRATEGY_DEFAULT
- PNG_STRATEGY_FILTERED
- PNG_STRATEGY_HUFFMAN_ONLY
- PNG_STRATEGY_RLE
- PNG_STRATEGY_FIXED

*Values*: An integer from 0 to 9. A higher value means a smaller size and longer compression time. Default value is 3.