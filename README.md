# cimgui.zig
> [!NOTE]
> This is a fork of [tiawl/cimgui.zig][1] with added [wgpu-native][15] support

### cimgui.zig as a library
If you want to add `cimgui.zig` as a library to your project, you can do the following (do know that it requires a zig version `>0.13`) :

Fetch this repository :
```sh
$ zig fetch --save git+https://github.com/tiawl/cimgui.zig
```

Add it to your `build.zig` :
```diff
const std = @import("std");
+const cimgui = @import("cimgui_zig");

pub fn build(b: *std.Build) void {
    // -- snip --

+    const cimgui_dep = b.dependency("cimgui_zig", .{
+        .target = target,
+        .optimize = optimize,
+        .platform = cimgui.Platform.GLFW,
+        .renderer = cimgui.Renderer.Wgpu,
+    });

    // Where `exe` represents your executable/library to link to
+    exe.linkLibrary(cimgui_dep.artifact("cimgui"));

    // -- snip --
}
```

And that's it ! You're ready to go ! See the `examples` directory on how to move forward from there.

## Backends
The backends are separated in two categories : the platforms (handling windows, events, ...) and the renderers (draw to screen, ..).

### Platform
  - [GLFW][4]
  - [SDL3][11]
  - [SDLGPU3][11] (technically a renderer but needs linkage againt OpenGL/Vulkan)

### Renderers
  - [Vulkan][5]
  - [OpenGL][12]
  - [WGPU][15]

> As you can see, these backends do not support all of those supported by ImGUI. Adding a backend is a bit of work because of the needed *maintenance*. Please do not ask for backends to be added if you don't feel like adding them yourselves !

## Dependencies

The [Zig][2] part of this package is relying on the latest [Zig][2] release (0.14.1) and will only be updated for the next one (so for the 0.15.0).

Here the repositories' version used by this fork:
* [ocornut/imgui](https://github.com/tiawl/cimgui.zig/blob/trunk/.references/imgui)

Currently there are no tags/release for [dearimgui/dear_bindings][3] so **cimgui.zig** is relying on the last commit.

For backends see [the build.zig.zon](https://github.com/tiawl/cimgui.zig/blob/trunk/build.zig.zon)

## CICD reminder

These repositories are automatically updated when a new release is available:
* [tiawl/spaceporn][6]

This repository is automatically updated when a new release is available from these repositories:
* [ocornut/imgui][1]
* [dearimgui/dear_bindings][3]
* [tiawl/toolbox][7]
* [tiawl/vulkan.zig][8]
* [tiawl/glfw.zig][9]
* [castholm/SDL][13]
* [castholm/zigglgen][14]

## `zig build` options

These additional options have been implemented for maintainability tasks:
```
  -Dfetch=[bool]               Update .references folder and build.zig.zon then stop execution
  -Dupdate=[bool]              Update binding
  -Drenderer=[enum]            Specify the renderer backend
                                 Supported Values:
                                   Vulkan
                                   OpenGL3
  -Dplatform=[enum]            Specify the platform backend
                                 Supported Values:
                                   GLFW
                                   SDL3
                                   SDLGPU3
```

## License

This repository is not subject to a unique License:

The parts of this repository originated from this repository are dedicated to the public domain. See the LICENSE file for more details.

**For other parts, it is subject to the License restrictions their respective owners choosed. By design, the public domain code is incompatible with the License notion. In this case, the License prevails. So if you have any doubt about a file property, open an issue.**

[1]:https://github.com/tiawl/cimgui.zig
[2]:https://github.com/ziglang/zig
[3]:https://github.com/dearimgui/dear_bindings
[4]:https://github.com/glfw/glfw
[5]:https://github.com/KhronosGroup/Vulkan-Headers
[6]:https://github.com/tiawl/spaceporn
[7]:https://github.com/tiawl/toolbox
[8]:https://github.com/tiawl/vulkan.zig
[9]:https://github.com/tiawl/glfw.zig
[10]:https://github.com/tiawl/spaceporn/blob/trunk/src/spaceporn/bindings/imgui/imgui.zig
[11]:https://wiki.libsdl.org/SDL3/FrontPage
[12]:https://www.opengl.org/
[13]:https://github.com/castholm/SDL
[14]:https://github.com/castholm/zigglgen
[15]:https://github.com/gfx-rs/wgpu-native
