`imagenet_tiny-groundtruth.txt` is a manual annotation for the `v0_7/datasets/imagenet_tiny` dataset.

`ade20k-tiny-saved-output` is an artificial "groundtruth" for the `v0_7/datasets/ade20k_tiny`dataset.
It was created by running `v2.0 Image Segmentation` task and saving the model output. It must never be used for real accuracy validation.
It's intended to be used for accuracy validation in an integration test.
