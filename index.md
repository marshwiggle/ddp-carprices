Predicting Car Prices in Russia 
========================================================
author: Simeon Evlakhov 
date: 12-10-2017
autosize: true

Objectives
========================================================

I build a model that predicts car prices in Moscow Region,
Russia as of August 2017.

The data are "real". They are taken from a website, that
distributes autos, and parsed into the dataframe named
*carsTbl*.

carsTbl Structure
========================================================




```r
dim(carsTbl)
```

```
[1] 8969   13
```


```r
names(carsTbl)
```

```
 [1] "X.num"     "brand"     "model"     "disp"      "trans"    
 [6] "hp"        "bodyType"  "fuelType"  "driveType" "year"     
[11] "mileage"   "price"     "city"     
```

Predictors
========================================================

These are characteristics that we use as predictors
- Brand 
- Milage
- Year of Issue
- Horse Powers
- Displacement
- Transmission Type
- Drive Type
- Fuel Type



Model
========================================================

We use General Linear Model for prediction:


```r
model <- glm(price ~  brand + mileage + year + hp + disp + trans + driveType + fuelType, family = poisson(), data = carsTbl) 
str(model$coefficients)
```

```
 Named num [1:44] -178.52 -0.356 -0.242 -0.571 -0.363 ...
 - attr(*, "names")= chr [1:44] "(Intercept)" "brandBMW" "brandCadillac" "brandChevrolet" ...
```

Example
========================================================

Let's see an example. Here "полный" means 4-wheel drive.


```r
prediction <- predict(model, data.frame(brand="Audi", mileage = 177000, year = 2007, hp = 350,disp=4.16, trans="AT", driveType="полный", fuelType = "petrol"))
```
The estimated price (in Russian Roubles) is:

```r
  price <- exp(prediction)
  price
```

```
      1 
1351812 
```
So, the auto with the given characteristics costs about
1 352 000 Rub.

The end
========================================================

Thank you for your attention!

P.S. There is only 5 slides in this work! (Titlepage and
this page should not be considered as content.)
