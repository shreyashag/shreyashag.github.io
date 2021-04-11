---
date: "2017-08-13T00:00:00Z"
time: "2017-08-13 21:53:34"
title: Implementing High Scores in Android
---
To implement high scores in an Android game, there are a few options- 
1. To use LocalStorage.
2. To use a DB locally.
3. To use a cloud based DB service, such as FireCloud. 

 In this post I will be describing about how I have implemented highscores for my application QuizApp using LocalStorage. I will be talking about the other two in a later post. 

SharedPreferences is used to setup an acess to key-value pairs that can be stored locally on the device. A key needs to be supplied for identifying the StoredPreferences uniquely, here we are using __myPrefsKey__ as the identifier. 

SharedPreferences differs from Preferences as it can be accessed across activities, which is required nice the Highscore might be required to beaccessible from more than one Activity. 

The high score can be saved in the Preferences by identifying it with a _unique_ key for high-scores in a similar manner to how we used myPrefsKey to _uniquely_ identify the Preferences store. I have used __highScore__ as a key for my HighScore key inside the SharedPreferences store.


# This is how to set the high score -
{{< highlight java >}}
    public void setHighScore(int score){
        SharedPreferences sharedPref = this.getSharedPreferences("myPrefsKey",Context.MODE_PRIVATE);
        SharedPreferences.Editor editor = sharedPref.edit();
        editor.putInt("highScore", score);
        editor.commit();
        Log.d("WRITTEN highscore"+ score, "to preferences ");
        return;
    }
{{< / highlight >}}

A SharedPreferences Editor is required to be called upon our SharedPreferences folder ( which is uniquely identified by myPrefsKey ). On the editor, the putInt method is called to set the score on the high score key ( highScore). __It is important__ to follow up changes made by the editor with a commit call, as it writes the changes to our SharedPreferences store.

# This is how we can get the high score from the sharedPreferences.
{{< highlight java >}}
  public int getHighScore(){
        SharedPreferences sharedPref = this.getSharedPreferences("myPrefsKey",Context.MODE_PRIVATE);
        Integer highScore= sharedPref.getInt("highScore", 0 );
        Log.d("getHighScore: ",highScore.toString() );
        return highScore;
    }
{{< / highlight >}} 

Check out the latest release of QuizApp (v0.1.1), which has integrated High Scores as I have mentioned here -
[github.com/shreyashag/QuizApp/releases/](https://github.com/shreyashag/QuizApp/releases/) 

I am currently thinking about giving the app a fresh look and you contact me on twitter at [@shreyash_ag](https://twitter.com/shreyash_ag) if you have any ideas!



