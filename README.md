# Dev Helper Commands

Useful commands for every Developer

## Usage

### Git commands

* `make git.status`


### Composer commands

* `make composer.download`
* `make composer.install`
    * dependency on `composer.download`
* `make composer.update`
    * dependency on `composer.download`

### Symfony

#### Running tests in parallel using Robo

* `make symfony.test.run`
    * dependency on Robo

#### Running Behat tests

* `make symfony.test.bdd`
    * dependency on Behat & SymfonyBehat bundle
    
#### Running PHPSpec

* `make symfony.test.spec`
    * dependency on PHPSpec
    
#### Running PHPUnit

* `symfony.test.unit`

