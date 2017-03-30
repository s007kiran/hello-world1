/* this is front end designing of the project
Activity-main.xml 
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/activity_main"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:paddingBottom="@dimen/activity_vertical_margin"
android:paddingLeft="@dimen/activity_horizontal_margin"
android:background="#6fa9a1"
android:paddingRight="@dimen/activity_horizontal_margin"
android:paddingTop="@dimen/activity_vertical_margin"
tools:context="com.example.personal.yamyah.MainActivity">

<TextView
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="user name"
android:textSize="15sp"
android:textStyle="bold"
android:id="@+id/textView" />


<EditText
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:inputType="textPersonName"
android:hint="enter user name"
android:ems="10"
android:layout_alignParentTop="true"
android:layout_alignParentRight="true"
android:layout_alignParentEnd="true"
android:id="@+id/editText2" />

<TextView
android:text="password"
android:textSize="15sp"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_below="@+id/editText2"
android:layout_alignRight="@+id/textView"
android:layout_alignEnd="@+id/textView"
android:layout_marginTop="59dp"
android:id="@+id/textView3" />

<EditText
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:inputType="textPersonName"
android:hint="enter password"
android:ems="10"
android:layout_below="@+id/editText2"
android:layout_alignParentRight="true"
android:layout_alignParentEnd="true"
android:layout_marginRight="22dp"
android:layout_marginEnd="22dp"
android:layout_marginTop="44dp"
android:id="@+id/editText3" />

<Button
android:text="REgister"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:background="#a49d9d"
android:textColor="#101010"
android:onClick="button"
android:layout_centerVertical="true"
android:layout_alignLeft="@+id/editText2"
android:layout_alignStart="@+id/editText2"
android:id="@+id/button" />

<TextView
android:text="Already register ? sign in here "

android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_below="@+id/button"
android:layout_marginTop="74dp"
android:id="@+id/textViewsignin"
android:textAlignment="center"
android:layout_alignParentRight="true"
android:layout_alignParentEnd="true"
android:layout_alignLeft="@+id/textView3"
android:layout_alignStart="@+id/textView3" />

</RelativeLayout>
// in the front end we have created  2 edit text,2 textview,a button

/* This is java coding for the project */
Main activity
package com.example.personal.yamyah;

import android.app.ProgressDialog;
import android.support.annotation.NonNull;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.text.TextUtils;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ProgressBar;
import android.widget.TextView;
import android.widget.Toast;

import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;

public class MainActivity extends AppCompatActivity implements View.OnClickListener {
private Button signup;
private EditText email;
private EditText password;
private TextView already;
private FirebaseAuth firebaseauth;

private ProgressDialog progressdialog;

@Override
protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
progressdialog = new ProgressDialog(this);
firebaseauth = FirebaseAuth.getInstance();

signup = (Button) findViewById(R.id.button);
email = (EditText) findViewById(R.id.editText2);
password = (EditText) findViewById(R.id.editText3);
already = (TextView) findViewById(R.id.textViewsignin);
signup.setOnClickListener(this);
signup.setOnClickListener(this);
email.setOnClickListener(this);
password.setOnClickListener(this);
    }

private void registeruser() {
        String email1 = email.getText().toString().trim();
        String password1 = password.getText().toString().trim();
if (TextUtils.isEmpty(email1)) {
//should not be empty
Toast.makeText(this, "enter mail id", Toast.LENGTH_SHORT).show();
return;
        }
if (TextUtils.isEmpty(password1)) {
//should not be empty
Toast.makeText(this, "enter password", Toast.LENGTH_SHORT).show();
return;
        }
progressdialog.setMessage("registering user");
progressdialog.show();

firebaseauth.createUserWithEmailAndPassword(email1, password1)
                .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
@Override
public void onComplete(@NonNull Task<AuthResult> task) {
if (task.isSuccessful()) {
                            Toast.makeText(MainActivity.this, "registered successfully", Toast.LENGTH_SHORT).show();
                            Toast.makeText(MainActivity.this, " cannot registered ,please try again", Toast.LENGTH_SHORT).show();
                        }
                    }
                });

    }

@Override
public void onClick(View v) {
if (v == signup) {
            registeruser();
        }
if (v == already) {
        }
    }
}

