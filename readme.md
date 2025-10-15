![](figures/logosQTML2024.jpg)

# Vision Transformer Embeddings and Quantum Pyramidal Circuits for Biomedical Image Analysis

This work presents a novel quantum-hybrid pipeline for lung nodule classification in computed tomography (CT) scans, combining Vision Transformer (ViT) embeddings with quantum orthogonal neural networks 

---

# Contents of the work

## Authors
- Xavi F. Aragones¹²
- Miguel A. González Ballester¹³⁴

### Affiliations
1. BCN Medtech, Dept. of Engineering, Universitat Pompeu Fabra, Barcelona, Spain
2. Parc Tecnològic TecnoCampus Mataró-Maresme - UPF, Spain
3. Quantic, Barcelona Supercomputing Center, Barcelona, Spain
4. ICREA, Barcelona, Spain


## Figures

![ViT embedding extraction](figuresPaper/XeviArticleFinalPetitImatgeP1.png)
*Trained ViT splits CT images into patches and produces embedding heatmaps used as fixed features.*

![End-to-end quantum-hybrid pipeline](figuresPaper/XeviArticleTerceraPetit.png)
*Pipeline: ViT embeddings → PCA (k ∈ {2,4,8,16}) → orthogonal pyramidal RBS circuit → binary classification.*

![CT planes and examples](figuresPaper/Pulmons_Sagittal_Xevi.jpg)
*Representative 32×32 central slices per plane (axial, sagittal, coronal) for benign vs. malignant nodules.*

![Accuracy — ViT₁ vs Quantum](figuresPaper/VITperfPlusQH1accV2_6b.png)
*Accuracy distributions comparing classical ViT₁ (1 head, 4 layers) with quantum configurations.*

![Accuracy — ViT₂ vs Quantum](figuresPaper/VITperfPlusQH4accV2_6b.png)
*Accuracy distributions comparing classical ViT₂ (4 heads, 8 layers) with quantum configurations.*

![ROC–AUC — ViT₁ vs Quantum](figuresPaper/VITperfPlusQH1rocV2_6b.png)
*ROC–AUC distributions for ViT₁ vs. quantum configurations.*

![ROC–AUC — ViT₂ vs Quantum](figuresPaper/VITperfPlusQH4rocV2_6b.png)
*ROC–AUC distributions for ViT₂ vs. quantum configurations.*
