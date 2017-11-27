[projectUri]: https://github.com/sketch7/ssv-ng2-command
[projectGit]: https://github.com/sketch7/ssv-ng2-command.git
[changeLog]: ./doc/CHANGELOG.md

[contribWiki]: ./doc/CONTRIBUTION.md
[releaseWorkflowWiki]: ./doc/RELEASE-WORKFLOW.md

[npm]: https://www.npmjs.com
[jspm]: http://jspm.io
[typings]: https://github.com/typings/typings
[commandPatternWiki]: https://en.wikipedia.org/wiki/Command_pattern

# @ssv/ngx.command
[![Build status](https://ci.appveyor.com/api/projects/status/0yno0mn184bj5tbd?svg=true)](https://ci.appveyor.com/project/chiko/ssv-ng2-command)
[![Build status](https://ci.appveyor.com/api/projects/status/0yno0mn184bj5tbd/branch/master?svg=true)](https://ci.appveyor.com/project/chiko/ssv-ng2-command/branch/master)
[![bitHound Overall Score](https://www.bithound.io/github/sketch7/ssv-ng2-command/badges/score.svg)](https://www.bithound.io/github/sketch7/ssv-ng2-command)
[![npm version](https://badge.fury.io/js/%40ssv%2Fng2-command.svg)](https://badge.fury.io/js/%40ssv%2Fng2-command)

[Command pattern][commandPatternWiki] implementation for angular. Command's are used to encapsulate information which is needed to perform an action.

Primary usage is to disable a button when an action is executing, or not in a valid state (e.g. busy, invalid), and also to show an activity progress while executing.


In order to contribute please read the [Contribution guidelines][contribWiki].

**Quick links**

[Change logs][changeLog] | [Project Repository][projectUri] | [Contribution guidelines][contribWiki]

# Installation

Get library via [npm]
```bash
npm install @ssv/ngx.command --save
```

# Usage

## Register module

```ts
import { CommandModule } from "@ssv/ngx.command";

@NgModule({
    imports: [
        CommandModule
    ],
    declarations: [
        AppComponent
    ]
}
export class AppModule {
}
```

## Command
In order to start working with Command, you need to create a new instance of it.

```ts
import { CommandDirective, Command, ICommand } from "@ssv/ngx.command";

isValid$ = new BehaviorSubject(false);
saveCmd: ICommand = new Command(() => this.save()), this.isValid$);

// usage when execute function returns an observable - NOTE: 3rd argument must be true!
saveCmd: ICommand = new Command(() => Observable.timer(2000), this.isValid$, true);
```

## Command Attribute (Directive)
Handles the command `canExecute$`, `isExecuting` and `execute` functions of the `Command`, in order to
enable/disable, add/remove a cssClass while executing in order alter styling during execution (if desired)
and execute when its enabled and clicked.

Generally used on a `<button>` as below.

### Usage

```html
<!-- simple usage -->
<button [command]="saveCmd">Save</button>

<!-- using isExecuting + showing spinner -->
<button [command]="saveCmd">
    <i *ngIf="saveCmd.isExecuting" class="ai-circled ai-indicator ai-dark-spin small"></i>
    Save
</button>

```

## Usage without Attribute
It can also be used as below without the command attribute.
```html
<button
    [disabled]="!saveCmd.canExecute"
    (click)="saveCmd.execute()">
    Save
</button>
```

## Configure
In order to configure globally, you can do so as following:

```ts
import { CommandModule } from "@ssv/ngx.command";

    imports: [
        CommandModule.forRoot({ executingCssClass: "is-busy" })
    ],
```


## Getting Started

### Setup Machine for Development
Install/setup the following:

- NodeJS v9+
- Visual Studio Code or similar code editor
- TypeScript 2.6+
- Git + SourceTree, SmartGit or similar (optional)
- Ensure to install **global NPM modules** using the following:


```bash
npm install -g git gulp yarn devtool
```


#### Cloning Repo

- Run `git clone https://github.com/sketch7/ssv-ng2-command.git`
- Switch to `develop` branch


### Project Setup
The following process need to be executed in order to get started.

```bash
npm install
```


### Building the code

```
npm run build
```

### Running the tests

```
npm test
```


### Development utils

#### Watch
Builds on changes.

```
npm start
```


#### Running Continuous Tests
Spawns test runner and keep watching for changes.
```
npm run tdd
```


### Preparation for Release

```
npm run prepare-release -- --bump major|minor|patch|prerelease (default: patch)
```
Check out the [release workflow guide][releaseWorkflowWiki] in order to guide you creating a release and publishing it.