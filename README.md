# Tensorflow-object-detection-tutorial

## 其他的python依赖包

	pip install pillow
	pip install lxml
	pip install jupyter
	pip install matplotlib

## 下载tensorflow模型

	git clone https://github.com/tensorflow/models.git

## 添加环境变量（注意当重启或关闭终端时需要重新添加）

	protoc object_detection/protos/*.proto --python_out=.
	export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim

可以把环境变量写入bashrc文件里，这样就不需要每次都添加了<br>

	echo "export PYTHONPATH=$PYTHONPATH=/home/username/models/research:home/username/models/slim">> ~/.bashrc

If you get an error on the protoc command on Ubuntu, check the version you are running with protoc --version, <br>
if it's not the latest version, you might want to update. As of my writing of this, we're using 3.4.0. <br>
In order to update or get protoc, head to the protoc releases page. Download the python version, extract, <br>
navigate into the directory and then do: <br>

	sudo ./configure
	sudo make check
	sudo make install
	sudo ldconfig

# Tensorflow object-detection-tutorial

## Clone github repositories 
	
	git clone https://github.com/dj140/Tensorflow.git

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
