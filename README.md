****This document is under construction****

**Android Coding Guidelines**

At TAB we follow Android Code Style guidelines

https://source.android.com/source/code-style.html#follow-field-naming-conventions

On top of rules listed there we have few extra rules and exceptions:

Follow Field Naming Conventions
- Do NOT use m or s prefix in fields inside POJO (models, events)
*good:* 
    public class LoginEvent {
        private boolean success;
        
        public LoginEvent (boolean success) {
          this.success = success;
        }
   
        public boolean getSuccess() {
          return success;
        }
    }

*bad:*
    public class LoginEvent {
      private boolean mSuccess;
      
      public LoginEvent (boolean success) {
        mSuccess = success;
      }
   
      public boolean getSuccess() {
        return mSuccess;
      }
    }

- Use full words

*good :* mInitalDownloadTimestamp

*bad :* mInitDlTimestamp

- Try to place most important part of the name in the first or last part of the name
good: mInitialDownloadTimestamp
not so good: mDownloadInitialTimestamp
(important part is that this is a timestamp and it is initial one)
- be explicit in names
good: calculateDownloadDuration()
not so good: duration()
(we use obfuscation so there is no harm done in long names)

Use Standard Brace Style
- Avoid one line braceless conditions
bad: if (condition) body();

Use Standard Java Annotations
- Even a single annotation should be above the annotated field/method/class

good:
@Override
public void onCrate(Bundle savedInstanceState) {

bad:
@Override public void onCreate(Bundle savedInstanceState) {

(we want to keep method signature lines short as possible to use more explicit method names)


Log Sparingly
Implement or use Logger which allows filtering log calls per subsystem
good:
TabLog.e(TabLog.UI,"Cannot determine image size");
not so good:
Log.e("Cannot determine image size");
