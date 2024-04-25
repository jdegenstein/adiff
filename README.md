# adiff - wordwise diff

adiff - wordwise diff
This tool is a replacement for GNU wdiff that provides the ability to generate context and unified diffs based on the wordwise diff. It's written in Perl instead of C, so it's both shorter and slower. It doesn't have as many options as wdiff, but it provides some others.

You can find the man-page here or you can generate it from the embedded pod in adiff.

## Example
Consider the standard placeholder text:

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis
nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu
fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
culpa qui officia deserunt mollit anim id est laborum.
Let's remove a few words near the top and add a few words near the bottom, then look at a unified diff:

`$ diff -u 1.txt 2.txt`
```diff
@@ -1,6 +1,6 @@
 Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
-incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis
-nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
-Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu
-fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
-culpa qui officia deserunt mollit anim id est laborum.
+incididunt ut labore. Ut enim ad minim veniam, quis nostrud exercitation ullamco
+laboris nisi ut aliquip ex ea commodo consequat.  Duis aute irure dolor in
+reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
+Excepteur foo bar baz quux sint occaecat cupidatat non proident, sunt in culpa
+qui officia deserunt mollit anim id est laborum.
```

That isn't very helpful. Here's the adiff unified output:

`$ adiff -u 1.txt 2.txt`
```udiff
@@ -1,6 +1,6 @@
 Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
-incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco
+incididunt ut labore. Ut enim ad minim veniam, quis nostrud exercitation ullamco
 laboris nisi ut aliquip ex ea commodo consequat.  Duis aute irure dolor in
 reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
-Excepteur sint occaecat cupidatat non proident, sunt in culpa
+Excepteur foo bar baz quux sint occaecat cupidatat non proident, sunt in culpa
 qui officia deserunt mollit anim id est laborum.
```
And here's the standard adiff output which mimics wdiff output:

`$ adiff 1.txt 2.txt`
```diff
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
incididunt ut [-labore et dolore magna aliqua.-]{+labore.+} Ut enim ad minim veniam, quis nostrud exercitation ullamco
laboris nisi ut aliquip ex ea commodo consequat.  Duis aute irure dolor in
reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
Excepteur {+foo bar baz quux+} sint occaecat cupidatat non proident, sunt in culpa
qui officia deserunt mollit anim id est laborum.
```

## Downloads
```
Filename	Date                    Size	MD5
adiff-1.4	11-Dec-2007 14:11	10.6K	e9b710985a9d1831d366393515ff1b50
adiff-1.3	21-Jun-2007 04:38	10.1K	17aac1756d8233f9f50874e9922af009
adiff-1.2	15-Aug-2005 11:33	9.9K	7f802ef3f3cb638767f554dcac860e72
```

## adiff with subversion

The main reason I wrote adiff was so I could get meaningful diff mails from subversion when Word documents are checked in. To make this happen, I tie together run-mailcap, antiword and adiff. Since it uses run-mailcap, the system should work for arbitrary binary files.

