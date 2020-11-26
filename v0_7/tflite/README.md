# TFLite models for MLPerf

This directory contains all models in TFLite that are used for MLPerf.

## Image classification

1.  mobilenet_edgetpu_224_1.0_float, mobilenet_edgetpu_224_1.0_uint8 and mobilenet_edgetpu_224_1.0_int8

    *   Source:
        https://storage.cloud.google.com/mobilenet_edgetpu/checkpoints/mobilenet_edgetpu_224_1.0.tgz
        listed on https://github.com/tensorflow/models/tree/master/research/slim/nets/mobilenet

## Object detection

1.  ssd_mobilenet_v2_300_float

    *   Source:
        http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz
        listed on https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md
    *   After downloading, the frozen graph is exported using
        export_tflite_ssd_graph.py:

        ```
        <path to be configured>/export_tflite_ssd_graph.py \
        --pipeline_config_path=pipeline.config \
        --output_directory=<output path> \
        --trained_checkpoint_prefix=model.ckpt \
        --add_postprocessing_op=true --use_regular_nms=true
        ```

    *   Then it is converted to TFLite format using tflite_convert:

        ```
        tflite_convert --graph_def_file tflite_graph.pb \
        --enable_v1_converter \
        --experimental_new_converter=False \
        --output_file /tmp/ssdv2.tflite \
        --input_shapes=1,300,300,3 \
        --input_arrays=normalized_input_image_tensor \
        --output_arrays='TFLite_Detection_PostProcess','TFLite_Detection_PostProcess:1','TFLite_Detection_PostProcess:2','TFLite_Detection_PostProcess:3'  \
        --change_concat_input_ranges=false \
        --allow_custom_ops
        ```

2.  ssd_mobilenet_v2_300_uint8

    *   Source:
        http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_quantized_300x300_coco_2019_01_03.tar.gz
    *   After downloading, the frozen graph is converted to TFLite format using
        tflite_convert:

        ```
        tflite_convert --graph_def_file tflite_graph.pb \
        --enable_v1_converter \
        --experimental_new_converter=False \
        --output_file /tmp/ssdv2.tflite \
        --input_shapes=1,300,300,3 \
        --input_arrays=normalized_input_image_tensor \
        --output_arrays='TFLite_Detection_PostProcess','TFLite_Detection_PostProcess:1','TFLite_Detection_PostProcess:2','TFLite_Detection_PostProcess:3'  \
        --inference_type=QUANTIZED_UINT8 \
        --mean_values=128 --std_dev_values=128 \
        --change_concat_input_ranges=false \
        --allow_custom_ops
        ```

## Semantic Segmentation

1. deeplabv3_mnv2_ade20k_float

    *   Source:
        http://download.tensorflow.org/models/deeplabv3_mnv2_ade20k_train_2018_12_03.tar.gz
        listed on https://github.com/tensorflow/models/blob/master/research/deeplab/g3doc/model_zoo.md
    *   After downloading, the frozen graph is converted to TFLite format using
        tflite_convert:

        ```
        tflite_convert \
        --graph_def_file=<model dir>/frozen_inference_graph.pb \
        --output_file=<model dir>/deeplabv3_mnv2_ade20k_float.tflite \
        --output_format=TFLITE \
        --input_shape=1,513,513,3 \
        --input_arrays="MobilenetV2/MobilenetV2/input" \
        --change_concat_input_ranges=true \
        --output_arrays="ArgMax"
        ```

## Language Understanding

1. mobilebert_float_384_20200602

    *   Source:
        https://zenodo.org/record/3878955#.Xtpz9p5KjUI

    *   Accuracy: 90 F1

2. mobilebert_int8_384_20200602

    *   Source:
        https://zenodo.org/record/3878955#.Xtpz9p5KjUI

    *   Accuracy: 88 F1
