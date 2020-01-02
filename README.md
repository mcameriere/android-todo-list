# android-todo-list

Simple todo list app for Android

## Create AddTaskActivity

LinearLayout
- EditText (editTextTaskDescription)
- RadioGroup (radioGroupPriority)
- Button (buttonSave)
    
## Modify MainActivity

FrameLayout
- Button (buttonAdd) layout_gravity="bottom|right"

## Create TaskEntry class

    package com.example.todolist;

    import java.util.Date;

    public class TaskEntry {
        private int id;
        private String description;
        private int priority;
        private Date updatedAt;

        public TaskEntry(String description, int priority, Date updatedAt) {
            this.description = description;
            this.priority = priority;
            this.updatedAt = updatedAt;
        }

        public TaskEntry(int id, String description, int priority, Date updatedAt) {
            this.id = id;
            this.description = description;
            this.priority = priority;
            this.updatedAt = updatedAt;
        }

        // getters and setters here
    }

## (1) Add Room dependency

    implementation "android.arch.persistence.room:runtime:1.1.1"
    annotationProcessor "android.arch.persistence.room:compiler:1.1.1"

## (2) Annotate class with Entity(tablename = "task")

## (3) Annotate the id with PrimaryKey(autoGenerate = true)

## (4) Annotate the 3 parameters constructor with @Ignore

## Add RecyclerView

Add RecyclerView dependency

    implementation 'com.android.support:recyclerview-v7:28.0.0'

Add RecyclerView to layout

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recyclerViewTasks"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

Create task_layout.xml

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        xmlns:tools="http://schemas.android.com/tools"
        android:orientation="horizontal"
        android:paddingLeft="16dp"
        android:paddingTop="8dp"
        android:paddingRight="16dp"
        android:paddingBottom="8dp">

        <LinearLayout
            android:layout_width="0dp"
            android:layout_weight="1"
            android:layout_height="wrap_content"
            android:orientation="vertical">

            <TextView
                android:id="@+id/textViewTaskDescription"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                tools:text="Description" />

            <TextView
                android:id="@+id/textViewTaskUpdatedAt"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                tools:text="11/11/1111"/>

        </LinearLayout>

        <TextView
            android:id="@+id/textViewTaskPriority"
            style="@style/TextAppearance.AppCompat.Small"
            android:layout_width="22dp"
            android:layout_height="22dp"
            android:layout_gravity="center"
            android:layout_marginLeft="8dp"
            android:gravity="center"
            android:textAlignment="center"
            android:textColor="@android:color/primary_text_light"
            tools:text="1"/>

    </LinearLayout>
