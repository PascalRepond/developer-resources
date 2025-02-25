# How to integrate UI in RERO-ils

## From NPM latest published version

If you want to use the last NPM published version, do:

```bash
cd path/to/invenio/instance/folder/static
npm install @rero/rero-ils-ui@latest
```

## From a PR

This should be done in several steps.

First, in rero-ils-ui:

```bash
cd path/to/rero-ils-ui
git checkout rero/pr/xxx
npm install
npm run pack
```

Then use **bootstrap script** with this new file:

```bash
cd path/to/rero-ils
poetry run bootstrap -t ../rero-ils-ui/rero-rero-ils-ui-0.0.x.tgz
```

## Integrate specific branches of ng-core and rero-ils-ui in rero-ils

To integrate specific branches of ng-core and rero-ils-ui - in order to run Cypress tests, for example - you must have the corresponding branch of each repo set locally. Then this command will launch a script to automatically integrate ng-core into rero-ils-ui, then rero-ils-ui in rero-ils:

```
cd path/to/rero-ils
poetry run ./scripts/russian_dolls -c path/to/rero/ng-core -u path/to/rero/rero-ils-ui
```

This script must be used after the bootstrap to overwrite it, otherwise the used versions of rero-ils ui and ng-core will be the npm published ones.

## Run only the UI in local

If you need to test a change only in the `rero-ils-ui`, you can use the 
existing `ils-dev` testing instance as a backend. Make sure the server version 
is compatible with your local UI.

Place [the dev proxy file](dev.proxy.conf.json) in the root of the project and run:

```bash
ng serve --proxy-config dev.proxy.conf.json
```

You need Angular CLI in your environment: `npm install -g @angular/cli`

Then sign in at: [http://localhost:4200/signin/](http://localhost:4200/signin/)