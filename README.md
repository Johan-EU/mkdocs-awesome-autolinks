# mkdocs-awesome-autolinks

The MkDocs Awesome Autolinks plugin makes it possible to link to pages and images without specifying the full relative path. In addition, to ease using the file structure to generate navigation, it will remove a configurable part from the directory and page file name that can be used to order the navigation and page structure.<br>
As a result the part of directory and page names that is used to order pages does not have to be included in links and will not show in the URLs of the built site. Otherwise links would break when the page order is changed and the part used for sorting would clutter the site URLs.

This plugin has been built to be used in combination with the 
[Awesome Pages plugin][awesome-pages] that allows [combination of custom navigation with file
structure][combine-nav-filestructure]. Hence the awesome in the name of this plugin.
Tough there is no relation with or dependency on the Awesome Pages Plugin.

The functionality to remove a part of file and directory names can be disabled in `mkdocs.yml` and
the autolink functionality will continue to work.

[awesome-pages]: https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin
[combine-nav-filestructure]: https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin#combine-custom-navigation--file-structure

## Installation

> **Note:** This package requires Python >=3.7 and MkDocs version 1.4 or higher.  

Install the package with pip:

```bash
pip install mkdocs-awesome-autolinks
```

Enable the plugin in your `mkdocs.yml`:

```yaml
plugins:
    - awesome-autolinks
```

Configuration of the plugin is possible but not necessary if the default behavior suits your need.

## Usage
More information will be provided in the future. Here is a short summary of how the
automatic linking can be used.

* The default pattern for the sorting part of directory and file names is that the start
of each file/directory name contains numbers followed by a `-`. For example `010-about.md` or
in case of a file in a directory `100-examples/010-about.md`.<br>
There is no limit to the amount of numbers.
* Instead of specifying the full relative path in a link only include the file name. From here on
it will be called a *short link*. An example of a short link is
`[About](about.md)`. This plugin will replace `about.md` with the relative path to the page file.
Normal MkDocs processing will transform the Markdown link with relative path to HTML.
* In case there is a short link on a page but there are multiple files in the whole docs directory
with the file name of that short link a warning will be logged but this depends of the `warn_less` 
setting. If `warn_less` is true, the default, a warning is only logged if there is no file with the
same name in the same directory branch or if there are multiple files with the same name in the same 
directory branch.<br>
So it is safe to have link `[About](about.md)` on a page if file `about.md` is located somewhere in
a subdirectory of the directory where the page with the short link is located. Even if there are
other `about.md` files in other directory branches, as long as they can only be reached by going
higher up in the directory tree (do a ../ first).
* Some page file names are very common. Instead of forcing unique file names the directory
the file is located in can be included in the short link. For example `[Subject A](subject-a/index.md)`.
* Normal relative links such as `[Subject A](../subjects/subject-a/index.md)` can still be used.
Configuration setting `warn_on_no_use` will determine whether a warning will be logged about not
using the autolink functionality.
* Removal of a part from the directory and page file names can be disabled by setting
`remove_re` to an empty string.



## Configuration

The following configuration options can be set in `mkdocs.yml`. Values shown here are the default.

``` yaml
plugins:
  - awesome-autolinks:
      remove_re: '^[0-9]+-'
      warn_less: true
      warn_on_no_use: true
      ignore_dirs:
        - css
        - fonts
        - img
        - js
        - search
      debug: false
```
