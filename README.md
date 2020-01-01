# android-todo-list

How to program a simple todo list app for Android

## Add FAB dependency

    implementation 'com.android.support:design:28.0.0'
    
## Add FAB to MainActivity Layout

    <?xml version="1.0" encoding="utf-8"?>
    <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <com.google.android.material.floatingactionbutton.FloatingActionButton
            android:id="@+id/fab"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="bottom|end"
            android:layout_margin="16dp"
            android:tint="@android:color/white"
            android:src="@android:drawable/ic_input_add"/>

    </FrameLayout>

## Room dependency

    implementation "android.arch.persistence.room:runtime:1.1.1"
    annotationProcessor "android.arch.persistence.room:compiler:1.1.1"

## Dependencies

    // RecyclerView dependency
    implementation 'com.android.support:recyclerview-v7:28.0.0'

