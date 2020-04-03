# Catch errors

```bash
catchError() {
    errorCode=$?;

    if [[ $? != 0 ]]; then
        print_style "error code: $errorCode\n" "danger";
        print_style "The command executing at the time of the error was:\n" "danger";
        print_style "- command: $BASH_COMMAND\n" "danger";
        print_style "- on line: ${BASH_LINENO[0]}\n" "danger";
    fi
}

# catch an error on the ERR pseudo signal
trap catchError ERR;
```
