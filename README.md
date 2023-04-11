# Cloud Native Development with Tailwind, Google Cloud, and Firebase

## Monorepo

Lerna: tool to manage and optimise the workflow of mlti-package JS respositories with git and npm.

We configure dependencies, test configurations and linting configurations in the parent directory. We have a `services` folder that contains all individual apps.

# firebase `package.json`

We add this to package.json:
`"deploy:firebase": "npm run deploy --prefix firebase"`
We add --prefix firebase. This will run the deploy script in the firebase directory before running in the web directory.

`"deploy": "run-s deploy:clean export deploy:firebase"` // 'run-s' is equivalent to 'npm-run-all' and executes commands in a given sequential order. It firstly removes extra directories, then runs the export script, and then deploy's the application to firebase.

Install run-s first with `npm install npm-run-all --save-dev` to run the command.

### Development
```
"dev": "run-p dev:*",
"dev:firebase": "npm run dev --prefix firebase",
"dev:sapper": "sapper dev"
```
Note: run-p is provided by the npm-run-all dev dependency. It runs all dev:* scripts in parallel. In our case, that’s dev:firebase and dev:sapper.

# Monorepo Template

A minimal monorepo template with:
* [Lerna](https://lerna.js.org/)
* [TypeScript](http://www.typescriptlang.org/)

## Install dependencies

1. `npm install`
1. `npm run bootstrap`

## To add a new service

Run the following command:

```sh
npm run generate service
```

## Generators

The `npm run generate` command uses `plop` ([https://plopjs.com/](https://plopjs.com/)).

It all starts with the `./generators/index.js` file.

### Add a new service template

1. Create a new directory in `./templates/services`. Lower case letters and hyphens only.
1. Use the `*.hbs` file extension and Handlebar template syntax for files with dynamic content.

Look at other service templates in `./templates/services` for further guidance.