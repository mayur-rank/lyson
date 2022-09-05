# LYSON
**Lyrical.ly  Script Object Notation** `VERSION 8.0`

## Common Notation
- **~~type~~**
   > type is always none in lyson 7.0+
  
   > `"type": "none"`

- **nophoto**
   *nophoto is max number of multiple photo need to selected*
   > `"nophoto": "6"`

- **time**
  *time mention timeline for effect and animation draw in canvas*
  > `"time": "0:0,4:2,8:0,12:0,16:0,20:18,26:0"`
  ![Sample](https://github.com/mayur-rank/lyson/blob/main/images/timeline.jpg)

- **length**
   *length is length of overlay.webm menas is length of video will be render. `In second`*
   > `"length": "26"`

- **logoplace**
  *logoplace is define position where logo will be display `Default: TR`*
  > `"logoplace": "TR`
  | Code | Position |  
  ---------|------------  
  | TR | Top, Right|  
  | BR | Bottom, Right|  
  | TL | Top, Left|  
  | BL | Bottom, Left|  
  | CC | Center |
    
  