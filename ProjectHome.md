The generated class will have all the tedious code for persisting the object described by the interface.  It will be generated by the plugin at project build time from an annotated interface that described the table and fields for the class.  The generated class will be designed to be efficient at runtime; it won't need to use reflection etc.

## 0.1.18 plugin, 0.1.6 library ##

Update for obscure issue in underlying classwriter library that would cause it to fail to read some class files.  No compelling need to update if you do not see this problem.  Binary compatible with previous release.

## 0.1.5 library (still goes with 0.1.16 plugin) ##

Add close to cursor in Gen\_read method.  Suggested by Marek Wrobel.

## 0.1.4 library ##

IdImplementation base class has added Gen\_read method, to populate a single instance from the database.  Suggested by Matt Smith

## 0.1.16 plugin, 0.1.3 library ##

Create table code will honor `Nullable` and `DefaultValue` annotations

## 0.1.15 plugin, 0.1.3 library ##

Plugin will generate files in gen fragment root, to match where
ADT plugin generates R file.

Patch from koushd ([Issue 1](https://code.google.com/p/sqlitegen/issues/detail?id=1)) so it will work as `ContentProvider`.  Use
lowercase `_id` as default primary key.  Patch modified so it will work
with databases generated with previous code, and with code that
depends on code generated with previous code.

## 0.1.12 Initial working version ##

Not all the features have been tested, but the plugin will generate usable code.

# Installation #

You will need to download 2 files to use the plugin.

`sqlitegen_eclipse_site_xxx.jar` is a file containing an Eclipse plugin installation site in jar form.  Download this file and configure it as a feature download site in the Eclipse software update panel; then you can install the plugin from it.

`com.antlersoft.android.db_xxx.jar` is a library jar with the dependencies required by the code generated by the plugin.  Add this file as a library to the build path of any Eclipse project that will use the plugin.

# Using the Plugin #

The plugin will only work with Android projects.  Enable it on a project by right-clicking
on the project and setting the checkbox on the _SQLiteGen..._ option in the project menu.

The plugin will look for interfaces in the project that have the annotation `com.antlersoft.android.db.TableInterface`  Accessor methods within the interface annotated with `com.antlersoft.android.db.FieldAccessor` will define columns in the table.  You can specify names and column types through fields in the annotation; refer to
the (sadly incomplete) Javadoc for details.  When the plugin sees the annotated interface,
it will create an (optionally abstract) class implementing the interface that includes
implementations of the accessor methods, static fields for field names and the table name,
and methods for reading from, inserting and updating records in the table.

## Example ##

This code:

```
/**
 * Copyright (C) 2009 Michael A. MacDonald
 */
package android.androidVNC;

import com.antlersoft.android.db.*;

@TableInterface(ImplementingClassName="AbstractConnectionBean",TableName="CONNECTION_BEAN")
interface IConnectionBean {
	@FieldAccessor
	long get_Id();
	@FieldAccessor
	String getNickname();
	@FieldAccessor
	String getAddress();
	@FieldAccessor
	int getPort();
	@FieldAccessor
	String getPassword();
	@FieldAccessor
	String getColorModel();
	@FieldAccessor
	boolean getForceFull();
	@FieldAccessor
	String getRepeaterId();
}
```

generates this file:

```
// This class was generated from android.androidVNC.IConnectionBean by a tool
// Do not edit this file directly
package android.androidVNC;

public abstract class AbstractConnectionBean extends com.antlersoft.android.dbimpl.IdImplementationBase implements IConnectionBean {

    public static final String GEN_TABLE_NAME = "CONNECTION_BEAN";
    public static final int GEN_COUNT = 8;

    // Field constants
    public static final String GEN_FIELD__ID = "_ID";
    public static final int GEN_ID__ID = 0;
    public static final String GEN_FIELD_NICKNAME = "NICKNAME";
    public static final int GEN_ID_NICKNAME = 1;
    public static final String GEN_FIELD_ADDRESS = "ADDRESS";
    public static final int GEN_ID_ADDRESS = 2;
    public static final String GEN_FIELD_PORT = "PORT";
    public static final int GEN_ID_PORT = 3;
    public static final String GEN_FIELD_PASSWORD = "PASSWORD";
    public static final int GEN_ID_PASSWORD = 4;
    public static final String GEN_FIELD_COLORMODEL = "COLORMODEL";
    public static final int GEN_ID_COLORMODEL = 5;
    public static final String GEN_FIELD_FORCEFULL = "FORCEFULL";
    public static final int GEN_ID_FORCEFULL = 6;
    public static final String GEN_FIELD_REPEATERID = "REPEATERID";
    public static final int GEN_ID_REPEATERID = 7;

    // SQL Command for creating the table
    public static String GEN_CREATE = "CREATE TABLE CONNECTION_BEAN (" +
    "_ID INTEGER PRIMARY KEY AUTOINCREMENT," +
    "NICKNAME TEXT," +
    "ADDRESS TEXT," +
    "PORT INTEGER," +
    "PASSWORD TEXT," +
    "COLORMODEL TEXT," +
    "FORCEFULL INTEGER," +
    "REPEATERID TEXT" +
    ")";

    // Members corresponding to defined fields
    private long gen__Id;
    private java.lang.String gen_nickname;
    private java.lang.String gen_address;
    private int gen_port;
    private java.lang.String gen_password;
    private java.lang.String gen_colorModel;
    private boolean gen_forceFull;
    private java.lang.String gen_repeaterId;


    public String Gen_tableName() { return GEN_TABLE_NAME; }

    // Field accessors
    public long get_Id() { return gen__Id; }
    public void set_Id(long arg__Id) { gen__Id = arg__Id; }
    public java.lang.String getNickname() { return gen_nickname; }
    public void setNickname(java.lang.String arg_nickname) { gen_nickname = arg_nickname; }
    public java.lang.String getAddress() { return gen_address; }
    public void setAddress(java.lang.String arg_address) { gen_address = arg_address; }
    public int getPort() { return gen_port; }
    public void setPort(int arg_port) { gen_port = arg_port; }
    public java.lang.String getPassword() { return gen_password; }
    public void setPassword(java.lang.String arg_password) { gen_password = arg_password; }
    public java.lang.String getColorModel() { return gen_colorModel; }
    public void setColorModel(java.lang.String arg_colorModel) { gen_colorModel = arg_colorModel; }
    public boolean getForceFull() { return gen_forceFull; }
    public void setForceFull(boolean arg_forceFull) { gen_forceFull = arg_forceFull; }
    public java.lang.String getRepeaterId() { return gen_repeaterId; }
    public void setRepeaterId(java.lang.String arg_repeaterId) { gen_repeaterId = arg_repeaterId; }

    public android.content.ContentValues Gen_getValues() {
        android.content.ContentValues values=new android.content.ContentValues();
        values.put(GEN_FIELD__ID,Long.toString(this.gen__Id));
        values.put(GEN_FIELD_NICKNAME,this.gen_nickname);
        values.put(GEN_FIELD_ADDRESS,this.gen_address);
        values.put(GEN_FIELD_PORT,Integer.toString(this.gen_port));
        values.put(GEN_FIELD_PASSWORD,this.gen_password);
        values.put(GEN_FIELD_COLORMODEL,this.gen_colorModel);
        values.put(GEN_FIELD_FORCEFULL,(this.gen_forceFull ? "1" : "0"));
        values.put(GEN_FIELD_REPEATERID,this.gen_repeaterId);
        return values;
    }

    /**
     * Return an array that gives the column index in the cursor for each field defined
     * @param cursor Database cursor over some columns, possibly including this table
     * @return array of column indices; -1 if the column with that id is not in cursor
     */
    public int[] Gen_columnIndices(android.database.Cursor cursor) {
        int[] result=new int[GEN_COUNT];
        result[0] = cursor.getColumnIndex(GEN_FIELD__ID);
        result[1] = cursor.getColumnIndex(GEN_FIELD_NICKNAME);
        result[2] = cursor.getColumnIndex(GEN_FIELD_ADDRESS);
        result[3] = cursor.getColumnIndex(GEN_FIELD_PORT);
        result[4] = cursor.getColumnIndex(GEN_FIELD_PASSWORD);
        result[5] = cursor.getColumnIndex(GEN_FIELD_COLORMODEL);
        result[6] = cursor.getColumnIndex(GEN_FIELD_FORCEFULL);
        result[7] = cursor.getColumnIndex(GEN_FIELD_REPEATERID);
        return result;
    }

    /**
     * Populate one instance from a cursor 
     */
    public void Gen_populate(android.database.Cursor cursor,int[] columnIndices) {
        if ( columnIndices[GEN_ID__ID] >= 0 && ! cursor.isNull(columnIndices[GEN_ID__ID])) {
            gen__Id = cursor.getLong(columnIndices[GEN_ID__ID]);
        }
        if ( columnIndices[GEN_ID_NICKNAME] >= 0 && ! cursor.isNull(columnIndices[GEN_ID_NICKNAME])) {
            gen_nickname = cursor.getString(columnIndices[GEN_ID_NICKNAME]);
        }
        if ( columnIndices[GEN_ID_ADDRESS] >= 0 && ! cursor.isNull(columnIndices[GEN_ID_ADDRESS])) {
            gen_address = cursor.getString(columnIndices[GEN_ID_ADDRESS]);
        }
        if ( columnIndices[GEN_ID_PORT] >= 0 && ! cursor.isNull(columnIndices[GEN_ID_PORT])) {
            gen_port = (int)cursor.getInt(columnIndices[GEN_ID_PORT]);
        }
        if ( columnIndices[GEN_ID_PASSWORD] >= 0 && ! cursor.isNull(columnIndices[GEN_ID_PASSWORD])) {
            gen_password = cursor.getString(columnIndices[GEN_ID_PASSWORD]);
        }
        if ( columnIndices[GEN_ID_COLORMODEL] >= 0 && ! cursor.isNull(columnIndices[GEN_ID_COLORMODEL])) {
            gen_colorModel = cursor.getString(columnIndices[GEN_ID_COLORMODEL]);
        }
        if ( columnIndices[GEN_ID_FORCEFULL] >= 0 && ! cursor.isNull(columnIndices[GEN_ID_FORCEFULL])) {
            gen_forceFull = (cursor.getInt(columnIndices[GEN_ID_FORCEFULL]) != 0);
        }
        if ( columnIndices[GEN_ID_REPEATERID] >= 0 && ! cursor.isNull(columnIndices[GEN_ID_REPEATERID])) {
            gen_repeaterId = cursor.getString(columnIndices[GEN_ID_REPEATERID]);
        }
    }

    /**
     * Populate one instance from a ContentValues 
     */
    public void Gen_populate(android.content.ContentValues values) {
        gen__Id = values.getAsLong(GEN_FIELD__ID);
        gen_nickname = values.getAsString(GEN_FIELD_NICKNAME);
        gen_address = values.getAsString(GEN_FIELD_ADDRESS);
        gen_port = (int)values.getAsInteger(GEN_FIELD_PORT);
        gen_password = values.getAsString(GEN_FIELD_PASSWORD);
        gen_colorModel = values.getAsString(GEN_FIELD_COLORMODEL);
        gen_forceFull = (values.getAsInteger(GEN_FIELD_FORCEFULL) != 0);
        gen_repeaterId = values.getAsString(GEN_FIELD_REPEATERID);
    }
}
```