# Commit style

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

## Module/submodule reference

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

In addition, each project has its own modules/submodules; see the respective COMMIT_STYLE.md files in those repositories for more information.
