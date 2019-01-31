
## Create and Test a Chocolatey Package ##

Create a package definition, package the package, and test it using [the environment](https://github.com/chocolatey/chocolatey-test-environment) that Chocolatey's verifier uses.


### Create the package definition ###

Run ```choco new your-package-name``` and follow the instructions presented in the ```your-package-name.nuspec``` file.

Delete any unneeded files from the ```tools``` directory.

This is the part of the project that should be checked into VCS (```.nuspec``` + the ```tools``` directory).


### Package and prepare the Chocolatey package ###

A package definition has the extension ```.nuspec```.
A package has the extension ```.nupkg```.

This was learned the hard way after spending the better part of 2 days trying to install ```.nuspec``` files.

To generate a ```.nupkg``` from a ```.nuspec```:
```
choco pack your-package-name.nuspec --outputdirectory $PWD
```

The package has now been generated.


### Testing on the host machine ###

Though Chocolatey recommends performing package testing in a VM (which is a good idea; instructions are below), a quick-and-dirty test install can be done anywhere.

```
choco install your-package-name -dv --source $PWD
```

The ```--source``` or ```-s``` option tells Chocolatey where to look for packages.
Assuming we haven't changed directories since the previous step, this should pick up our package from the current working directory.

#### Dealing with dependencies ####

If your package has dependencies, you'll need to explicitly tell Chocolatey where to resolve those as well since ```--source``` overrides the default Chocolatey API.

```
choco install your-package-name --source="$PWD;https://chocolatey.org/api/v2"
```


### Testing via Chocolatey VM test environment ###

### On the host machine ###

Install dependencies:
```
choco install vagrant
choco install virtualbox
vagrant plugin install sahara
```

Clone the choco test environment:
```
git clone https://github.com/chocolatey/chocolatey-test-environment
```

Move into the root of the cloned repo (all ```vagrant``` commands expect this working directory):
```
cd chocolatey-test-environment
ls Vagrantfile
```

Download the image (first time only) and bring the VM up:
```
vagrant up
```

While that's downloading (it'll take awhile), copy your ```.nupkg``` file from the first section to the ```packages``` folder in the root of the cloned repo.
This folder is shared with the VM, so any files you drop there will be available under ```C:\packages``` on the VM.
```
cp other-directory\your-package-name.0.1.nupkg .\packages
```

Once the VM is up, create a restore point (this should run on the host machine's console, not inside the VM):
```
vagrant sandbox on
```


### On the VM ###

Install the package:
```
choco install your-package-name --version X.X.X --source="C:\packages"
```

#### Dealing with dependencies ####

If your package has dependencies, you'll need to explicitly tell Chocolatey where to resolve those since ```--source``` overrides the default Chocolatey API.
```
choco install your-package-name --source="C:\packages;https://chocolatey.org/api/v2"
```

The ```-fdv``` (force, debug, verbose) options can be used to get more information if install runs into any problems.

If all goes according to plan, your package is ready to head to release.


### Starting fresh (back on the host machine) ###

If install did not go as planned, it's best to rollback the VM and start fresh.
```
vagrant sandbox rollback
```

Once the VM restarts, the [testing process](#on-the-vm) can be repeated.


### Cleaning up ###

Stop the VM using:
```
vagrant suspend
    OR
vagrant halt
```

Delete the VM using:
```
vagrant destroy
```

Source: 
- https://github.com/chocolatey/chocolatey-test-environment
- https://github.com/chocolatey/chocolatey-test-environment/blob/master/Testing.md
- https://github.com/chocolatey/choco/wiki/CreatePackages#build-your-package
- https://www.vagrantup.com/docs/cli/index.html
