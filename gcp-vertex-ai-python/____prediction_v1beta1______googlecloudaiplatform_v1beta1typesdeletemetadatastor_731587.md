---
merged_at: 2026-01-27T07:03:44.002852
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/prediction_v1beta1 -->

# Types for Google Cloud Aiplatform V1beta1 Schema Predict Prediction v1beta1 API

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ClassificationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Image and Text Classification.

#### ids()

The resource IDs of the AnnotationSpecs that had been identified.

**Type**MutableSequence[

[int](https://docs.python.org/3/library/functions.html#int)]

#### display_names()

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### confidences()

The Model’s confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

**Type**MutableSequence[

[float](https://docs.python.org/3/library/functions.html#float)]

#### confidences(*: MutableSequence[*[float](https://docs.python.org/3/library/functions.html#float) )

[float](https://docs.python.org/3/library/functions.html#float)

#### display_names(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### ids(*: MutableSequence[*[int](https://docs.python.org/3/library/functions.html#int) )

[int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ImageObjectDetectionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Image Object Detection.

#### ids()

The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly.

**Type**MutableSequence[

[int](https://docs.python.org/3/library/functions.html#int)]

#### display_names()

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### confidences()

The Model’s confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

**Type**MutableSequence[

[float](https://docs.python.org/3/library/functions.html#float)]

#### bboxes()

Bounding boxes, i.e. the rectangles over the image, that
pinpoint the found AnnotationSpecs. Given in order that
matches the IDs. Each bounding box is an array of 4 numbers
`xMin`

, `xMax`

, `yMin`

, and `yMax`

, which represent
the extremal coordinates of the box. They are relative to
the image size, and the point 0,0 is in the top left of the
image.

**Type**MutableSequence[

[google.protobuf.struct_pb2.ListValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/struct_pb2.html#google.protobuf.struct_pb2.ListValue)]

#### bboxes(*: MutableSequence[*[google.protobuf.struct_pb2.ListValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/struct_pb2.html#google.protobuf.struct_pb2.ListValue) )

[google.protobuf.struct_pb2.ListValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/struct_pb2.html#google.protobuf.struct_pb2.ListValue)

#### confidences(*: MutableSequence[*[float](https://docs.python.org/3/library/functions.html#float) )

[float](https://docs.python.org/3/library/functions.html#float)

#### display_names(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### ids(*: MutableSequence[*[int](https://docs.python.org/3/library/functions.html#int) )

[int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.ImageSegmentationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Image Segmentation.

#### category_mask()

A PNG image where each pixel in the mask represents the category in which the pixel in the original image was predicted to belong to. The size of this image will be the same as the original image. The mapping between the AnntoationSpec and the color can be found in model’s metadata. The model will choose the most likely category and if none of the categories reach the confidence threshold, the pixel will be marked as background.

**Type**

#### confidence_mask()

A one channel image which is encoded as an 8bit lossless PNG. The size of the image will be the same as the original image. For a specific pixel, darker color means less confidence in correctness of the cateogry in the categoryMask for the corresponding pixel. Black means no confidence and white means complete confidence.

**Type**

#### category_mask(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### confidence_mask(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TabularClassificationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Tabular Classification.

#### classes()

The name of the classes being classified, contains all possible values of the target column.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### scores()

The model’s confidence in each class being correct, higher value means higher confidence. The N-th score corresponds to the N-th class in classes.

**Type**MutableSequence[

[float](https://docs.python.org/3/library/functions.html#float)]

#### classes(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### scores(*: MutableSequence[*[float](https://docs.python.org/3/library/functions.html#float) )

[float](https://docs.python.org/3/library/functions.html#float)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TabularRegressionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Tabular Regression.

#### value()

The regression value.

**Type**

#### lower_bound()

The lower bound of the prediction interval.

**Type**

#### upper_bound()

The upper bound of the prediction interval.

**Type**

#### lower_bound(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### upper_bound(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

#### value(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TextExtractionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Text Extraction.

#### ids()

The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly.

**Type**MutableSequence[

[int](https://docs.python.org/3/library/functions.html#int)]

#### display_names()

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

**Type**MutableSequence[

[str](https://docs.python.org/3/library/stdtypes.html#str)]

#### text_segment_start_offsets()

The start offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet.

**Type**MutableSequence[

[int](https://docs.python.org/3/library/functions.html#int)]

#### text_segment_end_offsets()

The end offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet.

**Type**MutableSequence[

[int](https://docs.python.org/3/library/functions.html#int)]

#### confidences()

The Model’s confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

**Type**MutableSequence[

[float](https://docs.python.org/3/library/functions.html#float)]

#### confidences(*: MutableSequence[*[float](https://docs.python.org/3/library/functions.html#float) )

[float](https://docs.python.org/3/library/functions.html#float)

#### display_names(*: MutableSequence[*[str](https://docs.python.org/3/library/stdtypes.html#str) )

[str](https://docs.python.org/3/library/stdtypes.html#str)

#### ids(*: MutableSequence[*[int](https://docs.python.org/3/library/functions.html#int) )

[int](https://docs.python.org/3/library/functions.html#int)

#### text_segment_end_offsets(*: MutableSequence[*[int](https://docs.python.org/3/library/functions.html#int) )

[int](https://docs.python.org/3/library/functions.html#int)

#### text_segment_start_offsets(*: MutableSequence[*[int](https://docs.python.org/3/library/functions.html#int) )

[int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TextSentimentPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Text Sentiment

#### sentiment()

The integer sentiment labels between 0 (inclusive) and sentimentMax label (inclusive), while 0 maps to the least positive sentiment and sentimentMax maps to the most positive one. The higher the score is, the more positive the sentiment in the text snippet is. Note: sentimentMax is an integer value between 1 (inclusive) and 10 (inclusive).

**Type**

#### sentiment(*: [int](*[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int) )

[https://docs.python.org/3/library/functions.html#int](https://docs.python.org/3/library/functions.html#int)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.TimeSeriesForecastingPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Time Series Forecasting.

#### value()

The regression value.

**Type**

#### value(*: [float](*[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float) )

[https://docs.python.org/3/library/functions.html#float](https://docs.python.org/3/library/functions.html#float)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoActionRecognitionPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Video Action Recognition.

#### id()

The resource ID of the AnnotationSpec that had been identified.

**Type**

#### display_name()

The display name of the AnnotationSpec that had been identified.

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end.

#### time_segment_end()

The end, exclusive, of the video’s time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end.

#### confidence()

The Model’s confidence in correction of this prediction, higher value means higher confidence.

#### confidence(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### display_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_end(*: [google.protobuf.duration_pb2.Duration](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration)

#### time_segment_start(*: [google.protobuf.duration_pb2.Duration](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoClassificationPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Video Classification.

#### id()

The resource ID of the AnnotationSpec that had been identified.

**Type**

#### display_name()

The display name of the AnnotationSpec that had been identified.

**Type**

#### type_()

The type of the prediction. The requested types can be configured via parameters. This will be one of

- segment-classification
- shot-classification
one-sec-interval-classification

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end. Note that for ‘segment-classification’ prediction type, this equals the original ‘timeSegmentStart’ from the input instance, for other types it is the start of a shot or a 1 second interval respectively.

#### time_segment_end()

The end, exclusive, of the video’s time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end. Note that for ‘segment-classification’ prediction type, this equals the original ‘timeSegmentEnd’ from the input instance, for other types it is the end of a shot or a 1 second interval respectively.

#### confidence()

The Model’s confidence in correction of this prediction, higher value means higher confidence.

#### confidence(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### display_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### time_segment_end(*: [google.protobuf.duration_pb2.Duration](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration)

#### time_segment_start(*: [google.protobuf.duration_pb2.Duration](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration)

#### type_(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

*class* google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


Prediction output format for Video Object Tracking.

#### id()

The resource ID of the AnnotationSpec that had been identified.

**Type**

#### display_name()

The display name of the AnnotationSpec that had been identified.

**Type**

#### time_segment_start()

The beginning, inclusive, of the video’s time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end.

#### time_segment_end()

The end, inclusive, of the video’s time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end.

#### confidence()

The Model’s confidence in correction of this prediction, higher value means higher confidence.

#### frames()

All of the frames of the video in which a single object instance has been detected. The bounding boxes in the frames identify the same object.

**Type**MutableSequence[

[google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult.Frame](https://docs.cloud.google.com/python/docs/reference/aiplatform/prediction_v1beta1/types_.md#google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult.Frame)]

*class* Frame(mapping=None, *, ignore_unknown_fields=False, **kwargs)

Bases: `proto.message.Message`


The fields `xMin`

, `xMax`

, `yMin`

, and `yMax`

refer to a
bounding box, i.e. the rectangle over the video frame pinpointing
the found AnnotationSpec. The coordinates are relative to the frame
size, and the point 0,0 is in the top left of the frame.

#### time_offset()

A time (frame) of a video in which the object has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with “s” appended at the end.

#### x_min()

The leftmost coordinate of the bounding box.

#### x_max()

The rightmost coordinate of the bounding box.

#### y_min()

The topmost coordinate of the bounding box.

#### y_max()

The bottommost coordinate of the bounding box.

#### time_offset(*: [google.protobuf.duration_pb2.Duration](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration](https://googleapis.dev/python/protobuf/latest/google/protobuf/duration_pb2.html#google.protobuf.duration_pb2.Duration)

#### x_max(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### x_min(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### y_max(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### y_min(*: [google.protobuf.wrappers_pb2.FloatValue](*[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue) )

[https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue](https://googleapis.dev/python/protobuf/latest/google/protobuf/wrappers_pb2.html#google.protobuf.wrappers_pb2.FloatValue)

#### confidence(*: wrappers_pb2.FloatValu* )

#### display_name(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

#### frames(*: MutableSequence[[Frame](../prediction_v1beta1/types*.md#google.cloud.aiplatform.v1beta1.schema.predict.prediction_v1beta1.types.VideoObjectTrackingPredictionResult.Frame)_ )

#### id(*: [str](*[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str) )

[https://docs.python.org/3/library/stdtypes.html#str](https://docs.python.org/3/library/stdtypes.html#str)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteMetadataStoreOperationMetadata -->

# Class DeleteMetadataStoreOperationMetadata (1.134.0)

```
DeleteMetadataStoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform MetadataService.DeleteMetadataStore.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for deleting a MetadataStore. |

## Methods

### DeleteMetadataStoreOperationMetadata

```
DeleteMetadataStoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform MetadataService.DeleteMetadataStore.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetTensorboardRunRequest -->

# Class GetTensorboardRunRequest (1.134.0)

`GetTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.GetTensorboardRun.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardRun resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|

## Methods

### GetTensorboardRunRequest

`GetTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.GetTensorboardRun.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateMetadataStoreOperationMetadata -->

# Class CreateMetadataStoreOperationMetadata (1.134.0)

```
CreateMetadataStoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform MetadataService.CreateMetadataStore.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
Operation metadata for creating a MetadataStore. |

## Methods

### CreateMetadataStoreOperationMetadata

```
CreateMetadataStoreOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Details of operations that perform MetadataService.CreateMetadataStore.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteIndexEndpointRequest -->

# Class DeleteIndexEndpointRequest (1.134.0)

`DeleteIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.DeleteIndexEndpoint.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the IndexEndpoint resource to be deleted. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|

## Methods

### DeleteIndexEndpointRequest

`DeleteIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.DeleteIndexEndpoint.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetadataSchema -->

# Class MetadataSchema (1.134.0)

`MetadataSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general MetadataSchema.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the MetadataSchema. |
`schema_version` |
`str`
The version of the MetadataSchema. The version's format must match the following regular expression: `^[0-9]+` .][0-9]`+` .][0-9]`+$` , which would allow to
order/compare different versions. Example: 1.0.0, 1.0.1,
etc.
|
`schema` |
`str`
Required. The raw YAML string representation of the MetadataSchema. The combination of [MetadataSchema.version] and the schema name given by `title` in
[MetadataSchema.schema] must be unique within a
MetadataStore.
The schema is defined as an OpenAPI 3.0.2 `MetadataSchema
Object |
`schema_type` |
The type of the MetadataSchema. This is a property that identifies which metadata types will use the MetadataSchema. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MetadataSchema was created. |
`description` |
`str`
Description of the Metadata Schema |

## Classes

### MetadataSchemaType

`MetadataSchemaType(value)`


Describes the type of the MetadataSchema.

## Methods

### MetadataSchema

`MetadataSchema(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general MetadataSchema.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployModelOperationMetadata -->

# Class DeployModelOperationMetadata (1.134.0)

```
DeployModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.DeployModel.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`deployment_stage` |
Output only. The deployment stage of the model. |

## Methods

### DeployModelOperationMetadata

```
DeployModelOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.DeployModel.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GcsDestination -->

# Class GcsDestination (1.134.0)

`GcsDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Google Cloud Storage location where the output is to be written to.

## Attribute |
|
|---|---|
Name |
Description |
`output_uri_prefix` |
`str`
Required. Google Cloud Storage URI to output directory. If the uri doesn't end with '/', a '/' will be automatically appended. The directory is created if it doesn't exist. |

## Methods

### GcsDestination

`GcsDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Google Cloud Storage location where the output is to be written to.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.specialist_pool_service.pagers.ListSpecialistPoolsAsyncPager -->

# Class ListSpecialistPoolsAsyncPager (1.134.0)

```
ListSpecialistPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse
],
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_specialist_pools`

requests.

This class thinly wraps an initial
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse) object, and
provides an `__aiter__`

method to iterate through its
`specialist_pools`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSpecialistPools`

requests and continue to iterate
through the `specialist_pools`

field on the
corresponding responses.

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSpecialistPoolsAsyncPager

```
ListSpecialistPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse
],
],
request: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1.types.specialist_pool_service.ListSpecialistPoolsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NetworkSpec -->

# Class NetworkSpec (1.134.0)

`NetworkSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Network spec.

## Attributes |
|
|---|---|
Name |
Description |
`enable_internet_access` |
`bool`
Whether to enable public internet access. Default false. |
`network` |
`str`
The full name of the Google Compute Engine `network ` __
|
`subnetwork` |
`str`
The name of the subnet that this instance is in. Format: `projects/{project_id_or_number}/regions/{region}/subnetworks/{subnetwork_id}`
|

## Methods

### NetworkSpec

`NetworkSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Network spec.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExecuteExtensionResponse -->

# Class ExecuteExtensionResponse (1.134.0)

`ExecuteExtensionResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExtensionExecutionService.ExecuteExtension.

## Attribute |
|
|---|---|
Name |
Description |
`content` |
`str`
Response content from the extension. The content should be conformant to the response.content schema in the extension's manifest/OpenAPI spec. |

## Methods

### ExecuteExtensionResponse

`ExecuteExtensionResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ExtensionExecutionService.ExecuteExtension.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteModelVersionRequest -->

# Class DeleteModelVersionRequest (1.134.0)

`DeleteModelVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.DeleteModelVersion.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the model version to be deleted, with a version ID explicitly included. Example: `projects/{project}/locations/{location}/models/{model}@1234`
|

## Methods

### DeleteModelVersionRequest

`DeleteModelVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.DeleteModelVersion.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TrajectoryInOrderMatchInput -->

# Class TrajectoryInOrderMatchInput (1.134.0)

`TrajectoryInOrderMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instances and metric spec for TrajectoryInOrderMatch metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for TrajectoryInOrderMatch metric. |
`instances` |
`MutableSequence[`
Required. Repeated TrajectoryInOrderMatch instance. |

## Methods

### TrajectoryInOrderMatchInput

`TrajectoryInOrderMatchInput(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instances and metric spec for TrajectoryInOrderMatch metric.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionsRequest -->

# Class ListModelVersionsRequest (1.134.0)

`ListModelVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModelVersions.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the model to list versions for. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via next_page_token of the previous ListModelVersions call. |
`filter` |
`str`
An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- \`labels.key:\* or labels:key - key existence
- A key including a space must be quoted.
`labels."a key"` .
Some examples:
- `labels.myKey="myValue"`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `create_time`
- `update_time`
Example: `update_time asc, create_time desc` .
|

## Methods

### ListModelVersionsRequest

`ListModelVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModelVersions.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GenerateContentResponse -->

# Class GenerateContentResponse (1.134.0)

`GenerateContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for [PredictionService.GenerateContent].

## Attributes |
|
|---|---|
Name |
Description |
`candidates` |
`MutableSequence[`
Output only. Generated candidates. |
`model_version` |
`str`
Output only. The model version used to generate the response. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the request is made to the server. |
`response_id` |
`str`
Output only. response_id is used to identify each response. It is the encoding of the event_id. |
`prompt_feedback` |
Output only. Content filter results for a prompt sent in the request. Note: Sent only in the first stream chunk. Only happens when no candidates were generated due to content violations. |
`usage_metadata` |
Usage metadata about the response(s). |

## Classes

### PromptFeedback

`PromptFeedback(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content filter results for a prompt sent in the request.

### UsageMetadata

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Usage metadata about response(s).

## Methods

### GenerateContentResponse

`GenerateContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for [PredictionService.GenerateContent].

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsPager -->

# Class ListFeatureViewSyncsPager (1.134.0)

```
ListFeatureViewSyncsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_feature_view_syncs`

requests.

This class thinly wraps an initial
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_view_syncs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureViewSyncs`

requests and continue to iterate
through the `feature_view_syncs`

field on the
corresponding responses.

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureViewSyncsPager

```
ListFeatureViewSyncsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs -->

# Class AutoMlTablesInputs (1.134.0)

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`optimization_objective_recall_value` |
`float`
Required when optimization_objective is "maximize-precision-at-recall". Must be between 0 and 1, inclusive. This field is a member of `oneof` _ `additional_optimization_objective_config` .
|
`optimization_objective_precision_value` |
`float`
Required when optimization_objective is "maximize-recall-at-precision". Must be between 0 and 1, inclusive. This field is a member of `oneof` _ `additional_optimization_objective_config` .
|
`prediction_type` |
`str`
The type of prediction the Model is to produce. "classification" - Predict one out of multiple target values is picked for each row. "regression" - Predict a value based on its relation to other values. This type is available only to columns that contain semantically numeric values, i.e. integers or floating point number, even if stored as e.g. strings. |
`target_column` |
`str`
The column name of the target column that the model is to predict. |
`transformations` |
`MutableSequence[`
Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. |
`optimization_objective` |
`str`
Objective function the model is optimizing towards. The training process creates a model that maximizes/minimizes the value of the objective function over the validation set. The supported optimization objectives depend on the prediction type. If the field is not set, a default objective function is used. classification (binary): "maximize-au-roc" (default) - Maximize the area under the receiver operating characteristic (ROC) curve. "minimize-log-loss" - Minimize log loss. "maximize-au-prc" - Maximize the area under the precision-recall curve. "maximize-precision-at-recall" - Maximize precision for a specified recall value. "maximize-recall-at-precision" - Maximize recall for a specified precision value. classification (multi-class): "minimize-log-loss" (default) - Minimize log loss. regression: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). |
`train_budget_milli_node_hours` |
`int`
Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won't be attempted and will error. The train budget must be between 1,000 and 72,000 milli node hours, inclusive. |
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. By default, the early stopping feature is enabled, which means that AutoML Tables might stop training before the entire training budget has been used. |
`weight_column_name` |
`str`
Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1. |
`export_evaluated_data_items_config` |
Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed. |
`additional_experiments` |
`MutableSequence[str]`
Additional experiment flags for the Tables training pipeline. |

## Classes

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### AutoMlTablesInputs

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### AutoMlTablesInputs

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.gen_ai_cache_service.pagers.ListCachedContentsAsyncPager -->

# Class ListCachedContentsAsyncPager (1.134.0)

```
ListCachedContentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_cached_contents`

requests.

This class thinly wraps an initial
[ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse) object, and
provides an `__aiter__`

method to iterate through its
`cached_contents`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListCachedContents`

requests and continue to iterate
through the `cached_contents`

field on the
corresponding responses.

All the usual [ListCachedContentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCachedContentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListCachedContentsAsyncPager

```
ListCachedContentsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsRequest,
response: google.cloud.aiplatform_v1beta1.types.gen_ai_cache_service.ListCachedContentsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_service.pagers.ListModelVersionCheckpointsPager -->

# Class ListModelVersionCheckpointsPager (1.134.0)

```
ListModelVersionCheckpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_model_version_checkpoints`

requests.

This class thinly wraps an initial
[ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsResponse) object, and
provides an `__iter__`

method to iterate through its
`checkpoints`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelVersionCheckpoints`

requests and continue to iterate
through the `checkpoints`

field on the
corresponding responses.

All the usual [ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionCheckpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionCheckpointsPager

```
ListModelVersionCheckpointsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_service.ListModelVersionCheckpointsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeployIndexOperationMetadata -->

# Class DeployIndexOperationMetadata (1.134.0)

```
DeployIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.DeployIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`deployed_index_id` |
`str`
The unique index id specified by user |

## Methods

### DeployIndexOperationMetadata

```
DeployIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.DeployIndex.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListSchedulesResponse -->

# Class ListSchedulesResponse (1.134.0)

`ListSchedulesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ScheduleService.ListSchedules

## Attributes |
|
|---|---|
Name |
Description |
`schedules` |
`MutableSequence[`
List of Schedules in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListSchedulesRequest.page_token to obtain that page. |

## Methods

### ListSchedulesResponse

`ListSchedulesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ScheduleService.ListSchedules

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.NasJobSpec -->

# Class NasJobSpec (1.134.0)

`NasJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a NasJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`multi_trial_algorithm_spec` |
The spec of multi-trial algorithms. This field is a member of `oneof` _ `nas_algorithm_spec` .
|
`resume_nas_job_id` |
`str`
The ID of the existing NasJob in the same Project and Location which will be used to resume search. search_space_spec and nas_algorithm_spec are obtained from previous NasJob hence should not provide them again for this NasJob. |
`search_space_spec` |
`str`
It defines the search space for Neural Architecture Search (NAS). |

## Classes

### MultiTrialAlgorithmSpec

`MultiTrialAlgorithmSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of multi-trial Neural Architecture Search (NAS).

## Methods

### NasJobSpec

`NasJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a NasJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.persistent_resource_service.pagers.ListPersistentResourcesPager -->

# Class ListPersistentResourcesPager (1.134.0)

```
ListPersistentResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
],
request: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_persistent_resources`

requests.

This class thinly wraps an initial
[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse) object, and
provides an `__iter__`

method to iterate through its
`persistent_resources`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPersistentResources`

requests and continue to iterate
through the `persistent_resources`

field on the
corresponding responses.

All the usual [ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListPersistentResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPersistentResourcesPager

```
ListPersistentResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
],
request: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1.types.persistent_resource_service.ListPersistentResourcesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Artifact -->

# Class Artifact (1.134.0)

`Artifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general artifact.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Artifact. |
`display_name` |
`str`
User provided display name of the Artifact. May be up to 128 Unicode characters. |
`uri` |
`str`
The uniform resource identifier of the artifact file. May be empty if there is no actual artifact file. |
`etag` |
`str`
An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Artifacts. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Artifact (System labels are excluded). |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Artifact was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Artifact was last updated. |
`state` |
The state of this Artifact. This is a property of the Artifact, and does not imply or capture any ongoing process. This property is managed by clients (such as Vertex AI Pipelines), and the system does not prescribe or check the validity of state transitions. |
`schema_title` |
`str`
The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`schema_version` |
`str`
The version of the schema in schema_name to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Artifact. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB. |
`description` |
`str`
Description of the Artifact |

## Classes

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

### State

`State(value)`


Describes the state of the Artifact.

## Methods

### Artifact

`Artifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general artifact.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.tensorboard_service.pagers.ListTensorboardExperimentsPager -->

# Class ListTensorboardExperimentsPager (1.134.0)

```
ListTensorboardExperimentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboard_experiments`

requests.

This class thinly wraps an initial
[ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboard_experiments`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboardExperiments`

requests and continue to iterate
through the `tensorboard_experiments`

field on the
corresponding responses.

All the usual [ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardExperimentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardExperimentsPager

```
ListTensorboardExperimentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
],
request: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1.types.tensorboard_service.ListTensorboardExperimentsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs -->

# Class AutoMlTablesInputs (1.134.0)

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`optimization_objective_recall_value` |
`float`
Required when optimization_objective is "maximize-precision-at-recall". Must be between 0 and 1, inclusive. This field is a member of `oneof` _ `additional_optimization_objective_config` .
|
`optimization_objective_precision_value` |
`float`
Required when optimization_objective is "maximize-recall-at-precision". Must be between 0 and 1, inclusive. This field is a member of `oneof` _ `additional_optimization_objective_config` .
|
`prediction_type` |
`str`
The type of prediction the Model is to produce. "classification" - Predict one out of multiple target values is picked for each row. "regression" - Predict a value based on its relation to other values. This type is available only to columns that contain semantically numeric values, i.e. integers or floating point number, even if stored as e.g. strings. |
`target_column` |
`str`
The column name of the target column that the model is to predict. |
`transformations` |
`MutableSequence[`
Each transformation will apply transform function to given input column. And the result will be used for training. When creating transformation for BigQuery Struct column, the column should be flattened using "." as the delimiter. |
`optimization_objective` |
`str`
Objective function the model is optimizing towards. The training process creates a model that maximizes/minimizes the value of the objective function over the validation set. The supported optimization objectives depend on the prediction type. If the field is not set, a default objective function is used. classification (binary): "maximize-au-roc" (default) - Maximize the area under the receiver operating characteristic (ROC) curve. "minimize-log-loss" - Minimize log loss. "maximize-au-prc" - Maximize the area under the precision-recall curve. "maximize-precision-at-recall" - Maximize precision for a specified recall value. "maximize-recall-at-precision" - Maximize recall for a specified precision value. classification (multi-class): "minimize-log-loss" (default) - Minimize log loss. regression: "minimize-rmse" (default) - Minimize root-mean-squared error (RMSE). "minimize-mae" - Minimize mean-absolute error (MAE). "minimize-rmsle" - Minimize root-mean-squared log error (RMSLE). |
`train_budget_milli_node_hours` |
`int`
Required. The train budget of creating this model, expressed in milli node hours i.e. 1,000 value in this field means 1 node hour. The training cost of the model will not exceed this budget. The final cost will be attempted to be close to the budget, though may end up being (even) noticeably smaller - at the backend's discretion. This especially may happen when further model training ceases to provide any improvements. If the budget is set to a value known to be insufficient to train a model for the given dataset, the training won't be attempted and will error. The train budget must be between 1,000 and 72,000 milli node hours, inclusive. |
`disable_early_stopping` |
`bool`
Use the entire training budget. This disables the early stopping feature. By default, the early stopping feature is enabled, which means that AutoML Tables might stop training before the entire training budget has been used. |
`weight_column_name` |
`str`
Column name that should be used as the weight column. Higher values in this column give more importance to the row during model training. The column must have numeric values between 0 and 10000 inclusively; 0 means the row is ignored for training. If weight column field is not set, then all rows are assumed to have equal weight of 1. |
`export_evaluated_data_items_config` |
Configuration for exporting test set predictions to a BigQuery table. If this configuration is absent, then the export is not performed. |
`additional_experiments` |
`MutableSequence[str]`
Additional experiment flags for the Tables training pipeline. |

## Classes

### Transformation

`Transformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Methods

### AutoMlTablesInputs

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

### AutoMlTablesInputs

`AutoMlTablesInputs(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UploadModelResponse -->

# Class UploadModelResponse (1.134.0)

`UploadModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message of ModelService.UploadModel operation.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
The name of the uploaded Model resource. Format: `projects/{project}/locations/{location}/models/{model}`
|
`model_version_id` |
`str`
Output only. The version ID of the model that is uploaded. |

## Methods

### UploadModelResponse

`UploadModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message of ModelService.UploadModel operation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchDataItemsResponse -->

# Class SearchDataItemsResponse (1.134.0)

`SearchDataItemsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.SearchDataItems.

## Attributes |
|
|---|---|
Name |
Description |
`data_item_views` |
`MutableSequence[`
The DataItemViews read. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to SearchDataItemsRequest.page_token to obtain that page. |

## Methods

### SearchDataItemsResponse

`SearchDataItemsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.SearchDataItems.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse -->

# Class ListTrialsResponse (1.134.0)

`ListTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListTrials.

## Attributes |
|
|---|---|
Name |
Description |
`trials` |
`MutableSequence[`
The Trials associated with the Study. |
`next_page_token` |
`str`
Pass this token as the `page_token` field of the request
for a subsequent call. If this field is omitted, there are
no subsequent pages.
|

## Methods

### ListTrialsResponse

`ListTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListTrials.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSpecialistPoolOperationMetadata -->

# Class CreateSpecialistPoolOperationMetadata (1.134.0)

```
CreateSpecialistPoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for SpecialistPoolService.CreateSpecialistPool.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### CreateSpecialistPoolOperationMetadata

```
CreateSpecialistPoolOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for SpecialistPoolService.CreateSpecialistPool.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PipelineTaskExecutorDetail.ContainerDetail -->

# Class ContainerDetail (1.134.0)

`ContainerDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The detail of a container execution. It contains the job names of the lifecycle of a container execution.

## Attributes |
|
|---|---|
Name |
Description |
`main_job` |
`str`
Output only. The name of the CustomJob for the main container execution. |
`pre_caching_check_job` |
`str`
Output only. The name of the CustomJob for the pre-caching-check container execution. This job will be available if the PipelineJob.pipeline_spec specifies the `pre_caching_check` hook in the lifecycle
events.
|
`failed_main_jobs` |
`MutableSequence[str]`
Output only. The names of the previously failed CustomJob for the main container executions. The list includes the all attempts in chronological order. |
`failed_pre_caching_check_jobs` |
`MutableSequence[str]`
Output only. The names of the previously failed CustomJob for the pre-caching-check container executions. This job will be available if the PipelineJob.pipeline_spec specifies the `pre_caching_check` hook in the lifecycle
events. The list includes the all attempts in chronological
order.
|

## Methods

### ContainerDetail

`ContainerDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The detail of a container execution. It contains the job names of the lifecycle of a container execution.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateRagEngineConfigOperationMetadata -->

# Class UpdateRagEngineConfigOperationMetadata (1.134.0)

```
UpdateRagEngineConfigOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for VertexRagDataService.UpdateRagEngineConfig.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateRagEngineConfigOperationMetadata

```
UpdateRagEngineConfigOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for VertexRagDataService.UpdateRagEngineConfig.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListMemoriesResponse -->

# Class ListMemoriesResponse (1.134.0)

`ListMemoriesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MemoryBankService.ListMemories.

## Attributes |
|
|---|---|
Name |
Description |
`memories` |
`MutableSequence[`
List of Memories in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListMemoriesRequest.page_token to obtain that page. |

## Methods

### ListMemoriesResponse

`ListMemoriesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for MemoryBankService.ListMemories.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelVersionsRequest -->

# Class ListModelVersionsRequest (1.134.0)

`ListModelVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModelVersions.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the model to list versions for. |
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. Typically obtained via next_page_token of the previous ListModelVersions call. |
`filter` |
`str`
An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- \`labels.key:\* or labels:key - key existence
- A key including a space must be quoted.
`labels."a key"` .
Some examples:
- `labels.myKey="myValue"`
|
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `create_time`
- `update_time`
Example: `update_time asc, create_time desc` .
|

## Methods

### ListModelVersionsRequest

`ListModelVersionsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelService.ListModelVersions.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CreateRagCorpusRequest -->

# Class CreateRagCorpusRequest (1.134.0)

`CreateRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.CreateRagCorpus.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the RagCorpus in. Format: `projects/{project}/locations/{location}`
|
`rag_corpus` |
Required. The RagCorpus to create. |

## Methods

### CreateRagCorpusRequest

`CreateRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.CreateRagCorpus.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCustomJobsResponse -->

# Class ListCustomJobsResponse (1.134.0)

`ListCustomJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListCustomJobs

## Attributes |
|
|---|---|
Name |
Description |
`custom_jobs` |
`MutableSequence[`
List of CustomJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListCustomJobsRequest.page_token to obtain that page. |

## Methods

### ListCustomJobsResponse

`ListCustomJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListCustomJobs

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsPager -->

# Class QueryDeployedModelsPager (1.134.0)

```
QueryDeployedModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `query_deployed_models`

requests.

This class thinly wraps an initial
[QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse) object, and
provides an `__iter__`

method to iterate through its
`deployed_models`

field.

If there are more pages, the `__iter__`

method will make additional
`QueryDeployedModels`

requests and continue to iterate
through the `deployed_models`

field on the
corresponding responses.

All the usual [QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QueryDeployedModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### QueryDeployedModelsPager

```
QueryDeployedModelsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.ListModelMonitorsAsyncPager -->

# Class ListModelMonitorsAsyncPager (1.134.0)

```
ListModelMonitorsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_model_monitors`

requests.

This class thinly wraps an initial
[ListModelMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_monitors`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelMonitors`

requests and continue to iterate
through the `model_monitors`

field on the
corresponding responses.

All the usual [ListModelMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitorsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelMonitorsAsyncPager

```
ListModelMonitorsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitorsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureGroupsAsyncPager -->

# Class ListFeatureGroupsAsyncPager (1.134.0)

```
ListFeatureGroupsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_feature_groups`

requests.

This class thinly wraps an initial
[ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_groups`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureGroups`

requests and continue to iterate
through the `feature_groups`

field on the
corresponding responses.

All the usual [ListFeatureGroupsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureGroupsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureGroupsAsyncPager

```
ListFeatureGroupsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureGroupsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Artifact -->

# Class Artifact (1.134.0)

`Artifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general artifact.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the Artifact. |
`display_name` |
`str`
User provided display name of the Artifact. May be up to 128 Unicode characters. |
`uri` |
`str`
The uniform resource identifier of the artifact file. May be empty if there is no actual artifact file. |
`etag` |
`str`
An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`labels` |
`MutableMapping[str, str]`
The labels with user-defined metadata to organize your Artifacts. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Artifact (System labels are excluded). |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Artifact was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this Artifact was last updated. |
`state` |
The state of this Artifact. This is a property of the Artifact, and does not imply or capture any ongoing process. This property is managed by clients (such as Vertex AI Pipelines), and the system does not prescribe or check the validity of state transitions. |
`schema_title` |
`str`
The title of the schema describing the metadata. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`schema_version` |
`str`
The version of the schema in schema_name to use. Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store. |
`metadata` |
`google.protobuf.struct_pb2.Struct`
Properties of the Artifact. Top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB. |
`description` |
`str`
Description of the Artifact |

## Classes

### LabelsEntry

`LabelsEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

### State

`State(value)`


Describes the state of the Artifact.

## Methods

### Artifact

`Artifact(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a general artifact.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.TimestampSplit -->

# Class TimestampSplit (1.134.0)

`TimestampSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on a provided timestamps. The youngest data pieces are assigned to training set, next to validation set, and the oldest to the test set.

Supported only for tabular Datasets.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |
`key` |
`str`
Required. The key is a name of one of the Dataset's data columns. The values of the key (the values in the column) must be in RFC 3339 `date-time` format, where
`time-offset` = `"Z"` (e.g. 1985-04-12T23:20:50.52Z). If
for a piece of data the key is not present or has an invalid
value, that piece is ignored by the pipeline.
|

## Methods

### TimestampSplit

`TimestampSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on a provided timestamps. The youngest data pieces are assigned to training set, next to validation set, and the oldest to the test set.

Supported only for tabular Datasets.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GenerateContentResponse -->

# Class GenerateContentResponse (1.134.0)

`GenerateContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for [PredictionService.GenerateContent].

## Attributes |
|
|---|---|
Name |
Description |
`candidates` |
`MutableSequence[`
Output only. Generated candidates. |
`model_version` |
`str`
Output only. The model version used to generate the response. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when the request is made to the server. |
`response_id` |
`str`
Output only. response_id is used to identify each response. It is the encoding of the event_id. |
`prompt_feedback` |
Output only. Content filter results for a prompt sent in the request. Note: Sent only in the first stream chunk. Only happens when no candidates were generated due to content violations. |
`usage_metadata` |
Usage metadata about the response(s). |

## Classes

### PromptFeedback

`PromptFeedback(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Content filter results for a prompt sent in the request.

### UsageMetadata

`UsageMetadata(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Usage metadata about response(s).

## Methods

### GenerateContentResponse

`GenerateContentResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for [PredictionService.GenerateContent].

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Model -->

# Class Model (1.134.0)

```
Model(
model_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
version: typing.Optional[str] = None,
)
```


Retrieves the model resource and instantiates its representation.

## Parameters |
|
|---|---|
Name |
Description |
`model_name` |
`str`
Required. A fully-qualified model resource name or model ID. Example: "projects/123/locations/us-central1/models/456" or "456" when project and location are initialized or passed. May optionally contain a version ID or version alias in {model_name}@{version} form. See version arg. |
`project` |
`str`
Optional project to retrieve model from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional location to retrieve model from. If not set, location set in aiplatform.init will be used. |
`version` |
`str`
Optional. Version ID or version alias. When set, the specified model version will be targeted unless overridden in method calls. When not set, the model with the "default" alias will be targeted unless overridden in method calls. No behavior change if only one version of a model exists. |

## Properties

### container_spec

The specification of the container that is to be used when deploying this Model. Not present for AutoML Models.

### create_time

Time this resource was created.

### description

Description of the model.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### predict_schemata

The schemata that describe formats of the Model's predictions and explanations, if available.

### preview

Return a Model instance with preview features enabled.

### resource_name

Full qualified resource name, without any version ID.

### supported_deployment_resources_types

List of deployment resource types accepted for this Model.

When this Model is deployed, its prediction resources are described by
the `prediction_resources`

field of the objects returned by
`Endpoint.list_models()`

. Because not all Models support all resource
configuration types, the configuration types this Model supports are
listed here.

If no configuration types are listed, the Model cannot be
deployed to an `Endpoint`

and does not support online predictions
(`Endpoint.predict()`

or `Endpoint.explain()`

). Such a Model can serve
predictions by using a `BatchPredictionJob`

, if it has at least one entry
each in `Model.supported_input_storage_formats`

and
`Model.supported_output_storage_formats`

.

### supported_export_formats

The formats and content types in which this Model may be exported. If empty, this Model is not available for export.

For example, if this model can be exported as a Tensorflow SavedModel and have the artifacts written to Cloud Storage, the expected value would be:

```
{'tf-saved-model': [<ExportableContent.ARTIFACT: 1>]}
```


### supported_input_storage_formats

The formats this Model supports in the `input_config`

field of a
`BatchPredictionJob`

. If `Model.predict_schemata.instance_schema_uri`

exists, the instances should be given as per that schema.

[Read the docs for more on batch prediction formats](https://cloud.google.com/vertex-ai/docs/predictions/batch-predictions#batch_request_input)

If this Model doesn't support any of these formats it means it cannot be
used with a `BatchPredictionJob`

. However, if it has
`supported_deployment_resources_types`

, it could serve online predictions
by using `Endpoint.predict()`

or `Endpoint.explain()`

.

### supported_output_storage_formats

The formats this Model supports in the `output_config`

field of a
`BatchPredictionJob`

.

If both `Model.predict_schemata.instance_schema_uri`

and
`Model.predict_schemata.prediction_schema_uri`

exist, the predictions
are returned together with their instances. In other words, the
prediction has the original instance data first, followed by the actual
prediction content (as per the schema).

[Read the docs for more on batch prediction formats](https://cloud.google.com/vertex-ai/docs/predictions/batch-predictions)

If this Model doesn't support any of these formats it means it cannot be
used with a `BatchPredictionJob`

. However, if it has
`supported_deployment_resources_types`

, it could serve online predictions
by using `Endpoint.predict()`

or `Endpoint.explain()`

.

### training_job

The TrainingJob that uploaded this Model, if any.

Exceptions |
|
|---|---|
Type |
Description |
`api_core.exceptions.NotFound` |
If the Model's training job resource cannot be found on the Vertex service. |

### update_time

Time this resource was last updated.

### uri

Path to the directory containing the Model artifact and any of its supporting files. Not present for AutoML Models.

### version_aliases

User provided version aliases so that a model version can be referenced via
alias (i.e. projects/{project}/locations/{location}/models/{model_id}@{version_alias}
instead of auto-generated version id (i.e.
projects/{project}/locations/{location}/models/{model_id}@{version_id}).
The format is `a-z][a-zA-Z0-9-]`

{0,126}[a-z0-9] to distinguish from
version_id. A default version alias will be created for the first version
of the model, and there must be exactly one default version alias for a model.

### version_create_time

Timestamp when this version was created.

### version_description

The description of this version.

### version_id

The version ID of the model. A new version is committed when a new model version is uploaded or trained under an existing model id. It is an auto-incrementing decimal number in string representation.

### version_update_time

Timestamp when this version was updated.

### versioned_resource_name

The fully-qualified resource name, including the version ID. For example, projects/{project}/locations/{location}/models/{model_id}@{version_id}

### versioning_registry

The registry of model versions associated with this Model instance.

## Methods

### batch_predict

```
batch_predict(
job_display_name: typing.Optional[str] = None,
gcs_source: typing.Optional[typing.Union[str, typing.Sequence[str]]] = None,
bigquery_source: typing.Optional[str] = None,
instances_format: str = "jsonl",
gcs_destination_prefix: typing.Optional[str] = None,
bigquery_destination_prefix: typing.Optional[str] = None,
predictions_format: str = "jsonl",
model_parameters: typing.Optional[typing.Dict] = None,
machine_type: typing.Optional[str] = None,
accelerator_type: typing.Optional[str] = None,
accelerator_count: typing.Optional[int] = None,
starting_replica_count: typing.Optional[int] = None,
max_replica_count: typing.Optional[int] = None,
generate_explanation: typing.Optional[bool] = False,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
encryption_spec_key_name: typing.Optional[str] = None,
sync: bool = True,
create_request_timeout: typing.Optional[float] = None,
batch_size: typing.Optional[int] = None,
service_account: typing.Optional[str] = None,
) -> google.cloud.aiplatform.jobs.BatchPredictionJob
```


Creates a batch prediction job using this Model and outputs
prediction results to the provided destination prefix in the specified
`predictions_format`

. One source and one destination prefix are
required.

Example usage: my_model.batch_predict( job_display_name="prediction-123", gcs_source="gs://example-bucket/instances.csv", instances_format="csv", bigquery_destination_prefix="projectId.bqDatasetId.bqTableId" )

Parameters |
|
|---|---|
Name |
Description |
`job_display_name` |
`str`
Optional. The user-defined name of the BatchPredictionJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`gcs_source` |
`typing.Union[str, typing.Sequence[str], NoneType]`
Optional[Sequence[str]] = None Google Cloud Storage URI(-s) to your instances to run batch prediction on. They must match |
`bigquery_source` |
`typing.Optional[str]`
Optional[str] = None BigQuery URI to a table, up to 2000 characters long. For example: |
`instances_format` |
`str`
str = "jsonl" The format in which instances are provided. Must be one of the formats listed in |
`gcs_destination_prefix` |
`typing.Optional[str]`
Optional[str] = None The Google Cloud Storage location of the directory where the output is to be written to. In the given directory a new directory is created. Its name is |
`bigquery_destination_prefix` |
`typing.Optional[str]`
Optional[str] = None The BigQuery URI to a project or table, up to 2000 characters long. When only the project is specified, the Dataset and Table is created. When the full table reference is specified, the Dataset must exist and table must not exist. Accepted forms: |
`predictions_format` |
`str`
str = "jsonl" Required. The format in which Vertex AI outputs the predictions, must be one of the formats specified in |
`model_parameters` |
`typing.Optional[typing.Dict]`
Optional[Dict] = None Optional. The parameters that govern the predictions. The schema of the parameters may be specified via the Model's |
`machine_type` |
`typing.Optional[str]`
Optional[str] = None Optional. The type of machine for running batch prediction on dedicated resources. Not specifying machine type will result in batch prediction job being run with automatic resources. |
`accelerator_type` |
`typing.Optional[str]`
Optional[str] = None Optional. The type of accelerator(s) that may be attached to the machine as per |
`accelerator_count` |
`typing.Optional[int]`
Optional[int] = None Optional. The number of accelerators to attach to the |
`starting_replica_count` |
`typing.Optional[int]`
Optional[int] = None The number of machine replicas used at the start of the batch operation. If not set, Vertex AI decides starting number, not greater than |
`max_replica_count` |
`typing.Optional[int]`
Optional[int] = None The maximum number of machine replicas the batch operation may be scaled to. Only used if |
`generate_explanation` |
`bool`
Optional. Generate explanation along with the batch prediction results. This will cause the batch prediction output to include explanations based on the |
`explanation_metadata` |
`aiplatform.explain.ExplanationMetadata`
Optional. Explanation metadata configuration for this BatchPredictionJob. Can be specified only if |
`explanation_parameters` |
`aiplatform.explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. Can be specified only if |
`labels` |
`typing.Optional[typing.Dict[str, str]]`
Optional[Dict[str, str]] = None Optional. The labels with user-defined metadata to organize your BatchPredictionJobs. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`credentials` |
`typing.Optional[google.auth.credentials.Credentials]`
Optional[auth_credentials.Credentials] = None Optional. Custom credentials to use to create this batch prediction job. Overrides credentials set in aiplatform.init. |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`create_request_timeout` |
`float`
Optional. The timeout for the create request in seconds. |
`batch_size` |
`int`
Optional. The number of the records (e.g. instances) of the operation given in each batch to a machine replica. Machine type, and size of a single record should be considered when setting this parameter, higher value speeds up the batch operation's execution, but too high value will result in a whole batch not fitting in a machine's memory, and the whole operation will fail. The default value is 64. |
`service_account` |
`str`
Optional. Specifies the service account for workload run-as account. Users submitting jobs must have act-as permission on this run-as account. |

Returns |
|
|---|---|
Type |
Description |
`job (jobs.BatchPredictionJob)` |
Instantiated representation of the created batch prediction job. |

### copy

```
copy(
destination_location: str,
destination_model_id: typing.Optional[str] = None,
destination_parent_model: typing.Optional[str] = None,
encryption_spec_key_name: typing.Optional[str] = None,
copy_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Model
```


Copys a model and returns a Model representing the copied Model resource. This method is a blocking call.

Example usage: copied_model = my_model.copy( destination_location="us-central1" )

Parameters |
|
|---|---|
Name |
Description |
`destination_location` |
`str`
The destination location to copy the model to. |
`destination_model_id` |
`str`
Optional. The ID to use for the copied Model, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`destination_parent_model` |
`str`
Optional. The resource name or model ID of an existing model that the newly-copied model will be a version of. Only set this field when copying as a new version of an existing model. |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`copy_request_timeout` |
`float`
Optional. The timeout for the copy request in seconds. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If both `destination_model_id` and `destination_parent_model` are set. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Instantiated representation of the copied model resource. |

### delete

`delete(sync: bool = True) -> None`


Deletes this Vertex AI resource. WARNING: This deletion is permanent.

### deploy

```
deploy(
endpoint: typing.Optional[
typing.Union[
google.cloud.aiplatform.models.Endpoint,
google.cloud.aiplatform.models.PrivateEndpoint,
]
] = None,
deployed_model_display_name: typing.Optional[str] = None,
traffic_percentage: typing.Optional[int] = 0,
traffic_split: typing.Optional[typing.Dict[str, int]] = None,
machine_type: typing.Optional[str] = None,
min_replica_count: int = 1,
max_replica_count: int = 1,
accelerator_type: typing.Optional[str] = None,
accelerator_count: typing.Optional[int] = None,
gpu_partition_size: typing.Optional[str] = None,
tpu_topology: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
metadata: typing.Optional[typing.Sequence[typing.Tuple[str, str]]] = (),
encryption_spec_key_name: typing.Optional[str] = None,
network: typing.Optional[str] = None,
sync=True,
deploy_request_timeout: typing.Optional[float] = None,
autoscaling_target_cpu_utilization: typing.Optional[int] = None,
autoscaling_target_accelerator_duty_cycle: typing.Optional[int] = None,
autoscaling_target_request_count_per_minute: typing.Optional[int] = None,
autoscaling_target_pubsub_num_undelivered_messages: typing.Optional[int] = None,
autoscaling_pubsub_subscription_labels: typing.Optional[
typing.Dict[str, str]
] = None,
enable_access_logging=False,
disable_container_logging: bool = False,
private_service_connect_config: typing.Optional[
google.cloud.aiplatform.models.PrivateEndpoint.PrivateServiceConnectConfig
] = None,
deployment_resource_pool: typing.Optional[
google.cloud.aiplatform.models.DeploymentResourcePool
] = None,
reservation_affinity_type: typing.Optional[str] = None,
reservation_affinity_key: typing.Optional[str] = None,
reservation_affinity_values: typing.Optional[typing.List[str]] = None,
spot: bool = False,
fast_tryout_enabled: bool = False,
system_labels: typing.Optional[typing.Dict[str, str]] = None,
required_replica_count: typing.Optional[int] = 0,
) -> typing.Union[
google.cloud.aiplatform.models.Endpoint,
google.cloud.aiplatform.models.PrivateEndpoint,
]
```


Deploys model to endpoint. Endpoint will be created if unspecified.

Parameters |
|
|---|---|
Name |
Description |
`endpoint` |
`Union[Endpoint, PrivateEndpoint]`
Optional. Public or private Endpoint to deploy model to. If not specified, endpoint display name will be model display name+'_endpoint'. |
`deployed_model_display_name` |
`str`
Optional. The display name of the DeployedModel. If not provided upon creation, the Model's display_name is used. |
`traffic_percentage` |
`int`
Optional. Desired traffic to newly deployed model. Defaults to 0 if there are pre-existing deployed models. Defaults to 100 if there are no pre-existing deployed models. Negative values should not be provided. Traffic of previously deployed models at the endpoint will be scaled down to accommodate new deployed model's traffic. Should not be provided if traffic_split is provided. |
`traffic_split` |
`Dict[str, int]`
Optional. A map from a DeployedModel's ID to the percentage of this Endpoint's traffic that should be forwarded to that DeployedModel. If a DeployedModel's ID is not listed in this map, then it receives no traffic. The traffic percentage values must add up to 100, or map must be empty if the Endpoint is to not accept any traffic at the moment. Key for model being deployed is "0". Should not be provided if traffic_percentage is provided. |
`machine_type` |
`str`
Optional. The type of machine. Not specifying machine type will result in model to be deployed with automatic resources. |
`min_replica_count` |
`int`
Optional. The minimum number of machine replicas this deployed model will be always deployed on. If traffic against it increases, it may dynamically be deployed onto more replicas, and as traffic decreases, some of these extra replicas may be freed. |
`max_replica_count` |
`int`
Optional. The maximum number of replicas this deployed model may be deployed on when the traffic against it increases. If requested value is too large, the deployment will error, but if deployment succeeds then the ability to scale the model to that many replicas is guaranteed (barring service outages). If traffic against the deployed model increases beyond what its replicas at maximum may handle, a portion of the traffic will be dropped. If this value is not provided, the smaller value of min_replica_count or 1 will be used. |
`accelerator_type` |
`str`
Optional. Hardware accelerator type. Must also set accelerator_count if used. One of ACCELERATOR_TYPE_UNSPECIFIED, NVIDIA_TESLA_K80, NVIDIA_TESLA_P100, NVIDIA_TESLA_V100, NVIDIA_TESLA_P4, NVIDIA_TESLA_T4 |
`accelerator_count` |
`int`
Optional. The number of accelerators to attach to a worker replica. |
`gpu_partition_size` |
`str`
Optional. The GPU partition Size for Nvidia MIG. |
`tpu_topology` |
`str`
Optional. The TPU topology to use for the DeployedModel. Requireid for CloudTPU multihost deployments. |
`service_account` |
`str`
The service account that the DeployedModel's container runs as. Specify the email address of the service account. If this service account is not specified, the container runs as a service account that doesn't have access to the resource project. Users deploying the Model must have the |
`explanation_metadata` |
`aiplatform.explain.ExplanationMetadata`
Optional. Metadata describing the Model's input and output for explanation. |
`explanation_parameters` |
`aiplatform.explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. For more details, see |
`metadata` |
`Sequence[Tuple[str, str]]`
Optional. Strings which should be sent along with the request as metadata. |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`network` |
`str`
Optional. The full name of the Compute Engine network to which the Endpoint, if created, will be peered to. E.g. "projects/12345/global/networks/myVPC" Private services access must already be configured for the network. If set or aiplatform.init(network=...) has been set, a PrivateEndpoint will be created. If left unspecified, an Endpoint will be created. Read more about PrivateEndpoints |
`deploy_request_timeout` |
`float`
Optional. The timeout for the deploy request in seconds. |
`autoscaling_target_cpu_utilization` |
`int`
Target CPU Utilization to use for Autoscaling Replicas. A default value of 60 will be used if not specified. |
`autoscaling_target_accelerator_duty_cycle` |
`int`
Target Accelerator Duty Cycle. Must also set accelerator_type and accelerator_count if specified. A default value of 60 will be used if not specified. |
`autoscaling_target_request_count_per_minute` |
`int`
Optional. The target number of requests per minute for autoscaling. If set, the model will be scaled based on the number of requests it receives. |
`autoscaling_target_pubsub_num_undelivered_messages` |
`int`
Optional. The target number of pubsub undelivered messages for autoscaling. If set, the model will be scaled based on the pubsub queue size. |
`autoscaling_pubsub_subscription_labels` |
`Dict[str, str]`
Optional. Monitored resource labels as key value pairs for metric filtering for pubsub_num_undelivered_messages. |
`disable_container_logging` |
`bool`
If True, container logs from the deployed model will not be written to Cloud Logging. Defaults to False. |
`private_service_connect_config` |
`PrivateEndpoint.PrivateServiceConnectConfig`
If true, the endpoint can be accessible via |
`deployment_resource_pool` |
`DeploymentResourcePool`
Resource pool where the model will be deployed. All models that are deployed to the same DeploymentResourcePool will be hosted in a shared model server. If provided, will override replica count arguments. |
`reservation_affinity_type` |
`str`
Optional. The type of reservation affinity. One of NO_RESERVATION, ANY_RESERVATION, SPECIFIC_RESERVATION, SPECIFIC_THEN_ANY_RESERVATION, SPECIFIC_THEN_NO_RESERVATION |
`reservation_affinity_key` |
`str`
Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use |
`reservation_affinity_values` |
`List[str]`
Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation. Format: 'projects/{project_id_or_number}/zones/{zone}/reservations/{reservation_name}' |
`spot` |
`bool`
Optional. Whether to schedule the deployment workload on spot VMs. |
`fast_tryout_enabled` |
`bool`
Optional. Defaults to False. If True, model will be deployed using faster deployment path. Useful for quick experiments. Not for production workloads. Only available for most popular models with certain machine types. |
`system_labels` |
`Dict[str, str]`
Optional. System labels to apply to Model Garden deployments. System labels are managed by Google for internal use only. |
`required_replica_count` |
`int`
Optional. Number of required available replicas for the deployment to succeed. This field is only needed when partial model deployment/mutation is desired, with a value greater than or equal to 1 and fewer than or equal to min_replica_count. If set, the model deploy/mutate operation will succeed once available_replica_count reaches required_replica_count, and the rest of the replicas will be retried. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |
`enable_access_logging` |
`bool`
Whether to enable endpoint access logging. Defaults to False. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `traffic_split` is set for PrivateEndpoint. |

Returns |
|
|---|---|
Type |
Description |
`endpoint (Union[Endpoint, PrivateEndpoint])` |
Endpoint with the deployed model. |

### evaluate

```
evaluate(
prediction_type: str,
target_field_name: str,
gcs_source_uris: typing.Optional[typing.List[str]] = None,
bigquery_source_uri: typing.Optional[str] = None,
bigquery_destination_output_uri: typing.Optional[str] = None,
class_labels: typing.Optional[typing.List[str]] = None,
prediction_label_column: typing.Optional[str] = None,
prediction_score_column: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
service_account: typing.Optional[str] = None,
generate_feature_attributions: bool = False,
evaluation_pipeline_display_name: typing.Optional[str] = None,
evaluation_metrics_display_name: typing.Optional[str] = None,
network: typing.Optional[str] = None,
encryption_spec_key_name: typing.Optional[str] = None,
experiment: typing.Optional[
typing.Union[
google.cloud.aiplatform.metadata.experiment_resources.Experiment, str
]
] = None,
enable_caching: typing.Optional[bool] = None,
) -> google.cloud.aiplatform.model_evaluation.model_evaluation_job._ModelEvaluationJob
```


Creates a model evaluation job running on Vertex Pipelines and returns the resulting ModelEvaluationJob resource.

Example usage:

```
```
my_model = Model(
model_name="projects/123/locations/us-central1/models/456"
)
my_evaluation_job = my_model.evaluate(
prediction_type="classification",
target_field_name="type",
data_source_uris=["gs://sdk-model-eval/my-prediction-data.csv"],
staging_bucket="gs://my-staging-bucket/eval_pipeline_root",
)
my_evaluation_job.wait()
my_evaluation = my_evaluation_job.get_model_evaluation()
my_evaluation.metrics
```
```


Parameters |
|
|---|---|
Name |
Description |
`prediction_type` |
`str`
Required. The problem type being addressed by this evaluation run. 'classification' and 'regression' are the currently supported problem types. |
`target_field_name` |
`str`
Required. The column name of the field containing the label for this prediction task. |
`gcs_source_uris` |
`List[str]`
Optional. A list of Cloud Storage data files containing the ground truth data to use for this evaluation job. These files should contain your model's prediction column. Currently only Google Cloud Storage urls are supported, for example: "gs://path/to/your/data.csv". The provided data files must be either CSV or JSONL. One of |
`bigquery_source_uri` |
`str`
Optional. A bigquery table URI containing the ground truth data to use for this evaluation job. This uri should be in the format 'bq://my-project-id.dataset.table'. One of |
`bigquery_destination_output_uri` |
`str`
Optional. A bigquery table URI where the Batch Prediction job associated with your Model Evaluation will write prediction output. This can be a BigQuery URI to a project ('bq://my-project'), a dataset ('bq://my-project.my-dataset'), or a table ('bq://my-project.my-dataset.my-table'). Required if |
`class_labels` |
`List[str]`
Optional. For custom (non-AutoML) classification models, a list of possible class names, in the same order that predictions are generated. This argument is required when prediction_type is 'classification'. For example, in a classification model with 3 possible classes that are outputted in the format: [0.97, 0.02, 0.01] with the class names "cat", "dog", and "fish", the value of |
`prediction_label_column` |
`str`
Optional. The column name of the field containing classes the model is scoring. Formatted to be able to find nested columns, delimited by |
`prediction_score_column` |
`str`
Optional. The column name of the field containing batch prediction scores. Formatted to be able to find nested columns, delimited by |
`staging_bucket` |
`str`
Optional. The GCS directory to use for staging files from this evaluation job. Defaults to the value set in aiplatform.init(staging_bucket=...) if not provided. Required if staging_bucket is not set in aiplatform.init(). |
`service_account` |
`str`
Specifies the service account for workload run-as account for this Model Evaluation PipelineJob. Users submitting jobs must have act-as permission on this run-as account. The service account running this Model Evaluation job needs the following permissions: Dataflow Worker, Storage Admin, Vertex AI Administrator, and Vertex AI Service Agent. |
`generate_feature_attributions` |
`boolean`
Optional. Whether the model evaluation job should generate feature attributions. Defaults to False if not specified. |
`evaluation_pipeline_display_name` |
`str`
Optional. The display name of your model evaluation job. This is the display name that will be applied to the Vertex Pipeline run for your evaluation job. If not set, a display name will be generated automatically. |
`evaluation_metrics_display_name` |
`str`
Optional. The display name of the model evaluation resource uploaded to Vertex from your Model Evaluation pipeline. |
`network` |
`str`
The full name of the Compute Engine network to which the job should be peered. For example, projects/12345/global/networks/myVPC. Private services access must already be configured for the network. If left unspecified, the job is not peered with any network. |
`encryption_spec_key_name` |
`str`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the job. Has the form: |
`experiment` |
`Union[str, experiments_resource.Experiment]`
Optional. The Vertex AI experiment name or instance to associate to the PipelineJob executing this model evaluation job. Metrics produced by the PipelineJob as system.Metric Artifacts will be associated as metrics to the provided experiment, and parameters from this PipelineJob will be associated as parameters to the provided experiment. |
`enable_caching` |
`bool`
Optional. Whether to turn on caching for the run. If this is not set, defaults to the compile time settings, which are True for all tasks by default, while users may specify different caching options for individual tasks. If this is set, the setting applies to all tasks in the pipeline. Overrides the compile time settings. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If staging_bucket was not set in aiplatform.init() and staging_bucket was not provided. If the provided `prediction_type` is not valid. If the provided `data_source_uris` don't start with 'gs://'. |

Returns |
|
|---|---|
Type |
Description |
`model_evaluation.ModelEvaluationJob` |
Instantiated representation of the _ModelEvaluationJob. |

### export_model

```
export_model(
export_format_id: str,
artifact_destination: typing.Optional[str] = None,
image_destination: typing.Optional[str] = None,
sync: bool = True,
) -> typing.Dict[str, str]
```


Exports a trained, exportable Model to a location specified by the user.
A Model is considered to be exportable if it has at least one `supported_export_formats`

.
Either `artifact_destination`

or `image_destination`

must be provided.

Example Usage: my_model.export( export_format_id="tf-saved-model", artifact_destination="gs://my-bucket/models/" )

```
or
my_model.export(
export_format_id="custom-model",
image_destination="us-central1-docker.pkg.dev/projectId/repo/image"
)
```


Parameters |
|
|---|---|
Name |
Description |
`export_format_id` |
`str`
Required. The ID of the format in which the Model must be exported. The list of export formats that this Model supports can be found by calling |
`artifact_destination` |
`str`
The Cloud Storage location where the Model artifact is to be written to. Under the directory given as the destination a new one with name " |
`image_destination` |
`str`
The Google Container Registry or Artifact Registry URI where the Model container image will be copied to. Accepted forms: - Google Container Registry path. For example: |
`sync` |
`bool`
Whether to execute this export synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If model does not support exporting. |
`ValueError` |
If invalid arguments or export formats are provided. |

Returns |
|
|---|---|
Type |
Description |
`output_info (Dict[str, str])` |
Details of the completed export with output destination paths to the artifacts or container image. |

### get_model_evaluation

```
get_model_evaluation(
evaluation_id: typing.Optional[str] = None,
) -> typing.Optional[
google.cloud.aiplatform.model_evaluation.model_evaluation.ModelEvaluation
]
```


Returns a ModelEvaluation resource and instantiates its representation. If no evaluation_id is passed, it will return the first evaluation associated with this model. If the aiplatform.Model resource was instantiated with a version, this will return a Model Evaluation from that version. If no version was specified when instantiating the Model resource, this will return an Evaluation from the default version.

Example usage: my_model = Model( model_name="projects/123/locations/us-central1/models/456" )

```
my_evaluation = my_model.get_model_evaluation(
evaluation_id="789"
)
# If no arguments are passed, this method returns the first evaluation for the model
my_evaluation = my_model.get_model_evaluation()
```


Parameter |
|
|---|---|
Name |
Description |
`evaluation_id` |
`str`
Optional. The ID of the model evaluation to retrieve. |

Returns |
|
|---|---|
Type |
Description |
`model_evaluation.ModelEvaluation` |
Instantiated representation of the ModelEvaluation resource. |

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.models.Model]
```


List all Model resource instances.

Example Usage: aiplatform.Model.list( filter='labels.my_label="my_label_value" AND display_name="my_model"', )

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: |
`project` |
`str`
Optional. Project to retrieve list from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve list from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve list. Overrides credentials set in aiplatform.init. |

Returns |
|
|---|---|
Type |
Description |
`List[models.Model]` |
A list of Model resource objects |

### list_model_evaluations

```
list_model_evaluations() -> (
typing.List[
google.cloud.aiplatform.model_evaluation.model_evaluation.ModelEvaluation
]
)
```


List all Model Evaluation resources associated with this model. If this Model resource was instantiated with a version, the Model Evaluation resources for that version will be returned. If no version was provided when the Model resource was instantiated, Model Evaluation resources will be returned for the default version.

Example Usage: my_model = Model( model_name="projects/123/locations/us-central1/models/456@1" )

```
my_evaluations = my_model.list_model_evaluations()
```


Returns |
|
|---|---|
Type |
Description |
`List[model_evaluation.ModelEvaluation]` |
List of ModelEvaluation resources for the model. |

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
) -> google.cloud.aiplatform.models.Model
```


Updates a model.

Example usage: my_model = my_model.update( display_name="my-model", description="my description", labels={'key': 'value'}, )

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`description` |
`str`
The description of the model. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `labels` is not the correct format. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Updated model resource. |

### upload

```
upload(
serving_container_image_uri: typing.Optional[str] = None,
*,
artifact_uri: typing.Optional[str] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: bool = True,
version_aliases: typing.Optional[typing.Sequence[str]] = None,
version_description: typing.Optional[str] = None,
serving_container_predict_route: typing.Optional[str] = None,
serving_container_health_route: typing.Optional[str] = None,
serving_container_invoke_route_prefix: typing.Optional[str] = None,
description: typing.Optional[str] = None,
serving_container_command: typing.Optional[typing.Sequence[str]] = None,
serving_container_args: typing.Optional[typing.Sequence[str]] = None,
serving_container_environment_variables: typing.Optional[
typing.Dict[str, str]
] = None,
serving_container_ports: typing.Optional[typing.Sequence[int]] = None,
serving_container_grpc_ports: typing.Optional[typing.Sequence[int]] = None,
local_model: typing.Optional[LocalModel] = None,
instance_schema_uri: typing.Optional[str] = None,
parameters_schema_uri: typing.Optional[str] = None,
prediction_schema_uri: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
display_name: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
sync=True,
upload_request_timeout: typing.Optional[float] = None,
serving_container_deployment_timeout: typing.Optional[int] = None,
serving_container_shared_memory_size_mb: typing.Optional[int] = None,
serving_container_startup_probe_exec: typing.Optional[typing.Sequence[str]] = None,
serving_container_startup_probe_period_seconds: typing.Optional[int] = None,
serving_container_startup_probe_timeout_seconds: typing.Optional[int] = None,
serving_container_health_probe_exec: typing.Optional[typing.Sequence[str]] = None,
serving_container_health_probe_period_seconds: typing.Optional[int] = None,
serving_container_health_probe_timeout_seconds: typing.Optional[int] = None,
model_garden_source_model_name: typing.Optional[str] = None,
model_garden_source_model_version_id: typing.Optional[str] = None
) -> Model
```


Uploads a model and returns a Model representing the uploaded Model resource.

Example usage: my_model = Model.upload( display_name="my-model", artifact_uri="gs://my-model/saved-model", serving_container_image_uri="tensorflow/serving" )

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If explanation_metadata is specified while explanation_parameters is not. Also if model directory does not contain a supported model file. If `local_model` is specified but `serving_container_spec.image_uri` in the `local_model` is None. If `local_model` is not specified and `serving_container_image_uri` is None. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Instantiated representation of the uploaded model resource. |

### upload_scikit_learn_model_file

```
upload_scikit_learn_model_file(
model_file_path: str,
sklearn_version: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
version_aliases: typing.Optional[typing.Sequence[str]] = None,
version_description: typing.Optional[str] = None,
instance_schema_uri: typing.Optional[str] = None,
parameters_schema_uri: typing.Optional[str] = None,
prediction_schema_uri: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
sync=True,
upload_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Model
```


Uploads a model and returns a Model representing the uploaded Model resource.

Example usage: my_model = Model.upload_scikit_learn_model_file( model_file_path="iris.sklearn_model.joblib" )

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If explanation_metadata is specified while explanation_parameters is not. Also if model directory does not contain a supported model file. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Instantiated representation of the uploaded model resource. |

### upload_tensorflow_saved_model

```
upload_tensorflow_saved_model(
saved_model_dir: str,
tensorflow_version: typing.Optional[str] = None,
use_gpu: bool = False,
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
version_aliases: typing.Optional[typing.Sequence[str]] = None,
version_description: typing.Optional[str] = None,
instance_schema_uri: typing.Optional[str] = None,
parameters_schema_uri: typing.Optional[str] = None,
prediction_schema_uri: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
sync=True,
upload_request_timeout: typing.Optional[str] = None,
) -> google.cloud.aiplatform.models.Model
```


Uploads a model and returns a Model representing the uploaded Model resource.

Example usage: my_model = Model.upload_scikit_learn_model_file( model_file_path="iris.tensorflow_model.SavedModel" )

Parameters |
|
|---|---|
Name |
Description |
`upload_request_timeout` |
`float`
Optional. The timeout for the upload request in seconds. |
`saved_model_dir` |
`str`
Required. Local directory of the Tensorflow SavedModel. |
`tensorflow_version` |
`str`
Optional. The version of the Tensorflow serving container. Supported versions: ["0.15", "2.1", "2.2", "2.3", "2.4", "2.5", "2.6", "2.7"]. If the version is not specified, the latest version is used. |
`use_gpu` |
`bool`
Whether to use GPU for model serving. |
`display_name` |
`str`
Optional. The display name of the Model. The name can be up to 128 characters long and can be consist of any UTF-8 characters. |
`description` |
`str`
The description of the model. |
`model_id` |
`str`
Optional. The ID to use for the uploaded Model, which will become the final component of the model resource name. This value may be up to 63 characters, and valid characters are |
`parent_model` |
`str`
Optional. The resource name or model ID of an existing model that the newly-uploaded model will be a version of. Only set this field when uploading a new version of an existing model. |
`is_default_version` |
`bool`
Optional. When set to True, the newly uploaded model version will automatically have alias "default" included. Subsequent uses of this model without a version specified will use this "default" version. When set to False, the "default" alias will not be moved. Actions targeting the newly-uploaded model version will need to specifically reference this version by ID or alias. New model uploads, i.e. version 1, will always be "default" aliased. |
`version_aliases` |
`Sequence[str]`
Optional. User provided version aliases so that a model version can be referenced via alias instead of auto-generated version ID. A default version alias will be created for the first version of the model. The format is |
`version_description` |
`str`
Optional. The description of the model version being uploaded. |
`instance_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in |
`parameters_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via |
`prediction_schema_uri` |
`str`
Optional. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via |
`explanation_metadata` |
`aiplatform.explain.ExplanationMetadata`
Optional. Metadata describing the Model's input and output for explanation. |
`explanation_parameters` |
`aiplatform.explain.ExplanationParameters`
Optional. Parameters to configure explaining for Model's predictions. For more details, see |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize your Models. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`Optional[str]`
Optional. The Cloud KMS resource identifier of the customer managed encryption key used to protect the model. Has the form: |
`staging_bucket` |
`str`
Optional. Bucket to stage local model artifacts. Overrides staging_bucket set in aiplatform.init. |
`sync` |
`bool`
Whether to execute this method synchronously. If False, this method will be executed in concurrent Future and any downstream object will be immediately returned and synced when the Future has completed. |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If explanation_metadata is specified while explanation_parameters is not. Also if model directory does not contain a supported model file. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Instantiated representation of the uploaded model resource. |

### upload_xgboost_model_file

```
upload_xgboost_model_file(
model_file_path: str,
xgboost_version: typing.Optional[str] = None,
display_name: typing.Optional[str] = None,
description: typing.Optional[str] = None,
model_id: typing.Optional[str] = None,
parent_model: typing.Optional[str] = None,
is_default_version: typing.Optional[bool] = True,
version_aliases: typing.Optional[typing.Sequence[str]] = None,
version_description: typing.Optional[str] = None,
instance_schema_uri: typing.Optional[str] = None,
parameters_schema_uri: typing.Optional[str] = None,
prediction_schema_uri: typing.Optional[str] = None,
explanation_metadata: typing.Optional[
google.cloud.aiplatform_v1.types.explanation_metadata.ExplanationMetadata
] = None,
explanation_parameters: typing.Optional[
google.cloud.aiplatform_v1.types.explanation.ExplanationParameters
] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
staging_bucket: typing.Optional[str] = None,
sync=True,
upload_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.models.Model
```


Uploads a model and returns a Model representing the uploaded Model resource.

Example usage: my_model = Model.upload_xgboost_model_file( model_file_path="iris.xgboost_model.bst" )

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If model directory does not contain a supported model file. |

Returns |
|
|---|---|
Type |
Description |
`model (aiplatform.Model)` |
Instantiated representation of the uploaded model resource. |

### wait

`wait()`


Helper method that blocks until all futures are complete.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookRuntimesAsyncPager -->

# Class ListNotebookRuntimesAsyncPager (1.134.0)

```
ListNotebookRuntimesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_notebook_runtimes`

requests.

This class thinly wraps an initial
[ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse) object, and
provides an `__aiter__`

method to iterate through its
`notebook_runtimes`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListNotebookRuntimes`

requests and continue to iterate
through the `notebook_runtimes`

field on the
corresponding responses.

All the usual [ListNotebookRuntimesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimesAsyncPager

```
ListNotebookRuntimesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookRuntimesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.EvaluatedAnnotation -->

# Class EvaluatedAnnotation (1.134.0)

`EvaluatedAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


True positive, false positive, or false negative.

EvaluatedAnnotation is only available under ModelEvaluationSlice
with slice of `annotationSpec`

dimension.

## Attributes |
|
|---|---|
Name |
Description |
`type_` |
Output only. Type of the EvaluatedAnnotation. |
`predictions` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Output only. The model predicted annotations. For true positive, there is one and only one prediction, which matches the only one ground truth annotation in ground_truths. For false positive, there is one and only one prediction, which doesn't match any ground truth annotation of the corresponding data_item_view_id. For false negative, there are zero or more predictions which are similar to the only ground truth annotation in ground_truths but not enough for a match. The schema of the prediction is stored in ModelEvaluation.annotation_schema_uri |
`ground_truths` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Output only. The ground truth Annotations, i.e. the Annotations that exist in the test data the Model is evaluated on. For true positive, there is one and only one ground truth annotation, which matches the only prediction in predictions. For false positive, there are zero or more ground truth annotations that are similar to the only prediction in predictions, but not enough for a match. For false negative, there is one and only one ground truth annotation, which doesn't match any predictions created by the model. The schema of the ground truth is stored in ModelEvaluation.annotation_schema_uri |
`data_item_payload` |
`google.protobuf.struct_pb2.Value`
Output only. The data item payload that the Model predicted this EvaluatedAnnotation on. |
`evaluated_data_item_view_id` |
`str`
Output only. ID of the EvaluatedDataItemView under the same ancestor ModelEvaluation. The EvaluatedDataItemView consists of all ground truths and predictions on data_item_payload. |
`explanations` |
`MutableSequence[`
Explanations of predictions. Each element of the explanations indicates the explanation for one explanation Method. The attributions list in the EvaluatedAnnotationExplanation.explanation object corresponds to the predictions list. For example, the second element in the attributions list explains the second element in the predictions list. |
`error_analysis_annotations` |
`MutableSequence[`
Annotations of model error analysis results. |

## Classes

### EvaluatedAnnotationType

`EvaluatedAnnotationType(value)`


Describes the type of the EvaluatedAnnotation. The type is determined

## Methods

### EvaluatedAnnotation

`EvaluatedAnnotation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


True positive, false positive, or false negative.

EvaluatedAnnotation is only available under ModelEvaluationSlice
with slice of `annotationSpec`

dimension.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorJobsPager -->

# Class ListFeatureMonitorJobsPager (1.134.0)

```
ListFeatureMonitorJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_feature_monitor_jobs`

requests.

This class thinly wraps an initial
[ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_monitor_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureMonitorJobs`

requests and continue to iterate
through the `feature_monitor_jobs`

field on the
corresponding responses.

All the usual [ListFeatureMonitorJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureMonitorJobsPager

```
ListFeatureMonitorJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorJobsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RestoreDatasetVersionOperationMetadata -->

# Class RestoreDatasetVersionOperationMetadata (1.134.0)

```
RestoreDatasetVersionOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.RestoreDatasetVersion.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### RestoreDatasetVersionOperationMetadata

```
RestoreDatasetVersionOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for DatasetService.RestoreDatasetVersion.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListEndpointsResponse -->

# Class ListEndpointsResponse (1.134.0)

`ListEndpointsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.ListEndpoints.

## Attributes |
|
|---|---|
Name |
Description |
`endpoints` |
`MutableSequence[`
List of Endpoints in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListEndpointsRequest.page_token to obtain that page. |

## Methods

### ListEndpointsResponse

`ListEndpointsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.ListEndpoints.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.NasJobSpec -->

# Class NasJobSpec (1.134.0)

`NasJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a NasJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`multi_trial_algorithm_spec` |
The spec of multi-trial algorithms. This field is a member of `oneof` _ `nas_algorithm_spec` .
|
`resume_nas_job_id` |
`str`
The ID of the existing NasJob in the same Project and Location which will be used to resume search. search_space_spec and nas_algorithm_spec are obtained from previous NasJob hence should not provide them again for this NasJob. |
`search_space_spec` |
`str`
It defines the search space for Neural Architecture Search (NAS). |

## Classes

### MultiTrialAlgorithmSpec

`MultiTrialAlgorithmSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The spec of multi-trial Neural Architecture Search (NAS).

## Methods

### NasJobSpec

`NasJobSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents the spec of a NasJob.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateTuningJobRequest -->

# Class CreateTuningJobRequest (1.134.0)

`CreateTuningJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.CreateTuningJob.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the TuningJob in. Format: `projects/{project}/locations/{location}`
|
`tuning_job` |
Required. The TuningJob to create. |

## Methods

### CreateTuningJobRequest

`CreateTuningJobRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for GenAiTuningService.CreateTuningJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetTensorboardRunRequest -->

# Class GetTensorboardRunRequest (1.134.0)

`GetTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.GetTensorboardRun.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the TensorboardRun resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`
|

## Methods

### GetTensorboardRunRequest

`GetTensorboardRunRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.GetTensorboardRun.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GcsDestination -->

# Class GcsDestination (1.134.0)

`GcsDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Google Cloud Storage location where the output is to be written to.

## Attribute |
|
|---|---|
Name |
Description |
`output_uri_prefix` |
`str`
Required. Google Cloud Storage URI to output directory. If the uri doesn't end with '/', a '/' will be automatically appended. The directory is created if it doesn't exist. |

## Methods

### GcsDestination

`GcsDestination(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The Google Cloud Storage location where the output is to be written to.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.HttpElementLocation -->

# Class HttpElementLocation (1.134.0)

`HttpElementLocation(value)`


Enum of location an HTTP element can be.

## Enums |
|
|---|---|
Name |
Description |
`HTTP_IN_UNSPECIFIED` |
No description available. |
`HTTP_IN_QUERY` |
Element is in the HTTP request query. |
`HTTP_IN_HEADER` |
Element is in the HTTP request header. |
`HTTP_IN_PATH` |
Element is in the HTTP request path. |
`HTTP_IN_BODY` |
Element is in the HTTP request body. |
`HTTP_IN_COOKIE` |
Element is in the HTTP request cookie. |

## Methods

### HttpElementLocation

`HttpElementLocation(value)`


Enum of location an HTTP element can be.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.notebook_service.pagers.ListNotebookExecutionJobsPager -->

# Class ListNotebookExecutionJobsPager (1.134.0)

```
ListNotebookExecutionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_notebook_execution_jobs`

requests.

This class thinly wraps an initial
[ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_execution_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookExecutionJobs`

requests and continue to iterate
through the `notebook_execution_jobs`

field on the
corresponding responses.

All the usual [ListNotebookExecutionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookExecutionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookExecutionJobsPager

```
ListNotebookExecutionJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.notebook_service.ListNotebookExecutionJobsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardRunsAsyncPager -->

# Class ListTensorboardRunsAsyncPager (1.134.0)

```
ListTensorboardRunsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboard_runs`

requests.

This class thinly wraps an initial
[ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsResponse) object, and
provides an `__aiter__`

method to iterate through its
`tensorboard_runs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTensorboardRuns`

requests and continue to iterate
through the `tensorboard_runs`

field on the
corresponding responses.

All the usual [ListTensorboardRunsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardRunsAsyncPager

```
ListTensorboardRunsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardRunsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.migration_service.pagers.SearchMigratableResourcesPager -->

# Class SearchMigratableResourcesPager (1.134.0)

```
SearchMigratableResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `search_migratable_resources`

requests.

This class thinly wraps an initial
[SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse) object, and
provides an `__iter__`

method to iterate through its
`migratable_resources`

field.

If there are more pages, the `__iter__`

method will make additional
`SearchMigratableResources`

requests and continue to iterate
through the `migratable_resources`

field on the
corresponding responses.

All the usual [SearchMigratableResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchMigratableResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### SearchMigratableResourcesPager

```
SearchMigratableResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.migration_service.SearchMigratableResourcesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.index_endpoint_service.pagers.ListIndexEndpointsAsyncPager -->

# Class ListIndexEndpointsAsyncPager (1.134.0)

```
ListIndexEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_index_endpoints`

requests.

This class thinly wraps an initial
[ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse) object, and
provides an `__aiter__`

method to iterate through its
`index_endpoints`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListIndexEndpoints`

requests and continue to iterate
through the `index_endpoints`

field on the
corresponding responses.

All the usual [ListIndexEndpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListIndexEndpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListIndexEndpointsAsyncPager

```
ListIndexEndpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsRequest,
response: google.cloud.aiplatform_v1beta1.types.index_endpoint_service.ListIndexEndpointsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureViewsAsyncPager -->

# Class ListFeatureViewsAsyncPager (1.134.0)

```
ListFeatureViewsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_feature_views`

requests.

This class thinly wraps an initial
[ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_views`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureViews`

requests and continue to iterate
through the `feature_views`

field on the
corresponding responses.

All the usual [ListFeatureViewsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureViewsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureViewsAsyncPager

```
ListFeatureViewsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse
],
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureViewsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureViewDirectWriteResponse -->

# Class FeatureViewDirectWriteResponse (1.134.0)

```
FeatureViewDirectWriteResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreService.FeatureViewDirectWrite.

## Attributes |
|
|---|---|
Name |
Description |
`status` |
`google.rpc.status_pb2.Status`
Response status for the keys listed in FeatureViewDirectWriteResponse.write_responses. The error only applies to the listed data keys - the stream will remain open for further [FeatureOnlineStoreService.FeatureViewDirectWriteRequest][] requests. Partial failures (e.g. if the first 10 keys of a request fail, but the rest succeed) from a single request may result in multiple responses - there will be one response for the successful request keys and one response for the failing request keys. |
`write_responses` |
`MutableSequence[`
Details about write for each key. If status is not OK, WriteResponse.data_key will have the key with error, but WriteResponse.online_store_write_time will not be present. |

## Classes

### WriteResponse

`WriteResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details about the write for each key.

## Methods

### FeatureViewDirectWriteResponse

```
FeatureViewDirectWriteResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreService.FeatureViewDirectWrite.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteIndexEndpointRequest -->

# Class DeleteIndexEndpointRequest (1.134.0)

`DeleteIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.DeleteIndexEndpoint.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the IndexEndpoint resource to be deleted. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`
|

## Methods

### DeleteIndexEndpointRequest

`DeleteIndexEndpointRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for IndexEndpointService.DeleteIndexEndpoint.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListRagFilesResponse -->

# Class ListRagFilesResponse (1.134.0)

`ListRagFilesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ListRagFiles.

## Attributes |
|
|---|---|
Name |
Description |
`rag_files` |
`MutableSequence[`
List of RagFiles in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListRagFilesRequest.page_token to obtain that page. |

## Methods

### ListRagFilesResponse

`ListRagFilesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ListRagFiles.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PipelineTaskExecutorDetail.ContainerDetail -->

# Class ContainerDetail (1.134.0)

`ContainerDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The detail of a container execution. It contains the job names of the lifecycle of a container execution.

## Attributes |
|
|---|---|
Name |
Description |
`main_job` |
`str`
Output only. The name of the CustomJob for the main container execution. |
`pre_caching_check_job` |
`str`
Output only. The name of the CustomJob for the pre-caching-check container execution. This job will be available if the PipelineJob.pipeline_spec specifies the `pre_caching_check` hook in the lifecycle
events.
|
`failed_main_jobs` |
`MutableSequence[str]`
Output only. The names of the previously failed CustomJob for the main container executions. The list includes the all attempts in chronological order. |
`failed_pre_caching_check_jobs` |
`MutableSequence[str]`
Output only. The names of the previously failed CustomJob for the pre-caching-check container executions. This job will be available if the PipelineJob.pipeline_spec specifies the `pre_caching_check` hook in the lifecycle
events. The list includes the all attempts in chronological
order.
|

## Methods

### ContainerDetail

`ContainerDetail(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The detail of a container execution. It contains the job names of the lifecycle of a container execution.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ExportModelRequest.OutputConfig -->

# Class OutputConfig (1.134.0)

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output configuration for the Model export.

## Attributes |
|
|---|---|
Name |
Description |
`export_format_id` |
`str`
The ID of the format in which the Model must be exported. Each Model lists the [export formats it supports][google.cloud.aiplatform.v1.Model.supported_export_formats]. If no value is provided here, then the first from the list of the Model's supported formats is used by default. |
`artifact_destination` |
The Cloud Storage location where the Model artifact is to be written to. Under the directory given as the destination a new one with name " `model-export-` ",
where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601
format, will be created. Inside, the Model and any of its
supporting files will be written. This field should only be
set when the `exportableContent` field of the
[Model.supported_export_formats] object contains
`ARTIFACT` .
|
`image_destination` |
The Google Container Registry or Artifact Registry uri where the Model container image will be copied to. This field should only be set when the `exportableContent` field of
the [Model.supported_export_formats] object contains
`IMAGE` .
|

## Methods

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output configuration for the Model export.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_garden_service.pagers.ListPublisherModelsAsyncPager -->

# Class ListPublisherModelsAsyncPager (1.134.0)

```
ListPublisherModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_publisher_models`

requests.

This class thinly wraps an initial
[ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse) object, and
provides an `__aiter__`

method to iterate through its
`publisher_models`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListPublisherModels`

requests and continue to iterate
through the `publisher_models`

field on the
corresponding responses.

All the usual [ListPublisherModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPublisherModelsAsyncPager

```
ListPublisherModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_garden_service.ListPublisherModelsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.reasoning_engine_service.pagers.ListReasoningEnginesAsyncPager -->

# Class ListReasoningEnginesAsyncPager (1.134.0)

```
ListReasoningEnginesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse
],
],
request: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_reasoning_engines`

requests.

This class thinly wraps an initial
[ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse) object, and
provides an `__aiter__`

method to iterate through its
`reasoning_engines`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListReasoningEngines`

requests and continue to iterate
through the `reasoning_engines`

field on the
corresponding responses.

All the usual [ListReasoningEnginesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListReasoningEnginesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListReasoningEnginesAsyncPager

```
ListReasoningEnginesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse
],
],
request: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesRequest,
response: google.cloud.aiplatform_v1.types.reasoning_engine_service.ListReasoningEnginesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FunctionDeclaration -->

# Class FunctionDeclaration (1.134.0)

`FunctionDeclaration(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Structured representation of a function declaration as defined by
the ```
OpenAPI 3.0
specification <https://spec.openapis.org/oas/v3.0.3>
```

__. Included in
this declaration are the function name, description, parameters and
response type. This FunctionDeclaration is a representation of a
block of code that can be used as a `Tool`

by the model and
executed by the client.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots and dashes, with a maximum length of 64. |
`description` |
`str`
Optional. Description and purpose of the function. Model uses it to decide how and whether to call the function. |
`parameters` |
Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema Value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1 |
`parameters_json_schema` |
`google.protobuf.struct_pb2.Value`
Optional. Describes the parameters to the function in JSON Schema format. The schema must describe an object where the properties are the parameters to the function. For example: :: { "type": "object", "properties": { "name": { "type": "string" }, "age": { "type": "integer" } }, "additionalProperties": false, "required": ["name", "age"], "propertyOrdering": ["name", "age"] } This field is mutually exclusive with `parameters` .
|
`response` |
Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function. |
`response_json_schema` |
`google.protobuf.struct_pb2.Value`
Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function. This field is mutually exclusive with `response` .
|

## Methods

### FunctionDeclaration

`FunctionDeclaration(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Structured representation of a function declaration as defined by
the ```
OpenAPI 3.0
specification <https://spec.openapis.org/oas/v3.0.3>
```

__. Included in
this declaration are the function name, description, parameters and
response type. This FunctionDeclaration is a representation of a
block of code that can be used as a `Tool`

by the model and
executed by the client.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.TimestampSplit -->

# Class TimestampSplit (1.134.0)

`TimestampSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on a provided timestamps. The youngest data pieces are assigned to training set, next to validation set, and the oldest to the test set.

Supported only for tabular Datasets.

## Attributes |
|
|---|---|
Name |
Description |
`training_fraction` |
`float`
The fraction of the input data that is to be used to train the Model. |
`validation_fraction` |
`float`
The fraction of the input data that is to be used to validate the Model. |
`test_fraction` |
`float`
The fraction of the input data that is to be used to evaluate the Model. |
`key` |
`str`
Required. The key is a name of one of the Dataset's data columns. The values of the key (the values in the column) must be in RFC 3339 `date-time` format, where
`time-offset` = `"Z"` (e.g. 1985-04-12T23:20:50.52Z). If
for a piece of data the key is not present or has an invalid
value, that piece is ignored by the pipeline.
|

## Methods

### TimestampSplit

`TimestampSplit(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Assigns input data to training, validation, and test sets based on a provided timestamps. The youngest data pieces are assigned to training set, next to validation set, and the oldest to the test set.

Supported only for tabular Datasets.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExampleParameters.ContentSearchKey -->

# Class ContentSearchKey (1.134.0)

`ContentSearchKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The chat history to use to generate the search key for retrieval.

## Attributes |
|
|---|---|
Name |
Description |
`contents` |
`MutableSequence[`
Required. The conversation for generating a search key. |
`search_key_generation_method` |
Required. The method of generating a search key. |

## Methods

### ContentSearchKey

`ContentSearchKey(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The chat history to use to generate the search key for retrieval.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeployIndexOperationMetadata -->

# Class DeployIndexOperationMetadata (1.134.0)

```
DeployIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.DeployIndex.

## Attributes |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |
`deployed_index_id` |
`str`
The unique index id specified by user |

## Methods

### DeployIndexOperationMetadata

```
DeployIndexOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for IndexEndpointService.DeployIndex.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSchedulesResponse -->

# Class ListSchedulesResponse (1.134.0)

`ListSchedulesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ScheduleService.ListSchedules

## Attributes |
|
|---|---|
Name |
Description |
`schedules` |
`MutableSequence[`
List of Schedules in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListSchedulesRequest.page_token to obtain that page. |

## Methods

### ListSchedulesResponse

`ListSchedulesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for ScheduleService.ListSchedules

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetMetadataSchemaRequest -->

# Class GetMetadataSchemaRequest (1.134.0)

`GetMetadataSchemaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetMetadataSchema.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the MetadataSchema to retrieve. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/metadataSchemas/{metadataschema}`
|

## Methods

### GetMetadataSchemaRequest

`GetMetadataSchemaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetMetadataSchema.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FeatureViewDirectWriteResponse -->

# Class FeatureViewDirectWriteResponse (1.134.0)

```
FeatureViewDirectWriteResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreService.FeatureViewDirectWrite.

## Attributes |
|
|---|---|
Name |
Description |
`status` |
`google.rpc.status_pb2.Status`
Response status for the keys listed in FeatureViewDirectWriteResponse.write_responses. The error only applies to the listed data keys - the stream will remain open for further [FeatureOnlineStoreService.FeatureViewDirectWriteRequest][] requests. Partial failures (e.g. if the first 10 keys of a request fail, but the rest succeed) from a single request may result in multiple responses - there will be one response for the successful request keys and one response for the failing request keys. |
`write_responses` |
`MutableSequence[`
Details about write for each key. If status is not OK, WriteResponse.data_key will have the key with error, but WriteResponse.online_store_write_time will not be present. |

## Classes

### WriteResponse

`WriteResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Details about the write for each key.

## Methods

### FeatureViewDirectWriteResponse

```
FeatureViewDirectWriteResponse(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Response message for FeatureOnlineStoreService.FeatureViewDirectWrite.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.notebook_service.pagers.ListNotebookRuntimeTemplatesPager -->

# Class ListNotebookRuntimeTemplatesPager (1.134.0)

```
ListNotebookRuntimeTemplatesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_notebook_runtime_templates`

requests.

This class thinly wraps an initial
[ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesResponse) object, and
provides an `__iter__`

method to iterate through its
`notebook_runtime_templates`

field.

If there are more pages, the `__iter__`

method will make additional
`ListNotebookRuntimeTemplates`

requests and continue to iterate
through the `notebook_runtime_templates`

field on the
corresponding responses.

All the usual [ListNotebookRuntimeTemplatesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimeTemplatesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListNotebookRuntimeTemplatesPager

```
ListNotebookRuntimeTemplatesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
],
request: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesRequest,
response: google.cloud.aiplatform_v1.types.notebook_service.ListNotebookRuntimeTemplatesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FunctionDeclaration -->

# Class FunctionDeclaration (1.134.0)

`FunctionDeclaration(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Structured representation of a function declaration as defined by
the ```
OpenAPI 3.0
specification <https://spec.openapis.org/oas/v3.0.3>
```

__. Included in
this declaration are the function name, description, parameters and
response type. This FunctionDeclaration is a representation of a
block of code that can be used as a `Tool`

by the model and
executed by the client.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots and dashes, with a maximum length of 64. |
`description` |
`str`
Optional. Description and purpose of the function. Model uses it to decide how and whether to call the function. |
`parameters` |
Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema Value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1 |
`parameters_json_schema` |
`google.protobuf.struct_pb2.Value`
Optional. Describes the parameters to the function in JSON Schema format. The schema must describe an object where the properties are the parameters to the function. For example: :: { "type": "object", "properties": { "name": { "type": "string" }, "age": { "type": "integer" } }, "additionalProperties": false, "required": ["name", "age"], "propertyOrdering": ["name", "age"] } This field is mutually exclusive with `parameters` .
|
`response` |
Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function. |
`response_json_schema` |
`google.protobuf.struct_pb2.Value`
Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function. This field is mutually exclusive with `response` .
|

## Methods

### FunctionDeclaration

`FunctionDeclaration(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Structured representation of a function declaration as defined by
the ```
OpenAPI 3.0
specification <https://spec.openapis.org/oas/v3.0.3>
```

__. Included in
this declaration are the function name, description, parameters and
response type. This FunctionDeclaration is a representation of a
block of code that can be used as a `Tool`

by the model and
executed by the client.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.Model.OriginalModelInfo -->

# Class OriginalModelInfo (1.134.0)

`OriginalModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the original Model if this Model is a copy.

## Attribute |
|
|---|---|
Name |
Description |
`model` |
`str`
Output only. The resource name of the Model this Model is a copy of, including the revision. Format: `projects/{project}/locations/{location}/models/{model_id}@{version_id}`
|

## Methods

### OriginalModelInfo

`OriginalModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the original Model if this Model is a copy.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateRagEngineConfigOperationMetadata -->

# Class UpdateRagEngineConfigOperationMetadata (1.134.0)

```
UpdateRagEngineConfigOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for VertexRagDataService.UpdateRagEngineConfig.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### UpdateRagEngineConfigOperationMetadata

```
UpdateRagEngineConfigOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for VertexRagDataService.UpdateRagEngineConfig.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchDataItemsResponse -->

# Class SearchDataItemsResponse (1.134.0)

`SearchDataItemsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.SearchDataItems.

## Attributes |
|
|---|---|
Name |
Description |
`data_item_views` |
`MutableSequence[`
The DataItemViews read. |
`next_page_token` |
`str`
A token to retrieve next page of results. Pass to SearchDataItemsRequest.page_token to obtain that page. |

## Methods

### SearchDataItemsResponse

`SearchDataItemsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.SearchDataItems.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportIndexRequest.ConnectorConfig.DatapointFieldMapping.Restrict -->

# Class Restrict (1.134.0)

`Restrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on string values.

## Attributes |
|
|---|---|
Name |
Description |
`namespace` |
`str`
Required. The namespace of the restrict in the index. |
`allow_column` |
`MutableSequence[str]`
Optional. The columns containing the allow values. |
`deny_column` |
`MutableSequence[str]`
Optional. The columns containing the deny values. |

## Methods

### Restrict

`Restrict(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Restrictions on string values.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateRagCorpusRequest -->

# Class CreateRagCorpusRequest (1.134.0)

`CreateRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.CreateRagCorpus.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to create the RagCorpus in. Format: `projects/{project}/locations/{location}`
|
`rag_corpus` |
Required. The RagCorpus to create. |

## Methods

### CreateRagCorpusRequest

`CreateRagCorpusRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for VertexRagDataService.CreateRagCorpus.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDataLabelingJobRequest -->

# Class DeleteDataLabelingJobRequest (1.134.0)

```
DeleteDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteDataLabelingJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DataLabelingJob to be deleted. Format: `projects/{project}/locations/{location}/dataLabelingJobs/{data_labeling_job}`
|

## Methods

### DeleteDataLabelingJobRequest

```
DeleteDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteDataLabelingJob.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UploadModelResponse -->

# Class UploadModelResponse (1.134.0)

`UploadModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message of ModelService.UploadModel operation.

## Attributes |
|
|---|---|
Name |
Description |
`model` |
`str`
The name of the uploaded Model resource. Format: `projects/{project}/locations/{location}/models/{model}`
|
`model_version_id` |
`str`
Output only. The version ID of the model that is uploaded. |

## Methods

### UploadModelResponse

`UploadModelResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message of ModelService.UploadModel operation.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListCustomJobsResponse -->

# Class ListCustomJobsResponse (1.134.0)

`ListCustomJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListCustomJobs

## Attributes |
|
|---|---|
Name |
Description |
`custom_jobs` |
`MutableSequence[`
List of CustomJobs in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListCustomJobsRequest.page_token to obtain that page. |

## Methods

### ListCustomJobsResponse

`ListCustomJobsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for JobService.ListCustomJobs

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrialsResponse -->

# Class ListTrialsResponse (1.134.0)

`ListTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListTrials.

## Attributes |
|
|---|---|
Name |
Description |
`trials` |
`MutableSequence[`
The Trials associated with the Study. |
`next_page_token` |
`str`
Pass this token as the `page_token` field of the request
for a subsequent call. If this field is omitted, there are
no subsequent pages.
|

## Methods

### ListTrialsResponse

`ListTrialsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListTrials.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SpeculativeDecodingSpec.DraftModelSpeculation -->

# Class DraftModelSpeculation (1.134.0)

`DraftModelSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Draft model speculation works by using the smaller model to generate candidate tokens for speculative decoding.

## Attribute |
|
|---|---|
Name |
Description |
`draft_model` |
`str`
Required. The resource name of the draft model. |

## Methods

### DraftModelSpeculation

`DraftModelSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Draft model speculation works by using the smaller model to generate candidate tokens for speculative decoding.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1.schema.trainingjob.definition_v1.types.AutoMlTablesInputs.Transformation.TextArrayTransformation -->

# Class TextArrayTransformation (1.134.0)

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

## Methods

### TextArrayTransformation

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

### TextArrayTransformation

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.pipeline_service.pagers.ListTrainingPipelinesAsyncPager -->

# Class ListTrainingPipelinesAsyncPager (1.134.0)

```
ListTrainingPipelinesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_training_pipelines`

requests.

This class thinly wraps an initial
[ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse) object, and
provides an `__aiter__`

method to iterate through its
`training_pipelines`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTrainingPipelines`

requests and continue to iterate
through the `training_pipelines`

field on the
corresponding responses.

All the usual [ListTrainingPipelinesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTrainingPipelinesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTrainingPipelinesAsyncPager

```
ListTrainingPipelinesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesRequest,
response: google.cloud.aiplatform_v1beta1.types.pipeline_service.ListTrainingPipelinesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateFeatureViewRequest -->

# Class UpdateFeatureViewRequest (1.134.0)

`UpdateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.UpdateFeatureView.

## Attributes |
|
|---|---|
Name |
Description |
`feature_view` |
Required. The FeatureView's `name` field is used to
identify the FeatureView to be updated. Format:
`projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|
`update_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Field mask is used to specify the fields to be overwritten in the FeatureView resource by the update. The fields specified in the update_mask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then only the non-empty fields present in the request will be overwritten. Set the update_mask to `*` to override all
fields.
Updatable fields:
- `labels`
- `service_agent_type`
- `big_query_source`
- `big_query_source.uri`
- `big_query_source.entity_id_columns`
- `feature_registry_source`
- `feature_registry_source.feature_groups`
- `sync_config`
- `sync_config.cron`
|

## Methods

### UpdateFeatureViewRequest

`UpdateFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.UpdateFeatureView.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PartnerModelTuningSpec -->

# Class PartnerModelTuningSpec (1.134.0)

`PartnerModelTuningSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning spec for Partner models.

## Attributes |
|
|---|---|
Name |
Description |
`training_dataset_uri` |
`str`
Required. Cloud Storage path to file containing training dataset for tuning. The dataset must be formatted as a JSONL file. |
`validation_dataset_uri` |
`str`
Optional. Cloud Storage path to file containing validation dataset for tuning. The dataset must be formatted as a JSONL file. |
`hyper_parameters` |
`MutableMapping[str, google.protobuf.struct_pb2.Value]`
Hyperparameters for tuning. The accepted hyper_parameters and their valid range of values will differ depending on the base model. |

## Classes

### HyperParametersEntry

`HyperParametersEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

## Methods

### PartnerModelTuningSpec

`PartnerModelTuningSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Tuning spec for Partner models.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.ModelDeploymentMonitoringJob -->

# Class ModelDeploymentMonitoringJob (1.134.0)

```
ModelDeploymentMonitoringJob(
model_deployment_monitoring_job_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Vertex AI Model Deployment Monitoring Job.

This class should be used in conjunction with the Endpoint class in order to configure model monitoring for deployed models.

## Properties

### create_time

Time this resource was created.

### display_name

Display name of this resource.

### encryption_spec

Customer-managed encryption key options for this Vertex AI resource.

If this is set, then all resources created by this Vertex AI resource will be encrypted with the provided encryption key.

### end_time

Time when the Job resource entered the `JOB_STATE_SUCCEEDED`

,
`JOB_STATE_FAILED`

, or `JOB_STATE_CANCELLED`

state.

### error

Detailed error info for this Job resource. Only populated when the
Job's state is `JOB_STATE_FAILED`

or `JOB_STATE_CANCELLED`

.

### gca_resource

The underlying resource proto representation.

### labels

User-defined labels containing metadata about this resource.

Read more about labels at [https://goo.gl/xmQnxf](https://goo.gl/xmQnxf)

### name

Name of this resource.

### resource_name

Full qualified resource name.

### start_time

Time when the Job resource entered the `JOB_STATE_RUNNING`

for the
first time.

### state

Fetch Job again and return the current JobState.

Returns |
|
|---|---|
Type |
Description |
`state (job_state.JobState)` |
Enum that describes the state of a Vertex AI job. |

### update_time

Time this resource was last updated.

## Methods

### ModelDeploymentMonitoringJob

```
ModelDeploymentMonitoringJob(
model_deployment_monitoring_job_name: str,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
)
```


Initializer for ModelDeploymentMonitoringJob.

Parameter |
|
|---|---|
Name |
Description |
`model_deployment_monitoring_job_name` |
`str`
Required. A fully-qualified ModelDeploymentMonitoringJob resource name or ID. Example: "projects/.../locations/.../modelDeploymentMonitoringJobs/456" or "456" when project and location are initialized or passed. |

### cancel

`cancel()`


Cancels this Job.

Success of cancellation is not guaranteed. Use `Job.state`

property to verify if cancellation was successful.

### create

```
create(
endpoint: typing.Union[str, google.cloud.aiplatform.models.Endpoint],
objective_configs: typing.Optional[
typing.Union[
google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig,
typing.Dict[
str, google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig
],
]
] = None,
logging_sampling_strategy: typing.Optional[
google.cloud.aiplatform.model_monitoring.sampling.RandomSampleConfig
] = None,
schedule_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.schedule.ScheduleConfig
] = None,
display_name: typing.Optional[str] = None,
deployed_model_ids: typing.Optional[typing.List[str]] = None,
alert_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.alert.EmailAlertConfig
] = None,
predict_instance_schema_uri: typing.Optional[str] = None,
sample_predict_instance: typing.Optional[str] = None,
analysis_instance_schema_uri: typing.Optional[str] = None,
bigquery_tables_log_ttl: typing.Optional[int] = None,
stats_anomalies_base_directory: typing.Optional[str] = None,
enable_monitoring_pipeline_logs: typing.Optional[bool] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
encryption_spec_key_name: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
create_request_timeout: typing.Optional[float] = None,
) -> google.cloud.aiplatform.jobs.ModelDeploymentMonitoringJob
```


Creates and launches a model monitoring job.

Parameters |
|
|---|---|
Name |
Description |
`endpoint` |
`Union[str, "aiplatform.Endpoint"]`
Required. Endpoint resource name or an instance of |
`logging_sampling_strategy` |
`model_monitoring.sampling.RandomSampleConfig`
Optional. Sample Strategy for logging. |
`schedule_config` |
`model_monitoring.schedule.ScheduleConfig`
Optional. Configures model monitoring job scheduling interval in hours. This defines how often the monitoring jobs are triggered. |
`display_name` |
`str`
Optional. The user-defined name of the ModelDeploymentMonitoringJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. Display name of a ModelDeploymentMonitoringJob. |
`deployed_model_ids` |
`List[str]`
Optional. Use this argument to specify which deployed models to apply the objective config to. If left unspecified, the same config will be applied to all deployed models. |
`alert_config` |
`model_monitoring.alert.EmailAlertConfig`
Optional. Configures how alerts are sent to the user. Right now only email alert is supported. |
`predict_instance_schema_uri` |
`str`
Optional. YAML schema file uri describing the format of a single instance, which are given to format the Endpoint's prediction (and explanation). If not set, the schema will be generated from collected predict requests. |
`sample_predict_instance` |
`str`
Optional. Sample Predict instance, same format as PredictionRequest.instances, this can be set as a replacement of predict_instance_schema_uri If not set, the schema will be generated from collected predict requests. |
`analysis_instance_schema_uri` |
`str`
Optional. YAML schema file uri describing the format of a single instance that you want Tensorflow Data Validation (TFDV) to analyze. If this field is empty, all the feature data types are inferred from predict_instance_schema_uri, meaning that TFDV will use the data in the exact format as prediction request/response. If there are any data type differences between predict instance and TFDV instance, this field can be used to override the schema. For models trained with Vertex AI, this field must be set as all the fields in predict instance formatted as string. |
`bigquery_tables_log_ttl` |
`int`
Optional. The TTL(time to live) of BigQuery tables in user projects which stores logs. A day is the basic unit of the TTL and we take the ceil of TTL/86400(a day). e.g. { second: 3600} indicates ttl = 1 day. |
`stats_anomalies_base_directory` |
`str`
Optional. Stats anomalies base folder path. |
`enable_monitoring_pipeline_logs` |
`bool`
Optional. If true, the scheduled monitoring pipeline logs are sent to Google Cloud Logging, including pipeline status and anomalies detected. Please note the logs incur cost, which are subject to |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize the ModelDeploymentMonitoringJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`encryption_spec_key_name` |
`str`
Optional. Customer-managed encryption key spec for a ModelDeploymentMonitoringJob. If set, this ModelDeploymentMonitoringJob and all sub-resources of this ModelDeploymentMonitoringJob will be secured by this key. |
`create_request_timeout` |
`int`
Optional. Timeout in seconds for the model monitoring job creation request. |

### delete

`delete() -> None`


Deletes an MDM job.

### done

`done() -> bool`


Method indicating whether a job has completed.

### list

```
list(
filter: typing.Optional[str] = None,
order_by: typing.Optional[str] = None,
project: typing.Optional[str] = None,
location: typing.Optional[str] = None,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
) -> typing.List[google.cloud.aiplatform.base.VertexAiResourceNoun]
```


List all instances of this Job Resource.

Example Usage:

aiplatform.BatchPredictionJobs.list( filter='state="JOB_STATE_SUCCEEDED" AND display_name="my_job"', )

Parameters |
|
|---|---|
Name |
Description |
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: |
`project` |
`str`
Optional. Project to retrieve list from. If not set, project set in aiplatform.init will be used. |
`location` |
`str`
Optional. Location to retrieve list from. If not set, location set in aiplatform.init will be used. |
`credentials` |
`auth_credentials.Credentials`
Optional. Custom credentials to use to retrieve list. Overrides credentials set in aiplatform.init. |

### pause

`pause() -> google.cloud.aiplatform.jobs.ModelDeploymentMonitoringJob`


Pause a running MDM job.

### resume

`resume() -> google.cloud.aiplatform.jobs.ModelDeploymentMonitoringJob`


Resumes a paused MDM job.

### to_dict

`to_dict() -> typing.Dict[str, typing.Any]`


Returns the resource proto as a dictionary.

### update

```
update(
*,
display_name: typing.Optional[str] = None,
schedule_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.schedule.ScheduleConfig
] = None,
alert_config: typing.Optional[
google.cloud.aiplatform.model_monitoring.alert.EmailAlertConfig
] = None,
logging_sampling_strategy: typing.Optional[
google.cloud.aiplatform.model_monitoring.sampling.RandomSampleConfig
] = None,
labels: typing.Optional[typing.Dict[str, str]] = None,
bigquery_tables_log_ttl: typing.Optional[int] = None,
enable_monitoring_pipeline_logs: typing.Optional[bool] = None,
objective_configs: typing.Optional[
typing.Union[
google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig,
typing.Dict[
str, google.cloud.aiplatform.model_monitoring.objective.ObjectiveConfig
],
]
] = None,
deployed_model_ids: typing.Optional[typing.List[str]] = None,
update_request_timeout: typing.Optional[float] = None
) -> google.cloud.aiplatform.jobs.ModelDeploymentMonitoringJob
```


Updates an existing ModelDeploymentMonitoringJob.

Parameters |
|
|---|---|
Name |
Description |
`display_name` |
`str`
Optional. The user-defined name of the ModelDeploymentMonitoringJob. The name can be up to 128 characters long and can be consist of any UTF-8 characters. Display name of a ModelDeploymentMonitoringJob. |
`schedule_config` |
`model_monitoring.schedule.ScheduleConfig`
Required. Configures model monitoring job scheduling interval in hours. This defines how often the monitoring jobs are triggered. |
`alert_config` |
`model_monitoring.alert.EmailAlertConfig`
Optional. Configures how alerts are sent to the user. Right now only email alert is supported. |
`logging_sampling_strategy` |
`model_monitoring.sampling.RandomSampleConfig`
Required. Sample Strategy for logging. |
`labels` |
`Dict[str, str]`
Optional. The labels with user-defined metadata to organize the ModelDeploymentMonitoringJob. Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See |
`bigquery_tables_log_ttl` |
`int`
Optional. The number of days for which the logs are stored. The TTL(time to live) of BigQuery tables in user projects which stores logs. A day is the basic unit of the TTL and we take the ceil of TTL/86400(a day). e.g. { second: 3600} indicates ttl = 1 day. |
`enable_monitoring_pipeline_logs` |
`bool`
Optional. If true, the scheduled monitoring pipeline logs are sent to Google Cloud Logging, including pipeline status and anomalies detected. Please note the logs incur cost, which are subject to |
`deployed_model_ids` |
`List[str]`
Optional. Use this argument to specify which deployed models to apply the updated objective config to. If left unspecified, the same config will be applied to all deployed models. |
`upate_request_timeout` |
`float`
Optional. Timeout in seconds for the model monitoring job update request. |

### wait

`wait()`


Helper method that blocks until all futures are complete.

### wait_for_completion

`wait_for_completion() -> None`


Waits for job to complete.

Exceptions |
|
|---|---|
Type |
Description |
`RuntimeError` |
If job failed or cancelled. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetFeatureViewRequest -->

# Class GetFeatureViewRequest (1.134.0)

`GetFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureView.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureView resource. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|

## Methods

### GetFeatureViewRequest

`GetFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureView.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListEndpointsResponse -->

# Class ListEndpointsResponse (1.134.0)

`ListEndpointsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.ListEndpoints.

## Attributes |
|
|---|---|
Name |
Description |
`endpoints` |
`MutableSequence[`
List of Endpoints in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListEndpointsRequest.page_token to obtain that page. |

## Methods

### ListEndpointsResponse

`ListEndpointsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for EndpointService.ListEndpoints.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListRagFilesResponse -->

# Class ListRagFilesResponse (1.134.0)

`ListRagFilesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ListRagFiles.

## Attributes |
|
|---|---|
Name |
Description |
`rag_files` |
`MutableSequence[`
List of RagFiles in the requested page. |
`next_page_token` |
`str`
A token to retrieve the next page of results. Pass to ListRagFilesRequest.page_token to obtain that page. |

## Methods

### ListRagFilesResponse

`ListRagFilesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VertexRagDataService.ListRagFiles.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ResourcesConsumed -->

# Class ResourcesConsumed (1.134.0)

`ResourcesConsumed(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Statistics information about resource consumption.

## Attribute |
|
|---|---|
Name |
Description |
`replica_hours` |
`float`
Output only. The number of replica hours used. Note that many replicas may run in parallel, and additionally any given work may be queued for some time. Therefore this value is not strictly related to wall time. |

## Methods

### ResourcesConsumed

`ResourcesConsumed(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Statistics information about resource consumption.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.model_monitoring_service.pagers.ListModelMonitoringJobsPager -->

# Class ListModelMonitoringJobsPager (1.134.0)

```
ListModelMonitoringJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_model_monitoring_jobs`

requests.

This class thinly wraps an initial
[ListModelMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`model_monitoring_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListModelMonitoringJobs`

requests and continue to iterate
through the `model_monitoring_jobs`

field on the
corresponding responses.

All the usual [ListModelMonitoringJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListModelMonitoringJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelMonitoringJobsPager

```
ListModelMonitoringJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.model_monitoring_service.ListModelMonitoringJobsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListNotebookRuntimesRequest -->

# Class ListNotebookRuntimesRequest (1.134.0)

`ListNotebookRuntimesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.ListNotebookRuntimes.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookRuntimes. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `notebookRuntime` supports = and !=. `notebookRuntime`
represents the NotebookRuntime ID, i.e. the last segment
of the NotebookRuntime's [resource name]
[google.cloud.aiplatform.v1.NotebookRuntime.name].
- `displayName` supports = and != and regex.
- `notebookRuntimeTemplate` supports = and !=.
`notebookRuntimeTemplate` represents the
NotebookRuntimeTemplate ID, i.e. the last segment of the
NotebookRuntimeTemplate's [resource name]
[google.cloud.aiplatform.v1.NotebookRuntimeTemplate.name].
- `healthState` supports = and !=. healthState enum:
[HEALTHY, UNHEALTHY, HEALTH_STATE_UNSPECIFIED].
- `runtimeState` supports = and !=. runtimeState enum:
[RUNTIME_STATE_UNSPECIFIED, RUNNING, BEING_STARTED,
BEING_STOPPED, STOPPED, BEING_UPGRADED, ERROR, INVALID].
- `runtimeUser` supports = and !=.
- API version is UI only: `uiState` supports = and !=.
uiState enum: [UI_RESOURCE_STATE_UNSPECIFIED,
UI_RESOURCE_STATE_BEING_CREATED, UI_RESOURCE_STATE_ACTIVE,
UI_RESOURCE_STATE_BEING_DELETED,
UI_RESOURCE_STATE_CREATION_FAILED].
- `notebookRuntimeType` supports = and !=.
notebookRuntimeType enum: [USER_DEFINED, ONE_CLICK].
- `machineType` supports = and !=.
- `acceleratorType` supports = and !=.
Some examples:
- `notebookRuntime="notebookRuntime123"`
- `displayName="myDisplayName"` and
`displayName=` "myDisplayNameRegex"`
- `notebookRuntimeTemplate="notebookRuntimeTemplate321"`
- `healthState=HEALTHY`
- `runtimeState=RUNNING`
- `runtimeUser="test@google.com"`
- `uiState=UI_RESOURCE_STATE_BEING_DELETED`
- `notebookRuntimeType=USER_DEFINED`
- `machineType=e2-standard-4`
- `acceleratorType=NVIDIA_TESLA_T4`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListNotebookRuntimesResponse.next_page_token of the previous NotebookService.ListNotebookRuntimes call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
Example: `display_name, create_time desc` .
|

## Methods

### ListNotebookRuntimesRequest

`ListNotebookRuntimesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.ListNotebookRuntimes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardTimeSeriesPager -->

# Class ListTensorboardTimeSeriesPager (1.134.0)

```
ListTensorboardTimeSeriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboard_time_series`

requests.

This class thinly wraps an initial
[ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboard_time_series`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboardTimeSeries`

requests and continue to iterate
through the `tensorboard_time_series`

field on the
corresponding responses.

All the usual [ListTensorboardTimeSeriesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardTimeSeriesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardTimeSeriesPager

```
ListTensorboardTimeSeriesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardTimeSeriesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient -->

# Class ExampleStoreServiceAsyncClient (1.134.0)

```
ExampleStoreServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.example_store_service.transports.base.ExampleStoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.example_store_service.transports.base.ExampleStoreServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


A service for managing and retrieving few-shot examples.

## Properties

### api_endpoint

Return the API endpoint used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The API endpoint used by the client instance. |

### transport

Returns the transport used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`ExampleStoreServiceTransport` |
The transport used by the client instance. |

### universe_domain

Return the universe domain used by the client instance.

Returns |
|
|---|---|
Type |
Description |
`str` |
The universe domain used by the client instance. |

## Methods

### ExampleStoreServiceAsyncClient

```
ExampleStoreServiceAsyncClient(
*,
credentials: typing.Optional[google.auth.credentials.Credentials] = None,
transport: typing.Optional[
typing.Union[
str,
google.cloud.aiplatform_v1beta1.services.example_store_service.transports.base.ExampleStoreServiceTransport,
typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.services.example_store_service.transports.base.ExampleStoreServiceTransport,
],
]
] = "grpc_asyncio",
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
client_info: google.api_core.gapic_v1.client_info.ClientInfo = google.api_core.gapic_v1.client_info.ClientInfo
)
```


Instantiates the example store service async client.

Parameters |
|
|---|---|
Name |
Description |
`credentials` |
`Optional[google.auth.credentials.Credentials]`
The authorization credentials to attach to requests. These credentials identify the application to the service; if none are specified, the client will attempt to ascertain the credentials from the environment. |
`transport` |
`Optional[Union[str,ExampleStoreServiceTransport,Callable[..., ExampleStoreServiceTransport]]]`
The transport to use, or a Callable that constructs and returns a new transport to use. If a Callable is given, it will be called with the same set of initialization arguments as used in the ExampleStoreServiceTransport constructor. If set to None, a transport is chosen automatically. |
`client_options` |
`Optional[Union[google.api_core.client_options.ClientOptions, dict]]`
Custom options for the client. 1. The |
`client_info` |
`google.api_core.gapic_v1.client_info.ClientInfo`
The client info used to send a user-agent string along with API requests. If |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTlsChannelError` |
If mutual TLS transport creation failed for any reason. |

### cancel_operation

```
cancel_operation(
request: typing.Optional[
google.longrunning.operations_pb2.CancelOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Starts asynchronous cancellation on a long-running operation.

The server makes a best effort to cancel the operation, but success
is not guaranteed. If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### common_billing_account_path

`common_billing_account_path(billing_account: str) -> str`


Returns a fully-qualified billing_account string.

### common_folder_path

`common_folder_path(folder: str) -> str`


Returns a fully-qualified folder string.

### common_location_path

`common_location_path(project: str, location: str) -> str`


Returns a fully-qualified location string.

### common_organization_path

`common_organization_path(organization: str) -> str`


Returns a fully-qualified organization string.

### common_project_path

`common_project_path(project: str) -> str`


Returns a fully-qualified project string.

### create_example_store

```
create_example_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.CreateExampleStoreRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
example_store: typing.Optional[
google.cloud.aiplatform_v1beta1.types.example_store.ExampleStore
] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Create an ExampleStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_create_example_store():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
example_store = aiplatform_v1beta1.[ExampleStore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExampleStore.html)()
example_store.display_name = "display_name_value"
example_store.example_store_config.vertex_embedding_model = "vertex_embedding_model_value"
request = aiplatform_v1beta1.[CreateExampleStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateExampleStoreRequest.html)(
parent="parent_value",
example_store=example_store,
)
# Make the request
operation = client.[create_example_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_create_example_store)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.CreateExampleStore. |
`parent` |
Required. The resource name of the Location to create the ExampleStore in. Format: |
`example_store` |
Required. The Example Store to be created. This corresponds to the |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be
|

### delete_example_store

```
delete_example_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.DeleteExampleStoreRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Delete an ExampleStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_delete_example_store():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[DeleteExampleStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteExampleStoreRequest.html)(
name="name_value",
)
# Make the request
operation = client.[delete_example_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_delete_example_store)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.DeleteExampleStore. |
`name` |
Required. The resource name of the ExampleStore to be deleted. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be `google.protobuf.empty_pb2.Empty` A generic empty message that you can re-use to avoid defining duplicated empty messages in your APIs. A typical example is to use it as the request or the response type of an API method. For instance: service Foo { rpc Bar(google.protobuf.Empty) returns (google.protobuf.Empty); } |

### delete_operation

```
delete_operation(
request: typing.Optional[
google.longrunning.operations_pb2.DeleteOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> None
```


Deletes a long-running operation.

This method indicates that the client is no longer interested
in the operation result. It does not cancel the operation.
If the server doesn't support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

### example_store_path

`example_store_path(project: str, location: str, example_store: str) -> str`


Returns a fully-qualified example_store string.

### fetch_examples

```
fetch_examples(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.FetchExamplesRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.FetchExamplesAsyncPager
)
```


Get Examples from the Example Store.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_fetch_examples():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[FetchExamplesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.FetchExamplesRequest.html)(
example_store="example_store_value",
)
# Make the request
page_result = client.[fetch_examples](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_fetch_examples)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.FetchExamples. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ExampleStoreService.FetchExamples. Iterating over this object will yield results and resolve additional pages automatically. |

### from_service_account_file

`from_service_account_file(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`ExampleStoreServiceAsyncClient` |
The constructed client. |

### from_service_account_info

`from_service_account_info(info: dict, *args, **kwargs)`


Creates an instance of this client using the provided credentials info.

Parameter |
|
|---|---|
Name |
Description |
`info` |
`dict`
The service account private key info. |

Returns |
|
|---|---|
Type |
Description |
`ExampleStoreServiceAsyncClient` |
The constructed client. |

### from_service_account_json

`from_service_account_json(filename: str, *args, **kwargs)`


Creates an instance of this client using the provided credentials file.

Parameter |
|
|---|---|
Name |
Description |
`filename` |
`str`
The path to the service account private key json file. |

Returns |
|
|---|---|
Type |
Description |
`ExampleStoreServiceAsyncClient` |
The constructed client. |

### get_example_store

```
get_example_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.GetExampleStoreRequest,
dict,
]
] = None,
*,
name: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.example_store.ExampleStore
```


Get an ExampleStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_get_example_store():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[GetExampleStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetExampleStoreRequest.html)(
name="name_value",
)
# Make the request
response = await client.[get_example_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_get_example_store)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.GetExampleStore. |
`name` |
Required. The resource name of the ExampleStore. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Represents an executable service to manage and retrieve examples. |

### get_iam_policy

```
get_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.GetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Gets the IAM access control policy for a function.

Returns an empty policy if the function exists and does not have a policy set.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### get_location

```
get_location(
request: typing.Optional[
google.cloud.location.locations_pb2.GetLocationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.Location
```


Gets information about a location.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Location object. |

### get_mtls_endpoint_and_cert_source

```
get_mtls_endpoint_and_cert_source(
client_options: typing.Optional[
google.api_core.client_options.ClientOptions
] = None,
)
```


Return the API endpoint and client cert source for mutual TLS.

The client cert source is determined in the following order:
(1) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is not "true", the
client cert source is None.
(2) if `client_options.client_cert_source`

is provided, use the provided one; if the
default client cert source exists, use the default one; otherwise the client cert
source is None.

The API endpoint is determined in the following order:
(1) if `client_options.api_endpoint`

if provided, use the provided one.
(2) if `GOOGLE_API_USE_CLIENT_CERTIFICATE`

environment variable is "always", use the
default mTLS endpoint; if the environment variable is "never", use the default API
endpoint; otherwise if client cert source exists, use the default mTLS endpoint, otherwise
use the default API endpoint.

More details can be found at [https://google.aip.dev/auth/4114](https://google.aip.dev/auth/4114).

Parameter |
|
|---|---|
Name |
Description |
`client_options` |
`google.api_core.client_options.ClientOptions`
Custom options for the client. Only the |

Exceptions |
|
|---|---|
Type |
Description |
`google.auth.exceptions.MutualTLSChannelError` |
If any errors happen. |

Returns |
|
|---|---|
Type |
Description |
`Tuple[str, Callable[[], Tuple[bytes, bytes]]]` |
returns the API endpoint and the client cert source to use. |

### get_operation

```
get_operation(
request: typing.Optional[
google.longrunning.operations_pb2.GetOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Gets the latest state of a long-running operation.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

### get_transport_class

```
get_transport_class(
label: typing.Optional[str] = None,
) -> typing.Type[
google.cloud.aiplatform_v1beta1.services.example_store_service.transports.base.ExampleStoreServiceTransport
]
```


Returns an appropriate transport class.

Parameter |
|
|---|---|
Name |
Description |
`label` |
`typing.Optional[str]`
The name of the desired transport. If none is provided, then the first transport in the registry is used. |

### list_example_stores

```
list_example_stores(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.ListExampleStoresRequest,
dict,
]
] = None,
*,
parent: typing.Optional[str] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> (
google.cloud.aiplatform_v1beta1.services.example_store_service.pagers.ListExampleStoresAsyncPager
)
```


List ExampleStores in a Location.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_list_example_stores():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[ListExampleStoresRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListExampleStoresRequest.html)(
parent="parent_value",
)
# Make the request
page_result = client.[list_example_stores](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_list_example_stores)(request=request)
# Handle the response
async for response in page_result:
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.ListExampleStores. |
`parent` |
Required. The resource name of the Location to list the ExampleStores from. Format: |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ExampleStoreService.ListExampleStores. Iterating over this object will yield results and resolve additional pages automatically. |

### list_locations

```
list_locations(
request: typing.Optional[
google.cloud.location.locations_pb2.ListLocationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.location.locations_pb2.ListLocationsResponse
```


Lists information about the supported locations for this service.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListLocations` method. |

### list_operations

```
list_operations(
request: typing.Optional[
google.longrunning.operations_pb2.ListOperationsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.ListOperationsResponse
```


Lists operations that match the specified filter in the request.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `ListOperations` method. |

### parse_common_billing_account_path

`parse_common_billing_account_path(path: str) -> typing.Dict[str, str]`


Parse a billing_account path into its component segments.

### parse_common_folder_path

`parse_common_folder_path(path: str) -> typing.Dict[str, str]`


Parse a folder path into its component segments.

### parse_common_location_path

`parse_common_location_path(path: str) -> typing.Dict[str, str]`


Parse a location path into its component segments.

### parse_common_organization_path

`parse_common_organization_path(path: str) -> typing.Dict[str, str]`


Parse a organization path into its component segments.

### parse_common_project_path

`parse_common_project_path(path: str) -> typing.Dict[str, str]`


Parse a project path into its component segments.

### parse_example_store_path

`parse_example_store_path(path: str) -> typing.Dict[str, str]`


Parses a example_store path into its component segments.

### remove_examples

```
remove_examples(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.RemoveExamplesRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.example_store_service.RemoveExamplesResponse
```


Remove Examples from the Example Store.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_remove_examples():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
request = aiplatform_v1beta1.[RemoveExamplesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveExamplesRequest.html)(
example_store="example_store_value",
)
# Make the request
response = await client.[remove_examples](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_remove_examples)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.RemoveExamples. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ExampleStoreService.RemoveExamples. |

### search_examples

```
search_examples(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.SearchExamplesRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.example_store_service.SearchExamplesResponse
```


Search for similar Examples for given selection criteria.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_search_examples():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
stored_contents_example_parameters = aiplatform_v1beta1.[StoredContentsExampleParameters](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.StoredContentsExampleParameters.html)()
stored_contents_example_parameters.search_key = "search_key_value"
request = aiplatform_v1beta1.[SearchExamplesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SearchExamplesRequest.html)(
stored_contents_example_parameters=stored_contents_example_parameters,
example_store="example_store_value",
)
# Make the request
response = await client.[search_examples](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_search_examples)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.SearchExamples. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ExampleStoreService.SearchExamples. |

### set_iam_policy

```
set_iam_policy(
request: typing.Optional[google.iam.v1.iam_policy_pb2.SetIamPolicyRequest] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.policy_pb2.Policy
```


Sets the IAM access control policy on the specified function.

Replaces any existing policy.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Defines an Identity and Access Management (IAM) policy. It is used to specify access control policies for Cloud Platform resources. A `Policy` is a collection of `bindings` . A `binding` binds one or more `members` to a single `role` . Members can be user accounts, service accounts, Google groups, and domains (such as G Suite). A `role` is a named list of permissions (defined by IAM or configured by users). A `binding` can optionally specify a `condition` , which is a logic expression that further constrains the role binding based on attributes about the request and/or target resource. **JSON Example** :: { "bindings": [ { "role": "roles/resourcemanager.organizationAdmin", "members": [ "user:mike@example.com", "group:admins@example.com", "domain:google.com", "serviceAccount:my-project-id@appspot.gserviceaccount.com" ] }, { "role": "roles/resourcemanager.organizationViewer", "members": ["user:eve@example.com"], "condition": { "title": "expirable access", "description": "Does not grant access after Sep 2020", "expression": "request.time < timestamp('2020-10-01t00:00:00.000z')",="" }="" }="" ]="" }="" **yaml="" example**="" ::="" bindings:="" -="" members:="" -="" user:mike@example.com="" -="" group:admins@example.com="" -="" domain:google.com="" -="" serviceaccount:my-project-id@appspot.gserviceaccount.com="" role:="" roles/resourcemanager.organizationadmin="" -="" members:="" -="" user:eve@example.com="" role:="" roles/resourcemanager.organizationviewer="" condition:="" title:="" expirable="" access="" description:="" does="" not="" grant="" access="" after="" sep="" 2020="" expression:="" request.time="">< timestamp('2020-10-01t00:00:00.000z')="" for="" a="" description="" of="" iam="" and="" its="" features,="" see="" the="">`IAM developer's guide ` __. |

### test_iam_permissions

```
test_iam_permissions(
request: typing.Optional[
google.iam.v1.iam_policy_pb2.TestIamPermissionsRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.iam.v1.iam_policy_pb2.TestIamPermissionsResponse
```


Tests the specified IAM permissions against the IAM access control policy for a function.

If the function does not exist, this will return an empty set of permissions, not a NOT_FOUND error.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for `TestIamPermissions` method. |

### update_example_store

```
update_example_store(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.UpdateExampleStoreRequest,
dict,
]
] = None,
*,
example_store: typing.Optional[
google.cloud.aiplatform_v1beta1.types.example_store.ExampleStore
] = None,
update_mask: typing.Optional[google.protobuf.field_mask_pb2.FieldMask] = None,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.api_core.operation_async.AsyncOperation
```


Update an ExampleStore.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_update_example_store():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
example_store = aiplatform_v1beta1.[ExampleStore](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExampleStore.html)()
example_store.display_name = "display_name_value"
example_store.example_store_config.vertex_embedding_model = "vertex_embedding_model_value"
request = aiplatform_v1beta1.[UpdateExampleStoreRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpdateExampleStoreRequest.html)(
example_store=example_store,
)
# Make the request
operation = client.[update_example_store](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_update_example_store)(request=request)
print("Waiting for operation to complete...")
response = (await operation).result()
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.UpdateExampleStore. |
`example_store` |
Required. The Example Store which replaces the resource on the server. This corresponds to the |
`update_mask` |
Optional. Mask specifying which fields to update. Supported fields: :: * |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
`google.api_core.operation_async.AsyncOperation` |
An object representing a long-running operation. The result type for the operation will be
|

### upsert_examples

```
upsert_examples(
request: typing.Optional[
typing.Union[
google.cloud.aiplatform_v1beta1.types.example_store_service.UpsertExamplesRequest,
dict,
]
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.cloud.aiplatform_v1beta1.types.example_store_service.UpsertExamplesResponse
```


Create or update Examples in the Example Store.

```
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in:
# https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import aiplatform_v1beta1
async def sample_upsert_examples():
# Create a client
client = aiplatform_v1beta1.
```[ExampleStoreServiceAsyncClient](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html)()
# Initialize request argument(s)
examples = aiplatform_v1beta1.[Example](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Example.html)()
examples.stored_contents_example.contents_example.contents.parts.text = "text_value"
examples.stored_contents_example.contents_example.expected_contents.content.parts.text = "text_value"
request = aiplatform_v1beta1.[UpsertExamplesRequest](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.UpsertExamplesRequest.html)(
example_store="example_store_value",
examples=examples,
)
# Make the request
response = await client.[upsert_examples](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.example_store_service.ExampleStoreServiceAsyncClient.html#google_cloud_aiplatform_v1beta1_services_example_store_service_ExampleStoreServiceAsyncClient_upsert_examples)(request=request)
# Handle the response
print(response)


Parameters |
|
|---|---|
Name |
Description |
`request` |
`Optional[Union[`
The request object. Request message for ExampleStoreService.UpsertExamples. |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
Response message for ExampleStoreService.UpsertExamples. |

### wait_operation

```
wait_operation(
request: typing.Optional[
google.longrunning.operations_pb2.WaitOperationRequest
] = None,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
) -> google.longrunning.operations_pb2.Operation
```


Waits until the specified long-running operation is done or reaches at most a specified timeout, returning the latest state.

If the operation is already done, the latest state is immediately returned.
If the timeout specified is greater than the default HTTP/RPC timeout, the HTTP/RPC
timeout is used. If the server does not support this method, it returns
`google.rpc.Code.UNIMPLEMENTED`

.

Parameters |
|
|---|---|
Name |
Description |
`request` |
The request object. Request message for |
`retry` |
`google.api_core.retry_async.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

Returns |
|
|---|---|
Type |
Description |
|
An `Operation` object. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListHyperparameterTuningJobsPager -->

# Class ListHyperparameterTuningJobsPager (1.134.0)

```
ListHyperparameterTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_hyperparameter_tuning_jobs`

requests.

This class thinly wraps an initial
[ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse) object, and
provides an `__iter__`

method to iterate through its
`hyperparameter_tuning_jobs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListHyperparameterTuningJobs`

requests and continue to iterate
through the `hyperparameter_tuning_jobs`

field on the
corresponding responses.

All the usual [ListHyperparameterTuningJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListHyperparameterTuningJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListHyperparameterTuningJobsPager

```
ListHyperparameterTuningJobsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListHyperparameterTuningJobsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.job_service.pagers.ListBatchPredictionJobsAsyncPager -->

# Class ListBatchPredictionJobsAsyncPager (1.134.0)

```
ListBatchPredictionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_batch_prediction_jobs`

requests.

This class thinly wraps an initial
[ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse) object, and
provides an `__aiter__`

method to iterate through its
`batch_prediction_jobs`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListBatchPredictionJobs`

requests and continue to iterate
through the `batch_prediction_jobs`

field on the
corresponding responses.

All the usual [ListBatchPredictionJobsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListBatchPredictionJobsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListBatchPredictionJobsAsyncPager

```
ListBatchPredictionJobsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsRequest,
response: google.cloud.aiplatform_v1beta1.types.job_service.ListBatchPredictionJobsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RemoveExamplesRequest -->

# Class RemoveExamplesRequest (1.134.0)

`RemoveExamplesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.RemoveExamples.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`stored_contents_example_filter` |
The metadata filters for StoredContentsExamples. This field is a member of `oneof` _ `metadata_filter` .
|
`example_store` |
`str`
Required. The name of the ExampleStore resource that the examples should be removed from. Format: `projects/{project}/locations/{location}/exampleStores/{example_store}`
|
`example_ids` |
`MutableSequence[str]`
Optional. Example IDs to remove. If both metadata filters and Example IDs are specified, the metadata filters will be applied to the specified examples in order to identify which should be removed. |

## Methods

### RemoveExamplesRequest

`RemoveExamplesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExampleStoreService.RemoveExamples.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExportModelRequest.OutputConfig -->

# Class OutputConfig (1.134.0)

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output configuration for the Model export.

## Attributes |
|
|---|---|
Name |
Description |
`export_format_id` |
`str`
The ID of the format in which the Model must be exported. Each Model lists the [export formats it supports][google.cloud.aiplatform.v1beta1.Model.supported_export_formats]. If no value is provided here, then the first from the list of the Model's supported formats is used by default. |
`artifact_destination` |
The Cloud Storage location where the Model artifact is to be written to. Under the directory given as the destination a new one with name " `model-export-` ",
where timestamp is in YYYY-MM-DDThh:mm:ss.sssZ ISO-8601
format, will be created. Inside, the Model and any of its
supporting files will be written. This field should only be
set when the `exportableContent` field of the
[Model.supported_export_formats] object contains
`ARTIFACT` .
|
`image_destination` |
The Google Container Registry or Artifact Registry uri where the Model container image will be copied to. This field should only be set when the `exportableContent` field of
the [Model.supported_export_formats] object contains
`IMAGE` .
|

## Methods

### OutputConfig

`OutputConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Output configuration for the Model export.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTensorboardRunsRequest -->

# Class ListTensorboardRunsRequest (1.134.0)

`ListTensorboardRunsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ListTensorboardRuns.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the TensorboardExperiment to list TensorboardRuns. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|
`filter` |
`str`
Lists the TensorboardRuns that match the filter expression. |
`page_size` |
`int`
The maximum number of TensorboardRuns to return. The service may return fewer than this value. If unspecified, at most 50 TensorboardRuns are returned. The maximum value is 1000; values above 1000 are coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous TensorboardService.ListTensorboardRuns call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to TensorboardService.ListTensorboardRuns must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the list. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListTensorboardRunsRequest

`ListTensorboardRunsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ListTensorboardRuns.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.CreateSessionRequest -->

# Class CreateSessionRequest (1.134.0)

`CreateSessionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.CreateSession.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the location to create the session in. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoning_engine}`
|
`session` |
Required. The session to create. |

## Methods

### CreateSessionRequest

`CreateSessionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for SessionService.CreateSession.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.PairwiseSummarizationQualityInput -->

# Class PairwiseSummarizationQualityInput (1.134.0)

```
PairwiseSummarizationQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise summarization quality metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for pairwise summarization quality score metric. |
`instance` |
Required. Pairwise summarization quality instance. |

## Methods

### PairwiseSummarizationQualityInput

```
PairwiseSummarizationQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise summarization quality metric.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringHelpfulnessInput -->

# Class QuestionAnsweringHelpfulnessInput (1.134.0)

```
QuestionAnsweringHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering helpfulness metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for question answering helpfulness score metric. |
`instance` |
Required. Question answering helpfulness instance. |

## Methods

### QuestionAnsweringHelpfulnessInput

```
QuestionAnsweringHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering helpfulness metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagVectorDbConfig.Weaviate -->

# Class Weaviate (1.134.0)

`Weaviate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Weaviate.

## Attributes |
|
|---|---|
Name |
Description |
`http_endpoint` |
`str`
Weaviate DB instance HTTP endpoint. e.g. 34.56.78.90:8080 Vertex RAG only supports HTTP connection to Weaviate. This value cannot be changed after it's set. |
`collection_name` |
`str`
The corresponding collection this corpus maps to. This value cannot be changed after it's set. |

## Methods

### Weaviate

`Weaviate(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The config for the Weaviate.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GroundingChunk.Maps -->

# Class Maps (1.134.0)

`Maps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from Google Maps.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
URI reference of the chunk. This field is a member of `oneof` _ `_uri` .
|
`title` |
`str`
Title of the chunk. This field is a member of `oneof` _ `_title` .
|
`text` |
`str`
Text of the chunk. This field is a member of `oneof` _ `_text` .
|
`place_id` |
`str`
This Place's resource name, in `places/{place_id}` format.
Can be used to look up the Place.
This field is a member of `oneof` _ `_place_id` .
|
`place_answer_sources` |
Sources used to generate the place answer. This includes review snippets and photos that were used to generate the answer, as well as uris to flag content. |

## Classes

### PlaceAnswerSources

`PlaceAnswerSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Methods

### Maps

`Maps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from Google Maps.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.RagManagedDbConfig -->

# Class RagManagedDbConfig (1.134.0)

`RagManagedDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration message for RagManagedDb used by RagEngine.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`enterprise` |
Sets the RagManagedDb to the Enterprise tier. This field is a member of `oneof` _ `tier` .
|
`scaled` |
Sets the RagManagedDb to the Scaled tier. This is the default tier if not explicitly chosen. This field is a member of `oneof` _ `tier` .
|
`basic` |
Sets the RagManagedDb to the Basic tier. This field is a member of `oneof` _ `tier` .
|
`unprovisioned` |
Sets the RagManagedDb to the Unprovisioned tier. This field is a member of `oneof` _ `tier` .
|

## Classes

### Basic

`Basic(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Basic tier is a cost-effective and low compute tier suitable for the following cases:

- Experimenting with RagManagedDb.
- Small data size.
- Latency insensitive workload.
- Only using RAG Engine with external vector DBs.

NOTE: This is the default tier if not explicitly chosen.

### Enterprise

`Enterprise(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Enterprise tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

### Scaled

`Scaled(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Scaled tier offers production grade performance along with autoscaling functionality. It is suitable for customers with large amounts of data or performance sensitive workloads.

### Unprovisioned

`Unprovisioned(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Disables the RAG Engine service and deletes all your data held within this service. This will halt the billing of the service.

NOTE: Once deleted the data cannot be recovered. To start using RAG Engine again, you will need to update the tier by calling the UpdateRagEngineConfig API.

## Methods

### RagManagedDbConfig

`RagManagedDbConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Configuration message for RagManagedDb used by RagEngine.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.specialist_pool_service.pagers.ListSpecialistPoolsAsyncPager -->

# Class ListSpecialistPoolsAsyncPager (1.134.0)

```
ListSpecialistPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_specialist_pools`

requests.

This class thinly wraps an initial
[ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse) object, and
provides an `__aiter__`

method to iterate through its
`specialist_pools`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListSpecialistPools`

requests and continue to iterate
through the `specialist_pools`

field on the
corresponding responses.

All the usual [ListSpecialistPoolsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListSpecialistPoolsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListSpecialistPoolsAsyncPager

```
ListSpecialistPoolsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsRequest,
response: google.cloud.aiplatform_v1beta1.types.specialist_pool_service.ListSpecialistPoolsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelEvaluationSlicesAsyncPager -->

# Class ListModelEvaluationSlicesAsyncPager (1.134.0)

```
ListModelEvaluationSlicesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_model_evaluation_slices`

requests.

This class thinly wraps an initial
[ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationSlicesResponse) object, and
provides an `__aiter__`

method to iterate through its
`model_evaluation_slices`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelEvaluationSlices`

requests and continue to iterate
through the `model_evaluation_slices`

field on the
corresponding responses.

All the usual [ListModelEvaluationSlicesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelEvaluationSlicesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelEvaluationSlicesAsyncPager

```
ListModelEvaluationSlicesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelEvaluationSlicesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QuestionAnsweringCorrectnessInput -->

# Class QuestionAnsweringCorrectnessInput (1.134.0)

```
QuestionAnsweringCorrectnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering correctness metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for question answering correctness score metric. |
`instance` |
Required. Question answering correctness instance. |

## Methods

### QuestionAnsweringCorrectnessInput

```
QuestionAnsweringCorrectnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering correctness metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SetPublisherModelConfigOperationMetadata -->

# Class SetPublisherModelConfigOperationMetadata (1.134.0)

```
SetPublisherModelConfigOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.SetPublisherModelConfig.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The operation generic information. |

## Methods

### SetPublisherModelConfigOperationMetadata

```
SetPublisherModelConfigOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for EndpointService.SetPublisherModelConfig.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPublisherModelsRequest -->

# Class ListPublisherModelsRequest (1.134.0)

`ListPublisherModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.ListPublisherModels.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the Publisher from which to list the PublisherModels. Format: `publishers/{publisher}`
|
`filter` |
`str`
Optional. The standard list filter. |
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListPublisherModelsResponse.next_page_token of the previous ModelGardenService.ListPublisherModels call. |
`view` |
Optional. PublisherModel view specifying which fields to read. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. |
`language_code` |
`str`
Optional. The IETF BCP-47 language code representing the language in which the publisher models' text information should be written in. If not set, by default English (en). |
`list_all_versions` |
`bool`
Optional. List all publisher model versions if the flag is set to true. |

## Methods

### ListPublisherModelsRequest

`ListPublisherModelsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ModelGardenService.ListPublisherModels.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetMetadataSchemaRequest -->

# Class GetMetadataSchemaRequest (1.134.0)

`GetMetadataSchemaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetMetadataSchema.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the MetadataSchema to retrieve. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}/metadataSchemas/{metadataschema}`
|

## Methods

### GetMetadataSchemaRequest

`GetMetadataSchemaRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for MetadataService.GetMetadataSchema.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.GetBatchPredictionJobRequest -->

# Class GetBatchPredictionJobRequest (1.134.0)

```
GetBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetBatchPredictionJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the BatchPredictionJob resource. Format: `projects/{project}/locations/{location}/batchPredictionJobs/{batch_prediction_job}`
|

## Methods

### GetBatchPredictionJobRequest

```
GetBatchPredictionJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.GetBatchPredictionJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetsRequest -->

# Class ListDatasetsRequest (1.134.0)

`ListDatasetsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasets.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the Dataset's parent resource. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `display_name` : supports = and !=
- `metadata_schema_uri` : supports = and !=
- `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- \`labels.key:\* or labels:key - key existence
- A key including a space must be quoted.
`labels."a key"` .
Some examples:
- `displayName="myDisplayName"`
- `labels.myKey="myValue"`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
|

## Methods

### ListDatasetsRequest

`ListDatasetsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasets.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExplainRequest -->

# Class ExplainRequest (1.134.0)

`ExplainRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.Explain.

## Attributes |
|
|---|---|
Name |
Description |
`endpoint` |
`str`
Required. The name of the Endpoint requested to serve the explanation. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`
|
`instances` |
`MutableSequence[google.protobuf.struct_pb2.Value]`
Required. The instances that are the input to the explanation call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the explanation call errors in case of AutoML Models, or, in case of customer created Models, the behaviour is as documented by that Model. The schema of any single instance may be specified via Endpoint's DeployedModels' [Model's][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] instance_schema_uri. |
`parameters` |
`google.protobuf.struct_pb2.Value`
The parameters that govern the prediction. The schema of the parameters may be specified via Endpoint's DeployedModels' [Model's ][google.cloud.aiplatform.v1beta1.DeployedModel.model] [PredictSchemata's][google.cloud.aiplatform.v1beta1.Model.predict_schemata] parameters_schema_uri. |
`explanation_spec_override` |
If specified, overrides the explanation_spec of the DeployedModel. Can be used for explaining prediction results with different configurations, such as: - Explaining top-5 predictions results as opposed to top-1; - Increasing path count or step count of the attribution methods to reduce approximate errors; - Using different baselines for explaining the prediction results. |
`concurrent_explanation_spec_override` |
`MutableMapping[str, `
Optional. This field is the same as the one above, but supports multiple explanations to occur in parallel. The key can be any string. Each override will be run against the model, then its explanations will be grouped together. Note - these explanations are run **In Addition** to the default Explanation in the deployed model. |
`deployed_model_id` |
`str`
If specified, this ExplainRequest will be served by the chosen DeployedModel, overriding Endpoint.traffic_split. |

## Classes

### ConcurrentExplanationSpecOverrideEntry

```
ConcurrentExplanationSpecOverrideEntry(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

## Methods

### ExplainRequest

`ExplainRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for PredictionService.Explain.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_online_store_admin_service.pagers.ListFeatureViewSyncsPager -->

# Class ListFeatureViewSyncsPager (1.134.0)

```
ListFeatureViewSyncsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_feature_view_syncs`

requests.

This class thinly wraps an initial
[ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_view_syncs`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureViewSyncs`

requests and continue to iterate
through the `feature_view_syncs`

field on the
corresponding responses.

All the usual [ListFeatureViewSyncsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureViewSyncsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureViewSyncsPager

```
ListFeatureViewSyncsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_online_store_admin_service.ListFeatureViewSyncsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.MetadataStore -->

# Class MetadataStore (1.134.0)

`MetadataStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a metadata store. Contains a set of metadata that can be queried.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the MetadataStore instance. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MetadataStore was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MetadataStore was last updated. |
`encryption_spec` |
Customer-managed encryption key spec for a Metadata Store. If set, this Metadata Store and all sub-resources of this Metadata Store are secured using this key. |
`description` |
`str`
Description of the MetadataStore. |
`state` |
Output only. State information of the MetadataStore. |
`dataplex_config` |
Optional. Dataplex integration settings. |

## Classes

### DataplexConfig

`DataplexConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents Dataplex integration settings.

### MetadataStoreState

`MetadataStoreState(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents state information for a MetadataStore.

## Methods

### MetadataStore

`MetadataStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a metadata store. Contains a set of metadata that can be queried.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GetFeatureViewRequest -->

# Class GetFeatureViewRequest (1.134.0)

`GetFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureView.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the FeatureView resource. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}`
|

## Methods

### GetFeatureViewRequest

`GetFeatureViewRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for FeatureOnlineStoreAdminService.GetFeatureView.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.Model.OriginalModelInfo -->

# Class OriginalModelInfo (1.134.0)

`OriginalModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the original Model if this Model is a copy.

## Attribute |
|
|---|---|
Name |
Description |
`model` |
`str`
Output only. The resource name of the Model this Model is a copy of, including the revision. Format: `projects/{project}/locations/{location}/models/{model_id}@{version_id}`
|

## Methods

### OriginalModelInfo

`OriginalModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Contains information about the original Model if this Model is a copy.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.feature_registry_service.pagers.ListFeatureMonitorsAsyncPager -->

# Class ListFeatureMonitorsAsyncPager (1.134.0)

```
ListFeatureMonitorsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_feature_monitors`

requests.

This class thinly wraps an initial
[ListFeatureMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse) object, and
provides an `__aiter__`

method to iterate through its
`feature_monitors`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListFeatureMonitors`

requests and continue to iterate
through the `feature_monitors`

field on the
corresponding responses.

All the usual [ListFeatureMonitorsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListFeatureMonitorsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureMonitorsAsyncPager

```
ListFeatureMonitorsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse
],
],
request: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsRequest,
response: google.cloud.aiplatform_v1beta1.types.feature_registry_service.ListFeatureMonitorsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.SpeculativeDecodingSpec.DraftModelSpeculation -->

# Class DraftModelSpeculation (1.134.0)

`DraftModelSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Draft model speculation works by using the smaller model to generate candidate tokens for speculative decoding.

## Attribute |
|
|---|---|
Name |
Description |
`draft_model` |
`str`
Required. The resource name of the draft model. |

## Methods

### DraftModelSpeculation

`DraftModelSpeculation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Draft model speculation works by using the smaller model to generate candidate tokens for speculative decoding.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.DeleteDataLabelingJobRequest -->

# Class DeleteDataLabelingJobRequest (1.134.0)

```
DeleteDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteDataLabelingJob.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the DataLabelingJob to be deleted. Format: `projects/{project}/locations/{location}/dataLabelingJobs/{data_labeling_job}`
|

## Methods

### DeleteDataLabelingJobRequest

```
DeleteDataLabelingJobRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for JobService.DeleteDataLabelingJob.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.v1beta1.schema.trainingjob.definition_v1beta1.types.AutoMlTablesInputs.Transformation.TextArrayTransformation -->

# Class TextArrayTransformation (1.134.0)

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

## Methods

### TextArrayTransformation

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

### TextArrayTransformation

`TextArrayTransformation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Treats the column as text array and performs following transformation functions.

- Concatenate all text values in the array into a single text value using a space (" ") as a delimiter, and then treat the result as a single text value. Apply the transformations for Text columns.
- Empty arrays treated as an empty text.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ExtensionManifest.ApiSpec -->

# Class ApiSpec (1.134.0)

`ApiSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The API specification shown to the LLM.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`open_api_yaml` |
`str`
The API spec in Open API standard and YAML format. This field is a member of `oneof` _ `api_spec` .
|
`open_api_gcs_uri` |
`str`
Cloud Storage URI pointing to the OpenAPI spec. This field is a member of `oneof` _ `api_spec` .
|

## Methods

### ApiSpec

`ApiSpec(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The API specification shown to the LLM.

This message has `oneof`

_ fields (mutually exclusive fields).
For each oneof, at most one member field can be set at the same time.
Setting any member of the oneof automatically clears all other
members.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardRunsRequest -->

# Class ListTensorboardRunsRequest (1.134.0)

`ListTensorboardRunsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ListTensorboardRuns.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the TensorboardExperiment to list TensorboardRuns. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`
|
`filter` |
`str`
Lists the TensorboardRuns that match the filter expression. |
`page_size` |
`int`
The maximum number of TensorboardRuns to return. The service may return fewer than this value. If unspecified, at most 50 TensorboardRuns are returned. The maximum value is 1000; values above 1000 are coerced to 1000. |
`page_token` |
`str`
A page token, received from a previous TensorboardService.ListTensorboardRuns call. Provide this to retrieve the subsequent page. When paginating, all other parameters provided to TensorboardService.ListTensorboardRuns must match the call that provided the page token. |
`order_by` |
`str`
Field to use to sort the list. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |

## Methods

### ListTensorboardRunsRequest

`ListTensorboardRunsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for TensorboardService.ListTensorboardRuns.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListNotebookRuntimesRequest -->

# Class ListNotebookRuntimesRequest (1.134.0)

`ListNotebookRuntimesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.ListNotebookRuntimes.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location from which to list the NotebookRuntimes. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
Optional. An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `notebookRuntime` supports = and !=. `notebookRuntime`
represents the NotebookRuntime ID, i.e. the last segment
of the NotebookRuntime's [resource name]
[google.cloud.aiplatform.v1beta1.NotebookRuntime.name].
- `displayName` supports = and != and regex.
- `notebookRuntimeTemplate` supports = and !=.
`notebookRuntimeTemplate` represents the
NotebookRuntimeTemplate ID, i.e. the last segment of the
NotebookRuntimeTemplate's [resource name]
[google.cloud.aiplatform.v1beta1.NotebookRuntimeTemplate.name].
- `healthState` supports = and !=. healthState enum:
[HEALTHY, UNHEALTHY, HEALTH_STATE_UNSPECIFIED].
- `runtimeState` supports = and !=. runtimeState enum:
[RUNTIME_STATE_UNSPECIFIED, RUNNING, BEING_STARTED,
BEING_STOPPED, STOPPED, BEING_UPGRADED, ERROR, INVALID].
- `runtimeUser` supports = and !=.
- API version is UI only: `uiState` supports = and !=.
uiState enum: [UI_RESOURCE_STATE_UNSPECIFIED,
UI_RESOURCE_STATE_BEING_CREATED, UI_RESOURCE_STATE_ACTIVE,
UI_RESOURCE_STATE_BEING_DELETED,
UI_RESOURCE_STATE_CREATION_FAILED].
- `notebookRuntimeType` supports = and !=.
notebookRuntimeType enum: [USER_DEFINED, ONE_CLICK].
- `machineType` supports = and !=.
- `acceleratorType` supports = and !=.
Some examples:
- `notebookRuntime="notebookRuntime123"`
- `displayName="myDisplayName"` and
`displayName=` "myDisplayNameRegex"`
- `notebookRuntimeTemplate="notebookRuntimeTemplate321"`
- `healthState=HEALTHY`
- `runtimeState=RUNNING`
- `runtimeUser="test@google.com"`
- `uiState=UI_RESOURCE_STATE_BEING_DELETED`
- `notebookRuntimeType=USER_DEFINED`
- `machineType=e2-standard-4`
- `acceleratorType=NVIDIA_TESLA_T4`
|
`page_size` |
`int`
Optional. The standard list page size. |
`page_token` |
`str`
Optional. The standard list page token. Typically obtained via ListNotebookRuntimesResponse.next_page_token of the previous NotebookService.ListNotebookRuntimes call. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Optional. Mask specifying which fields to read. |
`order_by` |
`str`
Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
Example: `display_name, create_time desc` .
|

## Methods

### ListNotebookRuntimesRequest

`ListNotebookRuntimesRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for NotebookService.ListNotebookRuntimes.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.persistent_resource_service.pagers.ListPersistentResourcesPager -->

# Class ListPersistentResourcesPager (1.134.0)

```
ListPersistentResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_persistent_resources`

requests.

This class thinly wraps an initial
[ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse) object, and
provides an `__iter__`

method to iterate through its
`persistent_resources`

field.

If there are more pages, the `__iter__`

method will make additional
`ListPersistentResources`

requests and continue to iterate
through the `persistent_resources`

field on the
corresponding responses.

All the usual [ListPersistentResourcesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListPersistentResourcesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListPersistentResourcesPager

```
ListPersistentResourcesPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
],
request: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesRequest,
response: google.cloud.aiplatform_v1beta1.types.persistent_resource_service.ListPersistentResourcesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.services.tensorboard_service.pagers.ListTensorboardExperimentsPager -->

# Class ListTensorboardExperimentsPager (1.134.0)

```
ListTensorboardExperimentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_tensorboard_experiments`

requests.

This class thinly wraps an initial
[ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsResponse) object, and
provides an `__iter__`

method to iterate through its
`tensorboard_experiments`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTensorboardExperiments`

requests and continue to iterate
through the `tensorboard_experiments`

field on the
corresponding responses.

All the usual [ListTensorboardExperimentsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListTensorboardExperimentsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListTensorboardExperimentsPager

```
ListTensorboardExperimentsPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
],
request: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsRequest,
response: google.cloud.aiplatform_v1beta1.types.tensorboard_service.ListTensorboardExperimentsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListDatasetVersionsResponse -->

# Class ListDatasetVersionsResponse (1.134.0)

`ListDatasetVersionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListDatasetVersions.

## Attributes |
|
|---|---|
Name |
Description |
`dataset_versions` |
`MutableSequence[`
A list of DatasetVersions that matches the specified filter in the request. |
`next_page_token` |
`str`
The standard List next-page token. |

## Methods

### ListDatasetVersionsResponse

`ListDatasetVersionsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for DatasetService.ListDatasetVersions.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SummarizationHelpfulnessSpec -->

# Class SummarizationHelpfulnessSpec (1.134.0)

```
SummarizationHelpfulnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness score metric.

## Attributes |
|
|---|---|
Name |
Description |
`use_reference` |
`bool`
Optional. Whether to use instance.reference to compute summarization helpfulness. |
`version` |
`int`
Optional. Which version to use for evaluation. |

## Methods

### SummarizationHelpfulnessSpec

```
SummarizationHelpfulnessSpec(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Spec for summarization helpfulness score metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.GroundingChunk.Maps -->

# Class Maps (1.134.0)

`Maps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from Google Maps.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`uri` |
`str`
URI reference of the chunk. This field is a member of `oneof` _ `_uri` .
|
`title` |
`str`
Title of the chunk. This field is a member of `oneof` _ `_title` .
|
`text` |
`str`
Text of the chunk. This field is a member of `oneof` _ `_text` .
|
`place_id` |
`str`
This Place's resource name, in `places/{place_id}` format.
Can be used to look up the Place.
This field is a member of `oneof` _ `_place_id` .
|
`place_answer_sources` |
Sources used to generate the place answer. This includes review snippets and photos that were used to generate the answer, as well as uris to flag content. |

## Classes

### PlaceAnswerSources

`PlaceAnswerSources(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


## Methods

### Maps

`Maps(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Chunk from Google Maps.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DeleteDatasetVersionRequest -->

# Class DeleteDatasetVersionRequest (1.134.0)

`DeleteDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDatasetVersion.

## Attribute |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The resource name of the Dataset version to delete. Format: `projects/{project}/locations/{location}/datasets/{dataset}/datasetVersions/{dataset_version}`
|

## Methods

### DeleteDatasetVersionRequest

`DeleteDatasetVersionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.DeleteDatasetVersion.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FeatureView.FeatureRegistrySource.FeatureGroup -->

# Class FeatureGroup (1.134.0)

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Features belonging to a single feature group that will be synced to Online Store.

## Attributes |
|
|---|---|
Name |
Description |
`feature_group_id` |
`str`
Required. Identifier of the feature group. |
`feature_ids` |
`MutableSequence[str]`
Required. Identifiers of features under the feature group. |

## Methods

### FeatureGroup

`FeatureGroup(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Features belonging to a single feature group that will be synced to Online Store.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.SearchMigratableResourcesRequest -->

# Class SearchMigratableResourcesRequest (1.134.0)

```
SearchMigratableResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MigrationService.SearchMigratableResources.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The location that the migratable resources should be searched from. It's the Vertex AI location that the resources can be migrated to, not the resources' original location. Format: `projects/{project}/locations/{location}`
|
`page_size` |
`int`
The standard page size. The default and maximum value is 100. |
`page_token` |
`str`
The standard page token. |
`filter` |
`str`
A filter for your search. You can use the following types of filters: - Resource type filters. The following strings filter for a specific type of MigratableResource: - `ml_engine_model_version:*`
- `automl_model:*`
- `automl_dataset:*`
- `data_labeling_dataset:*`
- "Migrated or not" filters. The following strings filter
for resources that either have or have not already been
migrated:
- `last_migrate_time:*` filters for migrated resources.
- `NOT last_migrate_time:*` filters for not yet migrated
resources.
|

## Methods

### SearchMigratableResourcesRequest

```
SearchMigratableResourcesRequest(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Request message for MigrationService.SearchMigratableResources.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.model_service.pagers.ListModelVersionCheckpointsAsyncPager -->

# Class ListModelVersionCheckpointsAsyncPager (1.134.0)

```
ListModelVersionCheckpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_model_version_checkpoints`

requests.

This class thinly wraps an initial
[ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionCheckpointsResponse) object, and
provides an `__aiter__`

method to iterate through its
`checkpoints`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListModelVersionCheckpoints`

requests and continue to iterate
through the `checkpoints`

field on the
corresponding responses.

All the usual [ListModelVersionCheckpointsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListModelVersionCheckpointsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListModelVersionCheckpointsAsyncPager

```
ListModelVersionCheckpointsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse
],
],
request: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsRequest,
response: google.cloud.aiplatform_v1.types.model_service.ListModelVersionCheckpointsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ListDatasetsRequest -->

# Class ListDatasetsRequest (1.134.0)

`ListDatasetsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasets.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The name of the Dataset's parent resource. Format: `projects/{project}/locations/{location}`
|
`filter` |
`str`
An expression for filtering the results of the request. For field names both snake_case and camelCase are supported. - `display_name` : supports = and !=
- `metadata_schema_uri` : supports = and !=
- `labels` supports general map functions that is:
- `labels.key=value` - key:value equality
- \`labels.key:\* or labels:key - key existence
- A key including a space must be quoted.
`labels."a key"` .
Some examples:
- `displayName="myDisplayName"`
- `labels.myKey="myValue"`
|
`page_size` |
`int`
The standard list page size. |
`page_token` |
`str`
The standard list page token. |
`read_mask` |
`google.protobuf.field_mask_pb2.FieldMask`
Mask specifying which fields to read. |
`order_by` |
`str`
A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: - `display_name`
- `create_time`
- `update_time`
|

## Methods

### ListDatasetsRequest

`ListDatasetsRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for DatasetService.ListDatasets.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResourceRuntime -->

# Class ResourceRuntime (1.134.0)

`ResourceRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Persistent Cluster runtime information as output

## Attributes |
|
|---|---|
Name |
Description |
`access_uris` |
`MutableMapping[str, str]`
Output only. URIs for user to connect to the Cluster. Example: { "RAY_HEAD_NODE_INTERNAL_IP": "head-node-IP:10001" "RAY_DASHBOARD_URI": "ray-dashboard-address:8888" } |
`notebook_runtime_template` |
`str`
Output only. The resource name of NotebookRuntimeTemplate for the RoV Persistent Cluster The NotebokRuntimeTemplate is created in the same VPC (if set), and with the same Ray and Python version as the Persistent Cluster. Example: "projects/1000/locations/us-central1/notebookRuntimeTemplates/abc123". |

## Classes

### AccessUrisEntry

`AccessUrisEntry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The abstract base class for a message.

Parameters |
|
|---|---|
Name |
Description |
`kwargs` |
`dict`
Keys and values corresponding to the fields of the message. |
`mapping` |
`Union[dict, `
A dictionary or message to be used to determine the values for this message. |
`ignore_unknown_fields` |
`Optional(bool)`
If True, do not raise errors for unknown fields. Only applied if |

## Methods

### ResourceRuntime

`ResourceRuntime(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Persistent Cluster runtime information as output

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.AugmentPromptRequest -->

# Class AugmentPromptRequest (1.134.0)

`AugmentPromptRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for AugmentPrompt.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

## Attributes |
|
|---|---|
Name |
Description |
`vertex_rag_store` |
Optional. Retrieves contexts from the Vertex RagStore. This field is a member of `oneof` _ `data_source` .
|
`parent` |
`str`
Required. The resource name of the Location from which to augment prompt. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .
|
`contents` |
`MutableSequence[`
Optional. Input content to augment, only text format is supported for now. |
`model` |
Optional. Metadata of the backend deployed model. |

## Classes

### Model

`Model(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Metadata of the backend deployed model.

## Methods

### AugmentPromptRequest

`AugmentPromptRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for AugmentPrompt.

.. _oneof: [https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields](https://proto-plus-python.readthedocs.io/en/stable/fields.html#oneofs-mutually-exclusive-fields)

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ImportExtensionRequest -->

# Class ImportExtensionRequest (1.134.0)

`ImportExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.ImportExtension.

## Attributes |
|
|---|---|
Name |
Description |
`parent` |
`str`
Required. The resource name of the Location to import the Extension in. Format: `projects/{project}/locations/{location}`
|
`extension` |
Required. The Extension to import. |

## Methods

### ImportExtensionRequest

`ImportExtensionRequest(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Request message for ExtensionRegistryService.ImportExtension.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.ResourcesConsumed -->

# Class ResourcesConsumed (1.134.0)

`ResourcesConsumed(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Statistics information about resource consumption.

## Attribute |
|
|---|---|
Name |
Description |
`replica_hours` |
`float`
Output only. The number of replica hours used. Note that many replicas may run in parallel, and additionally any given work may be queued for some time. Therefore this value is not strictly related to wall time. |

## Methods

### ResourcesConsumed

`ResourcesConsumed(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Statistics information about resource consumption.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListCachedContentsResponse -->

# Class ListCachedContentsResponse (1.134.0)

`ListCachedContentsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response with a list of CachedContents.

## Attributes |
|
|---|---|
Name |
Description |
`cached_contents` |
`MutableSequence[`
List of cached contents. |
`next_page_token` |
`str`
A token, which can be sent as `page_token` to retrieve the
next page. If this field is omitted, there are no subsequent
pages.
|

## Methods

### ListCachedContentsResponse

`ListCachedContentsResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response with a list of CachedContents.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.BatchCancelPipelineJobsOperationMetadata -->

# Class BatchCancelPipelineJobsOperationMetadata (1.134.0)

```
BatchCancelPipelineJobsOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for PipelineService.BatchCancelPipelineJobs.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### BatchCancelPipelineJobsOperationMetadata

```
BatchCancelPipelineJobsOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for PipelineService.BatchCancelPipelineJobs.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.MetadataStore -->

# Class MetadataStore (1.134.0)

`MetadataStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a metadata store. Contains a set of metadata that can be queried.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. The resource name of the MetadataStore instance. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MetadataStore was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this MetadataStore was last updated. |
`encryption_spec` |
Customer-managed encryption key spec for a Metadata Store. If set, this Metadata Store and all sub-resources of this Metadata Store are secured using this key. |
`description` |
`str`
Description of the MetadataStore. |
`state` |
Output only. State information of the MetadataStore. |
`dataplex_config` |
Optional. Dataplex integration settings. |

## Classes

### DataplexConfig

`DataplexConfig(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents Dataplex integration settings.

### MetadataStoreState

`MetadataStoreState(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Represents state information for a MetadataStore.

## Methods

### MetadataStore

`MetadataStore(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Instance of a metadata store. Contains a set of metadata that can be queried.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.feature_online_store_admin_service.pagers.ListFeatureOnlineStoresPager -->

# Class ListFeatureOnlineStoresPager (1.134.0)

```
ListFeatureOnlineStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_feature_online_stores`

requests.

This class thinly wraps an initial
[ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse) object, and
provides an `__iter__`

method to iterate through its
`feature_online_stores`

field.

If there are more pages, the `__iter__`

method will make additional
`ListFeatureOnlineStores`

requests and continue to iterate
through the `feature_online_stores`

field on the
corresponding responses.

All the usual [ListFeatureOnlineStoresResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListFeatureOnlineStoresResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### ListFeatureOnlineStoresPager

```
ListFeatureOnlineStoresPager(
method: typing.Callable[
[...],
google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
],
request: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresRequest,
response: google.cloud.aiplatform_v1.types.feature_online_store_admin_service.ListFeatureOnlineStoresResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiate the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.Retry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.deployment_resource_pool_service.pagers.QueryDeployedModelsAsyncPager -->

# Class QueryDeployedModelsAsyncPager (1.134.0)

```
QueryDeployedModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse
],
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `query_deployed_models`

requests.

This class thinly wraps an initial
[QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse) object, and
provides an `__aiter__`

method to iterate through its
`deployed_models`

field.

If there are more pages, the `__aiter__`

method will make additional
`QueryDeployedModels`

requests and continue to iterate
through the `deployed_models`

field on the
corresponding responses.

All the usual [QueryDeployedModelsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.QueryDeployedModelsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

## Methods

### QueryDeployedModelsAsyncPager

```
QueryDeployedModelsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse
],
],
request: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsRequest,
response: google.cloud.aiplatform_v1.types.deployment_resource_pool_service.QueryDeployedModelsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


Instantiates the pager.

Parameters |
|
|---|---|
Name |
Description |
`method` |
`Callable`
The method that was originally called, and which instantiated this pager. |
`request` |
The initial request object. |
`response` |
The initial response object. |
`retry` |
`google.api_core.retry.AsyncRetry`
Designation of what errors, if any, should be retried. |
`timeout` |
`float`
The timeout for this request. |
`metadata` |
`Sequence[Tuple[str, Union[str, bytes]]]`
Key/value pairs which should be sent along with the request as metadata. Normally, each value must be of type |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringHelpfulnessInput -->

# Class QuestionAnsweringHelpfulnessInput (1.134.0)

```
QuestionAnsweringHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering helpfulness metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for question answering helpfulness score metric. |
`instance` |
Required. Question answering helpfulness instance. |

## Methods

### QuestionAnsweringHelpfulnessInput

```
QuestionAnsweringHelpfulnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering helpfulness metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.UpdateExplanationDatasetOperationMetadata -->

# Class UpdateExplanationDatasetOperationMetadata (1.134.0)

```
UpdateExplanationDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for ModelService.UpdateExplanationDataset.

## Attribute |
|
|---|---|
Name |
Description |
`generic_metadata` |
The common part of the operation metadata. |

## Methods

### UpdateExplanationDatasetOperationMetadata

```
UpdateExplanationDatasetOperationMetadata(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Runtime operation information for ModelService.UpdateExplanationDataset.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.EvaluateDatasetResponse -->

# Class EvaluateDatasetResponse (1.134.0)

`EvaluateDatasetResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response in LRO for EvaluationService.EvaluateDataset.

## Attributes |
|
|---|---|
Name |
Description |
`aggregation_output` |
Output only. Aggregation statistics derived from results of EvaluationService.EvaluateDataset. |
`output_info` |
Output only. Output info for EvaluationService.EvaluateDataset. |

## Methods

### EvaluateDatasetResponse

`EvaluateDatasetResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response in LRO for EvaluationService.EvaluateDataset.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.RetrieveContextsRequest.VertexRagStore.RagResource -->

# Class RagResource (1.134.0)

`RagResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of the Rag resource.

## Attributes |
|
|---|---|
Name |
Description |
`rag_corpus` |
`str`
Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`
|
`rag_file_ids` |
`MutableSequence[str]`
Optional. rag_file_id. The files should be in the same rag_corpus set in rag_corpus field. |

## Methods

### RagResource

`RagResource(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The definition of the Rag resource.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.PairwiseSummarizationQualityInput -->

# Class PairwiseSummarizationQualityInput (1.134.0)

```
PairwiseSummarizationQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise summarization quality metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for pairwise summarization quality score metric. |
`instance` |
Required. Pairwise summarization quality instance. |

## Methods

### PairwiseSummarizationQualityInput

```
PairwiseSummarizationQualityInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for pairwise summarization quality metric.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1beta1.types.QuestionAnsweringCorrectnessInput -->

# Class QuestionAnsweringCorrectnessInput (1.134.0)

```
QuestionAnsweringCorrectnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering correctness metric.

## Attributes |
|
|---|---|
Name |
Description |
`metric_spec` |
Required. Spec for question answering correctness score metric. |
`instance` |
Required. Question answering correctness instance. |

## Methods

### QuestionAnsweringCorrectnessInput

```
QuestionAnsweringCorrectnessInput(
mapping=None, *, ignore_unknown_fields=False, **kwargs
)
```


Input for question answering correctness metric.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse -->

# Class ListStudiesResponse (1.134.0)

`ListStudiesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListStudies.

## Attributes |
|
|---|---|
Name |
Description |
`studies` |
`MutableSequence[`
The studies associated with the project. |
`next_page_token` |
`str`
Passes this token as the `page_token` field of the request
for a subsequent call. If this field is omitted, there are
no subsequent pages.
|

## Methods

### ListStudiesResponse

`ListStudiesResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Response message for VizierService.ListStudies.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.CodeExecutionResult.Outcome -->

# Class Outcome (1.134.0)

`Outcome(value)`


Enumeration of possible outcomes of the code execution.

## Enums |
|
|---|---|
Name |
Description |
`OUTCOME_UNSPECIFIED` |
Unspecified status. This value should not be used. |
`OUTCOME_OK` |
Code execution completed successfully. |
`OUTCOME_FAILED` |
Code execution finished but with a failure. `stderr` should contain the reason. |
`OUTCOME_DEADLINE_EXCEEDED` |
Code execution ran for too long, and was cancelled. There may or may not be a partial output present. |

## Methods

### Outcome

`Outcome(value)`


Enumeration of possible outcomes of the code execution.

---
<!-- Source: N/A -->

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.DatasetVersion -->

# Class DatasetVersion (1.134.0)

`DatasetVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the dataset version.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Output only. Identifier. The resource name of the DatasetVersion. |
`create_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DatasetVersion was created. |
`update_time` |
`google.protobuf.timestamp_pb2.Timestamp`
Output only. Timestamp when this DatasetVersion was last updated. |
`etag` |
`str`
Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens. |
`big_query_dataset_name` |
`str`
Output only. Name of the associated BigQuery dataset. |
`display_name` |
`str`
The user-defined name of the DatasetVersion. The name can be up to 128 characters long and can consist of any UTF-8 characters. |
`metadata` |
`google.protobuf.struct_pb2.Value`
Required. Output only. Additional information about the DatasetVersion. |
`model_reference` |
`str`
Output only. Reference to the public base model last used by the dataset version. Only set for prompt dataset versions. |
`satisfies_pzs` |
`bool`
Output only. Reserved for future use. |
`satisfies_pzi` |
`bool`
Output only. Reserved for future use. |

## Methods

### DatasetVersion

`DatasetVersion(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Describes the dataset version.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.FunctionResponse -->

# Class FunctionResponse (1.134.0)

`FunctionResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result output from a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function is used as context to the model. This should contain the result of a [FunctionCall] made based on model prediction.

## Attributes |
|
|---|---|
Name |
Description |
`name` |
`str`
Required. The name of the function to call. Matches [FunctionDeclaration.name] and [FunctionCall.name]. |
`response` |
`google.protobuf.struct_pb2.Struct`
Required. The function response in JSON object format. Use "output" key to specify function output and "error" key to specify error details (if any). If "output" and "error" keys are not specified, then whole "response" is treated as function output. |
`parts` |
`MutableSequence[`
Optional. Ordered `Parts` that constitute a function
response. Parts may have different IANA MIME types.
|

## Methods

### FunctionResponse

`FunctionResponse(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


The result output from a [FunctionCall] that contains a string representing the [FunctionDeclaration.name] and a structured JSON object containing any output from the function is used as context to the model. This should contain the result of a [FunctionCall] made based on model prediction.

---
<!-- Source: https://cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers -->

# Module pagers (1.134.0)

API documentation for `aiplatform_v1.services.vizier_service.pagers`

module.

## Classes

[ListStudiesAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListStudiesAsyncPager)

```
ListStudiesAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse
],
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_studies`

requests.

This class thinly wraps an initial
[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse) object, and
provides an `__aiter__`

method to iterate through its
`studies`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListStudies`

requests and continue to iterate
through the `studies`

field on the
corresponding responses.

All the usual [ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListStudiesPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListStudiesPager)

```
ListStudiesPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListStudiesResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_studies`

requests.

This class thinly wraps an initial
[ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse) object, and
provides an `__iter__`

method to iterate through its
`studies`

field.

If there are more pages, the `__iter__`

method will make additional
`ListStudies`

requests and continue to iterate
through the `studies`

field on the
corresponding responses.

All the usual [ListStudiesResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListStudiesResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrialsAsyncPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsAsyncPager)

```
ListTrialsAsyncPager(
method: typing.Callable[
[...],
typing.Awaitable[
google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary_async.AsyncRetry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse) object, and
provides an `__aiter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__aiter__`

method will make additional
`ListTrials`

requests and continue to iterate
through the `trials`

field on the
corresponding responses.

All the usual [ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.

[ListTrialsPager](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.services.vizier_service.pagers.ListTrialsPager)

```
ListTrialsPager(
method: typing.Callable[
[...], google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse
],
request: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsRequest,
response: google.cloud.aiplatform_v1.types.vizier_service.ListTrialsResponse,
*,
retry: typing.Optional[
typing.Union[
google.api_core.retry.retry_unary.Retry,
google.api_core.gapic_v1.method._MethodDefault,
]
] = _MethodDefault._DEFAULT_VALUE,
timeout: typing.Union[float, object] = _MethodDefault._DEFAULT_VALUE,
metadata: typing.Sequence[typing.Tuple[str, typing.Union[str, bytes]]] = ()
)
```


A pager for iterating through `list_trials`

requests.

This class thinly wraps an initial
[ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse) object, and
provides an `__iter__`

method to iterate through its
`trials`

field.

If there are more pages, the `__iter__`

method will make additional
`ListTrials`

requests and continue to iterate
through the `trials`

field on the
corresponding responses.

All the usual [ListTrialsResponse](/python/docs/reference/aiplatform/latest/google.cloud.aiplatform_v1.types.ListTrialsResponse)
attributes are available on the pager. If multiple requests are made, only
the most recent response is retained, and thus used for attribute lookup.
