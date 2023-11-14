# Ex.No:2 Create a simple application client and server service using AIDL interface in android studio.


## AIM:

To create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as CSAIDL and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display message give in MainActivity file(client/server).

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the client/server services using AIDL”.
Developed by:Yashaswi Mitta
Registeration Number :212221230062
*/
```
## AIDLColorService.java :
```
package com.example.aidlserver;

import android.app.Service;
import android.content.Intent;
import android.graphics.Color;
import android.os.IBinder;
import android.os.RemoteException;
import android.util.Log;

import java.util.Random;

public class AIDLColorService extends Service {
    private static final String TAG="AIDLColorService";
    public AIDLColorService() {
    }

    @Override
    public IBinder onBind(Intent intent) {
        // TODO: Return the communication channel to the service.
        return binder;
    }

    private final IAIDLColorInterface.Stub binder = new IAIDLColorInterface.Stub() {
        @Override
        public int getColor() throws RemoteException {
            Random rnd=new Random();
            int color= Color.argb(255,rnd.nextInt(256),rnd.nextInt(256),rnd.nextInt(256));
            Log.d(TAG,"getColor: "+color);
            return color;
        }
    };
}
```
## IAIDLColorInterface.aidl :

```
// IAIDLColorInterface.aidl
package com.example.aidlserver;

// Declare any non-default types here with import statements

interface IAIDLColorInterface {
    /**
     * Demonstrates some basic types that you can use as parameters
     * and return values in AIDL.
     */
    int getColor();
}
```
## AndroidManifest.xml :
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.AIDLServer"
        tools:targetApi="31">
        < service
            android:name=".AIDLColorService"
            android:enabled="true"
            android:exported="true">
            <intent-filter>
                <action android:name="AIDLColorService"/>
            </intent-filter>
        </service>
    </application>

</manifest>
```
## AIDLClient :
### MainActivity.java :
```
package com.example.aidlserver;

import androidx.appcompat.app.AppCompatActivity;

import android.content.ComponentName;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.os.RemoteException;
import android.util.Log;
import android.view.View;
import android.widget.Button;

import com.example.aidlclient.R;

public class MainActivity extends AppCompatActivity {

    IAIDLColorInterface iADILColorService;
    private static final String TAG ="MainActivity";

    private ServiceConnection mConnection = new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName componentName, IBinder iBinder) {
            iADILColorService = IAIDLColorInterface.Stub.asInterface(iBinder);
            Log.d(TAG, "Remote config Service Connected!!");
        }

        @Override
        public void onServiceDisconnected(ComponentName componentName) {

        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Intent intent = new Intent("AIDLColorService");
        intent.setPackage("com.example.aidlserver");

        bindService(intent,mConnection, BIND_AUTO_CREATE);

        // Create an onclick listener to button
        Log.d(TAG, "bindservice called");
        Button b = findViewById(R.id.button);

        b.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                try {
                    int color = iADILColorService.getColor();
                    view.setBackgroundColor(color);
                } catch (RemoteException e) {
                }
            }
        });


    }
}
```
###activity_main.xml :
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.example.aidlserver.MainActivity">

    <Button
        android:id="@+id/button"
        android:layout_width="289dp"
        android:layout_height="324dp"
        android:text="Click here to Change Color"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.499" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
### IAIDLColorInterface.aidl :
```
// IAIDLColorInterface.aidl
package com.example.aidlserver;

// Declare any non-default types here with import statements

interface IAIDLColorInterface {
    /**
     * Demonstrates some basic types that you can use as parameters
     * and return values in AIDL.
     */
    int getColor();
}
```
## OUTPUT
![282126997-3a28b9a0-f9d9-4918-bd5d-8be3f9bc20e1](https://github.com/Bhavishya203/Ex-02_ADL/assets/94679395/b6e6a44b-b5da-446b-9efd-d7d61665c39e)

![282127275-cd8a80bc-ae6d-4024-aa47-e97d00be2358](https://github.com/Bhavishya203/Ex-02_ADL/assets/94679395/3c9e0cce-5f19-4756-9797-9ede0acbf27c)



## RESULT
Thus a Simple Android Application to create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio is developed and executed successfully.

