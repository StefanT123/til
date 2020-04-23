# Brace expansion

Brace expansion using `{...}` can reduce having to re-type similar text and automate combinations of items.

This is helpful in examples like:
`mv foo.{txt,pdf} some-dir` -  moves both files
`cp somefile{,.bak}` - expands to `cp somefile somefile.bak`
`mkdir -p test-{a,b,c}/subtest-{1,2,3}` - expands all possible combinations and creates a directory tree
`echo {0..50}` - echos all numbers from 0 to 50
`echo {a..c}{1..3}` - echos all combinations (a1, a2, a3, b1, b2, b3, c1, c2, c3)

Brace expansion is performed before any other expansion.
