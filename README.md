
# three-dxf-loader

**three-dxf-loader** is a cross platform DXF file loader for THREE.js. It takes URL of a DXF file as input and returns THREE.js mesh entities. It internally uses dxf-parser for parsing DXF file. This library works out of the box with cross platform react-native and react-three-fiber.

#### Install
```
yarn add three-dxf-loader three
```
or
```
npm i three-dxf-loader three
```

#### Usage
```javascript
import * as THREE from 'three'
import { DXFLoader } from 'three-dxf-loader'

const loader = new DXFLoader();
// loader.setFont(font); // set fonts
loader.setEnableLayer(true); // set EnableLayer
loader.setDefaultColor(0x000000); // set DefaultColor : Default color will be applied when no color found for the entity
const scene = new THREE.Scene();
onLoad = (data) => {
    if (data?.root) {
      scene.add(data.root)
    }
}
const onError = (error) => {
  console.log(error);
}
const onProgress = (xhr) => {
  console.log( ( xhr.loaded / xhr.total * 100 ) + '% loaded' );
}
loader.load(url, onLoad, onProgress, onError);
```

#### Run Web Viewer Sample
![Example of the viewer](https://raw.githubusercontent.com/prolincur/three-dxf-loader/master/sample/data/snapshot.png "What the sample looks like")

```
# First, compile three-dxf-loader
> yarn install
> yarn build

# then install the sample's dependencies
> cd sample
> yarn install

# go back to the root and run http-server to run the sample
> cd ..
> npm install -g http-server@0.9.0
> http-server .
# use `http-server -c-1 .` to prevent caching
```

After performing the steps above, you can see the example at [http://127.0.0.1:8080/sample/index.html](http://127.0.0.1:8080/sample/index.html). You can use the DXF file included in the sample. **NOTE: the latest version of http-server will go into a redirect loop if you exclude "/index.html" from the url.**


### Supported DXF Features
Supports:
* Header
* Most LW entities (lines, polylines, circles, etc)
* Layers
* Some support for line types
* Simple Text
* Viewport
* Splines (Quadratic and Cubic)
* Ellipses
 
Does not yet support:
* Attributes
* 3DSolids
* All types of Leaders
* MText
* other less common objects and entities.

## License

[The MIT License](http://opensource.org/licenses/MIT)

