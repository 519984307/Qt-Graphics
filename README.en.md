# Qt Graphics

-   [Simplified Chinese](README.md)
-   [English](README.en.md)

> **Notice**: The renderings update may not be timely enough.

## Support more image formats

For support of more image formats, please refer to[kimageformats-binaries](https://github.com/RealChuan/kimageformats-binaries/tree/dev)：

1.  from`Actions`Download in`Artifacts`folder, will`kimg_*`Extract the library file to the Qt packaging directory`imageformats`in folder;
2.  Other dependent library files need to be placed in the same level directory as the main program or in a location where the main program can be loaded.

* * *

## Advantages and disadvantages of using GPU to render 2D textures (QRhiWidget, QVulkanWindow, QOpenGLWidget)

### advantage

-   **Excellent performance**: Compared with the image viewing interface based on QGraphicsView, GPU rendering is smoother and CPU usage is extremely low.

### shortcoming

-   **Rotation display problem**: When rotated at any angle, the texture aspect ratio may change, resulting in abnormal display.
    -   [openglview](src/gpugraphics/openglview.cc)A temporary solution is provided in which can maintain the original image aspect ratio when rotating, but the original scaling ratio needs to be discarded and adjusted to fit the window or original image size.
    -   Please refer to the specific implementation`rotatedTextureSize`、`rotateNinetieth`and`anti_rotateNinetieth`function.

* * *

## QVulkanWindow compilation instructions

### Known compilation issues

1.  **CMake（MacOS）**: Unable to find QVulkanWindow related header files, compilation failed.
2.  **qmake**：
    -   **MacOS**: The QVulkanWindowRenderer header file is missing and compilation fails.
    -   **Ubuntu**: QVulkanInstance header file is missing and compilation fails.
3.  Compilation for the above environments has been temporarily disabled.

* * *

## Multiple image file viewer

-   Supports downloading files from a single file such as`ico`、`gif`etc.) and display multiple images.
-   Other formats depend on`kimageformats-binaries`Plug-in support.

* * *

## ICO file production

### Known issues

-   **[FreeImage](https://github.com/danoli3/FreeImage)**In generating`256x256`There is a flaw in the ICO file of an image: it incorrectly sets the width and height fields directly to`256`, rather than required by the format specification`0`or`255`, causing Windows Explorer to not recognize the resolution correctly.
-   **solution**：
    -   Use based on[QtIcoHandler](https://github.com/qt/qtbase/blob/dev/src/plugins/imageformats/ico/qicohandler.h)Modified[icowriter](/src/utils/icowriter.hpp)。
-   **Recommended resolution**：`256x256`、`128x128`、`64x64`、`48x48`、`32x32`、`16x16`。

* * *

## Functional interface example

### 1. Picture viewing interface

<div align=center>
<img src="docs/ImageView.png" width="90%" height="90%">
</div>

* * *

### 2. Mosaic drawing (eraser effect)

<div align=center>
<img src="docs/MaskEdit.png" width="90%" height="90%">
</div>

* * *

### 3. Rounded/circular icon editing

> **Notice**: Please save in PNG format, otherwise the rounded corner area may appear black.
>
> <div align=center>
> <img src="docs/RoundEdit.jpg" width="90%" height="90%">
> </div>

* * *

### 4. Simple graphics drawing

<div align=center>
<img src="docs/DrawScene.png" width="90%" height="90%">
</div>

* * *

### 5. Movie subtitle splicing

-   The left side is a quick zoom preview (may be blurry), and the right side is the original image display.
-   The actual generation is based on the original image, and the clarity can be verified after saving.

<div align=center>
<img src="docs/FilmSubTiltleSplicing.png" width="90%" height="90%">
</div>

* * *

### 6. GIF recording (egif/gif-h library) and screenshot function

-   The following figure uses the GIF recording function to demonstrate the screenshot process:
-   After taking the screenshot, you can use the graphics drawing function in (4) for editing.

<div align=center>
<img src="docs/Record_Screenshot.gif" width="90%" height="90%">
</div>
