[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![CircleCI](https://circleci.com/gh/SodaLabs/android-looping-pager-layoutmanager.svg?style=svg)](https://circleci.com/gh/SodaLabs/android-looping-pager-layoutmanager) [![](https://jitpack.io/v/sodalabs/android-looping-pager-layoutmanager.svg)](https://jitpack.io/#sodalabs/android-looping-pager-layoutmanager)

A `RecyclerView.LayoutManager` library enabling you the looping pager layout (could swipe left or right) and supports AndroidX. It's pluggable and very lightweight unlike many other alternatives customizing a ViewPager/RecyclerView subclass.

Also, you don't need to do the funny trick in the *Adapter* layer for the ViewPager. It's just a matter of time for you to overflow the item pool. Moreover, you couldn't do swipe-left with the trick in the *Adapter* layer cause negative index is not allowed.

<p align="center">
  <img src="docs/demo.gif" width="240">
</p>

# Integration

### Gradle

#### Step 1

Add Jitpack to the dependency repositories:

```
// In root build.gradle
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
     }
}
```

#### Step 2

Add dependency to your project:

[![](https://jitpack.io/v/sodalabs/android-looping-pager-layoutmanager.svg)](https://jitpack.io/#sodalabs/android-looping-pager-layoutmanager)

```
// In application/library module's build.gradle
dependencies {
    implementation 'com.github.sodalabs:android-looping-pager-layoutmanager:v?.?.?' // Note prefix "v" is necessary!
}
```

#### Step 3

The library is very lightweight and provides:

* A custom LayoutManager, [LoopingPagerLayoutManager.kt](pager/src/main/java/co/sodalabs/pager/LoopingPagerLayoutManager.kt), which smartly knows where to place the item views so that you don't need to do the trick in the *Adapter* layer.
* A snap helper, [PagerSnapHelper.kt](pager/src/main/java/co/sodalabs/pager/PagerSnapHelper.kt), which follows the pluggable interface of RecyclerView and provides the snap scroll.

Above are the only two classes you need to add to your code. e.g.


```kotlin
recyclerView.setHasFixedSize(true) // Currently necessary for programmatic smooth scroll
recyclerView.layoutManager = LoopingPagerLayoutManager() // One line to enable infinite looping.
recyclerView.adapter = ...

// Enable the snap on fling through the plugable interface.
// Use co.sodalabs.PagerSnapHelper not the one under AndroidX namespace!
val snapHelper = PagerSnapHelper(resources.displayMetrics.density, 500)
snapHelper.attachToRecyclerView(recyclerView)
```

> Note: Currently, `setHasFixedSize(true)` is very necessary otherwise the library won't layout the item views correctly.

# Code Owners

* @boyw165
* @xuhaibahmad
* @kevinmmarlow
