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
  <img src="{{site.baseurl}}/assets/images/2019-02-04-using-object-detection-for-improving-price-estimation-1.jpeg" alt="Home"/>
  <figcaption>Reference: https://i.imgur.com/7Jk4R8h.jpg</figcaption>
</figure>

### Microsoft

```json
"categories":[{"name":"outdoor_pool","score":0.95703125}],
"requestId":"7462e05d-5cc3–4273-a6d6-e78edc916d34",
"metadata":{"width":2048,"height":1365,"format":"Jpeg"}
```

### Google

```json
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

```json
Building : 97.64356231689453
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

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-04-using-object-detection-for-improving-price-estimation-2.jpeg" alt="Home"/>
  <figcaption>Reference: https://i.imgur.com/Eic3Xam.jpg</figcaption>
</figure>

### Microsoft

```json
"categories":[{"name":"abstract_","score":0.01171875},{"name":"others_","score":0.01171875}],"requestId":"a7add036–54d5–4421-ab4c-889535161445","metadata":{"width":1905,"height":2000,"format":"Jpeg"}
```

### Google

```json
interior design : 0.7810790538787842
home : 0.6999193429946899
window : 0.6992332339286804
outdoor structure : 0.5407284498214722
furniture : 0.5291412472724915
```

### Amazon

```json
Flooring : 99.99893951416016
Floor : 99.8294448852539
Indoors : 94.28851318359375
Interior Design : 94.28851318359375
Plant : 89.50586700439453
Living Room : 85.67030334472656
Room : 85.67030334472656
Furniture : 83.99723052978516
Couch : 83.99723052978516
Hardwood : 82.8748550415039
Wood : 82.8748550415039
Jar : 78.75053405761719
Pottery : 78.75053405761719
Vase : 78.75053405761719
Blossom : 77.35748291015625
Flower Arrangement : 77.35748291015625
Flower : 77.35748291015625
Potted Plant : 76.62191009521484
Flower Bouquet : 72.43888854980469
Flagstone : 58.75558090209961
Door : 58.61599349975586
Corridor : 55.91652297973633
```

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-04-using-object-detection-for-improving-price-estimation-3.jpeg" alt="Home"/>
  <figcaption>Reference: https://i.imgur.com/6aGAOOp.jpg</figcaption>
</figure>

### Microsoft

```json
"categories":[{"name":"abstract_","score":0.01953125},{"name":"others_","score":0.00390625},{"name":"outdoor_","score":0.00390625}],"requestId":"0f4b81a5-b38f-47b0–93fa-61d93186a5bb","metadata":{"width":2048,"height":912,"format":"Jpeg"}
```

### Google

```json
property : 0.8942150473594666
countertop : 0.8445141911506653
kitchen : 0.8333971500396729
estate : 0.7475240230560303
interior design : 0.7038251161575317
real estate : 0.7007927894592285
cuisine classique : 0.6698155999183655
ceiling : 0.5234758257865906
```

### Amazon

```json
Indoors : 99.1664047241211
Room : 99.1664047241211
Kitchen : 94.69178009033203
Interior Design : 93.49835205078125
Flooring : 89.98771667480469
Wood : 85.61946868896484
Lamp : 83.11481475830078
Chandelier : 83.11481475830078
Kitchen Island : 81.20708465576172
Hardwood : 77.21861267089844
Furniture : 59.81884002685547
Floor : 58.4579963684082
```
<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-04-using-object-detection-for-improving-price-estimation-4.jpeg" alt="Home"/>
  <figcaption>Reference: https://i.imgur.com/2CQ2EyM.jpg</figcaption>
</figure>

### Microsoft

```json
"categories":[{"name":"abstract_","score":0.02734375},{"name":"building_pillar","score":0.3515625}],"requestId":"5e1faa3e-ac73–4a65-aaaf-84ec3d8547cd","metadata":{"width":2048,"height":944,"format":"Jpeg"}
```

### Google

```json
property : 0.8988840579986572
room : 0.8776835799217224
interior design : 0.7127363085746765
real estate : 0.6541785597801208
living room : 0.6493942141532898
estate : 0.6164873838424683
floor : 0.5910876989364624
ceiling : 0.5784943699836731
flooring : 0.5770671367645264
house : 0.5629818439483643
```

### Amazon

```json
Flooring : 99.9969482421875
Floor : 99.98954010009766
Wood : 98.96363830566406
Interior Design : 97.80683135986328
Indoors : 97.80683135986328
Hardwood : 92.8141098022461
Room : 82.762939453125
Living Room : 80.249267578125
Plywood : 72.39012145996094
Furniture : 69.56649780273438
Bedroom : 68.93217468261719
Bed : 61.190338134765625
Rug : 60.942543029785156
```
<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-04-using-object-detection-for-improving-price-estimation-5.jpeg" alt="Home"/>
  <figcaption>Reference: https://i.imgur.com/LGKVfzx.jpg</figcaption>
</figure>

### Microsoft

```json
"categories":[{"name":"indoor_room","score":0.93359375}],"requestId":"59e8b484–652a-4d78–90f6-d9fb4274c33f","metadata":{"width":2000,"height":2000,"format":"Jpeg"}
```

### Google

```json
room : 0.916010856628418
bathroom : 0.8526955842971802
interior design : 0.8033964037895203
floor : 0.8008365035057068
wall : 0.7690424919128418
flooring : 0.7259812951087952
home : 0.725638210773468
ceiling : 0.701020359992981
estate : 0.6925469040870667
real estate : 0.657813549041748
```

### Amazon

```json
Flooring : 99.98371887207031
Floor : 99.88095092773438
Furniture : 98.47281646728516
Couch : 88.17687225341797
Indoors : 87.85083770751953
Interior Design : 87.85083770751953
Living Room : 78.22207641601562
Room : 78.22207641601562
Wood : 71.65221405029297
Tub : 68.77200317382812
Hardwood : 62.696842193603516
Flagstone : 58.15713119506836
```
<figure>
  <img src="{{site.baseurl}}/assets/images/2019-02-04-using-object-detection-for-improving-price-estimation-6.jpeg" alt="Home"/>
  <figcaption>Reference: https://i.imgur.com/6PnuY0Q.jpg</figcaption>
</figure>

### Microsoft

```json
"categories":[{"name":"outdoor_","score":0.01171875},{"name":"outdoor_street","score":0.55078125}],"requestId":"88a759da-2b1c-43f9–9fec-c8cb07cb9fde","metadata":{"width":1769,"height":2000,"format":"Jpeg"}

### Google

```json
property : 0.9011626243591309
walkway : 0.7674194574356079
home : 0.7527650594711304
real estate : 0.7386894822120667
arecales : 0.7260463237762451
palm tree : 0.6820899248123169
estate : 0.6767517924308777
outdoor structure : 0.6750420928001404
villa : 0.6429499387741089
house : 0.6065300107002258
```

### Amazon

```json
Flagstone : 99.65138244628906
Tree : 95.78475952148438
Plant : 95.78475952148438
Patio : 91.34025573730469
Walkway : 90.66641235351562
Path : 90.66641235351562
Arecaceae : 88.72791290283203
Palm Tree : 88.72791290283203
Outdoors : 79.1570816040039
Sidewalk : 78.15443420410156
Pavement : 78.15443420410156
Human : 77.41170501708984
Person : 77.41170501708984
Building : 76.29102325439453
Banister : 74.00752258300781
Handrail : 74.00752258300781
Summer : 70.18952178955078
Hotel : 63.83850860595703
Arbour : 59.08328628540039
Garden : 59.08328628540039
Home Decor : 57.40121078491211
Pot : 56.944217681884766
```
