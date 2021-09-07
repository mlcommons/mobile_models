# TFLite models for MLPerf

This directory contains TFLite models used by MLPerf that are added in the version 1.1.

# Image classification

Generally, we are still using models from [v0.7](../../v0_7/tflite).
However, mobilenet model for float32 type in the v0.7 folder doesn't support resizing,
which is needed for Offline benchmark.

File `mobilenet_edgetpu_224_1.0_float.tflite` in this folder contains a modified model which supports resizing.
