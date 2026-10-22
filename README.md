# Victim Detection Research — Experiment Results

This repository organizes experiment outputs for a victim-detection research workflow. It is intended to keep detector-specific artifacts, comparative analysis, and hybrid-framework results easy to locate.

## Experiment groups

| Folder | Contents |
|---|---|
| `01_YOLOv11n/` | YOLOv11n experiment artifacts |
| `02_Faster_RCNN_ResNet50_FPN/` | Faster R-CNN / ResNet-50 FPN artifacts |
| `03_EfficientDet_D0/` | EfficientDet-D0 artifacts |
| `04_RT_DETR/` | RT-DETR artifacts |
| `05_HTVD_Net_CBAMH_Hybrid/` | Proposed HTVD-Net / CBAMH prototype artifacts |
| `06_Comparison/` | Comparison outputs |
| `07_Reports_and_Original_Package/` | Reports and preserved supporting files |
| `INDEX.md` | Results index and important status notes |

## Research workflow

The baseline comparison considers YOLOv11n, Faster R-CNN with ResNet-50 FPN, EfficientDet-D0, and RT-DETR before evaluating the proposed hybrid direction.

The broader project explores decision-level fusion of detector outputs and a leader–backup coordination strategy for UAV search missions. Experimental claims should be tied to reproducible runs and clearly identified datasets/splits.

## Result integrity

Please distinguish training, validation, and held-out test metrics. Do not treat incomplete training, a preliminary prototype, or unverified RGB/thermal pairing as a final result. The current limitations recorded in `INDEX.md` take precedence over any tentative charts or filenames.

For each reported result, document the model/configuration, dataset and split, image size, batch size, epoch count, checkpoint source, and metric calculation method. Do not label literature values or illustrative values as locally measured results.

## Usage

Browse the model-specific folders and read `INDEX.md` first. This repository stores experiment outputs; it may not contain all code, datasets, or large model weights required to reproduce each run.
