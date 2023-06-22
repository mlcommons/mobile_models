# TFLite v3.1

### mobilenet-edgetpu-v2-L_int8.tflite

downloaded from [tfhub.dev](https://tfhub.dev/google/lite-model/edgetpu/vision/mobilenet-edgetpu-v2/l/1)

### mobilenet-edgetpu-v2-L_fp32.tflite

Converted using this Python script:
```python
# TF2 version
import tensorflow as tf
import tensorflow_hub as hub

# Get the model
keras_layer = hub.KerasLayer('https://tfhub.dev/google/edgetpu/vision/mobilenet-edgetpu-v2/l/1')
model = tf.keras.Sequential([keras_layer])
model.build([None, 224, 224, 3])
input_tensor = tf.ones((4, 224, 224, 3))
output_tensor = model(input_tensor)

# Convert the model
converter = tf.lite.TFLiteConverter.from_keras_model(model)
converter.optimizations = [tf.lite.Optimize.DEFAULT]
converter.target_spec.supported_types = [tf.float32]
tflite_model = converter.convert()

# Save the model.
save_path = "./mobilenet-edgetpu-v2-L_fp32.tflite"
with open(save_path, 'wb') as f:
  f.write(tflite_model)

print(f"Model saved to {save_path}")
```
