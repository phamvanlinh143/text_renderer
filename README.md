# Text Renderer
Generate text images for training deep learning OCR model (e.g. [CRNN](https://github.com/bgshih/crnn)).
Support both latin and non-latin text.

# Setup
Install dependencies:
```
pip3 install -r requirements.txt
```

The code was only tested on Ubuntu 16.04.

# Demo
By default, simply run `python3 main.py` will generate 20 text images
and a labels.txt file in `output/default/`.

![example1.jpg](./imgs/example1.jpg)
![example2.jpg](./imgs/example2.jpg)

![example3.jpg](./imgs/example3.jpg)
![example4.jpg](./imgs/example4.jpg)

# Use your own data to generate image
1. Please run `python3 main.py --help` to see all optional arguments and their meanings.
And put your own data in corresponding folder.

2. Config text effects and fraction in `configs/default.yaml` file(or create a
new config file and use it by `--config_file` option), here are some examples:

|Effect name|Image|
|------------|----|
|Origin(Font size 25)|![origin](./imgs/effects/origin.jpg)|
|Perspective Transform|![perspective](./imgs/effects/perspective_transform.jpg)|
|Random char space big|![random char space big](./imgs/effects/random_space_big.jpg)|
|Random char space small|![random char space small](./imgs/effects/random_space_small.jpg)|
|Reverse color|![reverse color](./imgs/effects/reverse.jpg)|
|Blur|![blur](./imgs/effects/blur.jpg)|
|Font size(15)|![font size 15](./imgs/effects/font_size_15.jpg)|
|Font size(40)|![font size 40](./imgs/effects/font_size_40.jpg)|
|Middle line|![middle line](./imgs/effects/line_middle.jpg)|
|Table line|![table line](./imgs/effects/line_table.jpg)|
|Under line|![under line](./imgs/effects/line_under.jpg)|

3. Run `main.py` file.

All text effect can be setted in a `yaml` config file, here are some effects example:
|Effect|Image|
|-------|----|
|Origin||


# Strict mode
For no-latin language(e.g Chinese), it's very common that some fonts only support
limited chars. In this case, you will get bad results like these:

![bad_example1](./imgs/bad_example1.jpg)

![bad_example2](./imgs/bad_example2.jpg)

![bad_example3](./imgs/bad_example3.jpg)

Select fonts that support all chars in `--chars_file` is annoying.
Run `main.py` with `--strict` option, renderer will retry get text from
corpus during generate processing until all chars are supported by a font.

# Tools
You can use `check_font.py` script to check how many chars your font not support in `--chars_file`:
```bash
python3 tools/check_font.py

checking font ./data/fonts/eng/Hack-Regular.ttf
chars not supported(4971):
['第', '朱', '广', '沪', '联', '自', '治', '县', '驼', '身', '进', '行', '纳', '税', '防', '火', '墙', '掏', '心', '内', '容', '万', '警','钟', '上', '了', '解'...]
0 fonts support all chars(5071) in ./data/chars/chn.txt:
[]
```

# Generate image using GPU
If you want to use GPU to make generate image faster, first compile opencv with CUDA.
[Compiling OpenCV with CUDA support](https://www.pyimagesearch.com/2016/07/11/compiling-opencv-with-cuda-support/)

Then build Cython part, and add `--gpu` option when run `main.py`
```
cd libs/gpu
python3 setup.py build_ext --inplace
```

# Debug mode
Run `python3 main.py --debug` will save images with extract information.
You can see how perspectiveTransform works and all bounding/rotated boxes.

![debug_demo](./imgs/debug_demo.jpg)


# Todo
See https://github.com/Sanster/text_renderer/projects/1
