# Tensorflow-object-detection-tutorial

## 安装python依赖包

	pip install pillow
	pip install lxml
	pip install jupyter
	pip install matplotlib
## The remaining libraries can be installed on Ubuntu 16.04 using via apt-get:

	sudo apt-get install protobuf-compiler python-pil python-lxml python-tk
	pip install --user Cython
	pip install --user contextlib2
	pip install --user jupyter
	pip install --user matplotlib
	
## 下载tensorflow模型

	git clone https://github.com/tensorflow/models.git

## 添加环境变量（注意当重启或关闭终端时需要重新添加）

	protoc object_detection/protos/*.proto --python_out=.
	export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim

可以把环境变量写入bashrc文件里，这样就不需要每次都添加了<br>

	echo "export PYTHONPATH=$PYTHONPATH=/home/username/models/research:home/username/models/slim">> ~/.bashrc

如果执行protoc命令出错，查看一下protoc版本
	
	protoc --version

若小于3.4，请下载源码重新编译安装一遍

If you get an error on the protoc command on Ubuntu, check the version you are running with protoc --version, <br>
if it's not the latest version, you might want to update. As of my writing of this, we're using 3.4.0. <br>
In order to update or get protoc, head to the protoc releases page. Download the python version, extract, <br>
navigate into the directory and then do: <br>

	sudo ./configure
	sudo make check
	sudo make install
	sudo ldconfig


## 安装
	
	sudo python3 setup.py install


## Install labelImg

https://github.com/tzutalin/labelImg

	Python 3 + Qt5 (Recommanded)

	sudo apt-get install pyqt5-dev-tools
	sudo pip3 install -r requirements/requirements-linux-python3.txt
	make qt5py3
	python3 labelImg.py
	python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]

收集好图像并用labelImg生成xml文件后，执行xml_to_csv.py文件,将xml文件转化为csv文件
	
	python3 xml_to_csv.py

完成后再利用csv文件生成tf record

	python3 generate_tfrecord.py --csv_input=data/train_labels.csv --output_path=data/train.record --image_dir=images/

	python3 generate_tfrecord.py --csv_input=data/test_labels.csv --output_path=data/test.record --image_dir=images/

最后一步，train.py训练

	python3 train.py --logtostderr --train_dir=training/ --pipeline_config_path=config/ssd_mobilenet_v1_pets.config


导出训练模型

	python3 export_inference_graph.py \
    	    --input_type image_tensor \
    	    --pipeline_config_path config/ssd_mobilenet_v1_pets.config \
    	    --trained_checkpoint_prefix training/model.ckpt-28144 \
    	    --output_directory traffic_light_28144
参考链接：

https://pythonprogramming.net/introduction-use-tensorflow-object-detection-api-tutorial/

https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/installation.md

