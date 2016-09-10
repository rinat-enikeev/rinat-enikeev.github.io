---
layout: post
published: true
title: iOS App Architecture. VIPER with Layers. Version 1. 
description: Places around me. 
headline: 
modified: ""
categories: 
  - engineering
  - architecture
  - ios
  - viper
tags: "architecture,iOS,SOLID,Layers,VIPER"
imagefeature: ""
mathjax: false
featured: true
comments: true
---

The app shows different kind of places around me. 
 
## Missing

- Logging 
- Error handling
- File headers 
- Comments
- Typhoon assemblies initialization without Info.plist. 
- Nullability 

## Requirements

Scope
- Kind of places: restaurants or barbershops
 
Functional
- user must be able to see all nearby restaurants or barbershops
- user must be able to open restaurant or barbershops details

Non-functional:
- adding more source geo api's must take less than a day of work
- adding another kind of place should take less than a day 
- replacing the view from table to map should take less than an hour

## Project setup

1. Create "Single View Application" using XCode. Include tests. 

2. Add .gitignore
 
3. Add Podfile and run 'pod install' using terminal in the project directory.  

'''ruby
platform :ios, '8.0'

target ‘VIPERLayers’ do
  pod 'Typhoon'
  pod 'MagicalRecord'
  pod 'ViperMcFlurry'
end
'''

4. Open .xcworkspace file. 

5. Remove AppDelegate, ViewController and Main.storyboard files. 

6. Copy VIPERLayers folders (Classes, Resources, Supporting files) to your app target folder.
 
7. Move LaunchScreen.storyboard to Classes/PresentationLayer folder. 

8. Move Assets.xcassets to Resources/Images folder. 

9. Move Info.plist and main.m to 'Supporting files' folder. 

10. Remove all moved files from your app target folder.
  
11. Add files to project and select three folder (Classes, Resources, Supporting files). Include to all targets in 
options. 
  
12. Tap on project and select Info.plist file. 

13. Open 'Supporting files'/Info.plist. 
Add row with key TyphoonInitialAssemblies and array type. 
Add rows (string type) to the array: 
ApplicationAssembly
StoryboardAssembly
ServicesAssembly
DataFacadeAssembly
APIAssembly
PersistenceAssembly

Remove Info.plist from copy bundle resources phase if needed.

Great! You are ready to create a first screen. 

## Data Model

First of all, let's determine the source of our data. 
It is not our user generated content, and not from our api. 

Let's check what kind of model objects we can receive from obvious APIs: 

Yelp:
'''json
{
    "businesses": [
        {
            "categories": [
                [
                    "Local Flavor",
                    "localflavor"
                ],
                [
                    "Mass Media",
                    "massmedia"
                ]
            ],
            "display_phone": "+1-415-908-3801",
            "id": "yelp-san-francisco",
            "image_url": "http://s3-media3.fl.yelpcdn.com/bphoto/nQK-6_vZMt5n88zsAS94ew/ms.jpg",
            "is_claimed": true,
            "is_closed": false,
            "location": {
                "address": [
                    "140 New Montgomery St"
                ],
                "city": "San Francisco",
                "coordinate": {
                    "latitude": 37.7867703362929,
                    "longitude": -122.399958372115
                },
                "country_code": "US",
                "cross_streets": "Natoma St & Minna St",
                "display_address": [
                    "140 New Montgomery St",
                    "Financial District",
                    "San Francisco, CA 94105"
                ],
                "geo_accuracy": 9.5,
                "neighborhoods": [
                    "Financial District",
                    "SoMa"
                ],
                "postal_code": "94105",
                "state_code": "CA"
            },
            "mobile_url": "http://m.yelp.com/biz/yelp-san-francisco",
            "name": "Yelp",
            "phone": "4159083801",
            "rating": 2.5,
            "rating_img_url": "http://s3-media4.fl.yelpcdn.com/assets/2/www/img/c7fb9aff59f9/ico/stars/v1/stars_2_half.png",
            "rating_img_url_large": "http://s3-media2.fl.yelpcdn.com/assets/2/www/img/d63e3add9901/ico/stars/v1/stars_large_2_half.png",
            "rating_img_url_small": "http://s3-media4.fl.yelpcdn.com/assets/2/www/img/8e8633e5f8f0/ico/stars/v1/stars_small_2_half.png",
            "review_count": 7140,
            "snippet_image_url": "http://s3-media4.fl.yelpcdn.com/photo/YcjPScwVxF05kj6zt10Fxw/ms.jpg",
            "snippet_text": "What would I do without Yelp?\n\nI wouldn't be HALF the foodie I've become it weren't for this business.    \n\nYelp makes it virtually effortless to discover new...",
            "url": "http://www.yelp.com/biz/yelp-san-francisco"
        }
    ],
    "total": 2316
}
'''
Foursquare
https://developer.foursquare.com/docs/responses/venue

So lets define Model: 

'''objc
@protocol GeoObject <NSObject>

@property (strong, nonatomic) NSString* geoObjectID;
@property (strong, nonatomic) NSString* name;
@property (strong, nonatomic) NSNumber* latitude;
@property (strong, nonatomic) NSNumber* longitude;

@end
'''