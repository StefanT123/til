# Last Commit A File Appeared In

If you have a `README.md` file that you haven't modified in a while. If you want to see the last commit that modified it:
```bash
git log -1 -- README.md
    commit 6da76838549a43aa578604f8d0eee7f6dbf44168
    Author: jbranchaud <jbranchaud@gmail.com>
    Date:   Sun May 17 12:08:02 2015 -0500

        Add some documentation on configuring basic auth.
```

This same command will even work for files that have been deleted if you know the path and name of the file in question:
```bash
git log -1 -- some-deleted-file
    commit 0bb1d80ea8123dd12c305394e61ae27bdb706434
    Author: jbranchaud <jbranchaud@gmail.com>
    Date:   Sat May 16 14:53:57 2015 -0500

        Remove the ideas doc, it isn't needed anymore.
```
