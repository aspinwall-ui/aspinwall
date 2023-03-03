# Coding style

The Aspinwall coding style differs somewhat from standard coding conventions. This document outlines the Aspinwall-specific coding conventions that contributors should follow when contributing to the project.

## Coding conventions

Aspinwall's code follows a handful of coding conventions, some of which differ from standard ones.

 * **Try to keep lines in the code below 80 characters.** The absolute maximum is **100 characters**.
   * If the line contains a string, move the string to a separate line (see "Splitting lines" below) and add `# noqa: E501` at the end of the line.
   * This rule does not apply to GtkTemplate .ui files; they are allowed to go over 80 lines.
 * **Make sure every function has a docstring.** The only exception to this rule are non-user-facing function like callbacks, which have their purpose clearly defined in the function name.
 * **Add a newline after each function definition.**
 * For callback functions that provide arguments you don't need to parse, only add the arguments you'll use and **add `*args` to handle the rest**.

You can also use `flake8` to automatically lint your code, which will catch some coding issues not mentioned here. A flake8 config is provided in the repo's root for convenience.

### Splitting lines

If a line is above 80 characters, it's generally reccomended to split it. For function calls, this will look something like this:

```python
# This...
lots_of_arguments(long_argument_1, long_argument_2, long_argument_3, long_argument_4, long_function(long_function_argument))
# Becomes this:
lots_of_arguments(
  long_argument_1,
  long_argument_2,
  long_argument_3,
  long_argument_4,
  long_function(long_function_argument)
)
```

If the arguments are short and can fit on one line without hitting the limit, it's generally recommended to put them on the same line. TL;DR - do what looks best and stays below 80 lines.

### .ui file conventions

 * **Keep newlines before each child definition.**
 * If an object has multiple properties that serve a similar purpose (such as positioning, labels, etc.), you can **split them into groups and add newlines in between the groups**.
 * Property names must be written with dashes (`-`), not underscores. (For example - `<property name="margin-bottom">6</property>`, NOT `<property name="margin_bottom">6</property>`.)
 * Object IDs must use underscores (`_`), not dashes.

## Linting

Linting can help catch some coding style bugs before they make it into your commits. To run the linter, install flake8:

```shell
pip install flake8
```

then run `flake8` in the main code directory.
