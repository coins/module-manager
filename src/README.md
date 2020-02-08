# Modules Manager
Installation-free ES6 modules manager and CDN based on Github and Jasmine.
The *users* of modules require no setup. Just copy paste an ES6 import and you're good. 
Even module *developers* require nothing but git. No npm, no dependencies. Only module *publishers* require a dependency. 

- Native ES6 module imports
- Git as package manager
- Github pages used as CDN
- Testing with the Jasmine Standalone Framework (in browser and with TravisCLI)
- Documentation and type checking via JSDocs
- TODO: Compatibility with npm

```
/root
	/src
		/spec
	/dist
		/0.1/
			<copy of src at some point in time>
		/0.2/
			<copy of src at some point in time>
		...
```

## Publisher Setup
Publishing a module requires [Github's hub](https://hub.github.com/).  

```
brew install hub
ln -s "`pwd`/moma" /usr/local/bin/moma
```

## Publish Module
```
moma <name> <description>
```

## Run your own CDN
To run a CDN, simply checkout the root repository and upload the directory to some static web server.
The only requirement is that the server sends `access-control-allow-origin: *` HTTP headers to support imports of ES6 modules. Furthermore, enabling HTTP2 plays nicely together with ES6 modules.