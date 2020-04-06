# Searching for a file

```bash
# Find files by case-insensitive extension, such as `.jpg`, `.JPG`, & `.jpG`).
# By default, find(1) uses glob pathname pattern matching. To avoid shell
# interpretation, the glob either must be expanded or the string quoted.
find . -iname '*.jpg'

# Find directories.
find . -type d

# Find files. Specifically files; not directories, links, FIFOs, etc.
find . -type f

# Find files set to the provided octal mode (permissions).
find . -type f -perm 777

# Find files with setuid bit set, keeping to the same filesystem.
find . -xdev \( -perm -4000 \) -type f -print0 | xargs -0 ls -l
# The above is a useful demonstration of some pitfalls into which a user can
# fall, where the below is the above but corrected. Here is why:
#
#   * The `.` (current working directory) is assumed when no path is provided.
#   * Group syntax (parentheses) was used, but nothing was actually grouped.
#   * A lot of people have their ls(1) command aliased in many ways, -
#     potentially causing problems with the output and how xargs(1) handles it.
#     By escaping the command, we temporarily override any aliases and even
#     functions by the same name.
#   * At least in my experience, the prior xargs(1) is not as reliable.
#   * The `-print0` and `xargs -0` is great, but unnecessary (except when?).
#
# However, it might be more preferred to simply use find(1)'s own `-printf`
# flag, in order to avoid the need for xargs(1) and ls(1), which should be many
# times faster, and allows for more specificity.
find -perm -4000 -type f -print0 | xargs -I '{}' -0 \ls -l '{}'

# Find and remove files with case-senstive extension of `.txt`.
find [PATH] -name '*.txt' -exec rm '{}' \;
# The above is much more efficiently written as shown below, as find(1) has its
# own built-in delete function, not to mention a single rm(1) process was
# previously executed for each file processed, which is comparatively slow.
find [PATH] -name '*.txt' -delete

# Find files with extension '.txt' and look for a string into them.
find ./path/ -name '*.txt' | xargs grep 'string'

# Find files with size bigger than 5 Mb and sort them by size.
find . -size +5M -type f -print0 | xargs -0 ls -Ssh | sort -z

# Find files bigger thank 2 MB and list them.
find . -type f -size +20000k -exec ls -lh {} \; | awk '{ print $9 ": " $5 }'
# Alternative, faster approach* to the above.
#
# Why it's faster:
#
#   * No need for an external process, like ls(1).
#   * The use of `;` with the `-exec` flag executes an ls(1) process for each
#     file found, which is comparatively very slow.
#   * The `printf` feature is built in and special to awk(1).
#
# That said, awk(1) or gawk(1) is doing a little more here, in order to get
# somewhat of a human-readable file size, but its impact is likely negligible.
find -type f -size +20000k -printf '%s %P\n' |
    awk "{printf(\"%'dM %s\n\", \$1 / (1024 * 1024), \$2)}"

# Find files modified more than 7 days ago and list file information.
find . -type f -mtime +7d -ls

# Find symlinks owned by the given user, then list file information.
find -type l -user [NAME] -ls
# The following may be the syntax used on a Mac, however this is not valid on
# Linux, or at least version 4.7.0. All flags in GNU find(1) are one `-` only.
find . -type l --user=[NAME] -ls

# Search for and delete empty directories.
find . -type d -empty -exec rmdir {} \;
# A far more efficient approach to the above. If no path is provided, then the
# current working directory (CWD) is assumed, making the `.` superfluous.
find -type d -empty -delete

# Search for directories named `build` at a maximum depth of 2 directories.
# This means that find will not recursively search beyond two levels.
find . -maxdepth 2 -name build -type d

# Search all files which are not in a `.git` directory. Depending on the shell
# used, the bang (`!`) may need to be escaped, to avoid shell interpretation.
# Alternatively, although non-POSIX, the `-not` flag can be used.
find . \! -iwholename '*.git*' -type f

# Find all files that have the same inode (indicating hard link) as FILE. All
# output going to STDERR (typically error messages) will also be redirected to
# `/dev/null`, a special pseudo-file where data is sent to die.
find . -type f -samefile [FILE] 2>/dev/null

# Find all files in the current directory and modify their permissions.
find . -type f -exec chmod 644 {} \;

# Find files with extension `.txt` and edit all of them with vim(1).
#
# The use of `+` (escaped to avoid shell interpretation) with `-exec` means
# that only one process (in this case, `vim`) per `exec`ution is used. If `;`
# is instead used (would also need escaping), then one `vim` process would be
# used per file.
find . -iname '*.txt' -exec vim {} \+

# Find files with extension `.png`, then rename their extension to `.jpg`. It's
# highly important that `\;` is used here, instead of `\+`, otherwise it'd make
# a right mess of the files, due to the way in which mv(1) works.
find . -type f -iname '*.png' -exec bash -c 'mv "$0" "${0%.*}.jpg"' {} \;

# Use logic and grouping to delete extension-specific files.
find \( -iname "*.jpg" -or -iname "*.sfv" -or -iname "*.xspf" \) -type f -delete

# List executable files, by basename, found within PATH.
find ${PATH//:/ } -type f -executable -printf "%P\n"
```
