
# Cat and Dog Detection using Darknet/Yolov3-tiny

This project aims to detect cats and dogs using the Darknet/Yolov3-tiny model. The dataset is created by downloading images from the internet using DuckDuckGo and labeling them using Label Studio.

## Installation

### Darknet

To install Darknet on Linux (Debian based) run the following commands:

```bash
sudo apt-get install build-essential git libopencv-dev
mkdir ~/src
cd ~/src
git clone https://github.com/hank-ai/darknet.git
cd darknet
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make -j4 package
sudo dpkg -i darknet-*.deb
```
As suggested in [the yolo FAQ](https://www.ccoderun.ca/programming/yolo_faq/#how_to_build_on_linux). It is strongly recommended to have a GPU for training custom YOLO neural networks. You can always use Google Colab's GPU capabilities if you don't have the hardware available.

### DuckDuckGo Search and Label Studio

To install the required packages for downloading images and labeling them, run the following commands:

```bash
pip install duckduckgo-search
pip install label-studio
```

## Dataset Creation

In the provided Jupyter notebook, images are downloaded from the internet using DuckDuckGo and saved into the `dataset` folder. The images are then labeled using Label Studio and redownloaded in the dataset/images folder alongside their annotations.


## Usage

1. Run the Jupyter notebook to download images:
    ```bash
    jupyter notebook cat-dog-dataset-extractor.ipynb
    ```

2. Label the images using Label Studio:
    ```bash
    label-studio
    ```

3. To improve training time, it is important to resize the images and set their quality, which can be done in Linux running the following commands (within the folder that contains the images):
    ```bash
    sudo apt install imagemagick
    mogrify -verbose -strip -resize 416x416! -quality 75 *.jpg
    ```

4. Train the custom neural network by running:
    ```bash
    darknet detector -map -dont_show train ~/nn/animals/cat-dog.data ~/nn/animals/cat-dog.cfg
    ```


## Acknowledgements

- [Darknet](https://github.com/hank-ai/darknet)
- [DuckDuckGo Search](https://pypi.org/project/duckduckgo-search/)
- [Label Studio](https://labelstud.io/)
