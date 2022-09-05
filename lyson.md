# LYSON
**Lyrical.ly  Script Object Notation** `VERSION 8.0`


## Index
- [CommonNotation](https://github.com/mayur-rank/lyson/blob/main/lyson.md#common-notation)
- [MultiMaskInputs & HiddenMaskInputs](https://github.com/mayur-rank/lyson/blob/main/lyson.md#multimaskinputs--hiddenmaskinputs--maskinputs)
- [TextInputs](https://github.com/mayur-rank/lyson/blob/main/lyson.md#common-notation)
- [TextEffects](https://github.com/mayur-rank/lyson/blob/main/lyson.md#common-notation)
- [MaskSetting](https://github.com/mayur-rank/lyson/blob/main/lyson.md#common-notation)

## Common Notation

```
{
	"width": "720",
	"height": "1280",
	"fps": "20",
	"type": "none",
	"time": "0:0,15:0",
	"length": "15",
	"logoplace": "TR",
	"islogoblack": "false",
	"isexternalaudioallow": "true",
	"audiotitle": "Dil Se Bandhi Ek Dor",
	"backgroundvideo" : "background.mp4"
}
```

- **~~type:~~** *type is always none in lyson 7.0+*

  `"type": "none"`

- **width:** *output video width `Default: 720`*

  `"width": "1080"`

- **height:** *output video height `Default: 1280`*

  `"height": "1080"`

- **fps:** *output video fps(frame per second) `Default: 20`*

  `"fps": "30"`

- **nophoto:** *nophoto is max number of multiple photo need to selected*

  `"nophoto": "6"`

- **time:** *time mention timeline for effect and animation draw in canvas*
  
  `"time": "0:0,4:2,8:0,12:0,16:0,20:18,26:0"`
  ![Sample](https://github.com/mayur-rank/lyson/blob/main/images/timeline.jpg)

- **length:** *The length of the output video is defined by this value. `In second`*
  
  `"length": "26"`

- **logoplace:** *The logoplace specifies where the logo will be displayed `Default: TR`*
  
  `"logoplace": "TR"`

  | Code | Position |  
  -------|------------  
  | TR | Top, Right|  
  | BR | Bottom, Right|  
  | TL | Top, Left|  
  | BL | Bottom, Left|  
  | CC | Center |

- **logoalpha:** *The logoalpha value defines the logo's transparency. Range is 0 - 255 `Default: 255`*

  `"logoalpha": "255"`

- **islogoblack:** *The logo will be displayed in black if islogoblack is true, otherwise it will be displayed in white `Default: 255`*

  `"islogoblack": "false"`


- **videobitrate:** *The videobitrate determines the video output bitrate `Default: 2M`*

  `"videobitrate": "2M"`

- **backgroundvideo:** *Background video*

  `"backgroundvideo" : "background.mp4"`

- **crf:** *The value is used to compress the output video, the higher the value, the more compressed the video `Default: 30`*

  `"crf": "27"`

- **isexternalaudioallow:** *When isexternalaudioallow is true, the user can select audio from the SD card `Default: False`*

  `"isexternalaudioallow" : "true"`


- **audiotitle:** *Audio Title  `Default: Background Music`*

  `"audiotitle" : "Hey re meri moto"`
  
  - **selecetbyinput()**: *This eq is used when the audiotitle depends on the previous input, expression is join with (#) text1 join
    with (#) audio title list, It means title is selected from list by text1 input id*
    
  `"audiotitle" : "selecetbyinput()#text1#AudioM:AudioA:AudioY"`

- **audiofile:** *audiofile is name of audio file  `Default: audio.mp3`*

  `"audiofile": "y_audio.mp3"`

  - **selecetbyinput()**: *This eq is used when the audiofile depends on the previous input, expression is join with (#) text1 join
    with (#) audio file list, It means audio file is selected from list by text1 input id*

  `"audiofile": "selecetbyinput()#text1#m_audio.mp3:a_audio.mp3:y_audio.mp3"` 

- **aimodel:** *AI Models*

  `"aimodel": ["face278","facemask","disney","comic"]`

  | Effect | Need of Model |  
    -------|------------  
  | Face Key Point  | "face278" |  
  | Face Mask | "face278","facemask" |  
  | disney | "face278","facemask","disney" |  
  | removebg | - |  
  | skyseg | "skyseg" |
  | clothesseg | "clothesseg" |
  | hairseg | "hairseg" |
  | headseg | "face278","headseg" |
  | comic | "comic" |
  | cartoon | "cartoon" |


## MultiMaskInputs & HiddenMaskInputs & MaskInputs

```
{
	"multimaskinputs": [{
		"srno": "1",
		"maskid": "mask1",
		"maskimg": "mask1.png",
		"maskover": "over.png"
	}, {
		"maskid": "mask2",
		"maskratiosize": "720,1280",
		"maskratio": "1:2",
		"maskover": "over.png"
	}, {
		"maskid": "mask3",
		"masksize": "720,1280",
		"maskover": "over.png"
	}]
}
```

```
{
	"hiddenmaskinputs": [{
		"maskid": "hmask1",
		"maskimg": "mask1.png",
		"maskover": "over.png",
		"photoeq": "getMaskPhoto()#mask1"
	}, {
		"maskid": "hmask2",
		"maskimg": "mask2.png",
		"maskover": "over.png",
		"photoid": "2",
		"isgray": "false",
		"isblur": "false",
		"photoeffect": "multiply",
		"photoname": "addoverlay1.png"
	}]
}
```

```
{
	"maskinputs": [{
	    "srno": "1",
		"maskid": "fmask1",
		"maskimg": "mask1.png",
		"maskover": "over.png",
		"hs_bgremove": "true",
		"hs_bgremovetype": "face"
	}, {
	    "srno": "2",
		"maskid": "fmask1",
		"maskimg": "mask1.png",
		"maskover": "over.png",
		"hs_bgremove": "true",
		"hs_bgremovetype": "full",
		"isgray": "false",
		"isblur": "false",
		"photoeffect": "multiply",
		"photoname": "addoverlay1.png"
	}]
}
```

- **srno:** *The srno is the order number in this list, and the srno represents the input position to ask the user*

  `"srno" : "1"`

- **maskid:** *maskid is unique id in all inputs, maskid is used to get this user image*

  `"maskid": "mask1"`

- **maskimg:** *This is mask to reshape photo selected by user*

  `"maskimg": "page1_mask1.png"`

  - *selecetbyinput() eq is used to get mask image from previous text input, here selecetbyinput() join with (#) text1 join with (#) mask image list, It means image is selected from list base on text1 input*

    `"maskimg": "selecetbyinput()#text1#m_mask.png:a_mask.png:y_mask.png"`

- **maskover:** *maskover is a frame image that is overlaid above a user selected photo*

  `"maskover": "page1_frame1.png"`

  - *selecetbyinput() eq is used to get overlay image from previous text input, here selecetbyinput() join with (#) text1 join with (#) over image list, It means image is selected from list base on text1 input*

    `"maskover": "selecetbyinput()#text1#m_frame.png:a_frame.png:y_frame.png"`

- **photoid:** *This is id for pre-selected image from list previously get from multi photo selection.*

  `"photoid" :"1"`

- **photourl:** *Select photo direct from template asset folder.*

  `"photourl" :"sample_image.jpg"`

- **isskip:** *When the isskip value is true, this input is not required. `Default: false`*

  `"isskip": "true"`

- **isblur:** *If isblur is true, blur effect apply on user selected photo. `Default: false`*

  `"isblur": "true"`

- **isgray:** *If isgray is true, gray effect apply on user selected photo. `Default: false`*

  `"isgray": "true"`

- **photoeffect** *is effect name, define in table. `Default: false`*

  `"photoeffect": "addoverlay"`

- **photoname** *is image or color apply on photo with selected photoeffect. `Must be used with photoeffect`*

  `"photoname": "addoverlay1.png"`

 ##### Table3 here are some combination of photoeffect & photoname

  | photoeffect | photoname | notes |
  |------------ | --------- | ----- |
  | addoverlay | ImageName | Overlay photo and image |
  | darken | ImageName | Image and photo with darken effect |
  | lighten | ImageName | Image and photo with lighten effect |
  | multiply | ImageName | Image and photo with multiply effect |
  | add | ImageName | Image and photo with add effect |
  | overlay | ImageName | Image and photo with overlay effect |
  | screen | ImageName | Image and photo with screen effect |
  | blur | - | Photo with blur effect |
  | gray | - | Photo with gray effect |
  | color | orange, sky, red, yellow, cyan, blue, gray | Any one color you select for color effect with photo |

