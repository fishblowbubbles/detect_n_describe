# detect_n_describe

### Object Detection With Tiny YOLOv3

This project uses Joseph Redmon's [darknet](https://github.com/pjreddie/darknet).
Custom weights (`backup/tiny_6`) were trained on a subset of the [Open Images V4](https://storage.googleapis.com/openimages/web/index.html) dataset, to detect the following classes:

1. Handgun
2. Hat
3. Jacket
4. Knife
5. Rifle
6. Sunglasses

Relative paths to metafiles are:
`.data` - `cfg/custom.data`
`.cfg` - `cfg/custom.cfg`
`.weights` - `backup/tiny_6/custom_22000.weights` (best)

In `Makefile`, `GPU=1` and `OPENCV=1` by default, however `cuda` and `OpenCV` must be installed. Otherwise, set to `0` as required and run `make`. Detailed instructions can be found [here](https://pjreddie.com/darknet/yolo/).

If compilation fails, run `export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}` before `make` (edit `cuda` version accordingly).

To prepare training and validation datasets, use `utilities.ipynb`. During training, checkpoints are saved in `backup` every 100 iterations for the first 1000 iterations, and subsquently at intervals of 1000 iterations. You can change this behaviour in `examples/detector.c`.

**To train** - `./darknet detector train {path to .data} {path to .cfg} {path to .weights}` <br/>
**To test** - `./darknet detector test {path to .data} {path to .cfg} {path to .weights}` <br/>
**To demo (video)** - `./detector detector demo {path to .data} {path to .cfg} {path to .weights} {path to video file}` <br/>

At test/demo, add arguments `-thresh {% / 100}` to adjust confidence threshold (default is `o.5`).
