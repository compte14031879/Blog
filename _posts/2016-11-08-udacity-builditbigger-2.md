---
layout: post
title: "Build It Bigger - 2/2"
sub_title: "Product flavors, Interstitial Ad, Optimized loading and Custom Gradle test task (A project of Udacity Android Developer Nanodegree Program)"
excerpt_separator: "<!--more-->"
categories:
  - articles
tags:
  - developpement
  - android
  - udacity
header:
  teaser: images/udacity-builditbigger/002-th.jpg
---

## Add free and paid product flavors [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/f6daa7fedc40130d2edf137dfda4658e1cb49f4b?diff=split)

Create two productFlavors:

<div class="import_code"><div class="path_code">
app/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/f6daa7fedc40130d2edf137dfda4658e1cb49f4b/app/build.gradle
?slice=
16:24
&footer=0"></script></div>

<!--more-->

---

Ads are only for the free version. Replace this:

<div class="import_code"><div class="path_code">
app/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/e9e8d57c8782da3837be46e20fdaca6347a19b3d/app/build.gradle
?slice=
28
&footer=0"></script></div>

by this:

<div class="import_code"><div class="path_code">
app/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/f6daa7fedc40130d2edf137dfda4658e1cb49f4b/app/build.gradle
?slice=
36
&footer=0"></script></div>

---

Create a specific AndroidManifest for free productFlavor. Copy-Paste:

> Source: app/src/main/AndroidManifest.xml

> Target: app/src/free/AndroidManifest.xml

---

Create a specific MainActivityFragment.java for free productFlavor. Move:

> From: app/src/main/java/com/udacity/gradle/builditbigger/MainActivityFragment.java

> To: app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java

---

Create a specific fragment_main.xml for free productFlavor. Move:

> From: app/src/main/res/layout/fragment_main.xml

> To: app/src/free/res/layout/fragment_main.xml

---

The paid productFlavor don't have AndroidManifest. In this case, it will inherit the main AndroidManifest. We need to remove ads elements on the main AndroidManifest.

Delete this:

<div class="import_code"><div class="path_code">
app/src/main/AndroidManifest.xml
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/e9e8d57c8782da3837be46e20fdaca6347a19b3d/app/src/main/AndroidManifest.xml
?slice=
15:19
&footer=0"></script></div>

And delete this:

<div class="import_code"><div class="path_code">
app/src/main/AndroidManifest.xml
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/e9e8d57c8782da3837be46e20fdaca6347a19b3d/app/src/main/AndroidManifest.xml
?slice=
28:33
&footer=0"></script></div>

---

Create a specific MainActivityFragment.java for paid productFlavor:

<div class="import_code"><div class="path_code">
app/src/paid/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/f6daa7fedc40130d2edf137dfda4658e1cb49f4b/app/src/paid/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
13:26
&footer=0"></script></div>


Create a specific fragment_main.xml for paid productFlavor without Ads:

<div class="import_code"><div class="path_code">
app/src/paid/res/layout/fragment_main.xml
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/f6daa7fedc40130d2edf137dfda4658e1cb49f4b/app/src/paid/res/layout/fragment_main.xml
?slice=
0:27
&footer=0"></script></div>








## Fix bug "Not enough space to show ad" [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/006bfefded38918899fc0313b475d2b610902d8b?diff=split)

