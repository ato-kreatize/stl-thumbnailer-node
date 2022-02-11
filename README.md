# stl-thumbnailer-node

Create thumbnails from 3D STL files. Creates beautifully rendered PNG and JPEG images, server-side, with no GPU, from
ASCII and Binary STLs.

> This code is forked from [`node-stl-to-thumbnail`](https://github.com/fakhrullah/node-stl-to-thumbnail) by fakhrullah to update packages and improve rendering.

## Installation

```npm i -s stl-thumbnailer-node```

## Usage

The following snippet loads a file from the current directory (```./input.stl```), and creates a 500x500 png thumbnail
in the current directory called ```./output.png```.

```javascript
const StlThumbnailer = require('stl-thumbnailer-node');
const fs = require('fs');

const thumbnailer = new StlThumbnailer({
  filePath: __dirname + "/input.stl",
  requestThumbnails: [
    {
      width: 500,
      height: 500
    }
  ]
}).then(function (thumbnails) {
  // thumbnails is an array (in matching order to your requests) of Canvas objects
  // you can write them to disk, return them to web users, etc
  // see node-canvas documentation at https://github.com/Automattic/node-canvas
  thumbnails[0].toBuffer(function (err, buf) {
    if (err) return console.error(err);
    
    fs.writeFileSync(__dirname + "/output.png", buf);
  })
})
```
