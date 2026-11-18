# Potato Leaf Disease Classification using VGG16

Classification of potato leaf diseases (healthy, early blight, late blight) from the
PlantVillage dataset, comparing a small CNN baseline with VGG16 transfer learning.

# Team
- Aakash
- Rakshit
- Nikhil

## Dataset
PlantVillage (potato classes only): healthy, early_blight, late_blight.
Not included in this repo because of its size. Download:
git clone --depth 1 --filter=blob:none --sparse https://github.com/spMohanty/PlantVillage-Dataset

Split: 70% train / 15% validation / 15% test (stratified).
Test set: 323 images (23 healthy, 150 early blight, 150 late blight).

## What is done
- Dataset pipeline, class distribution analysis and OpenCV preprocessing
- Small CNN baseline
- VGG16 transfer learning
- VGG16 with data augmentation (flip, rotation, zoom, contrast)
- Evaluation: accuracy, precision, recall, F1, confusion matrices, correct/wrong prediction samples

## Training settings
Image size 224x224, batch size 32, Adam (learning rate 0.001), class weights for imbalance.
Epochs: CNN 10, VGG16 5, VGG16 + aug 5.

## Results (test set, macro-averaged)

| Model | Accuracy | Precision | Recall | F1 |
|-------|----------|-----------|--------|----|
| Small CNN | 0.9195 | 0.8723 | 0.9422 | 0.8959 |
| VGG16 | 0.9814 | 0.9548 | 0.9867 | 0.9695 |
| VGG16 + aug | 0.9567 | 0.9133 | 0.9689 | 0.9369 |

Observations:
- VGG16 is the best model: 317 of 323 test images correct.
- The small CNN confuses late blight with early blight and healthy (26 of 150 late blight images wrong).
- Augmentation did not improve results with only 5 epochs of training.
- The healthy class has only 23 test images, so its precision is sensitive to a few errors.
- VGG16 errors are mostly leaves with small or faint lesions.

Confusion matrices and prediction samples are in the notebook outputs.

## How to run
Open notebooks/plant_disease_vgg16.ipynb and run the cells in order.
Paths use Kaggle locations (/kaggle/working/...). Change them if you run it elsewhere.
Libraries: TensorFlow, OpenCV, scikit-learn, matplotlib, pandas, PIL.

## Remaining work
- [e.g. fine-tune VGG16 layers, train augmentation for more epochs, final report]
