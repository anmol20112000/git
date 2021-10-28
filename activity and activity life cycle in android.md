-   What is activity in android?

    An activity is a single, focused thing that the user can do. Almost
    all activities interact with the user. An Android app may contain
    one or more activities, meaning one or more screens. The Android app
    starts by showing the main activity, and from there the app may make
    it possible to open additional activities.

-   What is activity life cycle in android*?*

> An activity has various stages in its lifecycle. To transit from one
> stage to the other stage of the activity lifecycle activity class has
> six methods which are overided by the developers according to the
> need. These methods are termed as callbacks. The six callbacks are :

1.  onCreate()

2.  onStart()

3.  onResume()

4.  onPause()

5.  onStop()

6.  onDestroy()

 <img src "https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2019/08/Activity-Life-Cycle-Android-Activity-Life-Cycle-Edureka-1.png">

1.  * onCreate()*: It displays the UI given in the XML file when the
    activity starts . It calls the SetContentView() method.

2.  *onStart():* when our activity is in process to be displayed this
    callback method is called .And after this method onResume() callback
    is called.

3.  *onResume()* :The core functionality of application is written
    within this callback method.When the activity is just about to be
    displayed this callback method is called .Suppose if you start a new
    activity that hides the already ongoing activity , onResume() is
    called when the activity that was hidden comes back to the view on
    the screen again.

4.  *onPause()*: The code you want to be executed when app is being
    paused (minimised ) should be wriiten in this callback method and
    when the user resumes to the application onResume() callback method
    will be called again.

5.  *onStop():* when an activity is being minimised onPause() callback
    is immediately called and after a few miliseconds onStop will
    be called.onStop() will stop the API calls of the application.

6.  *onDestroy():* onDestroy callback is to be called when you need to
    shutdown all the operations .

*Starting Activities and Getting Results*

The *startActivity(Intent)* method is used to start a new activity,
which will be placed at the top of the activity stack. It takes a single
argument,
an [*Intent*](https://developer.android.com/reference/android/content/Intent),
which describes the activity to be executed.

Sometimes you want to get a result back from an activity when it ends.
For example, you may start an activity that lets the user pick a person
in a list of contacts; when it ends, it returns the person that was
selected. To do this, you call the *startActivityForResult(Intent,
int)* version with a second integer parameter identifying the call. The
result will come back through your *onActivityResult(int, int,
Intent)* method.

When an activity exits, it can call *setResult(int)* to return data back
to its parent. It must always supply a result code, which can be the
standard results RESULT\_CANCELED, RESULT\_OK, or any custom values
starting at RESULT\_FIRST\_USER. In addition, it can optionally return
back an Intent containing any additional data it wants. All of this
information appears back on the parent's Activity.onActivityResult(),
along with the integer identifier it originally supplied.

If a child activity fails for any reason (such as crashing), the parent
activity will receive a result with the code RESULT\_CANCELED.

 public class CalendarActivity extends Activity {\
     ...\
\
     static final int DAY\_VIEW\_MODE = 0;\
     static final int WEEK\_VIEW\_MODE = 1;\
\
     private SharedPreferences mPrefs;\
     private int mCurViewMode;\
\
     protected void onCreate(Bundle savedInstanceState) {\
         super.onCreate(savedInstanceState);\
\
         mPrefs = getSharedPreferences(getLocalClassName(),
MODE\_PRIVATE);\
         mCurViewMode = mPrefs.getInt("view\_mode", DAY\_VIEW\_MODE);\
     }\
\
     protected void onPause() {\
         super.onPause();\
\
         SharedPreferences.Editor ed = mPrefs.edit();\
         ed.putInt("view\_mode", mCurViewMode);\
         ed.commit();\
     }\
 }\