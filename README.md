# repo-stylelint-configbasedir-problem
Demo of StyleLint bug Stylelint(CssSyntaxError) when configBasedir path has lower-cased drive letter and/or backward slashes

Clone this repo using Windows OS to e.g. "C:/foo/repo-stylelint-configbasedir-problem".

Run `cd "C:/foo/repo-stylelint-configbasedir-problem" && npm install`.

In `.vscode/settings.json` set `stylelint.configBasedir` to `C:/foo/repo-stylelint-configbasedir-problem`.

Open folder `C:/foo/repo-stylelint-configbasedir-problem` in VSCode, open file test.html
and StyleLint works OK when you use upper-cased.

Now try to change `configBasedir` to one of:

 * 1.) Relative path

`"stylelint.configBasedir": ".."`

When debugged `configBasedir` in https://github.com/stylelint/stylelint/blob/6df74ebf70ede758049bb07d3550abf87478a2ef/lib/standalone.js#L93
it was automatically converted probably  by https://github.com/stylelint/vscode-stylelint to `c:\foo\repo-stylelint-configbasedir-problem` which
is unfortunately not working/valid for https://github.com/stylelint/stylelint see below 2.) and 3.).

 * 2.) Absolute path with lower-cased drive letter and forward slashes

`"stylelint.configBasedir": "c:/foo/repo-stylelint-configbasedir-problem"`

 * 3.) Absolute path with upper-cased drive letter and backward slashes

`"stylelint.configBasedir": "C:\\foo\\repo-stylelint-configbasedir-problem"`

For each of above you will see:
`Unknown word (CssSyntaxError) Stylelint(CssSyntaxError)`

The only one path which is working is with upper-cased drive letter and forward slashes.
