# How to Setup Angular2 DEV Environment behind Corporate Proxy

[Angular-2](https://angular.io/) is an amazing framework for fast web development across all platforms.

Though the framework provides very useful documentation, setting up the environment is a nightmare if you work behind corporate proxies.

The initial setup requires online connectivity and many steps fail if you have own firewall proxy setup in place.

## Installing Tools

The first step is to install all required tools. We are using Windows based system. Please install the tools below:
* Visual Studio Code IDE: Free IDE supporting Typescript language. Download the latest from [here](https://code.visualstudio.com/)
* Notepad++ Code Editor: Light and Powerful editor which can be used to edit all type of files. [Download latest](https://notepad-plus-plus.org)
* CMDer: Highly useful alternative to Default MS-DOS Prompt. Use the MINI version from [here](http://cmder.net/)
* Node.JS: Node is used extensively for Angular2 development. Install latest from [here](https://nodejs.org/).
* Google Chrome Browser. Download and install the latest and get familiar with the [F12 Developer tools](https://developer.chrome.com/devtools).

Install all the tools above before continuing.

## Configuring Proxy Details for NPM

Create a file .npmrc in folder C:\Users\<USERS> and include the content below in the file.

```shell
strict-ssl=false
http-proxy=http://<DOMAIN>%5C<USER>:123Pass%40@<PROXYIP>:<PROXY_PORT>
https-proxy=http://<DOMAIN>%5C<USER>:123Pass%40@<PROXYIP>:<PROXY_PORT>
proxy=http://<DOMAIN>%5C<USER>:123Pass%40@<PROXYIP>:<PROXY_PORT>
registry=http://registry.npmjs.org
```

Save the file before going ahead. Some points to note:
* If special characters are present, then they need to be encoded in % format.
* The example above considers password to be 123Pass@ and is encoded as 123Pass%40
* By deafult, the NPM registry access uses HTTPS. The registry setting has been overridden to use simple HTTP.

## Installing Global Packages
* [Typescript](https://www.typescriptlang.org/)
* [Angular-CLI](https://github.com/angular/angular-cli)
* [Typings](https://github.com/typings/typings/)

### Commands to be run on CMDer window
```shell
npm install -g --verbose typescript
npm install -g --verbose angular-cli
npm install -g --verbose typings

```

## Configuring Proxy Details for Typings
Typings also access some information online via HTTPS. This may fail when using the proxy. To override this, follow the steps below.
* Create a file .typingsrc in path C:\Users\<USERS>
* Open the file and include the contents below in the file.
* Proxy IP, Port, Domain, User and Password need to be updated based on actual values.
* HTTP encoding to be used.

```json
{
  "rejectUnauthorized": false,
  "registryURL": "http://api.typings.org/",
  "proxy": "http://<DOMAIN>%5C<USER>:123Pass%40@<PROXYIP>:<PROXY_PORT>",
  "httpProxy": "http://<DOMAIN>%5C<USER>:123Pass%40@<PROXYIP>:<PROXY_PORT>",
  "httpsProxy": "http://<DOMAIN>%5C<USER>:123Pass%40@<PROXYIP>:<PROXY_PORT>"
}
```

## Creating new Angular2 Project
For cerating the project, we will be using Angular-CLI tool. For more detail, please refer the [angular-cli Github page](https://github.com/angular/angular-cli).

Commands below can be run using CMDer in any local folder.

```shell
ng new angular2-hello-world
cd angular2-hello-world
ng build -prod
```

## Testing the Project
* Execute the command below in the folder using CMDER
```shell
ng new angular2-hello-world
cd angular2-hello-world
ng build -prod
ng serve -prod
```

* Open Google Chrome and type in [http://localhost:4200/](http://localhost:4200/)
 
You are Good to GO...

In some cases, you may require the company proxy to be overridden using another proxy. In this case, [CNTLM tool](https://cntlm.sourceforge.net) can be used. This will be covered in another post.
