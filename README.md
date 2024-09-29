
SkiaSharp 是一个跨平台的 2D 图形 API，用于 .NET 平台，基于 Google 的 Skia 图形库。它提供了全面的 2D API，可以在移动、服务器和桌面模型上渲染图像。SkiaSharp 可以在多个 .NET 平台上使用，包括 ASP.NET Core、WPF、Winform、MAUI、AvaloniaUI 和 Uno。

Skia是个2D向量图形处理函数库，包含字型、座标转换，以及点阵图都有高效能且简洁的表现。不仅用于Google Chrome浏览器， Android开放手机平台也采用Skia作为绘图处理，搭配OpenGL/ES与特定的硬体特征，强化显示的效果

自2005年Skia被Google收购后，一直相当神秘低调，直到2007年初，Skia GL相关的源代码才被揭露，作为Google Android平台的图形引擎，稍后的Google Chrome浏览器也采用Skia引擎。随着Android与Chrome (开源版本称为"Chromium")两大平台公布源代码后，skia也一并公开源代码，以Apache License v2发布(注意，这意味着与GPLv2授权不相容) ，而Android与Chrome的代码库中都有一份\[skia]的复制，因需求不同，做了部份的修改，比方说Chrome专案底下的 \[chrome/trunk/src/skia]，需要注意的是，Skia本身是不涉及底层环境，如Linux Framebuffer或Gtk\+衔接的处理，这也是何以Android (通过Linux Framebuffer)与Chrome (开发中的Linux版本使用Gtk\+)需要提供一份修改，以便系统接轨。

SkiaSharp是一个强大跨平台绘图框架，可以用SkiaSharp在WPF、安卓Xamarin.Forms客户端绘图，也可以用于创建PDF绘图，但是由于它不支持网页绘图，所以总觉得很遗憾，因为目前主流的浏览器都是谷歌Chrom内核，谷歌为什么不支持自家的Skia在网页直接绘图呢？如果SkiaSharp可以直接在网页绘图（Blazor webassembly），那它就是跨越全平台的绘图框架了。终于到了2021年10月12日，.NET 6发布RC2候选版本（正式发布前最后一版），宣布了一个突破性的技术：支持在Web网页上采用SkiaSharp画布绘图。这是.NET跨平台技术发展的一个创举，使用C\#可以直接在网页画布上绘图，打破了JavaScript\+canvas的长期垄断地位。C\#是强类型语言，可以无缝对接从服务端获取的结构化数据，有效提高开发效率和质量。


> [ASP.NET Core updates in .NET 6 Release Candidate 2 \- ASP.NET Blog (microsoft.com)](https://github.com)
> 
> SkiaSharp is a cross\-platform 2D graphics library for .NET based on the native Skia graphics library, and it now has preview support for Blazor WebAssembly. Let’s give it a try!

在 MAUI 中，SkiaSharp 是通过 Microsoft.Maui.Graphics 库使用的。Microsoft.Maui.Graphics 是一个跨平台的图形库，它使用 SkiaSharp 作为底层渲染引擎来提供一致的 API 访问本机图形功能。这意味着开发者可以在 MAUI 应用中使用 SkiaSharp 来绘制形状、文本和保存图像。此外，SkiaSharp 还可以用于创建自定义控件，例如在 MAUI 中绘制可定制颜色和角度的轮盘或圆饼图。

对于 Uno 平台，SkiaSharp 也可以集成到 Uno 中。开发者可以通过添加 NuGet 包 "SkiaSharp" 到共享类库，并在 XAML 中添加 SkXamlCanvas 控件来使用 SkiaSharp。然而，有时可能会遇到编译问题，需要确保找到正确的命名空间。

AvaloniaUI 默认使用 Skia 渲染引擎，这是因为 AvaloniaUI 的架构设计中包含了 SkiaSharp，为了提高图形渲染性能，AvaloniaUI 在其合成渲染器中增强了图形渲染能力，并且引入了 GPU 互操作功能，这使得 Avalonia 能够与 GPU 更高效地工作，从而提高渲染性能和视觉效果,然而，需要注意的是，AvaloniaUI 使用的 Skia 是一个有限的 Skia 子集，用于 Avalonia 运行所必需的功能，不包括图像处理、图像元数据和图像解码等功能。对于需要多用途图像处理的开发者来说，SkiaSharp 是更好的选择。在使用 SkiaSharp 3\.0 时，开发者需要手动包含目标平台的 NativeAssets 包.

SkiaSharp 在 MAUI、AvaloniaUI 和 Uno 中都有广泛应用，并且通过 Microsoft.Maui.Graphics 提供了一致的跨平台图形渲染能力。在不同的 .NET 平台（如 MAUI、AvaloniaUI 和 Uno）中都提供了高性能的图形渲染能力，但在移动设备上可能需要额外的优化以避免性能问题。SkiaSharp 的性能表现如下：

1. **AvaloniaUI**：Avalonia 使用 SkiaSharp 作为其渲染引擎，能够实现高性能的图形渲染，并在不同操作系统上实现一致的用户界面。然而，有观点认为 Avalonia 由于基于 Skia，可能会在移动设备上遇到性能问题。
2. **MAUI**：在 MAUI 中，Microsoft.Maui.Graphics 和 SkiaSharp 都是重要的库，它们为开发者提供了强大的图形绘制能力。MAUI 专为提高性能而设计，通过在原生平台控件上实现一种精简的、解耦的处理程序映射器模式，减少了 UI 渲染中的开销。
3. **Uno**：SkiaSharp 与 Uno Platform 的比较中，SkiaSharp 被描述为一个跨平台的 2D 图形 API，适用于 .NET 平台，提供了全面的 2D API，可以用于移动、服务器和桌面模型来渲染图像。

应用场景上来说，它适用于多种应用场景，包括但不限于：

* **绘图工具**：SkiaSharp 可以用于开发各种绘图工具，如富文本编辑器、图像绘制工具等。例如，可以使用 SkiaSharp 创建一个功能强大的绘图工具，支持复杂的图形绘制和编辑功能。
* **报表制作**：在报表开发中，SkiaSharp 可以用于生成高质量的报表图像，支持多种数据格式和布局需求。
* **图像生成**：SkiaSharp 可以用于生成各种图像，如验证码、二维码等。例如，可以使用 SkiaSharp 生成用于身份验证的二维码。
* **用户界面绘制**：在用户界面设计中，SkiaSharp 可以用于绘制复杂的图形和动画效果。例如，可以使用 SkiaSharp 在 WPF 应用程序中实现自绘的弹动小球、粒子花园等特效。
* **游戏开发**：SkiaSharp 可以用于开发简单的游戏，如投篮小游戏，通过自绘实现游戏中的动画和交互效果。
* **PDF 绘图**：SkiaSharp 还可以在 PDF 上进行绘图，支持在多种平台上生成 PDF 文件中的图形内容。
* **跨平台应用**：由于 SkiaSharp 是跨平台的，因此可以在 Windows、Linux、Android、iOS 等多个平台上使用，支持在不同设备上渲染图像和图形。
* **开源项目**：SkiaSharp 被广泛应用于各种开源项目中，如 Kimono 设计器，支持以图形化的方式创建二维图片，并生成跨平台的代码


 本博客参考[西部世界官网](https://tianchuang88.com)。转载请注明出处！
