# References
1. https://docs.nvidia.com/deeplearning/sdk/tensorrt-install-guide/index.html
2. https://medium.com/tensorflow/speed-up-tensorflow-inference-on-gpus-with-tensorrt-13b49f3db3fa
3. https://3sidedcube.com/guide-retraining-object-detection-models-tensorflow/
4. https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/running_pets.md
5. https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/challenge_evaluation.md
6. https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/oid_inference_and_evaluation.md

# Install TensorRT 4.x.x
~~~~
sudo dpkg -i nv-tensorrt-repo-ubuntu1604-cuda9.0-ga-trt4.0.1.6-20180612_1-1_amd64
sudo apt-get update
sudo apt-get install -y tensorrt
sudo apt-get install -y python-libnvinfer-doc
sudo apt-get install -y uff-converter-tf

pip install -U --user tensorflow_gpu-1.10.0-cp27-none-linux_x86_64.whl
~~~~

# Install TensorRT 3.x.x
~~~~
sudo dpkg -i nv-tensorrt-repo-ubuntu1604-ga-cuda9.0-trt3.0.4-20180208_1-1_amd64-deb
sudo apt-get update
sudo apt-get install -y tensorrt
sudo apt-get install -y python-libnvinfer-doc
sudo apt-get install -y uff-converter-tf

pip install -U --user tensorflow_gpu-1.10.0-cp27-none-linux_x86_64.whl
~~~~
