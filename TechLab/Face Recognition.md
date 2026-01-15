

# Deepface


If you run face recognition withh DeepFace, you get access to a set of features:

- **Face Verification**: The task of face verification refers to comparing a face with another to verify if it is a match or not. Hence, face verification is commonly used to compare a candidate's face to another. This can be used to confirm that a physical face matches the one in an ID document.
	
- **Face Recognition**: The task refers to finding a face in an image database. Performing face recognition requires running face verification many times.
	
- **Facial Attribute Analysis**: The task of facial attribute analysis refers to describing the visual properties of face images. Accordingly, facial attributes analysis is used to extract attributes such as age, gender, classification, **emotion analysis**, or race/ethnicity prediction.
	
- **Real-Time Face Analysis**: This feature includes testing face recognition and facial attribute analysis with the real-time video feed of your webcam.



### `DeepFace.verify`

**`distance`**
Distance between facial embeddings (0 = identical, higher = more different)

**`threshold`**
Model's decision boundary
	- If `distance` < `threshold` -> True (same person)
	- If `distance` > `threshold` -> False (different person)

**`confidence`**
Confidence percentage

- (1 - distance/threshold) x 100 when True
- (threshold/distance) x 100 when False

**`verified`**
Final decision (True/False)

**`facial_areas`**
Face detection coordinates and eye positions



```
{'verified': False,
 'distance': 0.827986,
 'threshold': 0.68,
 'confidence': 6.51,
 'model': 'VGG-Face',
 'detector_backend': 'opencv',
 'similarity_metric': 'cosine',
 'facial_areas': {'img1': {'x': 132,
   'y': 180,
   'w': 539,
   'h': 539,
   'left_eye': (479, 387),
   'right_eye': (352, 608)},
  'img2': {'x': 127,
   'y': 430,
   'w': 970,
   'h': 970,
   'left_eye': (734, 786),
   'right_eye': (415, 860)}},
 'time': 3.73}
```