# 4d-plugin-gd
Image manipulation based on [libgd](https://libgd.github.io)

###Example

Rotate + Animate

![sample](https://cloud.githubusercontent.com/assets/1725068/18774589/ca7dab4e-8195-11e6-85e1-aee11f061dc1.gif)

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
