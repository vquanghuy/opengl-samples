# Texture Mapping

Depended libraries

* GLFW
* GLAD
* _(new)_ [STB Image Loader](https://github.com/nothings/stb)

Generate Xcode project file

```
cmake -G Xcode -B ./build .
```

Open project and build

```
open build/TextureMapping.xcodeproj/
```

In this sample, we added a texture loader to load an image and put to a rectangle.

<img width="752" alt="Screenshot 2023-04-22 at 09 40 37" src="https://user-images.githubusercontent.com/11500792/233758103-84081660-7aba-4d9f-86ef-691cde66ceec.png">

### Keynotes

* Image loader
* Texture, texture coordinates
* Uniform
* Sampler2D
* `glDrawElements` and EBO (element buffer object) / IBO (index buffer object)
