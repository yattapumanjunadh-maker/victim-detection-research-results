# Victim Detection Research — Results Report

## Reporting rules

- Locally measured results are distinct from published literature.
- Validation results are not labelled as test results.
- Fixed-threshold precision/recall/F1 diagnostics are not mAP.
- Incomplete experiments and the hybrid prototype are clearly identified.

## Existing local results

The complete experiment table is `tables/all_experiments.csv`.
Pending and incomplete rows are in `tables/pending_experiments.csv`.
Published reference results are in `tables/published_literature_results.csv`.

### YOLOv11n — FLIR validation

- Precision: 81.44%
- Recall: 71.19%
- mAP@0.50: 80.11%
- mAP@0.50:0.95: 46.72%
- These are validation metrics; the listed FLIR dataset configuration has no independent test split.

### EfficientDet-D0 — FLIR validation

- Training: 10 epochs on the FLIR person training split.
- Selected checkpoint: epoch 4, based on the lowest recorded validation loss (0.3645).
- Validation: 1,144 images and 4,470 ground-truth person instances.
- Confidence threshold: 0.25; matching IoU threshold: 0.50.
- True positives: 2,298; false positives: 1,424; false negatives: 2,172.
- Precision: 61.74%; recall: 51.41%; F1: 56.10%; mean matched IoU: 72.94%.
- These are fixed-threshold validation diagnostics, not mAP and not held-out test results.

### YOLOv11n — SARD-labelled Roboflow held-out test

- Precision: 94.2%
- Recall: 86.7%
- mAP@0.50: 92.9%
- mAP@0.50:0.95: 61.3%
- Test set: 570 images and 732 labelled instances.

### Faster R-CNN and EfficientDet — held-out test diagnostics

The following fixed-threshold diagnostics were computed on the SARD-labelled Roboflow test split.
They are not COCO mAP values.

| Metric | Faster R-CNN ResNet50 FPN | EfficientDet-D0 |
|---|---:|---:|
| Test images | 570 | 570 |
| Ground-truth instances | 732 | 732 |
| True positives | 656 | 619 |
| False positives | 88 | 54 |
| False negatives | 76 | 113 |
| Precision | 88.17% | 91.98% |
| Recall | 89.62% | 84.56% |
| F1 | 88.89% | 88.11% |
| Mean matched IoU | 81.65% | 81.34% |

Thresholds differ between these diagnostic runs: Faster R-CNN confidence 0.50; EfficientDet confidence 0.25; both use IoU 0.50. Compare cautiously.

### COCO-style test metrics

- Faster R-CNN ResNet50 FPN: mAP@0.50 = 89.80%; mAP@0.50:0.95 = 57.28%.
- EfficientDet-D0: mAP@0.50 = 89.83%; mAP@0.50:0.95 = 54.91%. Its training history contains 20 logged epochs; the best validation-loss checkpoint was from epoch 9.
- These are the existing COCO-style evaluations. Evaluation settings should be aligned before claiming a definitive model ranking.

### RT-DETR

- The local FLIR RT-DETR-L log contains only two epochs.
- Precision 79.12%, recall 65.75%, mAP@0.50 73.04%, and mAP@0.50:0.95 36.30% are interim validation results, not a completed benchmark.
- SARD RT-DETR saved-checkpoint evaluation on the held-out test split: precision 45.4%, recall 37.4%, mAP@0.50 34.4%, and mAP@0.50:0.95 12.8%. This checkpoint came from an incomplete and unstable training run; it is not a completed 50-epoch benchmark.

### HTVD-Net + CBAMH

- The available model is a preliminary prototype trained for two smoke-test epochs.
- Its current test diagnostic was precision 4.28%, recall 6.42%, and F1 5.14%.
- The RGB and thermal datasets do not have verified aligned image pairs in the current loader. Therefore, this is not a validated multimodal fusion benchmark.
- Do not claim that the proposed hybrid outperforms the baseline detectors.

## FLIR model comparison summary

The consolidated FLIR comparison table is available at
`tables/flir_model_comparison.csv`.

