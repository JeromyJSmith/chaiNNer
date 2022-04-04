# chaiNNer

![GitHub Latest Release](https://img.shields.io/github/v/release/joeyballentine/chaiNNer) ![GitHub Total Downloads](https://img.shields.io/github/downloads/joeyballentine/chaiNNer/total) ![License](https://img.shields.io/github/license/joeyballentine/chaiNNer) ![Discord](https://img.shields.io/discord/930865462852591648?label=Discord&logo=Discord&logoColor=white)

<p align="center">
    <img src="src/public/chaiNNer screenshot.png" width="720" />
</p>

A flowchart/node-based image processing GUI aimed at making chaining image processing tasks (especially those done by neural networks) easy, intuitive, and customizable.

No existing GUI gives you the level of customization of your image processing workflow that chaiNNer does. Not only do you have full control over your processing pipeline, you can do incredibly complex tasks just by connecting a few nodes together.

chaiNNer is also cross-platform, meaning you can run it on Windows, MacOS, and Linux.

For help, suggestions, or just to hang out, you can join the [chaiNNer Discord server](https://discord.gg/pzvAKPKyHM)

## Installation

Download the latest release from the [Github releases page](https://github.com/joeyballentine/chaiNNer/releases) and run the installer. Simple as that.

You don't even need to have Python installed, as chaiNNer will download an isolated integrated Python build on startup. From there, you can install all the other dependencies via the Dependency Manager.

If you do wish to use your system Python installation still, you will need to turn the system Python setting on, and make sure you have a version between 3.7 and 3.9. However, it is much more recommended to use the integrated Python.

## How To Use

Using chaiNNer is pretty straightforward. First make sure you have the dependencies installed through the dependency manager. You can access this via the button in the upper-right-hand corner. After installing the dependencies and restarting chaiNNer, all you have to do is drag and drop (or double click) node names in the selection panel to bring them into the editor. Then, drag from one node handle to another to connect the nodes. See the image at the top of this README for an example.

To select multiple nodes, hold down shift and drag around all the nodes you want selected. You can also select an individual node by just clicking on it. When nodes are selected, you can press backspace to delete them from the editor.

Once you have a working chain set up in the editor, you can press the green "run" button in the top bar to run the chain you have made. You will see the connections between nodes become animated, and start to un-animate as they finish processing. You can stop or pause processing with the red "stop" and yellow "pause" buttons respectively.

To batch upscale, create an Image Iterator node and drag the nodes you want to use into the iterator's editor area. You can expand the iterator by clicking and dragging the bottom right corner outwards (like you would a UI window). Simply wire up a chain in an iterator the same as you would normally, and when you click run it will run on every image in the folder you chose.

## Building chaiNNer Yourself

I provide pre-built versions of chaiNNer here on GitHub. However, if you would like to build chaiNNer yourself, simply run `npm install` to install all the nodejs dependencies, and `npm run make` to build the application.

## GPU Support

For PyTorch inference, only Nvidia GPUs are supported. If you do not have an Nvidia GPU, you will have to use PyTorch in CPU mode. This is because PyTorch only support's Nvidia's CUDA. MacOS also does not support CUDA at all, so PyTorch will only work in CPU mode on MacOS.

If you have an AMD or Intel GPU that supports NCNN however, chaiNNer now supports NCNN inference. You can use any existing NCNN .bin/.param model files (only ESRGAN-related SR models have been tested), or use chaiNNer to convert a PyTorch model to ONNX, and then convert that to NCNN (via convertmodel.com). Conversion straight from PyTorch to NCNN may come in the future, however I currently have no easy way of doing this.

## Model Architecture Support

chaiNNer currently supports a limited amount of neural network architectures. More architectures will be supported in the future.

### Pytorch

* ESRGAN (RRDBNet)
  * This includes regular ESRGAN, ESRGAN+, "new-arch ESRGAN" (RealSR, BSRGAN), SPSR, and Real-ESRGAN
* Real-ESRGAN Compact (SRVGGNet)

### NCNN

* Technically, almost any SR model should work assuming they follow a typical CNN-based SR structure, however I have only tested with ESRGAN (and its variants) and with Waifu2x

## Planned Features

**Undo History, Copy & Paste**

* For now I am having difficulty adding these in. I plan on revisiting this later after I am forced to refactor my implementation due to the node-graph library I use releasing breaking changes soon.

**Drag and Drop Images**

* This is planned, ideally for both dragging into the file selection box and onto the window to make a new image read node

**Presets**

* Some things that are common tasks should have presets you can drag in, that are basically just multiple nodes packaged together

**More SR Networks, More Image Processing Libraries**

* What the title says

**Live Updating**

* This is something that will be a bit complex to do, but basically I'd like to have a mode where it constantly is running and refreshing on any node change, and displays previews of each node

## FAQ

**What does the name mean?**

* chaiNNer is a play on the fact that you can "chain" different tasks together, with the NN in the name being a common abbreviation for Neural Networks. This is following the brilliant naming scheme of victorca25's machine learning tools (traiNNer, iNNfer, augmeNNt) which he granted me permission to use for this as well.

**Why not just use Cupscale/IEU/CLI?**

* All of these tools are viable options, but as anyone who has used them before knows they can be limited in what they can do. Many features like chaining or interpolating models are hardcoded in and provide little flexibility. Certain features that would be useful, like being able to use a separate model on the alpha layer of an image for example, just do not exist in Cupscale. Inversely, you can pretty much do whatever you want with chaiNNer provided there are nodes implemented. Whatever weird feature you want implemented, you can implement yourself by connecting nodes however you want. Cupscale also does not have other image processing abilities like chaiNNer does, such as adjusting contrast.

* This all being said however, Cupscale, IEU, CLI, or other tools are still useful for things chaiNNer currently cannot do, like running ESRGAN on video.

**Wouldn't this make it more difficult to do things?**

* In a way, yes. Similarly to how programming your own script to do this stuff is more difficult, chaiNNer will also be a bit more difficult than simply dragging and dropping and image and messing with some sliders and pressing an upscale button. However, this gives you a lot more flexibility in what you can do. The added complexity is really just connecting some dots together to do what you want. That doesn't sound that bad, right?

**What platforms are supported?**

* Windows, Linux, and MacOS are all supported by chaiNNer. However, MacOS currently lacks GPU support for pytorch, so I highly recommend using another OS if you need that functionality.