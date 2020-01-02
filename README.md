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

## Dependencies

    // RecyclerView dependency
    implementation 'com.android.support:recyclerview-v7:28.0.0'