// In this java code we have created objects for the components in front end and gave connection using firebase
activity_admin_login.xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_admin_login"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:background="#6fa8a1"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.nani.firebaseyyp.AdminLogin">


    <LinearLayout
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <EditText
            android:layout_margin="17dp"
            android:inputType="textEmailAddress"
            android:hint="Enter Your Email"
            android:id="@+id/editTextEmail"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />

        <EditText
            android:layout_margin="13dp"
            android:inputType="textPassword"
            android:hint="Password"
            android:id="@+id/editTextPassword"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />
        <Button
            android:layout_margin="15dp"
            android:id="@+id/buttonLogin"
            android:text="Login"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />


            />



    </LinearLayout>



</RelativeLayout>

AdminLogin.java
package com.example.nani.firebaseyyp;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;

public class AdminLogin extends AppCompatActivity {

    private Button buttonLogin;
    private EditText editTextEmail;
    private EditText editTextPassword;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_admin_login);
        buttonLogin =(Button) findViewById(R.id.buttonLogin);
        editTextEmail =(EditText) findViewById(R.id.editTextEmail);
        editTextPassword = (EditText) findViewById(R.id.editTextPassword);

    }
}

AndroidMainfest.xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.nani.firebaseyyp">

    <user-permission android:name="android.permission.INTERNET" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <!--
 ATTENTION: This was auto-generated to add Google Play services to your project for
     App Indexing.  See https://g.co/AppIndexing/AndroidStudio for more information.
        -->
        <meta-data
            android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

        <activity android:name=".SignActivity" />
        <activity android:name=".AdminLogin" />
        <activity android:name=".products">
            <intent-filter>
                <action android:name="com.example.nani.firebaseyyp.products" />

                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
    </application>

</manifest>
activity_sign.xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_sign"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.nani.firebaseyyp.SignActivity">

</RelativeLayout>

activity_products.xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_products"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.nani.firebaseyyp.products">

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:inputType="textPersonName"
        android:ems="10"
        android:layout_alignParentTop="true"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"
        android:layout_marginLeft="49dp"
        android:layout_marginStart="49dp"
        android:layout_marginTop="96dp"
        android:id="@+id/pro"
        android:hint="product namr" />

    <Button
        android:text="upload"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/pro"
        android:layout_alignRight="@+id/pro"
        android:layout_alignEnd="@+id/pro"
        android:layout_marginRight="62dp"
        android:layout_marginEnd="62dp"
        android:layout_marginTop="124dp"
        android:id="@+id/ok"
        android:onClick="upload" />
</RelativeLayout>

products.java
package com.example.nani.firebaseyyp;

import android.app.ProgressDialog;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;

public class products extends AppCompatActivity {
EditText name;
    Button b;
    private ProgressDialog progressDialog;
    FirebaseDatabase firebaseDatabase;
    DatabaseReference databaseReference;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_products);
        name=(EditText)findViewById(R.id.pro);
        b=(Button)findViewById(R.id.ok);
        progressDialog = new ProgressDialog(this);
        firebaseDatabase=FirebaseDatabase.getInstance();
        databaseReference=firebaseDatabase.getReferenceFromUrl("https://fir-yamyah-project.firebaseio.com/products");
    }


    public void upload(View v)
    {

        DatabaseReference id = databaseReference .push();
        id.child("name").setValue(name.getText().toString());

        Toast.makeText(this, "ok", Toast.LENGTH_SHORT).show();
    }
}

signActivity.java
package com.example.nani.firebaseyyp;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class SignActivity extends AppCompatActivity {


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_sign);
    }
}

activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#6fa8a1"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.nani.firebaseyyp.MainActivity">



    <LinearLayout
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <EditText
            android:layout_margin="17dp"
            android:inputType="textEmailAddress"
            android:hint="Enter Your Email"
            android:id="@+id/editTextEmail"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />

        <EditText
            android:layout_margin="13dp"
            android:inputType="textPassword"
            android:hint="Password"
            android:id="@+id/editTextPassword"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />
        <Button
            android:layout_margin="15dp"
            android:id="@+id/buttonRegister"
            android:text="Register User"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />

        <TextView
            android:textAlignment="center"
            android:text="Already Registered? Sign In Here"
            android:id="@+id/textViewSignIn"

            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            />



    </LinearLayout>

    <Button
        android:text="ADMIN Login"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_alignParentRight="true"
        android:layout_alignParentEnd="true"
        android:id="@+id/admin" />

    <Button
        android:text="Button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"
        android:layout_marginLeft="22dp"
        android:layout_marginStart="22dp"
        android:id="@+id/button2"
        android:onClick="test" />


</RelativeLayout>





















