# Hello Triangle

Depended libraries

* GLFW
* GLAD

Generate Xcode project file

```
cmake -G Xcode -B ./build .
```

Open project and build

```
open build/HelloTriangle.xcodeproj/
```

In this sample, we added the loader for shaders and link them to a single program, and use it to render the coloful triangle

<img width="752" alt="Screenshot 2023-04-15 at 14 08 50" src="https://user-images.githubusercontent.com/11500792/232194512-158d26f1-26cb-4f8c-8d13-644e08bb4e3d.png">

## Keynotes

* Shader
* Program
* VAO and VBO
