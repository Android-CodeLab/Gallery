# Jamun-Gallery

Gallery have splendid UI Components with Single and Multi files Selection Mode for android Developers to give there app a A Rich look With with custom picker functionality to cover up maximum media type like Audio, Files (Docs, Text etc) and Images.

### What's New? (0.0.1)
* Stable **Official Version** for Developers and Live Apps.
* Easy Calling Mechanism with **Instant reply** via onActivityResult.
* Need less calls with many customs Tags in Intent Object to reach maximum developer satisfaction.
* Compatible With **[Camera](https://github.com/Lib-Jamun/camera.git)** Library for More Efficent Working;

### Why this library?

* This library Competible with all screen sizes and device (Tab with 7' inches and 10'inches).
* Library support both orientation that is portrait and landscape.
* Its Calling feature is very simple and easy to use.
* You don't need to add Multiple libraries and UI components, it have such Components inside that make Quality.
* Library is Customizable for **Enable Features like Only Audio, Only Files, and Only Images view**.

### Quality Measures? for (0.0.1)

The following apps are using this library without facing any kind of Bugs.

* **[SimplyBlood](https://play.google.com/store/apps/details?id=com.simplyblood)**

------

### Jamun-Gallery Preview

Activity View | Bottom Sheet View
---- | ----
![jamun_gallery_activity](https://user-images.githubusercontent.com/38988514/41310002-d9e0a5a4-6e9d-11e8-8d45-f8db58746b9d.png) | ![jamun_gallery_bottom](https://user-images.githubusercontent.com/38988514/41310006-dc0b4884-6e9d-11e8-9cd2-dd79e428a1a8.png)

Working Preview 
---- 
![gallery](https://user-images.githubusercontent.com/38988514/40283105-bb5783e6-5c96-11e8-993c-075c71f93955.gif) 

### Gradle Configuration

**Add the dependency**

Step 1\. Add the jCenter repository to your build file. Add it in your root build.gradle at the end of repositories:

```java
allprojects {
  repositories {
        mavenCentral()
  }
}
```

Step 2\. Add the dependency

```java
dependencies {
     compile 'tk.jamun.ui:gallery:0.0.1'
}
```

### Maven Config

```xml
<dependency>
  <groupId>tk.jamun.ui</groupId>
  <artifactId>gallery</artifactId>
  <version>0.0.1</version>
  <type>aar</type>
</dependency>
```
------

### How to Implement

Once the project has been added to gradle, You can use these lines of code to configure pickers....

### Activity View

##### Step 1. Define Intent Object

Simple Object declaration :

```
**Single**
Intent intent = new Intent(this, ActivityGallery.class)
                        .putExtra(GALLERY_INTENT_COME_FOR, GALLERY_TYPE_IMAGE)// Means Gallery type either IMAGE, AUDIO, FILES and all
                        .putExtra(GALLERY_INTENT_MODE, GALLERY_MODE_SINGLE);// Means Gallery Mode GALLERY_MODE_SINGLE or MODE_MULIT

**Multi**
//or For All-In-One

Intent intent =new Intent(this, ActivityGallery.class)
                        .putExtra(GALLERY_INTENT_COME_FOR, GALLERY_TYPE_ALL)
                        .putExtra(GALLERY_INTENT_MODE, GALLERY_MODE_MULTI);// Means Gallery Mode GALLERY_MODE_SINGLE or MODE_MULIT
```

#### Step 2. Start Module By Calling

This method is very common to Android Developer, Very easy calling way to Start an activity help you same for calling this Picker :

```
startActivityForResult(intent, ACTION_REQUEST_GALLERY);

```

#### Step 3. Get Result from Picker

```
 @Override
    public void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (resultCode == RESULT_OK) {
            switch (requestCode) {
                case ACTION_REQUEST_GALLERY:
                    if (data.getIntExtra(GALLERY_INTENT_MODE, GALLERY_MODE_SINGLE) == GALLERY_MODE_SINGLE) {
                        ModelChild modelChild = data.getParcelableExtra(GALLERY_INTENT_FOR_MODEL);
                        if (modelChild != null)
                            try {
                            file = new File(modelChild.getFilePath());
                                startActivityForResult(new Intent(ActivityCameraGallery.this, ActivityCamera.class)
                                                .putExtra(InterfaceUtils.INTENT_COME_FROM, LIBRARY_COME_FROM_GALLERY)
                                                .putExtra(RESULT_IMAGE_PATH, file.getAbsolutePath()),
                                        ACTION_REQUEST_CAMERA);
                            } catch (Exception ignored) {
                            }
                    } else {
                        ArrayList<ModelChild> childArrayList = data.getParcelableArrayListExtra(GALLERY_INTENT_FOR_MODEL);
                        for (ModelChild modelChild : childArrayList) {
                             file = new File(modelChild.getFilePath());
                        }
                    }
                    break;
            }
        }
    }

```
### Bottom Sheet View

##### Step 1. Define Intent Object

Object Declaration and Binding Response Listener:

```
**Single**
 new PickerMulti().setThings(this, getSupportFragmentManager(), GALLERY_TYPE_IMAGE,
                GALLERY_MODE_SINGLE).onClickListener(new InterfaceGallery.InterfaceSingleModeItemClickListener() {
            @Override
            public void getResponse(ModelChild modelChild) {

            }
        }).setColumnCount(4).showPicker();
        
**Multi**
//or For All-In-One

 new PickerMulti().setThings(this, getSupportFragmentManager(), GALLERY_TYPE_ALL,
                GALLERY_MODE_MULTI).onSubmitClickListener(new InterfaceGallery.InterfaceMultiModeItemClickListener() {
            @Override
            public void getResponse(ArrayList<ModelChild> selectedArrayList) {

            }
        }).showPicker();
```

### Gallery Customize 

Intent Object provide you custom functionality to work Module according to your requirement :

#### Set Title of the Gallery

```
**Activity View**
intent.putExtra(INTENT_SCANNER_ACTIVITY_NAME, "Title of the Scanner Activity");

or 

**Bottom Sheet View**
new PickerMulti().setTitle();
```

#### Set Column Count of the Gallery

```
**Activity View**
intent.putExtra(GALLERY_INTENT_COLUMN_COUNT, COUNT);

or 

**Bottom Sheet View**
new PickerMulti().setColumnCount();
```

------

# Dependency

* Goole Vision ``v15.0.2``
* SDK Version ``15 to 27``

## Credits

Desgin & Developed by : **[Jatin Sahgal](https://www.linkedin.com/in/jatinsahgal/)**
 (**[Linkedin](https://www.linkedin.com/in/jatinsahgal/)** & **[Website](https://blog.jamun.tk)**) 

## More Library under Jamun 

* **[Pickers](https://github.com/Lib-Jamun/Pickers.git)**
Pickers Library provide you a set of Pickers like Country, Language, Share and Intent Chooser.

* **[Country-Pickers](https://github.com/Lib-Jamun/Pickers.git)**
allow you to access Country picking functionality with great UI/UX design, and there are numberous of function which help you to modify picker as per your requirements. Library has been provided with four custom UI initate mode you can decide how the view of picker can be initate. You can also decide weather picker inheriate Single or Multi Selection property. Library consists of updated collection of country name, code and there flags. We are using APIs base structure to avoid increase in the size of apk due to flag Images. This module Maintain the database so that you don't need to call APIs again and again rather than you can choose when to refresh the Database and fetch new real time data.

* **[Language-Pickers](https://github.com/Lib-Jamun/Pickers.git)**
provides you read-made Language picker  which is easy to use and comes with great UI/UX, and there are numberous of function which help you to modify picker as per your requirements. Library has been provided with four custom UI initate mode you can decide how the view of picker can be initate. You can also decide weather picker inheriate Single or Multi Selection property.

* **[Calendar](https://github.com/Lib-Jamun/calendar.git)**
is a collection of Beautiful Activities which help others to make there Fully Custom Calendar View with Single and Multi Date Picker Functionality.

* **[Scanner](https://github.com/Lib-Jamun/scanner.git)**
is a collection of Beautiful Activity which help others to make there own Custom QR/Barcode Scanner. 

* **[Volley](https://github.com/Lib-Jamun/Volley.git)**
Library is a set of Custom Classes with UI components for network programming, integration and transaction handling in a better and standard way. This will help developers for making quality use of volley library. 

* **[UI](https://github.com/Lib-Jamun/ui.git)**
library is a set of UI Views, Custom Component and Collection of Helper Classes which help Developer for making quality Product. Such as Camera, Gallery, Number of Pickers, Calendar, Date Pickers, Dialogs and many more Heler UI and Backend Component.

* **[Camera](https://github.com/Lib-Jamun/ui.git)**
library provide you Custom Complete Camera view with full features like Flash, Rotation, Gallery Picker, Focus, Tap to capture, Confirmation window and last but not least croping feature. It also provide you file path in return so that developer can feel a friendly handy way to Deal After. 

* **[Gallery](https://github.com/Lib-Jamun/ui.git)**
have some Beautiful UI Components and Multi files Mode for android Developers to give there app a A Rich look With single and Multi picker Functionality.

* **[Elements](https://github.com/Lib-Jamun/elements.git)**
Library provide you a custom set of Android Elements that have custom views and properties like CircularImageView or CircularNetworkImageView and many more.

* **[Browser](https://github.com/Lib-Jamun/Browser.git)**
Library provide you two type Single Pager and Multi Pager In-APP Browser Functionality with Event Handling and Functions to Customize Views. It also provide you Copy to clipboard, Open in Browser and share link feature in-Bulit.

## License
    Copyright (c) 2018 Jatin Sahgal

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
  
  
