# Project Overview
The core of this project is a CrossModalClipFusionModel, a custom deep learning architecture designed for robust and stable cross-modal learning. The model takes an image and a text query as input and outputs the normalized coordinates of the bounding box for the object described in the text. The project was trained and evaluated on a custom subset of the RefCOCOg dataset, ensuring the data was compatible with the provided COCO 2014 images.

# Key Features
1. CLIP as Backbone: The model utilizes a pre-trained CLIP (ViT-B/32) model to extract powerful, semantically rich features from both images and text. The entire CLIP model is frozen during training to leverage its pre-trained knowledge efficiently.
2. Multi-Modal Fusion: A dedicated Transformer Encoder is used to effectively fuse the visual and textual features. This allows the model to learn the complex relationships between the two modalities, a critical step for accurate grounding.
3. Custom Dataset Pipeline: A custom RefCOCOgClipDataset class handles image loading, text tokenization, and bounding box normalization. A key preprocessing step was filtering the dataset to ensure all images were locally available, which resulted in 42,226 valid training samples.
4. Multi-Loss Strategy: A custom mixed loss function was implemented, combining Smooth L1 loss with an IoU loss for precise localization. This combination provides a stable and effective training objective.
5. Evaluation: The model's performance is measured using the Mean IoU (Intersection over Union) metric.

# Model Architecture
The model is built on a frozen CLIP backbone with a lightweight head for multi-modal fusion and bounding box prediction.
The CrossModalClipFusionModel: 
1. Visual & Text Encoders: Frozen CLIP encoders for efficient feature extraction.
2. Projection Layers: Linear layers to project visual and text features into a common, lower-dimensional space.
3. Transformer Fusion: A TransformerEncoder that processes the fused visual and text embeddings to create a joint representation.
4. Bounding Box Head: A small MLP with LeakyReLU activation, trained to predict the normalized (x_min, y_min, x_max, y_max) coordinates.
