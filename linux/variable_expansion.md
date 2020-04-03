# Variable expansion

In Bash, note there are lots of kinds of variable expansion.

Checking a variable exists: `${name:?error message}`. For example, if a Bash script requires a single argument, just write `input_file=${1:?usage: $0 input_file}`.

Using a default value if a variable is empty: `${name:-default}`.

If you want to have an additional (optional) parameter added to the previous example, you can use something like `output_file=${2:-logfile}`. If `$2` is omitted and thus empty, `output_file` will be set to logfile.

Arithmetic expansion: `i=$(( (i + 1) % 5 ))`.

Sequences: `{1..10}`.

Trimming of strings: `${var%suffix}` and `${var#prefix}`. For example if `var=foo.pdf`, then `echo ${var%.pdf}.txt` prints `foo.txt`.
