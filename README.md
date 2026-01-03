# Amazon Product Attribute Extraction

This project focuses on extracting product attributes (such as weight, dimensions, voltage, wattage, and volume) from Amazon product images using Optical Character Recognition (OCR) and computer vision techniques.

## Project Overview

The goal is to automatically extract structured product information from images, which is crucial for e-commerce platforms like Amazon to maintain accurate product catalogs and improve search functionality.

## Dataset

The dataset consists of:
- **Training Data** (`dataset/train.csv`): Contains image links, group IDs, entity names, and their corresponding values
- **Test Data** (`dataset/test.csv`): Contains image links, group IDs, and entity names (values to be predicted)
- **Sample Data** (`dataset/sample_test.csv`): Small sample for testing and development

### Entity Types
- `item_weight`: Product weight (gram, kilogram, etc.)
- `item_volume`: Product volume (litre, millilitre, etc.)
- `height`: Product height
- `width`: Product width
- `depth`: Product depth
- `voltage`: Electrical voltage
- `wattage`: Power consumption
- `maximum_weight_recommendation`: Maximum recommended weight

### Submission Format
Predictions should be submitted as a CSV file with columns:
- `index`: Corresponding to the test data index
- `prediction`: The predicted entity value (e.g., "500.0 gram") or empty string if not found

## Technologies Used

### OCR Engines
- **EasyOCR**: For general text extraction from images
- **Tesseract**: Google's OCR engine for text recognition
- **TrOCR**: Microsoft's Transformer-based OCR models (both printed and handwritten variants)

### Libraries
- Python 3.x
- Pandas, NumPy for data manipulation
- PIL (Pillow) for image processing
- Requests for image downloading
- Jupyter Notebooks for experimentation

## Project Structure

```
├── dataset/                 # Training and test datasets
│   ├── train.csv
│   ├── test.csv
│   ├── sample_test.csv
│   ├── sample_test_out.csv
│   └── sample_test_out_fail.csv
├── images/                  # Downloaded product images
├── src/                     # Source code
│   ├── constants.py         # Entity-unit mappings and allowed units
│   ├── utils.py             # Utility functions for parsing and image processing
│   ├── sanity.py            # Validation script for submission format
│   ├── trocr/               # TrOCR model files (printed text)
│   └── trocr_hand/          # TrOCR model files (handwritten text)
├── tesseract/               # Tesseract-related notebooks
├── .conda/                  # Conda environment configuration
└── *.ipynb                  # Jupyter notebooks for various experiments
```

## Setup and Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd amazon-product-extraction
   ```

2. **Create Conda Environment**
   ```bash
   conda env create -f environment.yml  # If available
   # or
   conda create -n amazon-ocr python=3.8
   conda activate amazon-ocr
   ```

3. **Install Dependencies**
   ```bash
   pip install pandas numpy pillow requests tqdm easyocr opencv-python
   # Additional packages as needed for specific OCR engines
   ```

## Usage

1. **Download Images**
   Run the image downloading scripts to fetch product images from Amazon.

2. **Extract Text**
   Use the OCR notebooks to extract text from images:
   - `Easyocr.ipynb` - EasyOCR implementation
   - `tess.ipynb` - Tesseract implementation
   - TrOCR models in the respective directories

3. **Process and Validate**
   Use `utils.py` functions to parse extracted text into structured entity values.

4. **Generate Predictions**
   Create your model predictions in the required CSV format.

5. **Validate Submission**
   ```bash
   python src/sanity.py --test_filename dataset/sample_test.csv --output_filename your_predictions.csv
   ```

## Notebooks Overview

- `DownloadImg.ipynb`: Image downloading utilities
- `Easyocr.ipynb`: EasyOCR text extraction experiments
- `tess.ipynb`: Tesseract OCR experiments
- `spatial.ipynb`, `spatial2.ipynb`: Spatial analysis of text in images
- `merge.ipynb`: Data merging and processing
- Various data cleaning and preprocessing notebooks

## Validation

Use the `sanity.py` script to validate your predictions:
- Checks CSV format compliance
- Validates entity value parsing
- Ensures all required indices are present

## Evaluation

The project evaluates performance on extracting accurate entity values from product images, handling various formats, units, and OCR challenges.

## Contributing

This appears to be a research/experimentation project with multiple approaches tested for optimal product attribute extraction from images.

## License

Please refer to the original dataset source for licensing information.