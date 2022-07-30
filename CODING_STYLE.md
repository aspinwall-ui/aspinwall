# Coding style

The Aspinwall coding style differs somewhat from standard coding conventions. This document outlines the Aspinwall-specific coding conventions that contributors should follow when contributing to the project.

## Commit style

Commits follow the following format:

```
module: submodule: short commit description

Long-form description.
```

The module and submodule are dictated by which part of the code you're modifying - see the reference section below. If you're modifying multiple parts of the code, they should be set to the part of the code which the commit primarily concerns.

Adding the `submodule:` is recommended, but not always required. If the commit summary already explains what element it concerns, the submodule can be omitted.

The short commit description **must be lowercase**, except for **names of objects** (like GtkBox, etc.); this capitalization rule doesn't apply to paraphrased names (like "widget box" instead of WidgetBox).

For larger features spanning multiple points, try to roll up your changes into multiple commits. A good rule of thumb is to make sure that a single commit is no larger than ~150 lines (excluding translation updates and new file additions).

If your commits don't follow these rules, you may be asked to re-make them during the review process.

### Module/submodule reference

Depending on the part of the code you're modifying, you'll want to include a different module in your commit summary. Refer to the following list to get the appropriate module/submodule for the part of the project that you're modifying.

The first level of the list shows modules, subpoints in the list show the module paired with submodules. **Modules and submodules from different points must not be mixed together.**

For more information on how to properly use them, see the above paragraphs.

 * `meta:` - README, CI, repo configuration, build system tweaks and other project management tasks.
   * `meta: code-quality:` - minor quality fixes in multiple places around the code; usually used for bulk linter issue fixes
 * `docs:` - everything in the `docs` directory. **Does not apply to other types of documentation, code comments etc.** - in most cases, for commits that clean up code and add comments you'll want to use `meta: code-quality:`.
 * `lang:` - everything in the `po` directory.
 * `tests:` - everything in the `tests` directory, as well as the `run-tests` script.
 * `widgets:` - everything in the `widgets` directory.

 * `data:` - used for everything in the `data` directory, except for the stylesheets. **This is used very rarely**; if you're adding a config option, it's better to simply include the config option addition alongside other changes you're making.
 * `stylesheets:` - everything in the `data/stylesheets` directory.

 * `launcher:` - everything in the `src/launcher` directory.
   * The submodule is derived from the name of the file you're working on, but with underscores (`_`) replaced with dashes (`-`). There are a few notable exceptions:
     * Commits to `launcher_boxes.py` are split into `launcher: widget-box:` and `launcher: clock-box:` based on which object you're modifying.
 * `widget-backend:` - everything in the `src/widgets` directory.
 * `utils:` - everything in the `src/utils` directory.

## Coding conventions

Aspinwall's code follows a handful of coding conventions, some of which differ from standard ones.

 * **Tabs are used for indentation.** This applies both to Python code and GtkTemplate .ui files.
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
