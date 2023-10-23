# PhotoEditor

![Github Action](https://github.com/burhanrashid52/PhotoEditor/actions/workflows/app_build_and_test.yml/badge.svg)
[![Downloads](https://img.shields.io/badge/Download-3.0.1-blue.svg)](https://search.maven.org/artifact/com.burhanrashid52/photoeditor/3.0.1/aar) ![API](https://img.shields.io/badge/API-21%2B-brightgreen.svg) [![JavaDoc](https://img.shields.io/badge/JavaDoc-PhotoEditor-blue.svg)](https://burhanrashid52.github.io/PhotoEditor/) [![Uplabs](https://img.shields.io/badge/Uplabs-PhotoEditor-orange.svg)](https://www.uplabs.com/posts/photoeditor)
[![AndroidArsenal](https://img.shields.io/badge/Android%20Arsenal-PhotoEditor-blue.svg)](https://android-arsenal.com/details/1/6736)
[![AndroidDevDigest](https://img.shields.io/badge/AndroidDev%20Digest-%23185-brightgreen.svg)](https://www.androiddevdigest.com/digest-185)
[![AwesomeAndroid](https://img.shields.io/badge/Awesome%20Android-%2397-red.svg)](https://android.libhunt.com/newsletter/97)
[![AndroidWeekly](https://img.shields.io/badge/Android%20Weekly-%23312-blue.svg)](http://androidweekly.net/issues/issue-312)
[![Mindorks](https://img.shields.io/badge/Mindorks%20Newsletter-%234-ff69b4.svg)](https://mindorks.com/newsletter/edition/4)


A Photo Editor library with simple, easy support for image editing using Paints, Text, Filters, Emoji and Sticker like stories.

[Download link](https://drive.google.com/drive/folders/1pw_iZ_PIyOSJzCWR_uLnoe7PKCDTgosp?usp=sharing)

![](https://i.imgur.com/ZYtLHTZ.png)

<a href="https://www.producthunt.com/posts/photoeditor-2?utm_source=badge-featured&utm_medium=badge&utm_souce=badge-photoeditor-2" target="_blank"><img src="https://api.producthunt.com/widgets/embed-image/v1/featured.svg?post_id=297508&theme=light" alt="PhotoEditor - Android SDK with simple, easy support for image editing. | Product Hunt" style="width: 250px; height: 54px;" width="250" height="54" /></a>

<a href="https://www.buymeacoffee.com/burhanrashid52" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>

## Features

- [**Drawing**](#drawing) on image with option to change its Brush's Color, Size, Opacity, Erasing and basic shapes.
- Apply [**Filter Effect**](#filter-effect) on image using MediaEffect
- Adding/Editing [**Text**](#text) with option to change its Color with Custom Fonts.
- Adding [**Emoji**](#emoji) with Custom Emoji Fonts.
- Adding [**Images/Stickers**](#adding-imagesstickers)
- Pinch to Scale and Rotate views.
- [**Undo and Redo**](#undo-and-redo) for Brush and Views.
- [**Deleting**](#deleting) Views
- [**Saving**](#saving) Photo after editing.
- More [**FAQ**](#faq).
- [Lesson Learned from building successful android library PhotoEditor: Droidcon Berlin 2021](#lesson-learned-from-building-successful-android-library-photoeditor-droidcon-berlin-2021)



## Benefits
- Hassle free coding
- Increase efficiency
- Easy image editing

## Getting Started
To start with this, we need to simply add the dependencies from `mavenCentral()` in the gradle file of our app module like this
```groovy
implementation 'com.burhanrashid52:photoeditor:3.0.1'
```
or we can also import the :photoeditor module from sample for further customization

## Migrations
### AndroidX
PhotoEditor [v.1.0.0](https://github.com/burhanrashid52/PhotoEditor/releases/tag/v.1.0.0) is a migration to androidX and dropping the support of older support library. There are no API changes. If you find any issue migrating to v.1.0.0 , please follow this [Guide](https://developer.android.com/jetpack/androidx/migrate). If you still facing the issue than you can always rollback to [v.0.4.0](https://github.com/burhanrashid52/PhotoEditor/releases/tag/v.0.4.0). Any fix in PR are Welcome :)

### Kotlin
PhotoEditor [v.2.0.0](https://github.com/burhanrashid52/PhotoEditor/releases/tag/v.2.0.0) is fully migrated to Kotlin. You can use [v.1.5.1](https://github.com/burhanrashid52/PhotoEditor/releases/tag/v.1.5.1) for the Java version. There are no breaking API changes in these two versions.

## Setting up the View
First we need to add `PhotoEditorView` in our xml layout

```xml
 <ja.burhanrashid52.photoeditor.PhotoEditorView
        android:id="@+id/photoEditorView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:photo_src="@drawable/got_s" />
  
```
We can define our drawable or color resource directly using `app:photo_src`

We can set the image programmatically by getting source from `PhotoEditorView` which will return a `ImageView` so that we can load image from resources,file or (Picasso/Glide)
```java
PhotoEditorView mPhotoEditorView = findViewById(R.id.photoEditorView);

mPhotoEditorView.getSource().setImageResource(R.drawable.got);
```

## Building a PhotoEditor
To use the image editing feature we need to build a PhotoEditor which requires a Context and PhotoEditorView which we have to setup in our xml layout


```java
//Use custom font using latest support library
Typeface mTextRobotoTf = ResourcesCompat.getFont(this, R.font.roboto_medium);

//loading font from asset
Typeface mEmojiTypeFace = Typeface.createFromAsset(getAssets(), "emojione-android.ttf");

mPhotoEditor = new PhotoEditor.Builder(this, mPhotoEditorView)
         .setPinchTextScalable(true)
         .setClipSourceImage(true)
         .setDefaultTextTypeface(mTextRobotoTf)
         .setDefaultEmojiTypeface(mEmojiTypeFace)
         .build();
 ```
We can customize the properties in the PhotoEditor as per our requirement

| Property  | Usage |
| ------------- | ------------- |
| `setPinchTextScalable()`  | set false to disable pinch to zoom on text insertion. Default: true. |
| `setClipSourceImage()` | set true to clip the drawing brush to the source image. Default: false. |
| `setDefaultTextTypeface()`  | set default text font to be added on image  |
| `setDefaultEmojiTypeface()`  | set default font specifc to add emojis |

That's it we are done with setting up our library


FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
 
