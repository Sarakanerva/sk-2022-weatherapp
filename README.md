# Weatherapp - Sara Kanerva's edits - 2022

### Instructions on running the app

- Start by cloning the repository

		cd ~/{{ Wished destination }}
		git clone {{ link to the repo}}
    
- Now you should have the repository cloned locally
- Navigate to the repository folder
- Insert your personal [API key](http://openweathermap.org) to the index.js file (or as a env variable)
- Start the application locally by using the command `npm i && npm start`. Or by using the docker-compose file (add your API key to the file) with the command `docker-compose up --build`
- The application frontend should now be reachable at localhost:8000
- (Running the ansible playbook install-application.yml included in the repository with the command `ansible-playbook --connection=local install-application.yml -f 10 -v` will automate this whole process for you.)

------------
* Below we'll go through each chosen exercise and the steps taken towards their completion. 
------------

### Docker

* Dockerfiles have been added to both the 
*frontend* and the *backend* directories, and they can be ran virtually on any environment when docker is installed eg. by running the command `docker build -t weatherapp_backend . && docker run --rm -i -p 9000:9000 --name weatherapp_backend -t weatherapp_backend`

* A docker-compose file has been added and it enables running the app in a connected set of containers, by connecting the front- and backend. The file can be run with the command `docker-compose up --build` inside the application folder. Your personal [API key](http://openweathermap.org) needs to be inserted into the docker-compose file (APPID) to enable smooth operations.

* By using volumes hot reload has been enabled to ensure smooth development operations when the app is ran locally.

### Cloud

* The service is set up in the Google Cloud Platform by using the Google App Engine.

* If you wish to deploy and host the application in your personal Google Cloud project please configure your connection to your Google Cloud Account and project, and install the [gcloud console](https://cloud.google.com/sdk/docs/install). 

* Navigate to each respective folder (backend/frontend/application root) and run the commands
1. `gcloud app deploy backend.yaml`
2. `gcloud app deploy frontend.yaml`
3. `gcloud app deploy dispatch.yaml`

* You should now have the services visible and reachable in the Google Cloud App Engine (The command `gcloud app browse -s {{ frontend/backend }}` can be used to view the application directly in your browser.)

### Ansible

* Playbooks have been created for installing docker and for downloading and running the weather application locally. 

* First make sure you have [ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) installed. To run the playbooks, use the ansible-playbook command. `ansible-playbook --connection=local install-{{ docker/application }}.yml -f 10 -v`

* Make sure you have your Git SSH key configured and have specified your wished destination folder in the install-app playbook before running.

* Run the playbooks in the order:
1. docker-playbook.yml 
2. application-playbook.yml 

### Disclaimer

* Tested only locally on macOS


