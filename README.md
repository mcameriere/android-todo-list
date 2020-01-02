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

    <LinearLayout android:orientation="horizontal"

        <LinearLayout android:orientation="vertical">

            <TextView android:id="@+id/textViewTaskDescription" />

            <TextView android:id="@+id/textViewTaskUpdatedAt" />

        </LinearLayout>

        <TextView android:id="@+id/textViewTaskPriority" />

    </LinearLayout>

Create class TaskAdapter
 
    public class TaskAdapter extends RecyclerView.Adapter<TaskAdapter.TaskViewHolder> {}

Create class AppDatabase

    @Database(entities = {TaskEntry.class}, version = 1, exportSchema = false)
    @TypeConverters(DateConverter.class)
    public abstract class AppDatabase extends RoomDatabase {

        private static final String LOG_TAG = AppDatabase.class.getSimpleName();
        private static final Object LOCK = new Object();
        private static final String DATABASE_NAME = "todolist";
        private static AppDatabase sInstance;

        public static AppDatabase getInstance(Context context) {
            if (sInstance == null) {
                synchronized (LOCK) {
                    Log.d(LOG_TAG, "Creating new database instance");
                    sInstance = Room.databaseBuilder(context.getApplicationContext(),
                            AppDatabase.class, AppDatabase.DATABASE_NAME)
                            // TODO (2) call allowMainThreadQueries before building the instance
                            .build();
                }
            }
            Log.d(LOG_TAG, "Getting the database instance");
            return sInstance;
        }

        public abstract TaskDao taskDao();

    }

Create class DateConverter

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
    
Create class TaskDao

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

        @Update(onConflict = OnConflictStrategy.REPLACE)
        void updateTask(TaskEntry taskEntry);

        @Delete
        void deleteTask(TaskEntry taskEntry);
    }
    
TODO's

    // TODO (1) Make updatedAt match a column named updated_at. Tip: Use the ColumnInfo annotation
    // TODO (2) call allowMainThreadQueries before building the instance
    // TODO (3) Create AppDatabase member variable for the Database
    // TODO (4) Initialize member variable for the data base
    // TODO (5) Create a description variable and assign to it the value in the edit text
    // TODO (6) Create a priority variable and assign the value returned by getPriorityFromViews()
    // TODO (7) Create a date variable and assign to it the current Date
    // TODO (8) Create taskEntry variable using the variables defined above
    // TODO (9) Use the taskDao in the AppDatabase variable to insert the taskEntry
    // TODO (10) call finish() to come back to MainActivity
    
To be continued...
