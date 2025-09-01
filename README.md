## Project Description & Problem Setting

### Sentinel‑2 Multiclass Land‑Cover & Cloud Classification

**Problem Setting**  
This project addresses **satellite image classification in Sentinel-2 imagery** as a **supervised multiclass classification task** using both pixel-based and patch-based approaches.  
Each pixel is represented by a 10-dimensional spectral vector (corresponding to 10 Sentinel-2 bands at 20m resolution), and labeled based on the Scene Classification Layer (SCL), which has been remapped into four meaningful land surface classes:
- `0`: Vegetation  
- `1`: Bare Soil  
- `2`: Water  
- `3`: Cloud  
- `-1`: Ignored (not used in training)

**Dataset**  
The dataset consists of 8 Sentinel-2 Level-2A scenes in `.SAFE` format. From each scene, we extract:
- 10 spectral bands at 20m resolution (`B01`, `B02`, `B03`, `B04`, `B05`, `B06`, `B07`, `B8A`, `B11`, `B12`)
- SCL masks at 20m resolution for ground truth labels

Each scene covers approximately **110km × 110km** (5490×5490 pixels at 20m resolution). After removing ignored pixels, the dataset contains **213 million labeled pixels** with the following distribution:
- Vegetation: 56.2% (119.8M pixels)
- Bare Soil: 18.2% (38.8M pixels)  
- Water: 8.9% (19.0M pixels)
- Cloud: 16.7% (35.4M pixels)

**Learning Task**  
- **Type**: Supervised multiclass classification  
- **Input**: Single pixel → 10-band spectral vector  
- **Output**: One of four land cover or cloud class labels  
- **Evaluation Metrics**: Overall accuracy, per-class precision/recall/F1, macro-averaged F1 score, confusion matrix

**Experimental Setup**  
Due to computational constraints, we work with a **stratified sample of 1 million pixels** (0.47% of total data) for model development and comparison. All models are trained on identical data splits (60% train, 20% validation, 20% test) with standardized features to ensure fair comparison.

**Project Goals**  
1. **Establish baseline performance** using pixel-based MLP to understand spectral-only classification
2. **Identify and address class imbalance** issues that affect minority classes (water and cloud)
3. **Compare pixel vs. patch approaches** to quantify the value of spatial context:
   - Pixel-based: MLP variants (baseline, regularized, weighted)
   - Patch-based: CNN, ResNet, U-Net architectures
     
4. **Analyze trade-offs** between model complexity, performance, and computational efficiency
**Key Challenges**
- **Class imbalance**: Vegetation dominates the dataset (3.3× more samples than cloud)
- **Spectral similarity**: Different land covers may have overlapping spectral signatures
- **Lack of spatial context**: Pixel-based methods ignore neighboring information
- **Scale**: Balancing computational efficiency with model performance on large-scale data

**Expected Contributions**
This project provides:
1. A systematic comparison of deep learning approaches for Sentinel-2 satellite image classification
2. Analysis of how architectural choices impact performance on imbalanced satellite data
3. Practical insights for deploying ML models on large-scale Earth observation data
4. Reproducible pipeline for multi-class classification of Sentinel-2 imagery
