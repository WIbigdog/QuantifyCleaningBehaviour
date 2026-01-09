# Model Card: Multi-Animal Fish Pose Estimation (Front-View)

## Model Details
- **Model type:** Multi-animal pose estimation
- **Framework:** DeepLabCut v2.2.3 (TensorFlow)
- **Architecture:** ResNet-50 with multi-stage refinement (dlcrnet_ms5)
- **Initialization:** ImageNet-pretrained ResNet-50
- **Training type:** Transfer learning
- **Model version:** v1.0
- **Date trained:** 2024

---

## Task
This model performs multi-animal pose estimation from video, detecting and tracking predefined body parts of a cleaner fish (*Labroides dimidiatus*) and a client fish from front-view aquarium recordings.  
The model outputs 2D coordinates and confidence (likelihood) scores for each body part in every video frame.

---

## Data

### Species
- Cleaner fish: *Labroides dimidiatus*
- Client fish: multiple species (treated as a single class)

### Recording setup
- Fixed front-view camera
- Controlled laboratory aquarium conditions
- Video resolution: 1920 × 1080 pixels

### Dataset size
- 6 videos
- Approximately 400 manually annotated frames

### Annotations
- 14 body parts total

### Train/test split
- 95% training / 5% testing (DeepLabCut default split)
- Splitting performed at the frame level
- The small size of the test set limits robust generalization assessment

---

## Training

- **Batch size:** 8
- **Input processing:**  
  - Hybrid cropping (400 × 400 px)  
  - Data augmentation including rotation, contrast adjustment, CLAHE, and scaling
- **Optimizer:** Adam
- **Learning rate schedule:**  
  - 0.0005 initial  
  - 0.0001 at 7,500 iterations  
  - 0.00005 at 12,000 iterations  
  - 0.00001 at 200,000 iterations

---

## Metrics

Model performance was evaluated using DeepLabCut’s standard metrics:
- Mean pixel error on training and test sets
- Confidence (likelihood) scores per body part
- Visual inspection of predicted poses and identity consistency

The model achieves low pixel error on held-out frames and shows stable identity assignment under typical experimental conditions.

---

## Intended Use
- Quantitative analysis of fish behavior in laboratory experiments
- Automated extraction of movement and interaction metrics
- Research in behavioral ecology and ethology

---

## Limitations
- Trained exclusively on front-view recordings; performance may degrade for top-view or angled cameras
- Optimized for controlled laboratory lighting and backgrounds
- Client fish include multiple species and morphologies, which may reduce precision for uncommon body shapes
- Performance decreases under strong occlusion, motion blur, or overlapping individuals
- Not validated for species, environments, or viewpoints outside the training data
- Small test set limits statistical robustness of performance estimates

---

## Ethical Considerations
- Based on non-invasive video recordings
- No physical interaction with animals
- Supports automated behavioral analysis, reducing observer bias and manual handling
- Users should avoid applying the model outside validated conditions, as this may lead to misleading behavioral interpretations

---

## Out-of-Scope Use
- Real-time welfare monitoring without additional validation
- Application to non-fish species or uncontrolled environments
- Use as a standalone decision-making system without human verification
