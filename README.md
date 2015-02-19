# Dev Helper Commands

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/eddiejaoude/dev-helper-cmds?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Useful commands for every Developer.

This abstracts the commands required for development.

For example:

If a developer/tester needs to start the webserver, then should **NOT* * care if you are using vagrant or php built-in webserver.
They should just run the same command (eg. make dev.server). This way, when updating the architecture, the same commands 
 can be run, even if they are doing something slightly different or more than in an earlier version.

## Usage

1. Create a `Makefile` in the root of your project.

2. Added a `LOCATION` parameter to the top of the `Makefile`

```
LOCATION=.
```

If you have brought in this Helper Library with `composer`, then you need to update the location of the include files.

In your main Makefile update the location parameter:

```
LOCATION=vendor/eddiejaoude/dev-helper-cmds
```

*Note: must **NOT** end in a `/`*

3. Now include the *commands* you want to use or include all by adding the following to your `Makefile`

```
include $(LOCATION)/include.all
```

4. Then you are done.

Below our the built-in commands. 
 
### Overriding commands

You can override these by adding to your Makefile that contains all the includes.

```
# ---
# Below is example overwriting commands
# Note: you will get warnings
# ---

symfony.test.spec:
	bin/phpspec run  --config test/phpspec.yml

symfony.test.bdd:
	bin/behat --config test/behat.yml 
```

### Combining commands to make new ones

It is also possible to combine exist or new commands with a new command:

```
new.command: old.cmd1 old.cmd2
    echo NEW CMD
```

### Added Custom commands

1. Create a directory in your project root `.make/`

2. Add command files inside new directory `.make/log`

3. In your Makefile include new custom files with
 
```
include .make/*
```

All done!


---

### Built-in commands

#### Git commands

* `make git.status`
* `make git.branch branch=build-feature/symfony2-behat-35` (this can be a branch or tag or commit hash)

#### Composer commands

* `make composer.download`
* `make composer.install`
    * dependency on `composer.download`
* `make composer.update`
    * dependency on `composer.download`

#### Symfony

##### Built-in Server

* `make symfony.server`

##### Dump logs

* `make symfony.logs`

##### Database

* `make symfony.dev.rebuild` runs all the commands below...

* `make symfony.dev.db.drop` drops the database
* `make symfony.dev.db.create` creates the database
* `make symfony.dev.db.update` updates the database
* `make symfony.dev.db.data` loads fixture data into database

##### Dump & commit assets

* `make build.assets`

Example usage / override, add the following to your custom Makefile (or include) 

```build.package: build.user build.version build.changelog build.assets build.tag```

##### Running tests in parallel using Robo

* `make symfony.test.run`
    * dependency on Robo

##### Running Behat tests

* `make symfony.test.bdd`
    * dependency on Behat & SymfonyBehat bundle
    
##### Running PHPSpec

* `make symfony.test.spec`
    * dependency on PHPSpec
    
##### Running PHPUnit

* `symfony.test.unit suite=app`



[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/eddiejaoude/dev-helper-cmds/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

