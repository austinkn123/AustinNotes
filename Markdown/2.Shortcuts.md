# Shortcuts

VSCode extensions: Prettier - Auto Rename Tag - x

## VSCode

`Ctrl K S` view keyboard shortcuts

`Ctrl P` search for a file

`Ctrl Shift P` view commands

`Ctrl ,` settings

`Ctrl \` split editor

`Ctrl Shift \` jump to matching bracket

`Ctrl ~` open terminal

`F11` fullscreen

`Ctrl /` toggle line comment

`Alt L O` open Live Server



`Ctrl X` cut line or selection

`Ctrl C` copy line or selection

`Ctrl V` paste line or selection

`Ctrl D` select next occurrence of the current selection

`Ctrl G` go to line

`F12` go to (variable) definition

`Shift F12` show all references (to variable)

`Alt F12` open (variable) definition in a new editor



`Ctrl .` quick fix/refactor suggestions (for selected)

`Ctrl space` trigger intellisense/code completion

`Alt up/down` move line up/down

`Ctrl Enter` insert line below

`Ctrl Shift Enter` insert line above

`Ctrl Shift up/down` add curser above/below



`Fn <-- -->` jump to beginning/end of line

`Fn Shift <-- -->` highlight left/right

`Ctrl <-- -->` jump to beginning/end of word

`Ctrl Shift <-- -->` highlight word

NEXT: Basic Editing



`Ctrl Alt U` compare file to HEAD commit



Debugging Node:

`F5` start debugger

`F9` toggle breakpoint

`F10` step over

`F11` step into

`Shift F11` step out



## Visual Studio

`Ctrl + '` = switch to integrated terminal

`Ctrl + Tab` = switch to editor window

edit shortcuts: Tools > Options > Keyboard



## Chrome

`Alt Shift D` - toggle dark mode (toggle Dark Reader chrome extension on/off)



`Ctrl N` - new window

`Ctrl Shift N` - new incognito window

`Ctrl T` - new tab

`Ctrl Shift T` - reopen previously closed tab



`Ctrl Tab` - cycle through tabs (forward)

`Ctrl Shift Tab` - cycle through tabs (backward)

`Ctrl 1` through `8` jump to a specific tab

`Ctrl 9` jump to the last tab



`Fn <-- -->` jump to beginning/end of page

`Alt <-- -->` go back/forward



`Ctrl click` on a link to open in a new tab



`Ctrl D` save current webpage as bookmark

`Ctrl H` view history

`Ctrl J` view downloads

`Ctrl L` highlight the URL

`Ctrl U` view source code

`Ctrl R` refresh page

`Ctrl Shift R` refresh page, without using cache (complete and fresh reload from the server)



`Ctrl 0` return to default zoom



`Ctrl W` close current tab

`Ctrl Shift W` close current window



NEXT: Google Chrome feature shortcuts

Custom: chrome://extensions/shortcuts



## Chrome DevTools

`Ctrl Shift C` open the Elements panel

`Ctrl Shift J` open the Console panel

`Ctrl Shift I` close DevTools

`Ctrl R` refresh page (chrome)

`Ctrl Shift R` refresh page, without using cache (complete and fresh reload from the server)

`Ctrl Shift I` open the last-used panel

`Esc` open the 'drawer'

`Ctrl ]` next panel

`Ctrl [` previous panel

`Ctrl Shift M` toggle Device Mode

`Ctrl Shift D` move DevTools to the last-used dock position



`Ctrl F` search for text within current panel

`Ctrl Shift F` search for text across all loaded resources



`Ctrl Shift P` commands >

`Show Changes` show the changes you've made to CSS and JS files in this DevTools session (does not show HTML changes)

`Show Coverage` show an overview of how much CSS or JavaScript is used from each file that the browser loads (green = used, red = unused) you can click on a file to view a breakdown of what CSS/JS is used in the current page print



`?` Settings > Shortcuts tab



`H` hide the currently-selected element



when a CSS style value is selected.. for example `padding: 10px;` and `10px` is selected..

