docker-digitalocean-ansible
===========================
Ansible script for creating the ubuntu 13.10 64bit docker image on digital ocean


Prerequisites
-------------

- Ansible installed.

    $ pip install -r requirements
    
- Digital Ocean Ubuntu 13.10 64bit Droplet with your SSH key installed

- Create a file called ```ansible_hosts``` with the ip address of your droplet

    $ echo "your-ip" > ~/ansible_hosts

- Add the 'ANSIBLE_HOSTS' ENV variable 

    $ export ANSIBLE_HOSTS=~/ansible_hosts

- Disable the ANSIBLE HOST KEY CHECKING

    $ export ANSIBLE_HOST_KEY_CHECKING=False


building an image
-----------------
1. create a new Ubuntu 13.10 64bit Droplet

2. get the IP address from the new droplet and add it to the ```~/ansible_hosts``` file. Make sure ```ANSIBLE_HOSTS``` and 'ANSIBLE_HOST_KEY_CHECKING' env variables are set. (see above)

3. Run ansible

    $ ansible-playbook docker.yml

4. login to server, make sure docker is running correctly. If so, reboot and make sure it starts up automatically

    $ reboot

5. If docker is still running, then it is good to go. Clean up the image. (remove some files)

    $ rm -rf ~/.ssh/authorized_keys ~/.bash_history ~/.ansible

6. stop the droplet from command line
    
    $ shutdown -H now
    
7. go into the control panel and create a snapshot of the droplet. label it "Docker-Ubuntu-13.10-x64"

8. On the control panel, look at the images, and make sure you replicate them across data centers. you do this by going to the images, find the image you just created and click on the globe icon "Distribute to all regions".

9. Find the imageId for the image you just created. You can find this by looking at the URL when you hover over the edit "pencil" icon of your image on the images page. Write that number down.

10. Send an email to Etel at Digitial Ocean, letting her know there is a new image available, and give her the new imageId, and she will work her magic to move it into production.


    