- **YOLOv11n:** 50-epoch validation; precision 81.44%, recall 71.19%,
  mAP@0.50 80.11%, and mAP@0.50:0.95 46.72%.
- **Faster R-CNN ResNet50 FPN:** 10 epochs; fixed-threshold validation
  diagnostics only, not mAP.
- **EfficientDet-D0:** 10 epochs; best validation-loss checkpoint from
  epoch 4; fixed-threshold validation diagnostics only, not mAP.
- **RT-DETR-L:** two logged epochs; preliminary validation metrics only.

These results should not be interpreted as a definitive model ranking:
training durations and evaluation protocols differ. The current FLIR
configuration has no independent test split.

## Figures and supporting files

- YOLO confusion matrices: `confusion_matrices/`.
- YOLO training curves and prototype loss curve: `training_curves/`.
- Faster R-CNN and EfficientDet TP/FP/FN outcome charts: `test_outcome_plots/`. These are outcome charts, not conventional confusion matrices.
- Local comparison plots: `graphs/`.
- Published literature values and URLs: `tables/published_literature_results.csv` and `references/bibliography.md`.

## Dataset naming

Use “SARD-labelled Roboflow dataset” for the downloaded RGB rescue dataset unless its provenance as the canonical SARD dataset has been independently verified.

## Limitations

The experiments use different architectures, training durations, thresholds, and evaluation procedures. Do not directly rank models using mixed metrics or different splits. Missing experiments remain pending rather than being filled with fabricated values.


## Final validation update — 2026-10-18

### Fresh RT-DETR validation

- **FLIR thermal, RT-DETR-L:** 1144 validation images and 4470 instances;
  precision 0.789, recall 0.659, mAP@0.50 0.730, and mAP@0.50:0.95 0.363.
  Inference time was 24.5 ms/image. Only two training epochs were logged,
  so this is a preliminary result.
- **SARD-labelled RGB, RT-DETR ResNet-50:** the recorded interim validation
  snapshot contains 1144 validation images and 1463 instances; precision
  0.433, recall 0.403, mAP@0.50 0.331, and mAP@0.50:0.95 0.118. Inference
  time was 29.8 ms/image. Training has since resumed from epoch 10 toward
  50 total epochs. These are historical interim metrics, not final results;
  the held-out test evaluation must be rerun after training completes.

### COCO-style FLIR validation

- **Faster R-CNN ResNet50 FPN:** AP@0.50:0.95 0.333932; AP@0.50 0.673247;
  AP@0.75 0.295996; AR@100 0.451521. Evaluated on 1144 validation images
  containing 4470 ground-truth instances.
- **EfficientDet-D0:** AP@0.50:0.95 0.221905; AP@0.50 0.523778;
  AP@0.75 0.157104; AR@100 0.359239. The selected checkpoint is epoch 4,
  chosen by validation loss. Evaluated on the same 1144-image validation split.

COCO AP metrics are not interchangeable with fixed-confidence precision and
recall diagnostics. Model-specific preprocessing and evaluation settings may
also differ; avoid treating the figures as a strict ranking without a fully
aligned evaluation protocol. The FLIR dataset setup has no independent test
split in this package, so these are validation results, not test results.

### HTVD-Net + CBAMH prototype status

The prototype diagnostic processed 570 SARD-labelled RGB test images,
with 732 ground-truth boxes and 1098 predicted boxes at confidence 0.50
and IoU threshold 0.50. Precision was 0.0428, recall 0.0642, and F1 0.0514.
This is not mAP. The current loader feeds the same RGB image to both branches;
verified paired RGB-thermal inputs are not available in this experiment.
Therefore, the hybrid is a prototype only and has not demonstrated valid
multimodal fusion performance.

### Completion status

The package contains artifacts for all nine planned experiment slots, but
this does not mean all nine are complete scientific benchmarks. YOLOv11n,
Faster R-CNN, and EfficientDet have recorded results for their relevant
dataset runs. RT-DETR runs remain preliminary/incomplete, and HTVD-Net + CBAMH
remains a smoke-test prototype. Refer to the CSV tables for the per-run status.
