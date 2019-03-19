---
layout: post
title:  "How to design the user interface for correcting and labeling machine learning inferences"
author: rajeev
categories: [ machine learning, user experience, user interface design ]
image: assets/images/2019-03-19-how-to-design-the-user-interface-for-correcting-and-labeling-machine-learning-inferences-1.png
featured: true
hidden: false
---
Machine learning algorithms are very dependent on accurate, clean, and well-labeled training data for training to produce accurate results. It's for this reason that the vast majority of the time spent during AI projects is during the data collection, cleaning, preparation, and labeling phases.
When an early-stage ML-based product, trained on limited data, is deployed in production, the results are not accurate. The results may contain false negatives which wrongly indicates that a particular condition or attribute is absent or false positives which wrongly indicates that a particular condition or attribute is present.

ML models mature slowly as more and more labeled data is available. To start with, any early-stage product needs to work with a limited amount of labeled data and slowly build the repository as more such data is collected and interpreted by humans. In the beginning, such a product can be positioned as first-pass automation which needs second pass inspection by humans to rectify any incorrect results from machine learning. The results of the second pass are exposed to end consumers. They can also be used to correctly identify the type of mistakes done by the ML algorithms and attach correct labels so that labeled data can be fed back to improve the model. Eventually, there will be a large amount of already trained neural networks that can be used by organizations for their own model purposes, or extended via transfer learning to new applications. But until that time, organizations need to deal with the human-dominated labor involved in the second pass correction and data labeling. Such products still improve overall efficiency by significantly reducing the amount of manual work needed.
Such human-powered second-pass correction and labeling of unstructured data requires a user interface that allows quick visual review of the first-pass output, ease of correcting errors, providing feedback and attaching labels.

Some examples of products that require the second pass human intervention for corrections are -
- Home value estimation using object detection in house pictures
- Automatic homework grading of handwritten answers to English literature questions based on correct grammar, references to author and characters, etc.
- Detection of disease codes in scanned Electronic Health Records based on OCR and health code dictionaries

Such user interfaces should have the following characteristics -
- Allow the reviewer to quickly visualize the unstructured data (images or text). This is important particularly to detect false negatives (detections missed by the machine learning automation).
- The reviewer should be able to see the navigable list of detected labels.
- The reviewer should be able to quickly traverse each labeled object or text. This allows the user to confirm the result as true positive or mark it as false positive.
- While traversing the detected objects, they should be highlighted on the viewer window for a quick inspection.
- The reviewer should be able to quickly switch between various ways of visualizing the unstructured data while maintaining the highlights. For example, the original PDF or handwritten document and text extracted by OCR for the same document or original clear image and image with objects highlighted with boundaries.
- The reviewer can zoom in/out in the view area.
Search based on labels or text should be provided.
- The reviewer should be easily able to navigate by any additional data extracted from the unstructured data.
- The interface should separately show the context surrounding the detected object in the unstructured document.
- The reviewer can choose whether the ML deleted label is "true positive", "false positive", or unsure.
- For each false positive or unsure, there should be a reviewer comment box to justify the classification.
- For each false negative, the reviewer should be able to add the missing label and corresponding details such as coordinates or position of the missing object.
- The user interface should capture the reviewer name, date and amount of time for review of each document. This time can be used to indicate overall efficiency added by ML first pass algorithm over the manual-only inspection process.

Though machine learning algorithms and models are being improved at a tremendous pace, it would be while before they can completely replace human tasks. In the interim, the combination of machine learning inferences augmented by human intelligence is needed. This article described an efficient user interface to support such second pass human intervention to correct output of machine learning algorithms. 
```
