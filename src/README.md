# Module Manager
Installation-free ES6 module manager and CDN. The *users* of modules require no setup. Just copy paste an ES6 import and you're good. 

Even module *developers* require nothing but git. No npm, no dependencies. Only module *publishers* require a dependency, and only if they do not want to create Github repositories by hand. 

- Native ES6 module imports
- Git as version manager
- Github pages used as CDN
- Testing with the Jasmine Standalone Framework (in browser and with TravisCLI)
- Documentation and type checking via JSDocs
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
```
/root
	/src
		/spec
	/version
		/0.1/
			<copy of src at some point in time>
		/0.2/
			<copy of src at some point in time>
		...
```
Code changes happens only in the `src` folder. Versions are published by copying the full source folder to the `version` folder.
Directories in `version` may never change once they are published. The integrity of versions is based on the files' hashes.
The security model is: 
> Adding folders to `version` is allowed, but changing an existing version is an attack on the module's users.

It also means, clients can cache any file in `version` forever.