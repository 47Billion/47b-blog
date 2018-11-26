---
layout: post
title:  "How to evolve product with machine learning intelligence"
author: rajeev
categories: [ machine learning, architecture ]
image: assets/images/2018-11-27-how-to-evolve-product-with-machine-learning-intelligence-1.png
featured: false
hidden: false
---
As an architecture team developing solutions for many startups, we are frequently asked one question—how can I incorporate machine learning algorithms in our product. The question comes mainly from startup founders who are eager to differentiate their product by incorporating machine learning early in the product development cycle.

For a startup, there is no large data set available at the beginning to train the machine learning models. However the machine learning algorithm is effective only when you use a model that has been trained on the data specifically related to your users.

Here are different ways startups can slowly bridge the gap between developing a product that works well with initial users and no large data to developing a fully matured solution that uses machine learning algorithms with models trained with large data gathered over a period of time.

1. Ask short but relevant questions to the user in your application or portal. Use them to build user profile and provide personalization.
2. Capture user location, device data and other context data in your application or portal and add it to the user profile.
3. Capture user behavior in the app and feed it back into your personalization engine to enrich the initial profile.
4. Use rules engine to co-relate different profile values, their weightage and classify users based on the rules engine output.
5. Use regular expressions and look-up dictionaries to interpret the free text for natural language understanding.
6. Use hybrid approach for text interpretation: Some natural language processing libraries like Stanford NLP provides part of speech (POS) and named entity recognition (NER) tags that you can use in regular expression along with the text to provide rich interpretation of text.
7. Narrow down the interpretation of an unstructured data based on other related structured data.
8. Tag data based on rules or regular expressions.
9. Provide manual review of tags or meta-data extracted from unstructured data and ways to correct it. This can be done using backend portal which allows reviewers to easy way of quickly inspecting the unstructured data and do the corrections. There are also third-party services like Amazon Mechanical Turk which can be used to augment and correct meta-data using human intelligence.
10. Provide ways for user to manually tag data in your backend admin portal.
11. Use weighted average of attributes. Initially you have structured data and meta-data extracted from unstructured data. It is not possible to use feature engineering to decide on important attributes in data due to initial lack of large amount of data. In such cases, weights can be assigned to different attributes based on human knowledge and final predicted value can be calculated as weighted average of these attributes.
12. Use the above tagged data to train ML models.
13. Leverage data acquired through your products in the market.
14. Scrape relevant data from sources on the web and use it to train ML models.
15. Generate synthetic data programmatically and use it to train the models: The success this method total depends on how close you can generate synthetic data to real-data with all the randomness and distributions and should be chosen carefully.
16. New cloud based services with prebuilt vertical AI ML models are coming up which can be accessed through APIs.This can be the first step to incorporate ML in your product.
17. Use Machine Learning APIs from cloud providers with built-in models. For speech and text processing, you can use Amazon—Lex, Transcribe, Polly, Comprehed, Translate or Google—DialogFlow, Cloud Natural Language API, Cloud Speech API, Cloud Translation API or Microsoft Speech and Language APIs. For video and image processing, you can use Amazon Rekognition, Google Vision, Microsoft Azure Image and video processing APIs or Google’s Cloud Vision APIs.
18. User MLaaS services like Amazon SageMaker, Microsoft Azure Machine Learning Studio, Google Cloud Machine Learning Engine, IBM Watson Machine Learning Studio.
19. If you wish to develop stack from scratch, choose technology stack like Apache Spark, Flink that provide libraries to run ML algorithms at scale: You can initially run rules engine or procedural programs at scale within these frameworks till enough data is gathered to train ML models. You can then introduce ML algorithms within the same frameworks without needing to choose another stack.
20. Make sure to capture all the raw data right from the start. When you have enough data, use it to train your supervised leaning models and you are on your way to take advantage of machine learning algorithms in your product.

What other techniques have you used in your products in early stages without access to large amount data for personalization or natural language understanding?