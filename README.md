***This document is under construction***

# Android Coding Guidelines Android

## 1. Project structure

New projects should follow the Android Gradle project structure that is defined on the [Android Gradle plugin user guide](http://tools.android.com/tech-docs/new-build-system/user-guide#TOC-Project-Structure).

### 1.1 Package structure

It's recommended to structure in the following way:

### App

* network
	* picasso
	* dashboard 	
	* matchfeed
* model 
* injection
	* modules
	* component
	* qualifiers	 	
* ui
	* dashboard
	* notifications 	
	* matchfeed
* persistence
	* dashboard
	* matchfeed	
* analytics
* ads
* utils

#### 1.1.1 Network

Contains all the network related files (Http services, deserializers, image loading...). Try to group network files for different parts of the app in different subpackages.

#### 1.1.2 Model

Contains all the model related files.

#### 1.1.3 Injection

We use depency injection usually using [Dagger 2](http://google.github.io/dagger/). This package will contain all the dependency injection related files (modules, components, qualifiers, scopes...).

#### 1.1.4 Ui

Contains all ui related files (Views, adapters...). Try to group ui files for different parts of the app into different subpackages.

#### 1.1.5 Persistence

Contains all the persistence related files (Shared preferences, sqlite, files storage...). Try to group persistence files for different parts of the app into different subpackages.

#### 1.1.6 Analytics

Contains all the analytics related files

#### 1.1.7 Ads

Contains all the adverts related files

#### 1.1.8 Utils

Contains all the utility related files, usually they are files containing only static methods that helps to do some specific task that it's repeated all over the app and doesn't really belong to any other part of the app (TimeUtils, FontUtils, ViewUtils...) 




## 2. Coding Style

At TAB we follow [Android Code Style](https://source.android.com/source/code-style.html#follow-field-naming-conventions) guidelines


On top of rules listed there we have few extra rules and exceptions:

### 2.1 Name conventions

- **Do NOT use m or s prefix in fields inside POJO (models, events)**

*good:* 

``` java
public class League {
   	private String id;
   	private String name;
   	 	
 	public String getId() {
      	return id;
   	}

 	public void setId(String id) {
    	this.id = id;
   	}

   	public String getName() {
      	return name;
   	}

   	public void setName(String name) {
      	this.name = name;
   	}
}
```
   	
*bad:*

``` java
public class League {
   	private String mId;
   	private String mName;
   	 	
 	public String getId() {
      	return mId;
   	}

 	public void setId(String id) {
    	mId = id;
   	}

   	public String getName() {
      	return mName;
   	}

   	public void setName(String name) {
      	mName = name;
   	}
}
```  

- **Use full words**

*good:* 

    mInitalDownloadTimestamp

*bad:* 

    mInitDlTimestamp

- Try to place most important part of the name in the first or last part of the name

*good:* 

    mInitialDownloadTimestamp

*not so good:* 

    mDownloadInitialTimestamp

(important part is that this is a timestamp and it is initial one)

- **Be explicit in choosing names**

*good:*

     calculateDownloadDuration()

*not so good:* 

     duration()

### 2.2 Constants

- Always user string resources for user facing strings.
- Define all Intent extra keys, FragmentArgument keys, FragmentManager tags, "magic" values, etc as constants

*good:*

``` java
public class MyFragment extends Fragment{
	private static final String ARG_FIRST = "arg1";
	private static final String ARG_SECOND = "arg2";
	
	public static MyFragment newInstance(String arg1, int arg2){
		Bundle args = new Bundle();
		args.put(ARGS_FIRST, arg1);
		args.put(ARGS_SECOND, arg2);
		.....
	}
}
```

*bad:*

``` java
public class MyFragment extends Fragment{
	public static MyFragment newInstance(String arg1, int arg2){
		Bundle args = new Bundle();
		args.put("arg1" , arg1);
		args.put("arg2" , arg2);
		.....
	}
}
```

- Define constants into the file where they're mostly used or makes sense logically.
- Don't create specific files with loads of constants that it's not clear where they belong to
- Don't use enum when they can be replaced by constants. Use constants and make use of [Enumerated Annotations](https://developer.android.com/tools/debugging/annotations.html#enum-annotations) when possible

*good:*

``` java
	public static final int ONE = 0;
	public static final int TWO = 1;
	publci static final int THREE = 2;
```

*bad:*

``` java
	public enum Values{
		ONE(0), TWO(1), THREE(2)
	}
```

### 2.3 Use Standard Brace Style

- Avoid one line braceless conditions

*good:* 

``` java
if (condtion) {
	body();
}
```

*bad:* 

```
if	(condition)
	body()
```

*or:*

``` java 
if (condition) body();
```

### 2.4 Switch statements

- Braces should be on same line as case
- One space between the switch keyword and the open parenthesis, one space between the close parenthesis and the opening brace.
- Don't use "magic" words or numbers for each case, use always constants

*good:*

``` java
private static final int CASE_1 = 0;
private static final int CASE_2 = 1;
....

switch (expression) {
	case CASE_1:
		// code
		break;
	case CASE_2:
		// code
		break;
	default:
		// default code
}
```
*bad:*

``` java
switch (expression) {
	case 0:
		// code
		break;
	case 0:
		// code
		break;
	default:
		// default code
}
```

- Don't use the default case if it's not required

*good:*

``` java
switch (expresion) {
	case CASE_1:
		// code
		break;
	case CASE_2:
		// code
		break;
}
```

*bad:*

``` java
switch (expresion) {
	case CASE_1:
		// code
		break;
	case CASE_2:
		// code
		break;
	default:
}
```

### 2.5 Use Standard Java Annotations

- Even a single annotation should be above the annotated field/method/class

*good:*

    @Override
    public void onCrate(Bundle savedInstanceState) { ... }

*bad:*

    @Override public void onCreate(Bundle savedInstanceState) { ... }

(we want to keep method signature lines short as possible to use more explicit method names)


### 2.6 Log Sparingly

Implement or use Logger which allows filtering log calls per subsystem. It's recommended to use [Timber](https://github.com/JakeWharton/timber)

*good:*

    TabLog.e(TabLog.UI,"Cannot determine image size");

*not so good:*

    Log.e("App", "Cannot determine image size");