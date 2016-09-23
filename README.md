# 4d-plugin-gd
Image manipulation based on [libgd](https://libgd.github.io)

###Example

Rotate + Animate

![sample](https://cloud.githubusercontent.com/assets/1725068/18774589/ca7dab4e-8195-11e6-85e1-aee11f061dc1.gif)

Filter

* brightness
![brightness](https://cloud.githubusercontent.com/assets/1725068/18776435/30ccf874-81a4-11e6-9c69-e0a633fa82f3.png)

* colorize
![colorize](https://cloud.githubusercontent.com/assets/1725068/18776439/312aa032-81a4-11e6-9ebd-5e75e7b99ecc.png)

* contrast
![contrast](https://cloud.githubusercontent.com/assets/1725068/18776440/312d6786-81a4-11e6-8ae3-25c17c311a85.png)

* edgedetect
![edgedetect](https://cloud.githubusercontent.com/assets/1725068/18776441/3132c32a-81a4-11e6-899a-8db50f5a556b.png)

* emboss
![emboss](https://cloud.githubusercontent.com/assets/1725068/18776442/3135dd08-81a4-11e6-8852-9e17adff54d9.png)

* gaussian-blur
![gaussian-blur](https://cloud.githubusercontent.com/assets/1725068/18776438/3129a402-81a4-11e6-9a4a-f7b27072a9b6.png)

* grayscale
![grayscale](https://cloud.githubusercontent.com/assets/1725068/18776436/30f69a1c-81a4-11e6-9d7f-df85c49d87b1.png)

* mean-removal
![mean-removal](https://cloud.githubusercontent.com/assets/1725068/18776437/31229f54-81a4-11e6-9fb2-427b6a55a644.png)

* negate
![negate](https://cloud.githubusercontent.com/assets/1725068/18776443/31501e8e-81a4-11e6-82a0-8dea1172e548.png)

* selective-blur
![selective-blur](https://cloud.githubusercontent.com/assets/1725068/18776444/31502d02-81a4-11e6-82e6-709de495b774.png)

* smooth
![smooth](https://cloud.githubusercontent.com/assets/1725068/18776445/3154e89c-81a4-11e6-922b-6c64aa160618.png)

###Rotation

```
$path:=Get 4D folder(Current resources folder)

READ PICTURE FILE($path+"1.png";$image)

$pathDst:=Get 4D folder(Current resources folder)+"rotated"+Folder separator
CREATE FOLDER($pathDst;*)

For ($i;0;359)
$result:=GD Rotate ($image;$i)  //image is internally converted to PNG
WRITE PICTURE FILE($pathDst+String($i;"000")+".png";$result)
End for 
```

###Animation

```
$path:=Get 4D folder(Current resources folder)+"rotated"+Folder separator

ARRAY PICTURE($images;0)

DOCUMENT LIST($path;$paths;Absolute path | Recursive parsing | Ignore invisible)

For ($i;1;Size of array($paths))
READ PICTURE FILE($paths{$i};$image)
CREATE THUMBNAIL($image;$image;128;128)
APPEND TO ARRAY($images;$image)
End for 

$delay:=1  //delay before next frame (in 1/100 seconds)

$result:=GD Animate ($images;$delay)  //frames are internally converted to GIF

WRITE PICTURE FILE(System folder(Desktop)+"sample.gif";$result)
```

###Filter

The following filters are supported

```
IMG_FILTER_NEGATE 1
IMG_FILTER_GRAYSCALE 2
IMG_FILTER_EDGEDETECT 3
IMG_FILTER_EMBOSS 4
IMG_FILTER_GAUSSIAN_BLUR 5
IMG_FILTER_SELECTIVE_BLUR 6
IMG_FILTER_MEAN_REMOVAL 7
IMG_FILTER_SMOOTH 8
IMG_FILTER_CONTRAST 9
IMG_FILTER_BRIGHTNESS 10
IMG_FILTER_SCATTER 11
IMG_FILTER_PIXELATE 12
IMG_FILTER_COLORIZE 13
```

###Filter parameters

0 params

* IMG_FILTER_NEGATE
* IMG_FILTER_GRAYSCALE
* IMG_FILTER_EDGEDETECT
* IMG_FILTER_EMBOSS
* IMG_FILTER_SELECTIVE_BLUR
* IMG_FILTER_MEAN_REMOVAL

1 param

* IMG_FILTER_SMOOTH	(weight)
* IMG_FILTER_CONTRAST (contrast)
* IMG_FILTER_BRIGHTNESS (brightness)

2 params

* IMG_FILTER_SCATTER	(sub, plus)
* IMG_FILTER_PIXELATE (block_size, mode)
* IMG_FILTER_GAUSSIAN_BLUR (radius, sigma)

4 params

* IMG_FILTER_COLORIZE (red, green, blue, alpha)
