#HackCon 2016
##You Can't See Me

###Description
Your time is up, my time is now

You can't see me, my time is now

It's the franchise, boy I'm shinin' now

You can't see me, my time is now!

https://s3-us-west-2.amazonaws.com/hackcon/JohnCena.apk

Flag Format: lower alpha string with no spaces

Operating System: ?

Reported Difficulty: Easy


###Running the apk
By installing the apk in Genymotion, I was presented with a blank activity so nothing to do here.


###Decompiling the apk
Dex2jar allows us to obtain the jar file

d2j-dex2jar.sh JohnCena.apk

Now to extract the code, I used jd-gui (Java Decompiler)

The code for MainActivity is
```java
package com.mayank13059.theoracle;

import android.os.Bundle;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.widget.Toolbar;
import android.view.Menu;
import android.view.MenuInflater;
import android.view.MenuItem;
import android.widget.TextView;

public class MainActivity
  extends AppCompatActivity
{
  private String genLoginForm1()
  {
    Integer localInteger = Integer.valueOf(656);
    return Integer.valueOf(686964656).toString() + "c" + Integer.valueOf(696).toString() + "b" + Integer.valueOf(656163).toString() + Integer.valueOf(68616).toString() + "d" + localInteger.toString() + "c" + localInteger.toString() + "f6e";
  }
  
  private String genLoginForm2()
  {
    Integer localInteger = Integer.valueOf(696);
    return Integer.valueOf(6265).toString() + Integer.valueOf(66696).toString() + Integer.valueOf(57263656).toString() + "c" + localInteger.toString() + "b" + Integer.valueOf(65616).toString() + "c" + localInteger.toString() + "f6e";
  }
  
  protected void onCreate(Bundle paramBundle)
  {
    super.onCreate(paramBundle);
    setContentView(2130968601);
    paramBundle = (TextView)findViewById(2131492970);
    TextView localTextView = (TextView)findViewById(2131492971);
    paramBundle.setText(genLoginForm1());
    localTextView.setText(genLoginForm2());
    setSupportActionBar((Toolbar)findViewById(2131492969));
  }
  
  public boolean onCreateOptionsMenu(Menu paramMenu)
  {
    getMenuInflater().inflate(2131558400, paramMenu);
    return true;
  }
  
  public boolean onOptionsItemSelected(MenuItem paramMenuItem)
  {
    if (paramMenuItem.getItemId() == 2131492994) {
      return true;
    }
    return super.onOptionsItemSelected(paramMenuItem);
  }
}
```

So there are 2 TextViews populated by genLoginForm1() and genLoginForm2() that for some reason I can't see when I run the apk but we can write a small java program to see the output generated by these functions.

###Payload

```java
public class Payload {

    public static void main(String[] args) {
        Integer localInteger = Integer.valueOf(656);
	System.out.println(Integer.valueOf(686964656).toString() + "c" + Integer.valueOf(696).toString() + "b" + Integer.valueOf(656163).toString() + Integer.valueOf(68616).toString() + "d" + localInteger.toString() + "c" + localInteger.toString() + "f6e");

	localInteger = Integer.valueOf(696);
	System.out.println(Integer.valueOf(6265).toString() + Integer.valueOf(66696).toString() + Integer.valueOf(57263656).toString() + "c" + localInteger.toString() + "b" + Integer.valueOf(65616).toString() + "c" + localInteger.toString() + "f6e");}
}

```

When we run the program, we get the lines:
```
686964656c696b65616368616d656c656f6e
62656669657263656c696b65616c696f6e
```

This is encoded in hex, so by using the python interpreter we can convert it to ascii:
```
python
>>> "686964656c696b65616368616d656c656f6e".decode("hex")
'hidelikeachameleon'
>>> "62656669657263656c696b65616c696f6e".decode("hex")
'befiercelikealion'
```

So our flag is: hidelikeachameleonbefiercelikealion

