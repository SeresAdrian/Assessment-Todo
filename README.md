# Assessment-Todo
Deploy "Todo" app provided by Docker to one virtual machine (CentOS Linux 7) with ansible

I used two virtual machines , the main one is a Kali linux machine where I made the deployment of application into the CentOS machine.

Here I used two diffrent files : iventory and playbook.

The iventory file where I stored the IP_Addr of the host(192.168.50.141) , the port(22 for ssh) , and credentials for a successful login.
The ansible playbook file is getting-started_deploy.yaml where I had to put the task of copying all the files from the local path location to the remote server so I done the deploy.

For the task to be accomplished I used a single command : $ ansible-playbook -i inventory getting-started_deploy.yaml
where I specified the inventory for remote connection within parameter '-i inventory' and the plays with the playbook file 'getting-started_deploy.yaml'

After the command succesfully ran the screen should look like this
![returned playbook state](https://user-images.githubusercontent.com/48512041/138588044-fe74a827-840d-48e5-a814-d78925afcb3d.jpg)

On the remote server, the file appeared at the path specified in playbook which is /home , cd(change directory) into the /home/getting-started/app where I built the app with "# docker built -t getting-started . " and then I ran the app with "# docker run -dp 3000:3000 getting-started". The application works as expected, but I need to add a database(because I don't want to put items into the list everytime I ran the app) into it so I have to add a volume with "# docker volume create todo-db" I delete the old docker container with "# docker rm -f" and then I add again the app but with the specified db volume "# docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started"

For the application to be seen check the following link:
http://192.168.50.141:3000/
