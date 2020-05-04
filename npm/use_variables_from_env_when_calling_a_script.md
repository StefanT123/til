# Use variables from `.env` when calling a script

```json
{
    "scripts": {
        "start": "export $(cat .env | xargs) && node ./app/index.js"
    },
    "dependencies": {
    }
}
