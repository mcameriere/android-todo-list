# android-todo-list

Simple todo list app for Android

## Create class TaskEntry

    package com.example.todolist;

    import java.util.Date;

    public class TaskEntry {
        private int id;
        private String description;

        public TaskEntry(int id, String description) {
            this.id = id;
            this.description = description;
        }

        public TaskEntry(String description) {
            this.description = description;
        }

        // getters and setters here
    }

## Modify activity_main.xml

FrameLayout
- Button (buttonLoad) layout_gravity="bottom|left"
- Button (buttonAdd) layout_gravity="bottom|right"

## Add RecyclerView

### Add RecyclerView dependency

    implementation 'com.android.support:recyclerview-v7:28.0.0'

### Add RecyclerView to activity_main.xml

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recyclerViewTasks"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

### Create layout item_task.xml

LinearLayout
- TextView (textViewTaskDescription)

### Create class TaskAdapter
 
    public class TaskAdapter extends RecyclerView.Adapter<TaskAdapter.TaskViewHolder> {
    
        private List<TaskEntry> mTasks;
        
        ...
        
        class TaskViewHolder extends RecyclerView.ViewHolder {

            ...
            
        }
    }

## Add Room dependency

    implementation "android.arch.persistence.room:runtime:1.1.1"
    annotationProcessor "android.arch.persistence.room:compiler:1.1.1"

## Annotate class with Entity(tablename = "task")

## Annotate the id with PrimaryKey(autoGenerate = true)

## Annotate the 1 parameter constructor with @Ignore

## Create interface TaskDao

    package com.example.android.todolist.database;

    import android.arch.persistence.room.Dao;
    import android.arch.persistence.room.Delete;
    import android.arch.persistence.room.Insert;
    import android.arch.persistence.room.OnConflictStrategy;
    import android.arch.persistence.room.Query;
    import android.arch.persistence.room.Update;

    import java.util.List;

    @Dao
    public interface TaskDao {

        @Query("SELECT * FROM task ORDER BY priority")
        List<TaskEntry> loadAllTasks();

        @Insert
        void insertTask(TaskEntry taskEntry);

    }
    
## Create class AppDatabase

    @Database(entities = {TaskEntry.class}, version = 1, exportSchema = false)
    public abstract class AppDatabase extends RoomDatabase {

        private static final Object LOCK = new Object();
        private static final String DATABASE_NAME = "todolist";
        private static AppDatabase sInstance;

        public static AppDatabase getInstance(Context context) {
            if (sInstance == null) {
                synchronized (LOCK) {
                    sInstance = Room.databaseBuilder(context.getApplicationContext(),
                            AppDatabase.class, AppDatabase.DATABASE_NAME)
                            .allowMainThreadQueries()
                            .build();
                }
            }
            return sInstance;
        }

        public abstract TaskDao taskDao();

    }

## Create class DateConverter

    package com.example.android.todolist.database;

    import android.arch.persistence.room.TypeConverter;

    import java.util.Date;

    public class DateConverter {
        @TypeConverter
        public static Date toDate(Long timestamp) {
            return timestamp == null ? null : new Date(timestamp);
        }

        @TypeConverter
        public static Long toTimestamp(Date date) {
            return date == null ? null : date.getTime();
        }
    }
    
## To be continued...
