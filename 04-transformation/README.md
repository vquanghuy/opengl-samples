# 04 - Transformation

Depended libraries

* [GLFW](https://github.com/glfw/glfw)
* [GLAD](https://gen.glad.sh)
* [STB Image Loader](https://github.com/nothings/stb)
* _(new)_ [GLM](https://github.com/g-truc/glm)

Generate Xcode project file

```
cmake -G Xcode -B ./build .
```

Open project and build

```
open build/Transformation.xcodeproj/
```

In this sample, we added transformation consists model, view and projection matrix.

![ezgif-1-b81c94da5d](https://user-images.githubusercontent.com/11500792/233768076-69664e4e-221f-41b3-965c-124741f91caa.gif)

### Keynotes

* OpenGL Mathematics - GLM
* Uniform
* MVP matrix
