# References
1. https://docs.nvidia.com/deeplearning/sdk/tensorrt-install-guide/index.html
2. https://medium.com/tensorflow/speed-up-tensorflow-inference-on-gpus-with-tensorrt-13b49f3db3fa

# Install TensorRT
~~~~
sudo dpkg -i nv-tensorrt-repo-ubuntu1604-cuda9.0-ga-trt4.0.1.6-20180612_1-1_amd64
sudo apt-get update
sudo apt-get install -y tensorrt
sudo apt-get install -y python-libnvinfer-doc
sudo apt-get install -y uff-converter-tf

~~~~
