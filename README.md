
---

### README.md

```markdown
# Lacuna Malaria Detection Model

This project builds a convolutional neural network (CNN) model named `lacunamodel` to classify images for malaria detection using Keras and TensorFlow. Due to limited data availability, we use various data augmentation techniques to artificially expand the dataset and improve model generalization.

## Project Structure

```
data/
├── Phase A/                # Original images only
│   ├── train/
│   └── test/
├── Phase B/                # Augmented with rotation
│   ├── train/
│   └── test/
├── Phase C/                # Augmented with flipping
│   ├── train/
│   └── test/
...
├── Phase J/                # Augmented with cropping and padding
│   ├── train/
│   └── test/
```

- **data**: Contains the folders Phase A through Phase J. Each phase contains train and test subfolders.

## Steps

### 1. Data Augmentation (`augment.py`)

The `augment.py` script augments the dataset by applying different transformations to the images in folders `Phase B` through `Phase J`. Here’s a breakdown of each phase and the augmentation techniques used:

- **Phase A**: Contains the original, unaltered images as a control group.
  
- **Phase B**: **Rotation** – Images are rotated by a random angle between -20 and 20 degrees. This augmentation simulates slight orientation variations in microscope images.

- **Phase C**: **Horizontal Flip** – Images are flipped horizontally. This augmentation is useful for creating mirror-image versions of the original samples, which can enhance the model’s ability to generalize.

- **Phase D**: **Zoom** – Images are randomly zoomed in by 10-20%. This simulates varying levels of magnification, which can help the model detect features at different scales.

- **Phase E**: **Brightness Adjustment** – Brightness is randomly adjusted, creating both darker and brighter versions. This emulates different lighting conditions that may be encountered in lab environments.

- **Phase F**: **Contrast Adjustment** – Contrast is altered to generate images with both high and low contrast. This helps the model learn to detect features across varying contrasts in microscope images.

- **Phase G**: **Gaussian Noise** – Random noise is added to images. This augmentation simulates sensor noise, which is often present in imaging devices.

- **Phase H**: **Blur** – A slight Gaussian blur is applied. This mimics the natural blurring that can happen in microscopy images due to focus adjustments.

- **Phase I**: **Color Jitter** – Random changes to the hue and saturation create slight color variations. This can help the model be more robust to minor color changes in sample preparation.

- **Phase J**: **Random Cropping and Padding** – Random cropping followed by padding. This ensures that the model can handle partially cropped or slightly shifted images and learn to focus on the central features.

To apply these augmentations, run:

```bash
python augment.py
```

This script generates augmented images in each phase folder as specified above.

### 2. Train-Test Splitting (`split.py`)

The `split.py` script splits images in each phase folder into `train` and `test` sets, following a 75%-25% ratio, ensuring that each phase has separate data for training and testing.

- **Phase A**: Contains the original images split into `train` and `test` sets.
- **Phases B-J**: Each contains augmented images split into `train` and `test` sets.
  
To split the data into `train` and `test` subfolders, run:

```bash
python split.py
```

### 3. Model Creation and Training (`model.py`)

The `model.py` script contains a CNN model named `lacunamodel`, built using Keras and TensorFlow, to classify images as part of the malaria detection task.

- **Model Architecture**: The CNN consists of multiple convolutional, pooling, and dense layers. It is designed for binary classification.
- **Training**: The model is trained using images in the `train` and `test` subfolders created in each phase folder.
  
To train the model, run:

```bash
python model.py
```

The model will load the augmented and split data from `dataset10` and begin training on the prepared dataset.

## Requirements

Install the required packages using the following command:

```bash
pip install -r requirements.txt
```

### Notes

- **Data Augmentation**: Augmentations are only applied to Phases B-J, while Phase A remains the original dataset.
- **Train-Test Split**: Each phase has a separate `train` and `test` set to maintain consistent validation.
- **Model Evaluation**: After training, the model’s performance is evaluated on the test data for validation.

---

This `README.md` provides a structured explanation of the project flow without duplicating code. Below is the `requirements.txt` file to ensure the environment dependencies are met.

---
