# Repro for issue 6973

Deploying functions raises an error when `engines` is not specified in `package.json` even though `runtime` is set in `firebase.json`

`firebase.json`

```json
{
  "functions": [
    {
      "source": "api/career-functions",
      "codebase": "career-functions",
      "runtime": "nodejs18"
    }
  ]
}
```

`package.json`

```json
{
  "name": "functions",
  "description": "Cloud Functions for Firebase",
  "scripts": {
    "serve": "firebase emulators:start --only functions",
    "shell": "firebase functions:shell",
    "start": "npm run shell",
    "deploy": "firebase deploy --only functions",
    "logs": "firebase functions:log"
  },
  "main": "index.js",
  "dependencies": {
    "firebase-admin": "^11.8.0",
    "firebase-functions": "^4.9.0"
  },
  "devDependencies": {
    "firebase-functions-test": "^3.1.0"
  },
  "private": true
}
```

## Versions

firebase-tools: v13.7.1 and v13.6.0<br>
node: v18.16.1

## Steps to reproduce issue

1. Use `firebase-tools` v13.7.1
1. Run `firebase deploy --project PROJECT_ID`
   - Raises an error:

```
Error: `runtime` field is required but was not found in firebase.json or package.json.
To fix this, add the following lines to the `functions` section of your firebase.json:
"runtime": "nodejs20" or set the "engine" field in package.json
```

## Notes

### Using firebase-tools v13.6.0

1. Switch to `firebase-tools` v13.6.0
1. Run `firebase deploy --project PROJECT_ID`
   - Deployment works fine

### Using firebase-tools v13.6.1

1. Switch to `firebase-tools` v13.6.1
1. Run `firebase deploy --project PROJECT_ID`
   - Raises an error:

```
Error: `runtime` field is required but was not found in firebase.json or package.json.
To fix this, add the following lines to the `functions` section of your firebase.json:
"runtime": "nodejs20" or set the "engine" field in package.json
```