`Alt Up` increment by `0.1`

`Up` increment by `1`

`Shift Up` increment by `10`

`Ctrl Up` increment by `100`



any changes to CSS will be highlighted green (bc of Settings > Experiments > Sync CSS changes in the Styles Pane) and you can..

`right click` anywhere in the Styles Pane > Copy all CSS changes



`Ctrl` + click on a style in the Styles Pane takes you to that line in the CSS file



NEXT: Sources panel keyboard shortcuts



## Typora

`Ctrl ,` settings

`Ctrl Shift L` toggle sidebar

`Ctrl Shift 1` toggle outline

`Ctrl Shift 3` toggle file tree

`Ctrl F` search (in current note)

`Ctrl Shift F` search (in current folder)



`Ctrl /` view source code

`Ctrl K` hyperlink

`Ctrl Shift I` image



`Ctrl +` increase heading level

`Ctrl -` decrease heading level



`Ctrl L` select line / sentence

`Ctrl Shift V` paste as plain text

`Ctrl Shift C` copy as Markdown



## Windows





## Ubuntu

`Super` display all open windows (Activities Overview) - also from here you can search files, apps, and more

`Super Tab` switch between open windows

`Super '` switch between windows of the same application

`Super Shift ↑↓` move current window to monitor above/below



`Ctrl Alt T` open a terminal window

`Ctrl W` close the current file, folder, or (usually) application



`PrtScr` screenshot entire screen - automatically saved to `~/Pictures` directory

`Alt PrtScr` screenshot current window

`Shift PrtScr` select area to screenshot

`Shift Ctrl Alt R` start/stop screen recording - automatically saved to `~/Videos`



## Bash and the GNOME Terminal

**Keyboard Shortcuts**..

`F11` fullscreen

`Fn <-- -->` move cursor to beginning/end

`Ctrl A` move cursor to beginning

`Ctrl E` move cursor to end

`Ctrl <-- -->` move cursor to next word

`Ctrl U` delete left of cursor

`Ctrl K` delete right of cursor

`Ctrl Shift T` open new tab

`Ctrl Shift W` close current tab

`Ctrl (Fn) Pageup/Pagedown` switch between tabs

`Ctrl Shift N` open new window

`Ctrl Shift Q` close current window

`Ctrl R` search command history



WHEN `foo` is a **bash command**..

`help` list common commands and their syntax

`whatis foo`

`foo --help`

`man foo` --> use `/` to search

`tldr foo` a simplified version of `man` with practical examples

`apropos foo`

`man 8 foo`



**Search for directories or files (search paths)**

`locate <string>` after `updatedb` will search *all* paths for *string*

`?` represents any single character

`*` represents zero or more characters

`locate <string> | grep <string>`

`find` returns every path in the pwd

`find | grep <string>`

`fzf` is like `find` - displays all paths in the pwd - but also allows interactive searching - THIS

`fzf -q <string>` - start `fzf` by already searching for *string*

see SEARCHING in Linux notes for more info



**Search within files**

`grep`

*grep does not search file/directory names (only file *contents*)

*grep **does not** search **recursively** by default

`grep <string> foo.txt` search for *string* in foo.txt

`grep <string> *` search for *string* in all files in pwd

`grep -r <string> *` search recursively for *string* in pwd



`ack` 

*ack does not search file/directory names (only file *contents*)

*ack **does** search **recursively** by default

*ack will exclude files it finds to be logically irrelevant to the developer (for example ack excludes .gitlog files)

`find . | wc -l` list total number of files/directories in `.`

`ack -f | wc -l` list number of files `ack` will search the contents of

`ack -f` list the files `ack` will search the contents of

`ack -f --html` list all `html` files ack finds relevent

`ack <string>` search for *string* in all files in the pwd

`ack -w <string>` search for *string* where *string* is a complete word (not surrounded by any other letters)

`ack --html <string>` search for *string* but only in `html` files (also `css` `js` `python` `md` `txt` etc)

