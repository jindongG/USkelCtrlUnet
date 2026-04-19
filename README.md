# USkelCtrlNet: Skeleton-Free Structural Credibility Modeling for Topologically Accurate OCTA Segmentation


### Overview
USkelCtrlNet is a deep learning framework for **topologically accurate OCTA vessel segmentation**.  
It is designed to improve not only pixel-level overlap, but also vascular structural consistency under challenging OCTA degradations such as low contrast, speckle noise, projection artifacts, motion corruption, and signal attenuation.

Unlike conventional methods that mainly impose structural constraints on the final output, USkelCtrlNet introduces a **reliability-gated in-network structural control mechanism**. It estimates structural credibility during feature learning and uses it to guide feature calibration, cross-scale fusion, and decoder refinement, leading to better capillary continuity, fewer false bridges, and more stable artery-vein separation.

---

### Highlights
- Reliability-gated **in-network structural control** for OCTA segmentation
- **Skeleton-free dual-map design**:
  - structural credibility map
  - reliability suppression map
- Improves both **overlap-based metrics** and **topology-sensitive metrics**
- Supports multiple OCTA segmentation targets:
  - RV
  - Capillary
  - Artery
  - Vein
  - FAZ

---

### Framework
<p align="center">
  <img src="./fig1_framework.png.png" width="100%" alt="USkelCtrlNet framework">
</p>

The proposed framework contains four main components:

1. **Multi-DSConv Block**  
   Geometry-consistent local vessel representation using multi-view direction-aware dynamic deformable convolution.

2. **Deformable Swin-Transformer Block**  
   A warp-then-attend design that combines local continuity modeling and long-range dependency learning.

3. **Space Structure Calibration (SSC) Block**  
   Skeleton-free structural credibility estimation with reliability suppression for same-scale feature recalibration.

4. **Structure-Conditioned Cross-Scale Selective Fusion (SC-CSSF) Block**  
   Reliability-aware multi-scale feature routing for preserving vascular topology.

---

### Dataset
Experiments are conducted on the **OCTA-500** benchmark with two field-of-view settings:

- **OCTA_3M**: 200 images, resolution `304 × 304`
- **OCTA_6M**: 300 images, resolution `400 × 400`

Each setting contains five independent binary segmentation tasks:

- RV
- Capillary
- Artery
- Vein
- FAZ

Input projections include:

- `FULL`
- `ILM_OPL`
- `OPL_BM`

---

### Main Results

#### Vessel-related tasks
USkelCtrlNet achieves strong and balanced performance on **RV, Capillary, Artery, and Vein** segmentation under both 3M and 6M settings, with clear improvements in **Dice**, **clDice**, **BACC**, and **G-mean**.

<p align="center">
  <img src="./clDice_radar_OCTA_3M_6M_full_combined.png" width="100%" alt="clDice radar plot">
</p>

#### FAZ segmentation
USkelCtrlNet also shows competitive and stable results on **FAZ segmentation**, indicating that structural modulation improves topology-sensitive vessel tasks without sacrificing region-dominant targets.

<p align="center">
  <img src="./FAZ_3M_6M_dual_boxplot_Dice_latest6M_v4_tuned.png" width="100%" alt="FAZ boxplot">
</p>

---

### Code Structure
```bash
.
├── train.py
├── options.py
├── USkelCtrlUnet.py
├── conversion_and_visualize.py
├── loss_functions.py
├── dataset.py
├── metrics.py
└── README.md
