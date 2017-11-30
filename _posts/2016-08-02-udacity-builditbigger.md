---
layout: post
title: "Build It Bigger - 1/2"
sub_title: "Java Library, Android Library, and Google Cloud Endpoints (A project of Udacity Android Developer Nanodegree Program)"
excerpt_separator: "<!--more-->"
categories:
  - articles
tags:
  - developpement
  - android
  - udacity
header:
  teaser: images/udacity-builditbigger/001-th.jpg
gallery1:
  - url: /images/udacity-builditbigger/001.jpg
    image_path: /images/udacity-builditbigger/001.jpg
    alt: "Build It Bigger"  
---

For my first blog post, I propose the description step by step of my solution for the exercise **Udacity - Build it bigger**.

To better understand this exercise, some useful links:

* [the starting point provided](https://github.com/udacity/ud867/tree/master/FinalProject)
* [the compilation of instructions and expected requirements](https://github.com/fredericletellier/udacity-builditbigger/blob/master/README.md)
* [the repository of my solution](https://github.com/fredericletellier/udacity-builditbigger)

<!--more-->

Actually, I work on my capstone project. But when I have make this exercise, I already think to write this blog post. With this perspective,
I have voluntary make the smallest commit as possible to provide something readable. You can see the solution without read this post,
simply follow the commit step by step [here](https://github.com/fredericletellier/udacity-builditbigger/commits/master)

For those who want more details than only code, let's start!





## What we search to do 

This exercise is focus on interactions between libraries/modules and your app.
This exercise is focused primarily on the outright application of lessons offered in "Gradle for Android and Java".

If we atomize the final expected solution, we obtain:

* A Java library that provides jokes
* A Google Cloud Endpoints (GCE) project that serves those jokes
* An Android app who make the gap between the GCE module and the Android Library
* An Android Library containing an activity for displaying


The supplied diagram illustrates very well the interactions between elements:

{% include gallery id="gallery1" caption="" %}







## Create a Java library that provides jokes [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/6fe561a9e514de2e7175e2c16c5b3a1280223d2e?diff=split)

[Review the associated video lesson](https://www.youtube.com/watch?v=3CsgRnlVFkA&index=56&list=PLAwxTw4SYaPk2JP5TFPx7g63PCkyBqjZn)

After fork or copy-paste of the [starting point](https://github.com/udacity/ud867/tree/master/FinalProject), we should begin by create the java library.

Use the Wizard of Android Studio :

* In Android Studio: File > New Module...
* Choose "Java Library"
* Library name: jokelib
* Java Class name: JokeProvider


> Tips: When you use the wizard, files are created by gradle. If you want lost a lot of times with incomprehensible problems, open and modify files recently create before the end of gradle tasks.


The wizard do it for us. But it is useful to know that it was added to settings.gradle:

<div class="import_code"><div class="path_code">
settings.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/6fe561a9e514de2e7175e2c16c5b3a1280223d2e/settings.gradle
?slice=
0
&footer=0"></script></div>

---

Add this source compatibility in the new module:

<div class="import_code"><div class="path_code">
jokelib/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/6fe561a9e514de2e7175e2c16c5b3a1280223d2e/jokelib/build.gradle
?slice=
2
&footer=0"></script></div>

---

Create a static final array of Strings to stock the jokes. Here, the `getJoke` method choose randomly the joke to return.

<div class="import_code"><div class="path_code">
jokelib/src/main/java/com/joke/JokeProvider.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/6fe561a9e514de2e7175e2c16c5b3a1280223d2e/jokelib/src/main/java/com/joke/JokeProvider.java
?slice=
2:23
&footer=0"></script></div>


And that's all! Seriously, the hardest point, it's to find good jokes!










## Make the button display a toast showing a joke [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/4ad57176636f965472f8f0d06e9c99d71e4db316?diff=split)

We have good jokes, now we want to see them!

For this, import the new java library `jokelib` in the main project:

<div class="import_code"><div class="path_code">
app/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/4ad57176636f965472f8f0d06e9c99d71e4db316/app/build.gradle
?slice=
28
&footer=0"></script></div>


In the `MainActivity`, replace the Toast with a static message by a Toast who call the static method `getJoke` of `JokeProvider` class. I have increased the display time of Toast in order to have time to read the joke.

<div class="import_code"><div class="path_code">
app/src/main/java/com/udacity/gradle/builditbigger/MainActivity.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/4ad57176636f965472f8f0d06e9c99d71e4db316/app/src/main/java/com/udacity/gradle/builditbigger/MainActivity.java
?slice=
44
&footer=0"></script></div>




You can already build, run, click on the button, and laugh! Isn't it wonderful?











## Create a new empty Activity library/module [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/57b9eea1eacd2bdafc2a9a12c57b2ab0c4c4be14?diff=split)

[Review the associated video lesson](https://www.youtube.com/watch?v=jvJQHXe-vFc&index=57&list=PLAwxTw4SYaPk2JP5TFPx7g63PCkyBqjZn)

View a joke in a toast isn't ideal, we would display it in a new Activity to have time to enjoy. But we want to reuse this Activity in another project, so we need to put it in an android library.

Create a new empty android library with the wizard:

* In Android Studio: File > New Module...
* Choose "Android Library"
* Application/Library name: JokeActivity
* Module name: jokedisplay


> Tips: If you are in a hurry, wait... (the end of gradle tasks)


Like before, the wizard do it for us. But it is useful to know that it was added to settings.gradle:

<div class="import_code"><div class="path_code">
settings.gradle 
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/57b9eea1eacd2bdafc2a9a12c57b2ab0c4c4be14/settings.gradle
?slice=
0
&footer=0"></script></div>








## Display a joke passed to it as an intent extra [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/18f05db686dbe811cc8437c49953e2e9c5e8121a?diff=split)

My wizard do strange things. To ensure that you do not have the same problem as me, check the module created is a library not an application:

<div class="import_code"><div class="path_code">
jokedisplay/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/18f05db686dbe811cc8437c49953e2e9c5e8121a/jokedisplay/build.gradle
?slice=
0
&footer=0"></script></div>

Check if you have an appliId in your android library. In this case, delete it:

<div class="import_code"><div class="path_code">
jokedisplay/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/57b9eea1eacd2bdafc2a9a12c57b2ab0c4c4be14/jokedisplay/build.gradle
?slice=
7
&footer=0"></script></div>

And now, you have two manifests in your project. Change `allowBackup="false"` to avoid conflict.

<div class="import_code"><div class="path_code">
jokedisplay/src/main/AndroidManifest.xml
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/18f05db686dbe811cc8437c49953e2e9c5e8121a/jokedisplay/src/main/AndroidManifest.xml
?slice=
5
&footer=0"></script></div>

---

Import the new module android library in the main application:

<div class="import_code"><div class="path_code">
app/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/18f05db686dbe811cc8437c49953e2e9c5e8121a/app/build.gradle
?slice=
30
&footer=0"></script></div>

---

In the android library `jokedisplay`, catch the bundle of intent, and extract the joke to set a textview:

<div class="import_code"><div class="path_code">
jokedisplay/src/main/java/com/joke/JokeActivity.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/18f05db686dbe811cc8437c49953e2e9c5e8121a/jokedisplay/src/main/java/com/joke/JokeActivity.java
?slice=
16:23
&footer=0"></script></div>

---

In the main app, replace the toast by an explicit intent. And put the joke in extras of intent:

<div class="import_code"><div class="path_code">
app/src/main/java/com/udacity/gradle/builditbigger/MainActivity.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/18f05db686dbe811cc8437c49953e2e9c5e8121a/app/src/main/java/com/udacity/gradle/builditbigger/MainActivity.java
?slice=
44:50
&footer=0"></script></div>

---

Replace the method called when the button is clicked:

<div class="import_code"><div class="path_code">
app/src/main/res/layout/fragment_main.xml
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/18f05db686dbe811cc8437c49953e2e9c5e8121a/app/src/main/res/layout/fragment_main.xml
?slice=
21
&footer=0"></script></div>

---

We took the opportunity to add a default text if no joke has been extracted from the intent:

<div class="import_code"><div class="path_code">
jokedisplay/src/main/res/layout/activity_joke.xml
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/18f05db686dbe811cc8437c49953e2e9c5e8121a/jokedisplay/src/main/res/layout/activity_joke.xml
?slice=
15
&footer=0"></script></div>

<div class="import_code"><div class="path_code">
jokedisplay/src/main/res/values/strings.xml
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/18f05db686dbe811cc8437c49953e2e9c5e8121a/jokedisplay/src/main/res/values/strings.xml
?slice=
2
&footer=0"></script></div>





## Create a new empty Google Cloud Endpoint [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/88369a293cd5111597874ff170a0c039a8f2873c?diff=split)

Now, we want to put in the cloud the java library who provide the jokes. We need to create a Google Cloud Endpoint who do the gap between the java library and the main application.

To begin, create a new Google Cloud Endpoint with the wizard:

* In Android Studio: File > New Module...
* Choose "Google Cloud Module"
* Module type: App Engine Java Endpoints Module
* Module name: backend
* Package Name: com.joke.endpoint.backend
* Client Module: app(com.udacity.gradle.builditbigger)


> Tips: Wait... (take the opportunity to comment)


Like before, the wizard do it for us:

<div class="import_code"><div class="path_code">
settings.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/88369a293cd5111597874ff170a0c039a8f2873c/settings.gradle
?slice=
0
&footer=0"></script></div>


And the wizard do this too:

<div class="import_code"><div class="path_code">
app/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/88369a293cd5111597874ff170a0c039a8f2873c/app/build.gradle
?slice=
32
&footer=0"></script></div>





## Modify the GCE starter code to pull jokes from Java library [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/29fdd296c7d98015044ef3ba9d52f648a9348084?diff=split)


Import the java library module `jokelib` in the Google Cloud Endpoint module `backend`:

<div class="import_code"><div class="path_code">
backend/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/29fdd296c7d98015044ef3ba9d52f648a9348084/backend/build.gradle
?slice=
29
&footer=0"></script></div>


Modify the GCE to provide joke from `JokeProvider`class:

<div class="import_code"><div class="path_code">
backend/src/main/java/com/joke/endpoint/backend/MyEndpoint.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/29fdd296c7d98015044ef3ba9d52f648a9348084/backend/src/main/java/com/joke/endpoint/backend/MyEndpoint.java
?slice=
25:33
&footer=0"></script></div>














## Connect Android app to the backend


###  Emulator with local dev server [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/90175c9bae197435cbdb634a81e65d20887a6f9b?diff=split)


Now, it's GCE who provide joke, the java library doesn't need to be connected directly to the main application. Delete the import of libjoke in the main application:

<div class="import_code"><div class="path_code">
app/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/4ad57176636f965472f8f0d06e9c99d71e4db316/app/build.gradle
?slice=
28
&footer=0"></script></div>

---

Create and configure the EndpointAsyncTask to test on emulator with local dev server:

<div class="import_code"><div class="path_code">
app/src/main/java/com/udacity/gradle/builditbigger/EndpointsAsyncTask.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/90175c9bae197435cbdb634a81e65d20887a6f9b/app/src/main/java/com/udacity/gradle/builditbigger/EndpointsAsyncTask.java
?slice=
19:63
&footer=0"></script></div>

---

In the main application, replace the intent by a call to EndpointsAsyncTask:

<div class="import_code"><div class="path_code">
app/src/main/java/com/udacity/gradle/builditbigger/MainActivity.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/90175c9bae197435cbdb634a81e65d20887a6f9b/app/src/main/java/com/udacity/gradle/builditbigger/MainActivity.java
?slice=
40:44
&footer=0"></script></div>

---

You can test this configuration launching a local dev server for the GCE, and running the main app on emulator!















### Real device with local dev server [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/677bbf0412be0231c87182aa24d6d388d8597b42?diff=split)

Get your IP address on your computer, go to `cmd -> ipconfig -> IPV4 address with port number` and modify the API Builder:

<div class="import_code"><div class="path_code">
app/src/main/java/com/udacity/gradle/builditbigger/EndpointsAsyncTask.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/677bbf0412be0231c87182aa24d6d388d8597b42/app/src/main/java/com/udacity/gradle/builditbigger/EndpointsAsyncTask.java
?slice=
28:35
&footer=0"></script></div>


Set the `httpAddress` in build.gradle:

<div class="import_code"><div class="path_code">
backend/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/677bbf0412be0231c87182aa24d6d388d8597b42/backend/build.gradle
?slice=
41:44
&footer=0"></script></div>

---

You can test this configuration launching a local dev server for the GCE, and running the main app on a real device!







### Real device with backend deploy to App Engine [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/0fb25e463f453daafe309b75ba8f1eac93283329?diff=split)


Get your real url of backend deployed and modify the API Builder:

<div class="import_code"><div class="path_code">
app/src/main/java/com/udacity/gradle/builditbigger/EndpointsAsyncTask.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/0fb25e463f453daafe309b75ba8f1eac93283329/app/src/main/java/com/udacity/gradle/builditbigger/EndpointsAsyncTask.java
?slice=
28:30
&footer=0"></script></div>


Don't forget to delete this:

<div class="import_code"><div class="path_code">
backend/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/677bbf0412be0231c87182aa24d6d388d8597b42/backend/build.gradle
?slice=
41:44
&footer=0"></script></div>

---

You can test this configuration deploying backend to App Engine, and running the main app on a real device!







## Add functional test to check Async task successfully retrieves a non-empty string [(commit)](https://github.com/fredericletellier/udacity-builditbigger/commit/e9e8d57c8782da3837be46e20fdaca6347a19b3d?diff=split)

Set AndroidJUnitRunner as the default test instrumentation runner:

<div class="import_code"><div class="path_code">
app/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/e9e8d57c8782da3837be46e20fdaca6347a19b3d/app/build.gradle
?slice=
14
&footer=0"></script></div>


Add this for Testing Support Library:

<div class="import_code"><div class="path_code">
app/build.gradle
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/e9e8d57c8782da3837be46e20fdaca6347a19b3d/app/build.gradle
?slice=
34:38
&footer=0"></script></div>


Create test who check the returned string is not null and not empty:

<div class="import_code"><div class="path_code">
app/src/androidTest/java/com/udacity/gradle/builditbigger/EndpointsAsyncTaskTest.java
</div><script src="http://gist-it.appspot.com/
https://github.com/fredericletellier/udacity-builditbigger/blob/e9e8d57c8782da3837be46e20fdaca6347a19b3d/app/src/androidTest/java/com/udacity/gradle/builditbigger/EndpointsAsyncTaskTest.java
?slice=
18:35
&footer=0"></script></div>
