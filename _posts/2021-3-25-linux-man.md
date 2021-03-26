---
title: Linux man 命令
layout: posts
tags: linux
---

`man`命令是`Linux`下最核心的命令之一。而`man`命令也并不是英文单词"man"的意思，它是单词**manual**的缩写，即用手册。`man`可以列出命令完整的说明, 其内容包括命令语法、各选项的意义及相关命令。更为强大的是，不仅可以查看Linux中命令的使用帮助，还可以查看软件服务配置文件、系统调用、库函数等帮助信息。

我们先用`man man`看看它是如何介绍自己的。

```
NAME
       man - format and display the on-line manual pages
SYNOPSIS
       man [-acdDfFhkKtwW] [--path] [-m system] [-p string] [-C config_file] [-M pathlist] [-P pager] [-B browser] [-H htmlpager] [-S section_list] [sec-
       tion] name ...
DESCRIPTION
       man formats and displays the on-line manual pages.  If you specify section, man only looks in that section of the manual.  name  is  normally  the
       name  of  the manual page, which is typically the name of a command, function, or file.  However, if name contains a slash (/) then man interprets
       it as a file specification, so that you can do man ./foo.5 or even man /cd/foo/bar.1.gz.
       See below for a description of where man looks for the manual page files.
MANUAL SECTIONS
       The standard sections of the manual include:
       1      User Commands
       2      System Calls
       3      C Library Functions
       4      Devices and Special Files
       5      File Formats and Conventions
       6      Games et. Al.
       7      Miscellanea
       8      System Administration tools and Deamons
       Distributions customize the manual section to their specifics, which often include additional sections.
OPTIONS
       -C  config_file
              Specify the configuration file to use; the default is @man_config_file@.  (See man.conf(5).)
       -M  path
              Specify the list of directories to search for man pages.  Separate the directories with colons.  An empty list is the same as not  specifying -M at all.  See SEARCH PATH FOR MANUAL PAGES.
       -P  pager
              Specify  which  pager  to  use.   This  option overrides the MANPAGER environment variable, which in turn overrides the PAGER variable.  By default, man uses @pager@.
       -B     Specify which browser to use on HTML files.  This option overrides the BROWSER environment variable. By default, man uses @browser@,
       -H     Specify a command that renders HTML files as text.  This option overrides the HTMLPAGER environment variable. By default, man  uses  @html-
              pager@,
       -S  section_list
              List is a colon separated list of manual sections to search.  This option overrides the MANSECT environment variable.
       -a     By  default,  man  will exit after displaying the first manual page it finds.  Using this option forces man to display all the manual pages that match name, not just the first.
       -c     Reformat the source man page, even when an up-to-date cat page exists.  This can be meaningful if the cat page was formatted for  a  screen with a different number of columns, or if the preformatted page is corrupted.
       -d     Don’t actually display the man pages, but do print gobs of debugging information.
       -D     Both display and print debugging info.
       -f     Equivalent to whatis.
       -F or --preformat
              Format only - do not display.
       -h     Print a help message and exit.
       -k     Equivalent to apropos.
       -K     Search  for  the  specified string in *all* man pages. Warning: this is probably very slow! It helps to specify a section.  (Just to give a rough idea, on my machine this takes about a minute per 500 man pages.)
       -m  system
              Specify an alternate set of man pages to search based on the system name given.
       -p  string
              Specify the sequence of preprocessors to run before nroff or troff.  Not all installations will have a full set of preprocessors.  Some  of the  preprocessors  and  the  letters  used to designate them are: eqn (e), grap (g), pic (p), tbl (t), vgrind (v), refer (r).  This option overrides the MANROFFSEQ environment variable.
       -t     Use @troff@ to format the manual page, passing the output to stdout.  The default output format of @troff@ is Postscript, refer to the manual page of @troff@ for ways to pick an alternate format.

       Depending  on the selected format and the availability of printing devices, the output may need to be passed through some filter or another before being printed.
       -w or --path
              Don’t actually display the man pages, but do print the location(s) of the files that would be formatted or displayed.  If  no  argument  is given:  display  (on  stdout) the list of directories that is searched by man for man pages. If manpath is a link to man, then "manpath" is
       -W     Like -w, but print file names one per line, without additional information.  This is useful in shell commands like man -aW man |  xargs  ls -l

CAT PAGES
       Man  will  try  to  save the formatted man pages, in order to save formatting time the next time these pages are needed.  Traditionally, formatted versions of pages in DIR/manX are saved in DIR/catX, but other mappings from man dir to cat dir can be specified  in  @man_config_file@.   No  cat pages  are  saved when the required cat directory does not exist.  No cat pages are saved when they are formatted for a line length different from 80.  No cat pages are saved when man.conf contains the line NOCACHE.
       It is possible to make man suid to a user man. Then, if a cat directory has owner man and mode 0755 (only writable by man), and the cat files have owner  man  and  mode 0644 or 0444 (only writable by man, or not writable at all), no ordinary user can change the cat pages or put other files in the cat directory. If man is not made suid, then a cat directory should have mode 0777 if all users should be able to leave cat pages there.
       The option -c forces reformatting a page, even if a recent cat page exists.
HTML PAGES
       Man will find HTML pages if they live in directories named as expected to be ".html", thus a valid name for an HTML version of the ls(1) man  page
       would be /usr/share/man/htmlman1/ls.1.html.
SEARCH PATH FOR MANUAL PAGES
       man  uses  a  sophisticated  method of finding manual page files, based on the invocation options and environment variables, the @man_config_file@ configuration file, and some built in conventions and heuristics.
       First of all, when the name argument to man contains a slash (/), man assumes it is a  file  specification  itself,  and  there  is  no  searching involved.
       But  in  the  normal case where name doesn’t contain a slash, man searches a variety of directories for a file that could be a manual page for the topic named.
       If you specify the -M pathlist option, pathlist is a colon-separated list of the directories that man searches.
       If you don’t specify -M but set the MANPATH environment variable, the value of that variable is the list of the directories that man searches.
       If you don’t specify an explicit path list with -M or MANPATH, man develops its own path list based on the  contents  of  the  configuration  file @man_config_file@.  The MANPATH statements in the configuration file identify particular directories to include in the search path.
       Furthermore,  the  MANPATH_MAP statements add to the search path depending on your command search path (i.e. your PATH environment variable).  For each directory that may be in the command search path, a MANPATH_MAP statement specifies a directory that should be added to the search  path  for manual  page  files.   man  looks at the PATH variable and adds the corresponding directories to the manual page file search path.  Thus, with the proper use of MANPATH_MAP, when you issue the command man xyz, you get a manual page for the program that would run if you issued the command xyz.
       In  addition,  for  each directory in the command search path (we’ll call it a "command directory") for which you do not have a MANPATH_MAP statement, man automatically looks for a manual page directory "nearby" namely as a subdirectory in the command  directory  itself  or  in  the  parent directory of the command directory.
       You can disable the automatic "nearby" searches by including a NOAUTOPATH statement in @man_config_file@.
       In  each directory in the search path as described above, man searches for a file named topic.section, with an optional suffix on the section number and possibly a compression suffix.  If it doesn’t find such a file, it then looks in any subdirectories named manN or catN where N is the manual  section number.  If the file is in a catN subdirectory, man assumes it is a formatted manual page file (cat page).  Otherwise, man assumes it is unformatted.  In either case, if the filename has a known compression suffix (like .gz), man assumes it is gzipped.
       If you want to see where (or if) man would find the manual page for a particular topic, use the --path (-w) option.

ENVIRONMENT
       MANPATH
              If MANPATH is set, man uses it as the path to search for manual page files.  It overrides the configuration file and the  automatic  search path, but is overridden by the -M invocation option.  See SEARCH PATH FOR MANUAL PAGES.
       MANPL  If MANPL is set, its value is used as the display page length.  Otherwise, the entire man page will occupy one (long) page.

       MANROFFSEQ
              If  MANROFFSEQ  is  set,  its value is used to determine the set of preprocessors run before running nroff or troff.  By default, pages are passed through the tbl preprocessor before nroff.

       MANSECT
              If MANSECT is set, its value is used to determine which manual sections to search.
       MANWIDTH
              If MANWIDTH is set, its value is used as the width manpages should be displayed.  Otherwise the pages may be displayed over the whole width of your screen.

       MANPAGER
              If  MANPAGER  is set, its value is used as the name of the program to use to display the man page.  If not, then PAGER is used. If that has no value either, @pager@ is used.

       BROWSER
              The name of a browser to use for displaying HTML manual pages.  If it is not set, @browser@ is used.

       HTMLPAGER
              The command to use for rendering HTML manual pages as text.  If it is not set, @htmlpager@ is used.

       LANG   If LANG is set, its value defines the name of the subdirectory where man first looks for man pages. Thus, the command ‘LANG=dk man  1  foo’
              will cause man to look for the foo man page in .../dk/man1/foo.1, and if it cannot find such a file, then in .../man1/foo.1, where ... is a directory on the search path.

       NLSPATH, LC_MESSAGES, LANG
              The environment variables NLSPATH and LC_MESSAGES (or LANG when the latter does not exist) play a role in  locating  the  message  catalog. (But  the English messages are compiled in, and for English no catalog is required.)  Note that programs like col(1) called by man also use e.g. LC_CTYPE.
       PATH   PATH helps determine the search path for manual page files.  See SEARCH PATH FOR MANUAL PAGES.
       SYSTEM SYSTEM is used to get the default alternate system name (for use with the -m option).
BUGS
       The -t option only works if a troff-like program is installed.
       If you see blinking \255 or <AD> instead of hyphens, put ‘LESSCHARSET=latin1’ in your environment.
TIPS
       If you add the line
        (global-set-key [(f1)] (lambda () (interactive) (manual-entry (current-word))))
       to your .emacs file, then hitting F1 will give you the man page for the library call at the current cursor position.
       To get a plain text version of a man page, without backspaces and underscores, try
         # man foo | col -b > foo.mantxt
AUTHOR
       John W. Eaton was the original author of man.  Zeyd M. Ben-Halim released man 1.2, and Andries Brouwer followed up with versions  1.3  thru  1.5p.
       Federico Lucifredi <flucifredi@acm.org> is the current maintainer.

SEE ALSO
       apropos(1), whatis(1), less(1), groff(1), man.conf(5).

                              September 19, 2005                        man(1)

```

man是按照手册的章节号的顺序依次进行搜索的，比如：
```
man sleep
```

只会显示sleep命令的手册, 因为sleep命令在手册的第一章, 如果想查看库函数sleep，就要输入:

```
man 3 sleep
```

```
 apropos(1), whatis(1), less(1), groff(1), man.conf(5).
 这些后面的数字就是所在章节
```