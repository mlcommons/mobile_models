# TFLite models for MLPerf

This directory contains all models in TFLite that are used for MLPerf.

## Image classification

Same as [v0.7](https://github.com/fatihcakirs/mobile_models/tree/main/v0_7).

- https://github.com/fatihcakirs/mobile_models/blob/main/v0_7/tflite/mobilenet_edgetpu_224_1.0_float.tflite
- https://github.com/fatihcakirs/mobile_models/blob/main/v0_7/tflite/mobilenet_edgetpu_224_1.0_int8.tflite
- https://github.com/fatihcakirs/mobile_models/blob/main/v0_7/tflite/mobilenet_edgetpu_224_1.0_uint8.tflite

## Object detection

*   Source: `http://download.tensorflow.org/models/object_detection/ssdlite_mobiledet_edgetpu_320x320_coco_2020_05_19.tar.gz`

1.  mobiledet.tflite

    *   After downloading, edit the `score_threshold` to 0.3 in `fp32/pipeline.config` and export the frozen graph using 
        `export_tflite_ssd_graph.py` with regular nms post-processing:

        ```
        <path to be configured>/export_tflite_ssd_graph.py --input_type image_tensor --pipeline_config_path ${TF_MODEL_DIR}/fp32/pipeline.config --trained_checkpoint_prefix ${TF_MODEL_DIR}/fp32/model.ckpt-400000 --output_directory ${TFLITE_MODEL_DIR}/fp32/ --add_postprocessing_op=true --use_regular_nms=true --max_detections=10
        ```

    *   Then this `tflite_graph.pb` is converted to TFLite format using TOCO:

        ```
        bazel run -c opt tensorflow/lite/toco:toco -- --input_file=/path/to/ssdlite_mobiledet_edgetpu_320x320_coco_2020_05_19/fp32/tflite_graph.pb --output_file=/path/to/research/ssdlite_mobiledet_edgetpu_320x320_coco_2020_05_19/fp32/mobiledet.tflite --input_shapes=1,320,320,3 --input_arrays=normalized_input_image_tensor --output_arrays='TFLite_Detection_PostProcess','TFLite_Detection_PostProcess:1','TFLite_Detection_PostProcess:2','TFLite_Detection_PostProcess:3'  --inference_type=FLOAT --allow_custom_ops
        ```

2.  mobiledet_qat.tflite

    *   Edit the `score_threshold` to 0.3 in `uint8/pipeline.config`, and export the frozen graph using 
        `export_tflite_ssd_graph.py`  with regular nms post-processing:

        ```
        <path to be configured>/export_tflite_ssd_graph.py --input_type image_tensor --pipeline_config_path ${TF_MODEL_DIR}/uint8/pipeline.config --trained_checkpoint_prefix ${TF_MODEL_DIR}/uint8/model.ckpt-400000 --output_directory ${TFLITE_MODEL_DIR}/uint8/ --add_postprocessing_op=true --use_regular_nms=true --max_detections=10
        ```
    
    *   Then this `tflite_graph.pb` is converted to TFLite format using TOCO:

        ```
        bazel run -c opt tensorflow/lite/toco:toco -- --input_file=/path/to/ssdlite_mobiledet_edgetpu_320x320_coco_2020_05_19/uint8/tflite_graph.pb --output_file=/path/to/ssdlite_mobiledet_edgetpu_320x320_coco_2020_05_19/uint8/mobiledet_qat.tflite --input_shapes=1,320,320,3 --input_arrays=normalized_input_image_tensor --output_arrays='TFLite_Detection_PostProcess','TFLite_Detection_PostProcess:1','TFLite_Detection_PostProcess:2','TFLite_Detection_PostProcess:3'  --inference_type=QUANTIZED_UINT8 --allow_custom_ops --mean_values=128 --std_values=128
        ```

## Semantic Segmentation

Same as [v0.7](https://github.com/fatihcakirs/mobile_models/tree/main/v0_7).

- https://github.com/fatihcakirs/mobile_models/blob/main/v0_7/tflite/deeplabv3_mnv2_ade20k_float.tflite
- https://github.com/fatihcakirs/mobile_models/blob/main/v0_7/tflite/deeplabv3_mnv2_ade20k_int8.tflite
- https://github.com/fatihcakirs/mobile_models/blob/main/v0_7/tflite/deeplabv3_mnv2_ade20k_uint8.tflite

## Language Understanding

Same as [v0.7](https://github.com/fatihcakirs/mobile_models/tree/main/v0_7) (TODO: check this statement, add v1.0 version of MobileBert)

- https://github.com/fatihcakirs/mobile_models/blob/main/v0_7/tflite/mobilebert_float_20191023.tflite
- https://github.com/fatihcakirs/mobile_models/blob/main/v0_7/tflite/mobilebert_float_384_20200602.tflite
- https://github.com/fatihcakirs/mobile_models/blob/main/v0_7/tflite/mobilebert_float_384_gpu.tflite
- https://github.com/fatihcakirs/mobile_models/blob/main/v0_7/tflite/mobilebert_int8_384_20200602.tflite
- https://github.com/fatihcakirs/mobile_models/blob/main/v0_7/tflite/mobilebert_int8_384_nnapi.tflite


