# Simple Flask app Deployment with Ansible

This is a simple flask app ready to be deployed with a simplified Ansible playbook.
The included `playbook` will do the following:

- install system apt packages
- clone this github repository
- create `venv` virtual environmen
- install packages found in `requirements.txt` in `venv`
- configure `gunicorn`, `nginx` and `UFW`
- enable and start `gunicorn` and `nginx` services

## Prerequisites
 - Ansible installed
 - SSH access to any host machine
 - customize the `.hosts` file as need be

```
    git clone https://github.com/codetaskmaster/app-deployment-with-ansible.git
    cd app-deployment-with-ansible/deploy
    vim .hosts
```

## Deploying the app
```
    cd app-deployment-with-ansible/deploy
    ansible-playbook playbook.yaml --ask-become-pass
```

## Debugging
To test connection with with host
```
    cd app-deployment-with-ansible/deploy
    ansible webservers -m ping
```

To check `systemd` status of the services on the host
```
    sudo systemctl status nginx
    sudo systemctl status app-deployment-with-ansible.service
```

To test the application on a host
```
    source venv/bin/activate
    python run.py
    open http://localhost:5000
```

To test `gunicorn` on the host
```
    gunicorn --bind 0.0.0.0:5000 run:app
```

To run `nginx` tests on the host
```
    sudo nginx -t
```

To check Ansible Facts

```
    ansible webservers -m setup
```