# One-Pager for submission
this project is made as submission for the lecture [Intelligent Production Systems](https://mciwing.github.io/)

## Purpose
On the aereal image the following objects has to be indentified and marked with a segmentation mask.
- Buildings
- Solar plants, in most of the cases installed on building roofs

The data should be saved in a format for further anaysis in the open Source GIS software QIS.


## Dataset
The source of the aereal image is the "Autonome Provinz Bozen - Südtirol". The aereal image is aviable in a resolution of 20cm per pixel on a WMS-Service. The aereal images are aviable via the Website [MapView](https://mapview.civis.bz.it/) in this resolution and quality are made aereal images for the years:

- 'p_bz-Orthoimagery:Aerial-2011-RGB-20CM',
- 'p_bz-Orthoimagery:Aerial-2014-RGB',
- 'p_bz-Orthoimagery:Aerial-2015-RGB',
- 'p_bz-Orthoimagery:Aerial-2017-RGB',
- 'p_bz-Orthoimagery:Aerial-2020-RGB',
- 'p_bz-Orthoimagery:Aerial-2023-RGB',

To train the model 250 images are downloaded in the size 640 x 640 pixel at locations with different kinds of vegetation and building styles from the aereal image of the year 2023 using the Notebook [01_Dataset.ipynb](/01_Dataset.ipynb) and the library [owslib](https://owslib.readthedocs.io/en/latest/usage.html#wms). The annotation was done using label-studio. There are annotated the segmentation masks for the class 'roof' and 'solar'. The dataset is split randomly to 200 images for training and 50 images for validation (proportion 20/80). The total annotated aerea is 640 x 640 pixel * 0,2 m/pixel = 16.384 m² * 250 images = 4.096.000 m² = 4,1 km². In the 50 images of the validation set are present 195 instances of class roof and 73 instances of class solar.


## Model
To resolve the task training on all avialbe YOLO11 segmentation models is performed on a workstation with a Intel... CPU, 128 GB memory and two GPU Nvidia RTX A5000 with 24 GB memory each. The training is performed using the Notebook [02_Training.ipynb](/02_Training.ipynb) for 100 epochs with the default hyperparameters. In the following graph the results are shown

| model | inference time | P roof | R roof | mAP50 roof | P solar | R solar | mAP50 solar |
|-------|---------------|--------|--------|------------|-------------|---------|---------|
|yolo11n-seg|000 ms|000|000|000|000|000|000|000|
|yolo11s-seg|000 ms|000|000|000|000|000|000|000|
|yolo11m-seg|000 ms|000|000|000|000|000|000|000|
|yolo11l-seg|000 ms|000|000|000|000|000|000|000|

The precisioan (P), recal (R) and mAP50 for the model XXX are the highest, becaus the model is not used for a time critical application like a real time detection the large model can be selected for further use. In the following image a prediction on the validation dataset is shown (ground truth on the left / prediction on the right).


## Use in QGIS

for the use of the trained model in QGIS the following two ways are taken in concern. To work directly on the data and because of difficults getting the desired output fomat the second way 'PNG with world-file' is implementet for this work.

### Plugin Deepness
The QGIS pluging [Deepness]() is made for the simple usage of AI-models on geodata. The model has to be made in ONNX format and give as output a tensor with shape [n_classes, width, height]. the plugin applies the model on a given input layer in raster format and save the segmentation masks as polygons.

### PNG with world-file
There are defined two simple functions in [xxx](xxx) to perform the following tasks:

- download the image from wMS service and save the world-file, a standardized file with information abaut the location of the image in a directory. the areal image can be eather stored in the same directory or returned as PIL image for further processing
- make prediction with a given yolo-model and PIl image as input and store the prediction as png file

The png files then can be loaded in QGIS for furth processing and analyzing. On the example image below the proportion of bebaung for the whole area of the 'Marktgemeinde Lana' is visualized.





## Problems and  Improvements
There are the following improvements wich can be optimized in further work

- xxx
- xxx
- xxx 



## Ergebnis

Bei 'RUN_6' werden viele Obstplantagen als 'Solar' erkannt. Vermutlich weil ein ähnliches Streifenmuster oder Raster erkannt wird. Bei der Auswahl der Trainingsdaten mit Ausreichend Beispielen und Negativbeispielen zu berücksichtigen.




## Probleme
Teilweise nicht perfekt von oben, auch fassaden ersichtlich > was wird markiert? nur die dachfläche oder generell das Gebäude? Im vorliegenden Fall das Gebäude
Grundsätzlich sehr verschiedene Oberflächen und strukturen, Satteldach mit Ziegeln bis hin zu begrünten falchdach. Letzteres schwierig von wiese zu unterscheiden. Bei Solaranlagen ist struktur grundsötzlich ähnlicher, kommt weniger oft vor.
Obstwiesen oder Straßen werden teilweise erkannt, negativbeispiele ergänzen.

## Links
- [Webseite zur Lehrveranstaltung](https://mciwing.github.io/)
- [Arbeiten mit virtuellen Umgebung](https://mciwing.github.io/python/packages/)
- [MapView - Darstellung und Download der Orthofotos](https://mapview.civis.bz.it/)


