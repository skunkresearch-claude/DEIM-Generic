# P004 NOVA AI — DEIM integration and artifact provenance

This note is an implementation handoff and provenance record, not a new production API contract.

P004 uses DEIM under/sides inference on the NOVA AI 5090, behind the RigScan Pro middle tier and the rigscan_web review surface. The camera control/transport boundary is vendor-neutral Aravis/GenICam plus Rust AF_PACKET/GVSP; the proprietary InfraTec SDK is not required by the inference runtime.

The first physical inference fixture is the **Hui Na Model 1501 Scania 770, 1/18 scale**. The fixture run must prove real RTX 5090 execution, selected checkpoint/config, preprocessing and label mapping, then emit a stable result contract for RigScan persistence/reporting and the UI. It is an integration fixture, not a full-size field-accuracy claim.

## Committed artifacts

This repository contains committed checkpoints for both configurations and both training stages:

- `deim_outputs/best_models/sides/best_stg1.pth`
- `deim_outputs/best_models/sides/best_stg2.pth`
- `deim_outputs/best_models/under/best_stg1.pth`
- `deim_outputs/best_models/under/best_stg2.pth`

These checkpoints are runtime/provenance inputs, not authored application source. Before production use, record the selected checkpoint identity, export/toolchain version, class-label mapping, thermal preprocessing/normalisation and validation result. Do not assume that a checkpoint is an ONNX export or that an ONNX export has the same preprocessing contract.

## P004 acceptance gate

Prove actual RTX 5090 CUDA provider selection and real under/sides inference, with no silent mock or CPU fallback. The adapter must emit a stable result contract that the middle tier and UI can persist, report and display, including model/config provenance and frame/session identity.

Dependencies, generated outputs, weights and export files must be inventoried for reproducibility and deployment, while remaining distinct from the authored model/application code.
