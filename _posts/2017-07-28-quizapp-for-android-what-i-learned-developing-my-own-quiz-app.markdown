---
title: QuizApp! for Android- What I learned developing my own quiz app
layout: post
time: 2017-07-28 19:50:56
---


I have been using Android for the longest time I can remember, and I have never owned an iPhone. I love the Android platform and the openness it provides. My current device is a OnePlus One that is running Slim7 ROM.

Android development has been on and off for me, but I was pretty familiar with Android because of my experience working in Ionic framework and a course in my college Curriculum called Mobile Application Development. I thought of creating an App for myself, and here is QuizApp!. 

QuizApp was developed using Android Studio, and how the application works is briefly explained here. The MainActivity asks the user to select the type of Quiz they would like to play. The App then loads the QuizActivity and feteches the quiz from OpenTriviaDatabase.

The view contains a TextViews for keeping track of score, number of questions and also for the question itself. The answers are present in a set of RadioGroup RadioButtons. 

{% include image name="Screenshot_1.png" caption="Main Activity" width="300"%}
{% include image name="Screenshot_2.png" caption="Selecting the quiz category" width="300"%}

When the QuizActivity loads, the layout loads the first question. Subsequently on clicking of the next button, the currently selected answer is checked and the Views are refreshed to contain the next question and the updated score.

For fetching the API request, I made use of Volley library, as it is well documented in the Android Developer Docs. 
MediaPlayer was used for playing the songs. One issue I encountered was while playing multiple sounds, as soon as the second started, the first would stop playing. The solution to this was to pause the previously playing instance and then play it again after initiating the second playback.

{% include image name="Screenshot_4.png" caption="The Quiz Activity.. I'm getting better at this, don't worry!" width="300"%}

Looking Ahead
I have started on the design and am thinking about how to implement Material Design for QuizApp! 

A nicer version of the application would use CardView or RecyclerView (going to be implemented soon) for the main quiz activity.

Also, the ScoreActivity is very,very,very basic. It literally has just a textview and a button right now. Lots of work to do on the UI! The category selector can be implemented as clickable cards with a background reperesenting the category with a text overlay. 

{% include image name="Screenshot_5.png" caption="The Score Activity" width="300"%}

Probably some animated baloons or confetti on the Score screen?  And need to find a better way than using Toast messages to let the users know if they were correct or wrong!

 Managing the LifeCycle and NavigationBar have not been implemented yet and are also on the tasklist. 

 I will be updating the app soon and will hopefully be uploading to the Play Store soon too. You can check it out on GitHub here- [https://github.com/shreyashag/QuizApp](https://github.com/shreyashag/QuizApp)

Thank you for reading and stay tuned!
