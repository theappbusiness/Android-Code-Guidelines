***This document is under construction***

# Android Coding Guidelines Android

## 1. Project structure

New projects should follow the Android Gradle project structure that is defined on the [Android Gradle plugin user guide](http://tools.android.com/tech-docs/new-build-system/user-guide#TOC-Project-Structure).

### 1.1 Package structure

It's recommended to structure in the following way:

    mainpackage
     * homescreen 			// 1.1.1. Activity level
	    * category 		// 1.1.2 Feature of the activity
            * di		// 1.1.3 Dependency Injection
            * presenter	// 1.1.4 Presentation layer
            * repository	// 1.1.5 Repository layer
            * navigator	// 1.1.6 Navigator layer
        * search
            * di 
            * presenter
            * repository
            * navigator

#### 1.1.1 Activity level 

Activity providing a context for multiple features

#### 1.1.2 Feature level

Feature level encapsulates all packages and classes required for delivering specific feature.

#### 1.1.3 Injection

Injection package will contain all components, modules, qualifiers and scopes used by this feature. If this feature requires more elaborate injection it is worth to split the package further by role 

	* components
	* modules
	* scopes
	* qualifiers

#### 1.1.4 Presenter

Presentation layer will contain interface and implementation(s) of view logic

#### 1.1.5 Repository

Repository package will encapsulate all interfaces and logic around requesting data from external and internal sources. It may contain packages e.g.

	* parsers
	* models
	* handlers

#### 1.1.6 Navigator

Navigator interface defines all navigational operations that can be performed on Fragments/Activity inside this Activity. e.g.

    public interface HomeSearchNavigator {
        void onFixedSearch(String search);
	void onRawSearch(String search);
	void onOpenSettings();
	void onExit();
    }

Implementation will handle creation of intents and dispatching them.


## 2. Coding Style

We are migrating from AOSP (Android Open Source Project) code guidelines to Google Java Style which can be found here

[Google Java Style](https://google.github.io/styleguide/javaguide.html)


