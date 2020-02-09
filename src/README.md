# Module Manager
Installation-free ES6 module manager and CDN. The *users* of modules require no setup. Just copy paste an ES6 import and you're good. 

Even module *developers* require nothing but git. No npm, no dependencies. Only module *publishers* require a dependency, and only if they do not want to create Github repositories by hand. 

- Native ES6 module imports
- Git as version manager
- Github pages used as CDN
- Testing with the Jasmine Standalone Framework (in browser and with TravisCLI)
- Documentation via JSDocs ([and type checking](https://medium.com/@trukrs/type-safe-javascript-with-jsdoc-7a2a63209b76) )
- TODO: Resource integrity verification with CSP
- TODO: Compatibility with npm


## Publisher Setup
Publishing a module requires [Github's hub](https://hub.github.com/).  

```
brew install hub
ln -s "`pwd`/src/moma" /usr/local/bin/moma
```

To delete modules you have to [grant your Github token access](https://github.com/settings/tokens) here.

## Publish Module
```
moma <name> <description>
```

## Run your own CDN
To run a CDN, simply checkout the root repository and upload the directory to some static web server.
The only requirement is that the server sends `access-control-allow-origin: *` HTTP headers to support imports of ES6 modules. Furthermore, enabling HTTP2 plays nicely together with ES6 modules.


## Directory Template
The directory includes all versions. A simple version scheme i.e. `2.0` is used. Increasing the decimal means all interfaces stay compatible.

```
/root
	/0.1
		<copy of src at some point in time>
	/0.2
		<copy of src at some point in time>
	/0.3
	...
	/head
		<copy of src at some point in time>
	/src
		/spec
```

Code changes are allowed only in the `src` folder. New versions are published by copying the full source folder to a version folder. Version folders may never change once they are published. The integrity of a version is based on its files' hashes.
The security model is: 
> Adding folders to `version` is allowed, but changing an existing version is an attack on the module's users.

It also means, clients can cache any file in any version folder forever.