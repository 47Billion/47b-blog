---
layout: post
title:  "Using object detection in home pictures for improving price estimation"
author: rajeev
categories: [ machine learning, data science ]
image: assets/images/2019-02-04-using-object-detection-for-improving-price-estimation-1.jpeg
featured: true
hidden: false
---

Estimating the price of a home is both science and art. Home characteristics, such as square footage, location or the number of bathrooms, are given different weights according to their influence on home sale prices in each specific geography over a specific period of time, resulting in a set of valuation rules, or models that are applied to generate each home's Zestimate.
Specifically, some of the structured data that is used in the estimation include:
Physical attributes: Location, lot size, square footage, number of bedrooms and bathrooms and many other details.
Tax assessments: Property tax information, actual property taxes paid, exceptions to tax assessments and other information provided in the tax assessors' records.
Prior and current transactions: Actual sale prices over time of the home itself and comparable recent sales of nearby homes.

Besides the structured data, there are a lot of other factors that constitute a so-called curb-appeal or the buyer's impression of the house. It is important to consider those factors in the estimation so as to match the human emotions and social norms. 
When agents assess a property, the first thing they typically do is study the home from an overhead, satellite view on Google. They note whether it backs up to a busy street, the proximity to commercial property or freeways, the size of other homes nearby, the vegetation and landscaping, its orientation to the sun and, if available, will view any photos of the exterior plus a street scene. A home with granite countertops and stainless steel appliances compared to a similar home with a Formica kitchen definitely commands a higher value. Similarly, a home that has been renovated should be estimated more than its next-door similar neighbor which is a decade or two out of date.
The companies like Zillow have been using such data extracted from home photos and satellite images of the neighborhood for some time. Armed with a large amount of data collected over a period of time, Zillow claims that its Zestimate is 15 percent more accurate when it incorporates machine learning to simulate human judgment.
Till recently, companies like Zillow had an advantage of a pool of data collected over many years from homes all over the US, based on which they have fine-tuned their machine learning models. With the availability of computer vision APIs for object detection from Microsoft, Google, and Amazon, and Foxy it is now possible for any company providing real-estate services, while starting from scratch, to make use of unstructured data in their estimation.
We tried Amazon, Google and Microsoft's Object Detection APIs on a suite of home photos. We wanted to find out the accuracy of these APIs with built-in generic object detection models and whether they can be used to augment home estimations. Please see the end of the article on details of objects detected using each of these APIs with the built-in model on a variety of home photos.

## Observations

- Amazon provides the most accurate results followed by Google and Microsoft.

- Microsoft detects only a single object and has poor accuracy as compared to the other two.

- Amazon returns multiple labels related to specific objects as well as its ancestors.

- For some photos, Google returned specific labels such as "hacienda" for "Spanish Estate" showing it might have a wider variety of photos from different countries.

- Foxy AI takes an approach to classify objects in known categories related to real-estate like Closet, Laundry etc. It is not clear if their model has any higher accuracy than the generic object models of other three companies.

- None of the results show adjectives like "Wooden floor" or "Granite countertop" etc. with default models which may limit their use in estimation.

## Improving detection 

- Images may not always be clear and sharp. It will be interesting to see how accurately objects in cluttered, out-of-focus or low-light images are detected.

- Amazon APIs can return the bounding box for common object labels such as people, cars, furniture, apparel or pets. Bounding boxes can be used to find the exact locations of objects in an image, count instances of detected objects, or to measure an object's size using bounding box dimensions. It would be interesting to see if we can detect additional characteristics of an object by feeding in zoomed in part of the image of the individual object. For real-estate photos, the useful adjectives to detect are - bright and spacious, marble, granite countertop, teak furniture, new refrigerator, wooden floor, Flaming birch cabinets, antique furniture, leather sofa, high ceiling, long, steep driveway, manicured garden, walk-in closet, long hallway, clean carpet.

 - Amazon API allows the use of parent labels to build groups of related labels and then querying of similar labels in one or more images. This can be used to compare bedroom photos of multiple homes and query objects within that room to compare.

- Microsoft provides the idea of scoped analysis where you can specify the model's name to get information relevant to that model. Currently, only Celebrities and Landmarks models are supported. But all the companies may eventually add real-estate as one of the categories or domains which may significantly improve the detection accuracy.

- Home styles, interiors change based on location and culture. Considering such aspects while detecting objects can improve detection accuracy.
A targeted machine learning model trained only on the photos of interior and exteriors of houses vs. generic model for any object detection can work well. There are companies like Foxy AI who take this approach. Foxy provides API endpoints specifically to detect objects in home pictures and also provide price predictions based on the input parameters.

- Google's AutoML Vision makes it possible for developers with limited machine learning expertise to train high-quality custom models. After uploading and labeling images, AutoML Vision trains a model that can scale as needed to adapt to demands. Such custom, production-ready models are better suited for our use case.

- Making a generic AI product that is genuinely useful to the custom scenario is very hard. A custom model development based on data collected from real users is always preferable to the exercise of fitting a square peg in a round hole. 

- Teaching a computer to appreciate curb appeal and the buyer's feel of the home is truly artificial intelligence. Using generic object detection APIs with built-in models can be a good start for the companies who do not have any data. As they gather data over time, a custom model built using local home photos can work well to extract additional home features. These along with structured variables like square footage can help hone in on more accurate estimations. In any case, we are far from eliminating expert real-estate agent's visit for a true valuation of real-estate.

## Object Detection Results on home photos

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-04-using-object-detection-for-improving-price-estimation-1" alt="Home"/>
  <figcaption>Reference: https://i.imgur.com/7Jk4R8h.jpg</figcaption>
</figure>

### Microsoft

```{
"categories":[{"name":"outdoor_pool","score":0.95703125}],
"requestId":"7462e05d-5cc3–4273-a6d6-e78edc916d34",
"metadata":{"width":2048,"height":1365,"format":"Jpeg"}
}
```

### Google

```
estate : 0.9384693503379822
property : 0.9383976459503174
mansion : 0.9083089828491211
villa : 0.8863233923912048
real estate : 0.8205443620681763
home : 0.8012939095497131
hacienda : 0.7106115221977234
building : 0.7076689004898071
sky : 0.6754202842712402
swimming pool : 0.6674705147743225
```

### Amazon

```Building : 97.64356231689453
Mansion : 93.88848876953125
House : 93.88848876953125
Housing : 93.88848876953125
Path : 93.61183166503906
Walkway : 93.61183166503906
Resort : 93.21076202392578
Hotel : 93.21076202392578
Flagstone : 91.89410400390625
Villa : 86.66985321044922
Water : 69.26892852783203
Pool : 69.26892852783203
Architecture : 61.82177734375
Sidewalk : 57.70322799682617
Pavement : 57.70322799682617
```
