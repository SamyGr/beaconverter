# beaconverter
beaconverter is a tool to switch between several CNN data types.

At the moment, it includes:
- [YOLO](https://pjreddie.com/darknet/yolo/) (You Only Look Once)
- [PascalVOC](http://host.robots.ox.ac.uk/pascal/VOC/) (Pascal Visual Object Classes)
- [COCO](https://cocodataset.org/) (COmmun Object in Context)
- [TFRecord](https://www.tensorflow.org/api_docs/python/tf/data/TFRecordDataset) (TensorFlow Record)

## Internal structure:
![code_structure](https://user-images.githubusercontent.com/72256967/124937971-292b5d00-e008-11eb-9d67-909705415115.jpg)


## Requirements
```
pip install pillow
pip install numpy
pip install tensorflow
pip install object_detection
```

## How to convert data to another type of data:
- Open example.py
- Depending on your current datatype, uncomment the necessary reader
- Adjust its inputs with directories
- Depending on datatype you want, uncomment the necessary writer
- Adjust its inputs with outputs directories

For example if you have YOLO datas and you want to convert to PascalVOC datas:
```
reader = YoloReader()
mediator = reader.translate2mediator(dataDir= './data/yolo_data/source', namesFname='./data/yolo_data/classes.names')

writer = PascalVocWriter()
writer.write(mediator=mediator, outputAnnotDir='./data/yolo_data/pascalvoc_annot/')
```

## Special cases
If you want to convert a dataset from **COCO to TFRecord**, it's strongly recommended to set enableDownload to True (in TfrecordsWriter.write).
COCO dataset is the only datas type that does not include raw images or filepaths in its structure. Therefore we have to download images from coco/flickr URL, specified in COCO annotations, to build TFRecords file.

## TO-DO:
- Handle sub-bboxs for PascalVOC reading and for all writing
