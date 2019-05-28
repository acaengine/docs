# User Interfaces

Building an interface for ACA Engine is the same as building any generic web application. We try to follow industry best practices and leverage the tools used by most developers in the industry.

* NOTE:: Windows users are recommended to install the [Linux subsystem for Windows](https://msdn.microsoft.com/en-au/commandline/wsl/install_guide).
  * Tools such as git and your preferred text editor make sense to run on Win32
  * Whilst both NodeJS and Ruby can run natively on Windows they are much harder to manage and use effectively when compared to their Linux counterparts.

## What you will need

Please install the following applications as they are core requirements for interface development

1. [git](https://git-scm.com/) - version control
2. A text editor
   * [Sublime Text](https://www.sublimetext.com/)
   * [Atom](https://atom.io/)
   * [Visual Studio Code](https://code.visualstudio.com/)
   * [Font Ligatures](https://github.com/tonsky/FiraCode) are cool
3. [NodeJS](https://nodejs.org/) - development platform
4. [Ruby](https://rvm.io/rvm/install)

## Install some core tools

The tools and libraries that help with development are available via `npm` which is the [Node Package Manager](https://www.npmjs.com/). We recommend installing the following command line helpers

* [Angular CLI](https://cli.angular.io/) `npm install -g @angular/cli`
* [Gulp](https://gulpjs.com/) `npm install --global gulp-cli`

## Running the Demo UI

This is a project that can run against the ACA Engine development environment, for those who want some instant gratification.

1. Create a folder for storing your interface projects
2. Open a command prompt at that location
3. Clone the [Composer Starter](https://github.com/acaprojects/ngx-composer-starter) `git clone https://github.com/acaprojects/ngx-composer-starter.git`
4. `cd ngx-composer-starter` to move into the folder
5. `npm install` to install the project dependencies
6. `gulp serve` to run the development server

## Angular Resources

Angular is our preferred web application framework. We recommend being familiar with it before continuing.

* [https://angular.io/guide/quickstart](https://angular.io/guide/quickstart) - for a basic understanding of Angular applications
* [https://angular.io/tutorial](https://angular.io/tutorial) - fundamentals of Angular

## Updating your environment

This will keep you running on the latest version of the platform as there are periodic updates.

* Updating NPM: `npm install npm@latest -g`
* Updating NodeJS \(Windows users should download the latest MSI, unless using the Linux subsystem\)
  * `sudo npm cache clean -f`
  * `sudo npm install -g n`
  * `sudo n stable`