*pipe output into `less` if it is a lot



`Ctrl Z` send nano to background

`fg` bring back to foreground



`cd -` previous directory

`ls` display contents of current working directory (sorted alphabetically)

`ls -a` show all (hidden) files/directories

`ls -d` show only directories

`ls -l` show permissions, number of hard links, owner, group owner, file size in **bytes**, last modified, and file/directroy name

*number of hard links can be confusing - it's not necessarly ones you have created with `ln` - don't worry about it

`ls -l -t` sort by most recent first - use `-r` to reverse the sort order

`ls -l -h` show human readable file sizes - use `-S` to sort by size (largest first)

Bit - smallest fundamental size of data storage - a binary digit - 1/8 of a byte

B byte = 8 bits - stores a string of eight 1's or 0's - the byte is the smallest unit for the base 1,024 naming system - **if no unit is displayed** in Linux -> the unit is **bytes**



K kibibyte = 1,024 bytes (2^10 bytes) = roughly 1 Kilobyte

M mebibyte = 1,048,576 bytes (2^20 bytes) = roughly 1 Megabyte

G gibibyte = 1,073,741,824 bytes (2^30 bytes) = roughly 1 Gigabyte

T tebibyte = 1,099,511,627,776 bytes (2^40 bytes) = roughly 1 Terabyte



KB kilobyte = 1,000 bytes (10^3 bytes) one thousand bytes

MB megabyte = 1,000,000 (10^6 bytes) one million bytes

GB gigabyte = 1,000,000,000 (10^9 bytes) one billion bytes

TB terabyte = 1,000,000,000,000 (10^12 bytes) one trillion bytes



`xdg-open` open file(s) with default program



`ps` display currently active processes

`top` display all running processes

`htop` a newer version of `top` - is better

`kill pid` kill process with ID `pid`

`xkill` allows you to select with your mouse, the window to kill

or open System Monitor and right click > kill

`bg` list stopped or background jobs

`df` list system storage usage

`pydf` is a colorized version of `df` - list system storage usage



NEXT: System Info



## Bash Tricks

#### Wget

easily download files using a variety of different protocols

will download to the pwd..

`wget https://download.com/file.zip`

you can also create a text file..

`gedit wget-downloads.txt` containing a list of files to download

`wget -i ./wget-downloads.txt` the i option stands for 'input file'



#### Download a file/folder from GitHub

use `svn` (subversion) which has many other options other than `export`

use `svn help` to learn more



first let's see what's in the remote with..

`svn ls URL.git`

for example..

`svn ls https://github.com/parktart/odin-recipes.git`



from there we can choose a branch for example..

`svn ls https://github.com/parktart/odin-recipes.git/trunk`



and continue to find the file/folder we want..

then we use..

`svn export <path>` to download the file/folder



if the file/folder is not on trunk (main)..

`svn export URL.git/branches/<branch_name>/<folder>`



for a specific tagged commit..

`svn export URL.git/tags/<tag_name>/<folder>`



**note** if there are special characters (like spaces) in the path then you must replace them with the correct URL encoding

for example replace a space with `%20`



#### Copy standard output

`cat foo.txt | xclip - selection clipboard` copy the contents of `foo.txt` to your clipboard



#### Compare files

`icdiff left_file right_file`

options..

`-N, --line-numbers` show line numbers

`-r, --recursive` recursively compare subdirectories

`-s` report when two files are the same



`code --diff left_file right_file` will compare them in VSCode



#### Fig autocomplete utility

https://fig.io/user-manual/linux#supported-distros

is in beta > did not install through `apt` > see above link to **uninstall**

if having **issues** with `fig` --> run `fig doctor` to debug it --> after that see above link

UNINSTALLED (didn't work well yet)



#### Merge PDF Files

`pdfunite` is part of the the `poppler-utils` package..

`sudo apt install poppler-utils`

`pdfunite file1.pdf file2.pdf merged_output.pdf`

ignore the errors

note: files to be merged need to be in the same directory that `pdfunite` is executed

