# React + Jenkins + OpenShift Deployment

This project builds a React.js app, creates a Docker image, and deploys it to OpenShift using Ansible and Jenkins CI/CD.

## Includes

- React App (Create React App)
- Dockerfile (Multi-stage with Nginx)
- Jenkinsfile (Pipeline for build, Docker, Ansible)
- Ansible Playbook (OpenShift deployment)

## Setup

- Configure Docker Hub credentials in Jenkins as `docker-hub-creds`
- Use Jenkins node with Docker, Node.js, Ansible installed
- Set OpenShift token and server in environment variables: `OPENSHIFT_TOKEN`, `OPENSHIFT_SERVER`


src/
├── App.js
├── index.js
├── components/
│   ├── Header.js
│   ├── Footer.js
│   └── Home.js
├── pages/
│   ├── About.js
│   └── Contact.js
├── styles/
│   └── App.css
