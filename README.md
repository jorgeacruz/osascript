# Osascript

Execute AppleScripts and other OSA language scripts. 
Executes the given script file, or standard input if none is given. Scripts can be plain text or compiled scripts. osascript was designed for use with AppleScript, but will work with any Open Scripting Architecture (OSA) language.

## Syntax
   osascript [-l language] [-e command] [-s flags] [programfile]

### Key:
   
   -e command
   
  Enter one line of a script.  Multiple -e commands can be given to build up a multi-line script.
  If -e is given, osascript will not look for a filename in the argument list.
  Because most scripts use characters that are special to many shell programs
  (e.g., Apple-Script uses single and double quote marks, (, ), and *), the command
  will have to be correctly quoted and escaped to get it past the shell intact.

   -i
  
  Interactive mode: osascript will prompt for one line at a time, and output the result, if applicable,
  after each line. Any script supplied as a command argument using -e or programfile will be loaded,
  but not executed, before starting the interactive prompt. 

   -l language
      
  Override the language for any plain text files.  Normally, plain text files are compiled as AppleScript.

   -s flags
     
  Modify the output style.  The flags argument is a string consisting of any of the
  modifier characters e, h, o, and s. 
  Multiple modifiers can be concatenated in the same string, and multiple -s options can be specified.

  The modifiers come in exclusive pairs;
  if conflicting modifiers are specified, the last one takes precedence.
  The meanings of the modifier characters are as follows:

        h  Print values in human-readable form (default).
        s  Print values in recompilable source form.

  osascript normally prints its results in human-readable form:
  strings do not have quotes around them, characters are not escaped,
  braces for lists and records are omitted, etc.  This is generally more useful, but can
  introduce ambiguities.  For example, the lists '{"foo", "bar"}' and '{{"foo", {"bar"}}}' would
  both be displayed as 'foo, bar'.  

  To see the results in an unambiguous form that could be recompiled into the same value, use
  the s modifier:

        e  Print script errors to stderr (default).
        o  Print script errors to stdout.
  
  osascript normally prints script errors to stderr, so downstream clients only see valid results. When running automated tests, however, using the o modifier lets you distinguish script errors, which you care about matching, from other      diagnostic output, which you don’t.




# Command
Shut down without showing a confirmation dialog:
```
osascript -e 'tell app "System Events" to shut down'
```

Shut down after showing a confirmation dialog:
```
osascript -e 'tell app "loginwindow" to «event aevtrsdn»'
```

Restart without showing a confirmation dialog:
```
osascript -e 'tell app "System Events" to restart'
```

Restart after showing a confirmation dialog:
```
osascript -e 'tell app "loginwindow" to «event aevtrrst»'
```

Log out without showing a confirmation dialog:
```
osascript -e 'tell app "System Events" to  «event aevtrlgo»'
```

Log out after showing a confirmation dialog:
```
osascript -e 'tell app "System Events" to log out'
```

Go to sleep (pmset):
```
pmset sleepnow
```

Go to sleep (AppleScript):
```
osascript -e 'tell app "System Events" to sleep'
```

Put displays to sleep (10.9 and later):
```
pmset displaysleepnow
```

Open or switch to Safari:

```
$ osascript -e 'tell app "Safari" to activate'
```
Close safari:
```
$ osascript -e 'quit app "safari.app"'
or
$ osascript -e ‘tell application “safari” to quit’
```
Empty the trash:
```
$ osascript -e 'tell application "Finder" to empty trash'
```
Set the output volume to 50%:
```
$ sudo osascript -e 'set volume output volume 50'
```
Input volume and Alert volume can also be set from 0 to 100%:
```
$ sudo osascript -e 'set volume input volume 40'
$ sudo osascript -e 'set volume alert volume 75'
```
Mute the output volume (True/False):
```
$ osascript -e 'set volume output muted TRUE'
```
Toggle volume muting:
```
$ osascript -e 'set volume output muted not (output muted of (get volume settings))'
```
Toggle system theme:
```
$ osascript -e 'tell application "System Events" to tell appearance preferences to set dark mode to not dark mode'
```
