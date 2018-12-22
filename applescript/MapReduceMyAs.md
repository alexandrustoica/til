#### AppleScript Map Reduce My As


Some things I learned about AppleScript while creating a small script for OmniFocus:

You cannot use a functional operator such as `map` on AppleScript’s standard list; you have to implement it yourself.

```applescript
on map(f, theData)
  global ff
  set ff to f
  set theResult to {}
  repeat with anItem in theData
    set end of theResult to ff(anItem)
  end repeat
  return theResult
end map
```

You can execute shell scripts to cut, replace or find substrings in a given text. To convert one type to another, you have to use `Y as X`, just like in Kotlin or Swift.

```applescript
on cutStoryPointChar(x)
  return (do shell script "echo " & x & " | cut -c -1" ) as number
end cutStoryPointChar
```

If you want to call your functions from our local script you have to use `my` as a keyword in front of your call. 

```applescript
tell application "OmniFocus"
  tell content of first document window of front document
    set selectedTags to name of (tags of value of selected trees) whose name ends with "🔸"
    set storyPoints to my map(my cutStoryPointChar, selectedTags)
    set sum to 0
    repeat with storyPoint in storyPoints
      set sum to sum + storyPoint
    end repeat
    display dialog sum
end tell
```

You don’t have other functional operators such as reduce to accumulate the ∑ of our list’s elements; you have to manually iterate your list using `repeat with x in xs`.