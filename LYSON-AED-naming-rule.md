🎨 LYSON Naming Rules (Designer Guide)
======================================

This guide defines how After Effects **layer names** must be written so the exporter script produces correct `.lyson.json`.

---

1\. **Compositions**
----------------

* **Main comp**:

  ```php-template
  COMP_LYSON_<TemplateName>

  ```

  Example: `COMP_LYSON_Birthday`
* **System / helper comps**:

  ```php-template
  COMP_SYS_<Name>
  COMP_SHARED_<Name>

  ```

---

2\. **Image Layers**
----------------

### 2.1 User-provided images

```php-template
IMG_INPUT_<maskid>

```

```php-template
IMG_INPUT_<maskid>_OVER[<OverImageName>]

```

* Marks an image that will come from user input.
* Exporter auto-calculates:

  * `maskratiosize` = `<width>,<height>`
  * `maskratio` = reduced ratio like `9:16`
  * `masksize` = same as `maskratiosize`

✅ Example:

```nginx
IMG_INPUT_maskuserphoto

```

```nginx
IMG_INPUT_maskuserphoto_OVER[userover.png]

```

### 2.2 Custom shape masks

```php-template
IMG_INPUT_<maskid>_SHAPE[<ShapeImageName>]

```

```php-template
IMG_INPUT_<maskid>_SHAPE[<ShapeImageName>]_OVER[<OverImageName>]

```

* Designer provides a **PNG/JPG file** with that shape.
* Exporter outputs:

  * `"maskimg": "mask.png"`

✅ Example:

```php-template
IMG_INPUT_usermask_SHAPE[usermask.png]_OVER[userover.png]

```

Will expect `userphoto.png` in the AE project.

---

### 2.3 Static images

```php-template
IMG_STATIC_IMG[<ImageName>]

```

* Exporter copies `<ImageName.png>` as static decoration.
* No user input.

✅ Example:

```nginx
IMG_STATIC_IMG[photoframe.jpg]

```

**Static Image fx**

```php-template
IMG_STATIC_FX[<fx>]

```
* Fx is set direct to imgname.
* No user input.

```php-template
IMG_STATIC_FX[randimg()#img_heart.png:img_heart1.png]
```
* randimg() function choose any random image from this list img_heart.png:img_heart1.png

```php-template
IMG_STATIC_FX[selecetbyinput()#text2#lg_hi.png:lg_ti.png:lg_te.png]
```
* selecetbyinput() function choose any image from this list lg_hi.png:lg_ti.png:lg_te.png where text2 text input has value idx, here text input is spinnerid

```php-template
IMG_STATIC_FX[createImgOnInput()#mask1#100#200#mask.jpg]
```

```php-template
IMG_STATIC_FX[crecreateImgOnInput()#mask1#100#200#mask.jpg#frame.jpg]
```

* createImgOnInput() function is used to crop image from (100,200) to base on mask.jpg, frame is optional to overlay on mask

---

3\. **Text Layers**
---------------

### 3.1 Dynamic text inputs

```bash
TXT_INPUT_TEXT[{id,key,maxchar[,label]}]_SUFFIXES

```

* `{id,key,maxchar}` = required
* `label` = optional user-friendly name
* Multiple placeholders can be combined:

  ```css
  TXT_INPUT_TEXT[{text1,AAA,20} love {text2,BBB,10}]_SUFFIXES

  ```

#### Properties:

* `textid` = `id`
* `textkey` = sample text (`key`)
* `textmaxchar` = max allowed chars
* `textlable` = `label` (if provided, else `id`)
* `textsample` = `key`

---

### 3.2 Static text

```php-template
TXT_STATIC_TEXT[<TextContent>]_SUFFIXES

```

* Direct static text, no user input.
* Example:

  ```nginx
  TXT_STATIC_TEXT[Happy Birthday]_CENTER

  ```

**Static Text fx**

```php-template
TXT_STATIC_FX[<fx>]_SUFFIXES

```

```php-template
TXT_STATIC_FX[getdate()#dd-MM-yyyy HH:mm#VAL is here]

```
* getdate() function is to draw current date 


```php-template
TXT_STATIC_FX[selectline()#I m here:You r here]_CENTER

```
* selectline() function is to choose any random line from  I m here:You r here


```php-template
TXT_STATIC_FX[selecetbyinput()#text2#Hindi:Tamil:Telugu"]_LINES4[30]

```
* selecetbyinput() function is to choose string from Hindi:Tamil:Telugu using text2 input's value


```php-template
TXT_STATIC_FX[selecttext()#txt1#latter:1#<VAL> is here"]

```
* selecttext() function is to choose substring from string value in input txt1., this are substring eq. latter:1 latter:N word:1 word:N substring:2 substring:0,2 substring:2,N

---

4\. **Suffix Rules for Text**
-------------------------

Suffixes can be combined at the end of layer names.

### 4.1 Alignment

* **Left (default):** nothing needed
* **Center (full width):**

  ```nginx
  _CENTER

  ```

  → `textaling = "center"`, `textwidth = comp.width`
* **Center (window):**

  ```sql
  _CENTER[left,right]

  ```

  → `textaling = "center"`, `textleft = left`, `textwidth = right-left`
* **Right aligned:**

  ```nginx
  _RIGHT

  ```

  → `textaling = "right"`

---

### 4.2 Multi-line text

```css
_LINESn[padding]

```

* `n` = number of lines
* `padding` = line spacing (optional)
* Default = 1 line

✅ Examples:

```css
TXT_INPUT_TEXT[{name,AAA,20}]_LINES2[40]_CENTER
TXT_INPUT_TEXT[{tagline,BBB,30}]_LINES4[30]_RIGHT

```

Outputs:

* `"textline": "2"`
* `"linePadding": "40"`

---

5\. **Animation**
-------------

* **Position animations** automatically export `textlefteq`, `texttopeq` (or `masklefteq`, `masktopeq`).
* **Scale / Rotation / Opacity** export as:

  * `textscaleeq`, `textrotateeq`, `textalphaeq`
  * `maskscaleeq`, `maskrotateeq`, `maskalphaeq`
* Values are always translated into LYSON coordinate system (0,0 top-left, width×height canvas).
* Opacity scaled from AE `0–100` → LYSON `0–255`.

---

6\. **Audio**
---------

```php-template
AUDIO_<title>

```

* Example: `AUDIO_Happy Birthday`
* Exporter looks for `Happy Birthday.mp3|.wav|.m4a`

---

✅ Summary Table
================

Type

Naming Rule

Notes

Comp

`COMP_LYSON_<Name>`

Main template comp

User Image

`IMG_INPUT_<id>`

Auto ratio/size

Custom Mask

`IMG_INPUT_<id>_SHAPE`

Needs `<id>.png`

Static Image

`IMG_STATIC_<name>`

Exported as PNG

Dynamic Text

`TXT_INPUT_TEXT[{id,key,maxchar[,label]}]_SUFFIXES`

Placeholders inside `{}`

Static Text

`TXT_STATIC_<text>_SUFFIXES`

Fixed

Alignment

`_CENTER`, `_CENTER[left,right]`, `_RIGHT`

Horizontal alignment

Multi-line

`_LINESn[padding]`

n lines with spacing

Audio

`AUDIO_<title>`

Picks MP3/WAV/M4A
