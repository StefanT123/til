# Brace expansion

Brace expansion using `{...}` can reduce having to re-type similar text and automate combinations of items.

This is helpful in examples like:
`mv foo.{txt,pdf} some-dir` -  moves both files
`cp somefile{,.bak}` - expands to `cp somefile somefile.bak`
`mkdir -p test-{a,b,c}/subtest-{1,2,3}` - expands all possible combinations and creates a directory tree

Brace expansion is performed before any other expansion.