This bug ("Not enough space to show ad")[http://stackoverflow.com/questions/21848532/not-enough-space-to-show-ad-admob] is caused by the left and right padding of RelativeLayout, which is consuming space required by the AdView.

We add one more relative layout, and we move in padding constraints to allow the display of ads:

<div class="import_code"><div class="path_code">
app/src/free/res/layout/fragment_main.xml
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/006bfefded38918899fc0313b475d2b610902d8b/app/src/free/res/layout/fragment_main.xml
?slice=
0:34
&footer=0"></script></div>







## Refactoring and add a callback for EndpointsAsyncTask [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/c266103ddba9ffe9eea142cf93c019a7b9280faf?diff=split)

Now, we meet the minimal requirements of Udacity project. Does that mean we stop here? Continue with optional features.

At this point, I commit some fix after a lint check. Nothing special to say. To see the [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/0482541eb706d8a1d3fd482c67267a6885bc0acd?diff=split).

For the next steps, we need to control what is happening before and after the call to the EndpointAsyncTask. To do this refactorization, we need to put all the logic in MainActivityFragment:

* OnClickListener for the button, to add some steps before the call to the EndpointAsyncTask
* OnTaskCompleted interface to have a callback when the joke is loaded, to add some steps before display the joke


---

Delete the part of launching joke in the main activity:

<div class="import_code"><div class="path_code">
app/src/main/java/com/udacity/gradle/builditbigger/MainActivity.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/0482541eb706d8a1d3fd482c67267a6885bc0acd/app/src/main/java/com/udacity/gradle/builditbigger/MainActivity.java
?slice=
40:44
&footer=0"></script></div>


Add an id in fragment.xml for free and paid flavors:

<div class="import_code"><div class="path_code">
app/src/free/res/layout/fragment_main.xml
<div class="path_code"></div>
app/src/paid/res/layout/fragment_main.xml
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/c266103ddba9ffe9eea142cf93c019a7b9280faf/app/src/free/res/layout/fragment_main.xml
?slice=
22
&footer=0"></script></div>


And delete the call of launching joke method for free and paid flavors:

<div class="import_code"><div class="path_code">
app/src/free/res/layout/fragment_main.xml
</div><div class="path_code">
app/src/paid/res/layout/fragment_main.xml
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/0482541eb706d8a1d3fd482c67267a6885bc0acd/app/src/free/res/layout/fragment_main.xml
?slice=
25
&footer=0"></script></div>

---

Create an interface:

<div class="import_code"><div class="path_code">
app/src/main/java/com/udacity/gradle/builditbigger/OnTaskCompleted.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/c266103ddba9ffe9eea142cf93c019a7b9280faf/app/src/main/java/com/udacity/gradle/builditbigger/OnTaskCompleted.java
?slice=
6:9
&footer=0"></script></div>


Implement this interface in MainActivityFragment for free and paid flavors:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><div class="path_code">
app/src/paid/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/c266103ddba9ffe9eea142cf93c019a7b9280faf/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
18
&footer=0"></script></div>

---

Add the listener for the button for free and paid flavors:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><div class="path_code">
app/src/paid/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/c266103ddba9ffe9eea142cf93c019a7b9280faf/app/src/paid/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
28:36
&footer=0"></script></div>


And the method who call EndpointAsyncTask for free and paid flavors:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><div class="path_code">
app/src/paid/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/c266103ddba9ffe9eea142cf93c019a7b9280faf/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
50:54
&footer=0"></script></div>

---

Modify the constructor of EndpointAsyncTask:

<div class="import_code"><div class="path_code">
app/src/main/java/com/udacity/gradle/builditbigger/EndpointsAsyncTask.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/c266103ddba9ffe9eea142cf93c019a7b9280faf/app/src/main/java/com/udacity/gradle/builditbigger/EndpointsAsyncTask.java
?slice=
14:21
&footer=0"></script></div>


And modify the onPostExcute:

<div class="import_code"><div class="path_code">
app/src/main/java/com/udacity/gradle/builditbigger/EndpointsAsyncTask.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/c266103ddba9ffe9eea142cf93c019a7b9280faf/app/src/main/java/com/udacity/gradle/builditbigger/EndpointsAsyncTask.java
?slice=
39:43
&footer=0"></script></div>


And finally add the callback method in MainActivityFragment for free and paid flavors:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><div class="path_code">
app/src/paid/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/c266103ddba9ffe9eea142cf93c019a7b9280faf/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
55:62
&footer=0"></script></div>


After that, the execution is the same for the user. But now it's easier to implement next features!








## Add Interstitial Ad for free product flavor [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/dffff176ba6a1efac1e31a4183135c53e7441cdb?diff=split)

In this step, we request an interstitial ad for free product flavor. When the user click on the button:

* if the interstitial ad is loaded, then it is displayed
* else the EndpointsAsyncTask is called


When the interstitial ad is closed, the EndpointsAsyncTask is called.

---

Instantiate and create a listener:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/dffff176ba6a1efac1e31a4183135c53e7441cdb/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
43:46
&footer=0"></script></div>


Request new interstitial in on create view activity method:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/dffff176ba6a1efac1e31a4183135c53e7441cdb/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
56
&footer=0"></script></div>


And the associated method:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/dffff176ba6a1efac1e31a4183135c53e7441cdb/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
86:97
&footer=0"></script></div>

---

Display the interstitial ad:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/dffff176ba6a1efac1e31a4183135c53e7441cdb/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
58:69
&footer=0"></script></div>


Set AdListener:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/dffff176ba6a1efac1e31a4183135c53e7441cdb/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
48:55
&footer=0"></script></div>









## Add a loading indicator while the joke is being retrieved [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/8bbe23224f429e71b8ea3b3dc7bc6c5e68d92e58?diff=split)

When the user click on the button, the EndpointsAsyncTask is called. But the data is not available immediately!
We want to display a loading indicator while waiting for the callback of EndpointsAsyncTask.


---

Define `ProgressBar` in xml:

<div class="import_code"><div class="path_code">
app/src/free/res/layout/fragment_main.xml
</div><div class="path_code">
app/src/paid/res/layout/fragment_main.xml
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/8bbe23224f429e71b8ea3b3dc7bc6c5e68d92e58/app/src/free/res/layout/fragment_main.xml
?slice=
28:35
&footer=0"></script></div>


Initialize the `ProgressBar`:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><div class="path_code">
app/src/paid/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/8bbe23224f429e71b8ea3b3dc7bc6c5e68d92e58/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
36
&footer=0"></script></div>

---

Set the visibility of `ProgressBar` visible when calling to EndpointsAsyncTask:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><div class="path_code">
app/src/paid/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/8bbe23224f429e71b8ea3b3dc7bc6c5e68d92e58/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
77:83
&footer=0"></script></div>


Set the visibility of `ProgressBar` gone when EndpointsAsyncTask call back:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><div class="path_code">
app/src/paid/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/8bbe23224f429e71b8ea3b3dc7bc6c5e68d92e58/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
84:93
&footer=0"></script></div>











## Load joke during interstitial ads displaying [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/9274ad5443acc81eba3a51b47bdcd0ec1d767407?diff=split)

Features are ok, but I'm a little bit frustrated! I click, I see an interstitial Ad, I close it and I need to wait to see the joke. Why the joke is not loaded during the Ad visualization?

We add two variable:

* `mAdsOnScreen` is a `boolean`, to know if interstitial ad is actually displayed on screen
* `mResult` is a `string`, that contains the joke. Null if the joke isn't loaded


In addition to the method `loadData`, the method `launchActivity` is called when:

* the user click
* the data is loaded
* the ads is closed


If the ad is not currently displayed, depending on the load of the joke, we display the progressbar or the joke.

---

When the Ad is closed, affect a value to `mAdsOnScreen` and call `launchActivity`:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/9274ad5443acc81eba3a51b47bdcd0ec1d767407/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
54:62
&footer=0"></script></div>


When the button is clicked, affect a value to `mAdsOnScreen` and call `launchActivity`:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/9274ad5443acc81eba3a51b47bdcd0ec1d767407/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
65:80
&footer=0"></script></div>

---

When the EndpointsAsyncTask is called, affect a value to `mResult`:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/9274ad5443acc81eba3a51b47bdcd0ec1d767407/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
84:89
&footer=0"></script></div>


When the EndpointsAsyncTask call back, affect a value to `mResult` and call `launchActivity`:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/9274ad5443acc81eba3a51b47bdcd0ec1d767407/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
90:95
&footer=0"></script></div>

---

The global logic with the method `launchActivity`:

<div class="import_code"><div class="path_code">
app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/9274ad5443acc81eba3a51b47bdcd0ec1d767407/app/src/free/java/com/udacity/gradle/builditbigger/MainActivityFragment.java
?slice=
96:115
&footer=0"></script></div>








## Gradle test task:  launch GCE local dev server, run all tests, shutdown server [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/a69dd4cd4812fb59921a5c64c9a2b7fd820a03ef?diff=split)

This gradle in a nutshell:

* `runAppEngineAndTest` call `startAppEngineAndTest`, and after execute the task `:backend:appengineStop`
* `startAppEngineAndTest` call `:backend:appengineRun`, and run `backend:appengineRun` task in `daemon` mode, execute the task `:app:connectedAndroidTest`


If we replace the tasks in the execution order, it gives:

* `:backend:appengineStop`: starts the GCE local developer server
* `backend.extensions.appengine.daemon = true`: [run appengine in daemon mode](http://stackoverflow.com/questions/31434928/android-gradle-task-google-appengine)
* `:app:connectedAndroidTest`: run on-device Android tests
* `:backend:appengineStop`: stop the GCE local developer server


<div class="import_code"><div class="path_code">
build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/a69dd4cd4812fb59921a5c64c9a2b7fd820a03ef/build.gradle
?slice=
20:35
&footer=0"></script></div>