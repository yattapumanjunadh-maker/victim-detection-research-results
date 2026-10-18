# Master Model Comparison

**Interpretation note:** P/R values use the recorded evaluation threshold, while AP/mAP values use their recorded evaluation protocol. Validation and held-out test results are not directly interchangeable.

| Model | Dataset | Split | Precision | Recall | AP50/mAP50 | AP50:95/mAP50:95 | Notes |
|---|---|---|---:|---:|---:|---:|---|
| YOLOv11n | FLIR Thermal | Validation | 0.8144 | 0.7119 | 0.8011 | 0.4672 | 50 epochs |
| YOLOv11n | SARD-labelled RGB | Held-out test | 0.9420 | 0.8670 | 0.9290 | 0.6130 | 50 epochs |
| Faster R-CNN ResNet-50 FPN | FLIR Thermal | Validation | 0.3467 | 0.7685 |  | 0.3339 | 10 epochs; AP50=0.67325 |
| Faster R-CNN ResNet-50 FPN | SARD-labelled RGB | Held-out test | 0.8817 | 0.8962 | 0.8980 | 0.5728 | 10 epochs; AP50=.8980; fixed-threshold P/R differ from COCO AP |
| EfficientDet-D0 | FLIR Thermal | Validation | 0.6174 | 0.5141 | 0.5238 | 0.2219 | 10 epochs; AP50=.52378 |
| EfficientDet-D0 | SARD-labelled RGB | Held-out test | 0.9198 | 0.8456 | 0.8983 | 0.5491 | 20 logged epochs; best validation loss at epoch 9 |
| RT-DETR-L | FLIR Thermal | Preliminary validation | 0.7912 | 0.6575 | 0.7304 | 0.3629 | Only 2 epochs; training incomplete |
| RT-DETR ResNet-50 | SARD-labelled RGB | Held-out test | 0.8730 | 0.6800 | 0.7630 | 0.4150 | 50 epochs total; inference 29.3 ms/image |
| HTVD-Net + CBAMH | FLIR + RGB | Prototype diagnostic | 0.0428 | 0.0642 |  |  | 2-epoch smoke test; same RGB image fed to both branches; not a valid multimodal result |

## Important limitations

- FLIR RT-DETR is incomplete and must not be presented as a final 50-epoch model.
- HTVD-Net + CBAMH is a preliminary prototype; paired RGB-thermal inputs have not been verified.
- The SARD-labelled Roboflow dataset and generic SARD dataset must not be treated as the same dataset without provenance verification.
