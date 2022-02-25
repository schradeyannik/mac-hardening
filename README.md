# mac-hardening
Resources for making your Mac more secure (targeted to developers)

## Containerization of development environments
### Idea
- Create containers (VMs) in which we develop our projects and can safely execute third party code
- We use Vagrant and Docker (if you have an Intel machine, you can also use VirtualBox but M1 only works with Docker atm)
- We will do code editing over SSH in VSCode
- This allows us to install and run devtools and VSCode extensions only in the local container and not our main machine, which is pretty cool.

### Setup
- Install Vagrant (https://www.vagrantup.com/downloads) and Docker (https://docs.docker.com/engine/install/)
- Create the dir storing our containers: `mkdir ~/vagrant`
- In order for making this system easier to use, I have create two aliases, you can place in your `~.zshrc` or `.bashrc` file:
  - `echo "alias start='sh ~/scripts/vagrant-start.sh'" >> ~.zshrc`
  - `echo "alias stop='sh ~/scripts/vagrant-stop.sh'" >> ~.zshrc`
- Now reload your terminal and open it again

### Creating a container
- First create a new dir under `/vagrant` with the name of your container (`mkdir ~vagrant/name`)
- In this repo under `vagrant` you will find an example `Dockerfile` and `Vagrantfile`
- Go into your new directory (`cd ~vagrant/name`) and place both of them in there
- You can configure the files to your liking (with the template you will run ubuntu:18.04 (with depending on wheter you have M1 or Intel, arm or amd x86)!)
- Now run `start name` with the name of your new container
- To stop a container (and retain RAM) call `stop name`
- After you have connected, run `exit`

### Container environment
- To enter a container, run `start name` with the name of your container
- To stop a container (and retain RAM) call `stop name`
- In the container you will be able to install all tools you need
- The basic Dockerfile provided will install `git and curl`

### Editing code in VSCode over SSH
- Download the "Remote - SSH" extension into VSCode (https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)
- Next (in the directory of your container) run `pbcopy < vagrant ssh-config`
- In VSCode, navigate in the sidebar to the "Remote Explorer"
- Next to "SSH Targets" press the cogwheel and select `Users/.../.ssh/config`
- Now paste the copied ssh-config and rename the Hostname from "default" to the name you have given your container
- That's it. Close the config file, and you can now connect to your container using the Remote Explorer and select individual folders.
